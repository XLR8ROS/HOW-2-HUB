# Visitor Access plugin reference
Source: https://docs.openclaw.ai/plugins/reference/visitor-access

<!-- Generated file. Do not edit by hand.
Run `pnpm plugins:inventory:gen` to rebuild it. Hand-written text survives only
between the openclaw-plugin-reference:manual-start and
openclaw-plugin-reference:manual-end comment markers. -->

Manage expiring visitor grants through one Cloudflare Access email policy.

## Distribution

- Package: `@openclaw/visitor-access`
- Install route: source checkout only

## Surface

- Contracts: `tools`

<!-- openclaw-plugin-reference:manual-start -->

GitHub login lookups use the Gateway's configured GitHub API credential
(`gateway.controlUi.github.token`, or `GH_TOKEN`/`GITHUB_TOKEN`). Rate-limit errors
report the retry/reset time and suggest configuring the credential when absent.

<!-- openclaw-plugin-reference:manual-end -->

---

