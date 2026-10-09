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
## Contents

- `docs/00_github_docs_repo/markdown/` — root files from the official GitHub Docs repo.
- `docs/01_docs_github_com_content/markdown/` — official docs.github.com content from `github/docs/content`.
- `docs/02_reusables_and_variables/markdown/` — official GitHub Docs reusable/variable source material.
- `docs/03_github_cli_manual/markdown/` — official GitHub CLI manual converted to Markdown.
- `docs/04_local_gh_cli_help/markdown/` — local installed `gh` CLI help captures.

## Boundary

This hub contains documentation only. It does not create SOP files, backlog files, task files, or Codi queue files.
