# GitHub HOW-TO HUB

Markdown documentation pulled from official GitHub sources.

## XOS self-hosted Paperclip GitHub workflow (2026-10-09)

Scope: XOS Mac Paperclip (verified server version 2026.1001.0), not the retired Ubuntu instance. Use the GitHub fine-grained personal access token (PAT) and Paperclip's company secret/agent environment bindings. No Paperclip Cloud enrollment is needed for this secret-based shell-access route.

### Navigation and setup

1. GitHub token creation: https://github.com/settings/personal-access-tokens/new . Resource owner `reginaldberry02-sys`; Reg selected **All repositories** for that owner. Set expiry and required permissions deliberately; never include a token in documentation, chat, issues, or commits.
2. In **Paperclip → Settings → Secrets**, use **New secret** at the main Secrets view (not New folder). Set **Scope: Company**, **Name: `GITHUB_TOKEN`**, **Key: `GITHUB_TOKEN`**, **Provider: Local encrypted**, **Provider vault: Deployment default**, and **Value: the private GitHub PAT**. Use description `GitHub API access for authorized XOS agents and repositories`.
3. Save and verify that the existing `GITHUB_TOKEN` appears in Secrets. Do not make duplicate credentials.
4. Open **GITHUB_TOKEN → Agent access → Add**. Select an agent and enter **Env var: `GH_TOKEN`**. Save. Repeat for **Alpha** and **Addy**, the two current agents. Provision future agents individually at onboarding; do not assume automatic inheritance.
5. Execute the verification *inside each actual Paperclip agent run* and record the result without exposing credentials:

```sh
test -n "$GH_TOKEN" && echo GH_TOKEN_PRESENT || echo GH_TOKEN_MISSING
gh api repos/reginaldberry02-sys/AlphaCore --jq '.full_name'
```

Also test each agent's own assigned repository. Validate any required GitHub write operation using an explicitly approved non-destructive test.

### Important boundaries

- **Connectors → GitHub → Connect with Paperclip** invokes managed Cloud enrollment. The XOS self-hosted instance returned `Paperclip Cloud enrollment could not be started`. This is **not** the GitHub PAT secret-entry route.
- **Settings → Secrets** plus `GH_TOKEN` grants provides an agent-process credential for GitHub CLI workflows. It **does not itself establish the native GitHub agent-tool connector**. Track that capability and its tests separately.
- A token under `reginaldberry02-sys` does not necessarily authorize repositories owned by the separate `XLR8ROS` organization. Verify each owner and effective permissions.
- GitHub API operations using this PAT are attributable to the GitHub account issuing it, not separate GitHub identities for Alpha and Addy.
- A successful `gh` command on the Mac host is **not** evidence that Paperclip injected the secret into an agent run.
- A secret existing in Paperclip is not proof of agent grants or read/write access.
- The **Plugins → Install plugin** feature is separate from secret storage and should not be confused with a verified native connector.

### Execution state captured on 2026-10-09

- Paperclip company secret `GITHUB_TOKEN` verified existing by Mac-local API.
- Reg reported Alpha's `GH_TOKEN` access grant added.
- Mac host `gh api` read `reginaldberry02-sys/AlphaCore` successfully using existing host authentication.
- Addy's grant and either agent's injected-token authentication **remain unverified**. Do not call the integration complete before testing both.

### Authoritative references

- Paperclip GitHub setup: https://docs.paperclip.ing/connectors/github-setup/
- Paperclip secret folders and agent access: https://docs.paperclip.ing/administration/secret-folders/
- GitHub PAT management: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
- GitHub CLI API: https://cli.github.com/manual/gh_api

---
## Agent operating guide: navigating and working in GitHub

This section is for **every current and future XOS agent**, not just the person configuring credentials. The primary reference is **GitHub's own documentation already preserved in this hub**, particularly the GitHub CLI manual in `docs/03_github_cli_manual/markdown/manual.md` and the installed-command reference files in `docs/04_local_gh_cli_help/markdown/`. Consult those authoritative references before relying on abbreviated examples.

### Determine the execution surface first

1. **Paperclip agent terminal/runtime:** use `gh` for GitHub API, repositories, issues, PRs, Actions, and searches; use `git` for local working-copy operations. The assigned Paperclip company secret maps to `GH_TOKEN` inside authorized agent processes. Never print or record the credential.
2. **GitHub connector tool exposed by a runtime:** use its documented tool names and inputs; verify availability and authorization in that specific runtime. A Paperclip secret by itself does **not** activate this tool surface.
3. **GitHub website:** useful for interactive review, branch protection, settings, access management, and debugging. Do not assume an agent has an interactive browser.
4. **GitHub workflow/coding-agent environment:** `GITHUB_TOKEN` issued to a GitHub Actions job differs from the company PAT saved in Paperclip; consult GitHub Actions token/security documentation before using it.

### Discover identity, account, repository and state

```sh
# Must run inside the actual agent's Paperclip execution environment
test -n "$GH_TOKEN" && echo GH_TOKEN_PRESENT || echo GH_TOKEN_MISSING
gh auth status
gh repo list reginaldberry02-sys --limit 100
gh repo list XLR8ROS --limit 100
gh repo view reginaldberry02-sys/AlphaCore
gh api repos/reginaldberry02-sys/AlphaCore --jq '.full_name'
```

Treat the two owners `reginaldberry02-sys` and `XLR8ROS` as **separate permission scopes**. A token scoped to the first owner does not authorize the second. Never assume that Mac host CLI authentication proves Paperclip agent access. Resolve your identity and assigned repository through your agent instructions and control plane; verify the owner/repo string before writes.

### Locate, clone, inspect and synchronize the assigned repository

```sh
gh repo clone OWNER/REPO
cd REPO
git remote -v
git status --short --branch
git branch -vv
git fetch --all --prune
git status
```

Use `OWNER/REPO` as a placeholder until resolved from authoritative assignment. **Do not clone over an existing worktree**, reset, rebase, overwrite, or perform a blind `git pull` on divergent work. Inspect local modifications, upstream tracking and ahead/behind state first. Preserve unique content, reconcile legitimate changes, run checks, and verify each push. Repository operations are execution tasks, not audit-only tasks, when the assignment authorizes cleanup/synchronization.

### Standard working operations

```sh
gh issue list -R OWNER/REPO
gh issue view 123 -R OWNER/REPO
gh pr list -R OWNER/REPO
gh pr view 123 -R OWNER/REPO
gh pr checks 123 -R OWNER/REPO
gh run list -R OWNER/REPO
gh workflow list -R OWNER/REPO
gh api repos/OWNER/REPO/contents/README.md
```

For authorized code changes, inspect the target branch and current worktree, create a task-specific branch, edit and test, inspect the diff, commit appropriate changes, push, then use `gh pr create` when required. Never silently change canonical governing documents, delete repositories, force-push, or bypass review/approval requirements. GitHub credential authority does not supersede XOS document and workflow authority.

### Failure diagnosis and agent onboarding

- `GH_TOKEN_MISSING`: verify the saved `GITHUB_TOKEN` company secret and that **Agent access → Env var: GH_TOKEN** was assigned to this specific agent; then start a new agent run to check injection.
- `401`: credential missing, invalid or revoked; `403`: authorization, token permission, organization policy or rate limit; `404`: wrong owner/path **or** a private repository not visible to that identity. Inspect the response before deciding.
- `gh` works in a Mac terminal but not an agent: verify the agent's adapter, environment-variable injection, executable availability and process environment.
- A new agent must be assigned its permanent identity and repository, granted access to the existing company credential as appropriate, instructed to use this hub, and tested **from that agent's runtime**. Do not assume future grants are automatic.
- Avoid token output: never run `gh auth status --show-token`, dump the process environment, or place token strings in logs.

### Official agent and CLI references

The complete preserved GitHub documentation tree is the primary operational library. Relevant source-of-truth links:

- GitHub CLI command index: https://cli.github.com/manual/gh
- GitHub CLI repository clone: https://cli.github.com/manual/gh_repo_clone
- GitHub CLI authentication status: https://cli.github.com/manual/gh_auth_status
- GitHub CLI authenticated REST/GraphQL calls: https://cli.github.com/manual/gh_api
- GitHub CLI issues: https://cli.github.com/manual/gh_issue
- GitHub CLI pull requests: https://cli.github.com/manual/gh_pr
- GitHub CLI Actions workflows: https://cli.github.com/manual/gh_workflow
- GitHub CLI Actions runs: https://cli.github.com/manual/gh_run
- GitHub CLI pull-request creation: https://cli.github.com/manual/gh_pr_create
- GitHub Copilot agent/custom instructions (different agent runtime): https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions
- Paperclip GitHub connector: https://docs.paperclip.ing/connectors/github-setup/
- Paperclip agent-secret access: https://docs.paperclip.ing/administration/secret-folders/

**Operational verification state (2026-10-09):** Mac-host GitHub access and the Paperclip company secret were verified. In-agent `GH_TOKEN` authorization, Addy's grant, and the native Paperclip GitHub connector are not yet independently verified. This document describes the method; it does not assert those tests passed.

## Contents

- `docs/00_github_docs_repo/markdown/` — root files from the official GitHub Docs repo.
- `docs/01_docs_github_com_content/markdown/` — official docs.github.com content from `github/docs/content`.
- `docs/02_reusables_and_variables/markdown/` — official GitHub Docs reusable/variable source material.
- `docs/03_github_cli_manual/markdown/` — official GitHub CLI manual converted to Markdown.
- `docs/04_local_gh_cli_help/markdown/` — local installed `gh` CLI help captures.

## Boundary

This hub contains documentation only. It does not create SOP files, backlog files, task files, or Codi queue files.
