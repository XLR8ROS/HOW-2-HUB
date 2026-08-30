# XOS PGVector Automatic Embeddings HOWTO

**Scope:** XOS Recall semantic-memory embedding generation, storage, retry, health checks, and retrieval.
**Status:** Active procedural how-to.

## Purpose

XOS Recall stores semantic-memory chunks in Supabase Postgres and retrieves them with pgvector. A row containing text is not semantically searchable until an embedding has been generated and stored in its vector column.

`pending` is a processing state, not a successful completion state. A memory workflow is incomplete when text rows remain indefinitely pending with `embedding IS NULL`.

## Core data path

1. Normalize source material into small semantic chunks.
2. XOS prefers three small semantic chunks when the source naturally divides that way.
3. Write each chunk to `public.memories` with source and metadata.
4. Queue embedding work automatically.
5. A worker sends the chunk text to the OpenAI Embeddings API.
6. Write the returned embedding into the pgvector-compatible `embedding` column.
7. Change metadata from `embedding_status=pending` to `embedding_status=embedded` and record an embedding timestamp.
8. Retrieval embeds the search query and passes it to `match_memories(query_embedding, match_count, match_threshold)`.

## Model and dimensions

Current model: `text-embedding-3-small`.

OpenAI documents that `text-embedding-3-small` returns 1536 dimensions by default. XOS must keep the database vector dimensionality and the model output dimensionality identical.

If the model or OpenAI `dimensions` parameter changes, update the database vector type, search function, tests, existing data migration plan, and this HOWTO together.

Do not silently mix embedding models or incompatible embedding spaces.

## What pgvector does and does not do

pgvector stores vectors and performs vector similarity search. It does **not** generate embeddings.

Responsibilities:

- OpenAI embedding model: converts text into numeric vectors.
- Supabase Edge Function / embedding worker: calls OpenAI and writes results.
- pgvector: stores vectors and performs similarity operations.
- `match_memories`: XOS retrieval function.

## Recommended automatic-processing architecture

Supabase's automatic-embeddings documentation uses an asynchronous pipeline:

`INSERT/UPDATE -> trigger -> pgmq queue -> pg_cron processor -> pg_net -> Edge Function -> OpenAI -> pgvector update`

Required components:

- `vector`: vector storage/search.
- `pgmq`: durable embedding-job queue.
- `pg_net`: asynchronous HTTP calls from Postgres to the Edge Function.
- `pg_cron`: scheduled queue processing and retries.
- database trigger: automatically queues rows when embeddable content is inserted or changed.
- Edge Function: requests embeddings and updates the row.

This is preferable to relying on a manually invoked backfill function because failed work remains observable and retryable instead of becoming forgotten `pending` rows.

## XOS RECALL diagnostic finding, 2026-08-30

Inspection of Supabase project `pvkgepftgyycwxhuvssi` found:

- `vector`: enabled.
- `pg_net`: enabled.
- `pgmq`: not enabled at inspection time.
- `pg_cron`: not enabled at inspection time.
- `public.memories.embedding`: vector column exists.
- `match_memories(query_embedding vector, match_count integer, match_threshold double precision)`: exists.
- Interview rows were stored successfully but showed `embedding_status=pending` with `embedding IS NULL`.
- `public.memories` had only the updated-at trigger; no embedding-enqueue trigger was present.

Conclusion: pgvector itself was functioning. The automatic embedding-generation conveyor belt was incomplete upstream.

## Health checks

### Pending/null count

Check for rows where the status is pending or the embedding is null. A persistent or growing count is a failure signal.

### Dimension check

Confirm generated embeddings match the configured vector dimensionality.

### Edge Function / worker logs

Confirm the worker receives jobs, reaches OpenAI successfully, and updates rows. Pending jobs plus empty worker logs usually indicate the worker was never invoked.

### Queue state

When pgmq is active, inspect queued, in-flight, failed/retried, and completed job behavior.

### End-to-end retrieval test

Insert a uniquely worded test memory, allow it to embed, then search semantically using a paraphrase that does not copy the original wording. Verify the test row is returned.

Storage-only verification is insufficient.

## Failure rules

- Never report semantic-memory ingestion as complete while required embeddings are null.
- Never blame pgvector merely because an embedding was never generated.
- Never leave failed work indefinitely in `pending` without observable retries or an explicit blocker.
- Never retry blindly without checking worker logs, queue state, secrets, and API errors.
- Never expose `OPENAI_API_KEY`, Supabase service/secret keys, or private auth tokens in source control, logs, or user-facing output.
- A failed embedding job must remain observable and retryable.

## Secrets

Store `OPENAI_API_KEY` as a Supabase Edge Function secret/environment variable. Supabase service or secret keys must never be committed to Git or shipped to a browser.

## pgvector indexing

pgvector supports exact search without an approximate index. At larger scale, HNSW or IVFFlat can be introduced after measuring table size and retrieval latency.

For OpenAI embeddings, cosine similarity is a normal retrieval choice. The index operator class and SQL distance operator must agree.

## Official documentation

- Supabase automatic embeddings: https://supabase.com/docs/guides/ai/automatic-embeddings
- Supabase AI & Vectors: https://supabase.com/docs/guides/ai
- Supabase pgvector extension: https://supabase.com/docs/guides/database/extensions/pgvector
- Supabase Edge Functions: https://supabase.com/docs/guides/functions
- Supabase Edge Function secrets: https://supabase.com/docs/guides/functions/secrets
- Supabase pg_net: https://supabase.com/docs/guides/database/extensions/pg_net
- Supabase scheduled Edge Functions / pg_cron: https://supabase.com/docs/guides/functions/schedule-functions
- OpenAI embeddings guide: https://developers.openai.com/api/docs/guides/embeddings
- OpenAI create embedding API reference: https://developers.openai.com/api/reference/resources/embeddings/methods/create
- pgvector upstream project: https://github.com/pgvector/pgvector

## Repo/navigation architecture

XOS repo navigation must not require a Mac-only Homebrew environment.

Preferred architecture:

- GitHub repositories are the machine-readable canonical source for repository structure.
- iCloud may remain a personal backup/workspace but is not a required dependency for a headless Linux server.
- Paperclip/Linux clones or pulls authorized GitHub repositories.
- A portable Linux-compatible generator, preferably Python or POSIX shell, enumerates checked-out repos or GitHub trees and writes the root `NAVIGATION.md`.
- Commit the generator to a repository and run it through cron, CI, or the Navigation refresh workflow.
- Homebrew may install tools on macOS, but the navigation algorithm itself must not depend on Homebrew.

If an authoritative repo exists only in iCloud, import/push it to GitHub before expecting Linux automation to map it.

## iCloud boundary

Linux is not an officially supported iCloud Drive sync-client platform. Do not make Paperclip depend on personal Apple Account credentials merely to discover Git repository structure. Git is the correct transport for Git repositories.

## Completion standard

XOS Recall ingestion is complete only when:

1. chunks are stored;
2. embeddings are non-null;
3. status is embedded;
4. semantic retrieval succeeds; and
5. failures/retries are observable.

Anything less is partial completion and must be reported as such.
