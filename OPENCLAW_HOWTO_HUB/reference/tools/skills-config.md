# Skills config
Source: https://docs.openclaw.ai/tools/skills-config

Most skills configuration lives under `skills` in
`~/.openclaw/openclaw.json`. Agent-specific visibility lives under
`agents.defaults.skills` and `agents.entries.*.skills`.

```json5
{
  skills: {
    allowBundled: ["gemini", "peekaboo"],
    load: {
      extraDirs: ["~/path/to/agent-scripts/skills"],
      allowSymlinkTargets: ["~/path/to/skills"],
      watch: true,
    },
    install: {
      preferBrew: true,
      nodeManager: "npm",
      allowUploadedArchives: false,
    },
    entries: {
      "image-lab": {
        enabled: true,
        apiKey: { source: "env", provider: "default", id: "GEMINI_API_KEY" },
        env: { GEMINI_API_KEY: "GEMINI_KEY_HERE" },
      },
      peekaboo: { enabled: true },
      sag: { enabled: false },
    },
  },
}
```

Note

  For built-in image generation, use `agents.defaults.mediaModels.image`
  plus the core `image_generate` tool instead of `skills.entries`. Skill
  entries are for custom or third-party skill workflows only.

## Loading (`skills.load`)

ParamField

  Additional skill directories to scan, at the lowest precedence (below
  bundled and plugin skills). Paths are expanded with `~` support.

ParamField

  Trusted real target directories that symlinked skill folders may resolve
  into, even when the symlink lives outside the configured root. Use this for
  intentional sibling-repo layouts such as
  `<workspace>/skills/manager -> ~/path/to/skills`. Keep this list
  narrow — do not point at broad roots like `~` or a whole projects directory.

ParamField

  Enable automatic skill discovery from filesystem events, including nested files
  under grouped roots. A safety rescan every 30 minutes catches missed events.
  Set to `false` to disable automatic observation. Explicit OpenClaw skill changes,
  relevant configuration changes, and Gateway startup still request an immediate
  rescan. Existing sessions use changed snapshots on their next agent turn.

## Install (`skills.install`)

ParamField

  Prefer Homebrew installers when `brew` is available.

ParamField

  Node package manager preference for skill installs. This only affects skill
  installs. Node remains the primary and recommended OpenClaw runtime; Bun 1.4.4+
  with WAL-reset-safe `node:sqlite` is supported as an explicit runtime opt-in.
  `openclaw setup --node-manager` and `openclaw onboard --node-manager` accept
  `npm`, `pnpm`, or `bun`; set `"yarn"` directly in config for Yarn-backed skill
  installs. Setup preserves this preference unless you pass `--node-manager`;
  fresh configurations default to `npm`.

ParamField

  Allow trusted `operator.admin` Gateway clients to install private zip
  archives staged through `skills.upload.*`. Normal ClawHub installs do not
  need this setting.

## Operator Install Policy (`security.installPolicy`)

Use `security.installPolicy` when operators need a trusted local command to
approve or block skill and plugin installs with host-specific policy. The
policy runs after OpenClaw has staged source material and before the install
or update continues. It applies to ClawHub skills, uploaded skills, Git/local
skills, skill dependency installers, and plugin install/update sources.

```json5
{
  security: {
    installPolicy: {
      enabled: true,
      // Omit targets to cover every supported target.
      targets: ["skill", "plugin"],
      exec: {
        source: "exec",
        command: "/usr/local/bin/openclaw-install-policy",
        args: ["--json"],
        timeoutMs: 10000,
        noOutputTimeoutMs: 10000,
        maxOutputBytes: 1048576,
        passEnv: ["OPENCLAW_STATE_DIR", "PATH"],
        env: { POLICY_MODE: "strict" },
        trustedDirs: ["/usr/local/bin"],
      },
    },
  },
}
```

ParamField

  Enables operator-owned install policy. When enabled without a valid `exec`
  command, installs are blocked.

ParamField

  Optional target filter. When omitted, policy applies to every supported
  target so new installs do not unexpectedly fail open.

ParamField

  Absolute path to the trusted policy executable. OpenClaw runs it without a
  shell and validates the path before use.

ParamField

  Static arguments passed after `command`.

ParamField

  Maximum wall-clock runtime for one policy decision.

ParamField

  Maximum time without stdout or stderr output before the policy blocks the install.

ParamField

  Maximum combined stdout and stderr bytes accepted from the policy process.

ParamField
">
  Literal environment variables provided to the policy process.

ParamField

  Environment variable names copied from the OpenClaw process into the
  policy process. Only named variables are passed.

ParamField

  Optional allowlist of directories that may contain the policy executable.

The policy command and interpreter script arguments must be direct regular
files with trusted ownership, restricted permissions, and verifiable parent
directories. Symlinks and insecure paths are rejected.

The policy receives one JSON object on stdin with `protocolVersion: 1`,
`openclawVersion`, `targetType`, `targetName`, `sourcePath`, `sourcePathKind`,
optional structured `source`, structured `origin`, and `request`. It must
write one JSON object on stdout with an `allow`, `warn`, or `block` decision.
`warn` and `block` require a non-empty `reason`; every decision may include a
`findings` array. Each finding requires non-empty string `ruleId` and `message`
fields plus a `severity` of `info`, `warn`, or `critical`. Optional `file` and
`evidence` values must be non-empty strings; a finite numeric `line` is rounded
down and clamped to the safe-integer range from 1 through `Number.MAX_SAFE_INTEGER`.
Malformed finding entries are ignored, and
invalid optional fields are omitted. A non-array `findings` value is treated as
absent. Operator-facing reason and finding text are limited to 1,000 characters.
OpenClaw retains at most 100 normalized findings for display. Only a `warn`
response with more than 100 valid findings blocks installation and cannot be
acknowledged; `allow` and `block` retain the first 100. A warning stops the
install before commit. A `warn` review whose fully rendered notice, including
its title, target, sanitized reason and findings, and recovery guidance, exceeds
the 4,000-character aggregate display limit blocks installation without presenting a
partial review. An over-budget `block` remains terminal with a
bounded denial, while over-budget findings on `allow` are summarized in bounded
diagnostic output. Interactive CLI
plugin and skill commands ask the operator to type the target name using the
same `install anyway` or `update anyway` copy as suspicious ClawHub releases,
then run policy again before continuing. Declined and non-interactive commands
on the direct CLI may use `--acknowledge-install-policy-warning` as explicit
approval after review for every warning in that command invocation;
every approved warning is re-evaluated before continuing.
The Control UI can review and approve warnings for its plugin install request;
that approval covers every warning in the invocation, and each warning is
still re-evaluated. Other Gateway-backed and automatic installs remain blocked
when they have no operator-confirmation flow. Use an equivalent direct plugin
or skill command to review and approve the warning when one exists. Otherwise,
change `security.installPolicy` to return `allow` for the reviewed request,
then retry the managed flow. `--force` does not approve policy warnings. A `block`,
non-zero exit, timeout, invalid JSON, non-object response, missing or invalid
protocol version or decision, or missing or empty `warn`/`block` reason always
blocks installation.

OpenClaw does not execute install policy during normal Gateway startup.
Installs and updates are blocked when policy is enabled but unavailable.
`openclaw doctor` performs static validation; `openclaw doctor --deep`
executes a synthetic install check against the configured command.

Bulk updates apply policy per target: a blocked skill or plugin update fails
that target without disabling the policy or skipping later targets in the
batch.

Example stdin:

```json
{
  "protocolVersion": 1,
  "openclawVersion": "2026.6.1",
  "targetType": "skill",
  "targetName": "weather",
  "sourcePath": "/var/folders/.../openclaw-skill-clawhub/root",
  "sourcePathKind": "directory",
  "source": {
    "kind": "clawhub",
    "authority": "openclaw",
    "mutable": false,
    "network": true
  },
  "origin": {
    "type": "clawhub",
    "registry": "https://clawhub.openclaw.ai",
    "slug": "weather",
    "version": "1.0.0"
  },
  "request": {
    "kind": "skill-install",
    "mode": "install",
    "requestedSpecifier": "clawhub:weather@1.0.0"
  },
  "skill": {
    "installId": "clawhub"
  }
}
```

Minimal policy command:

```js
#!/usr/bin/env node

let input = "";
process.stdin.setEncoding("utf8");
process.stdin.on("data", (chunk) => {
  input += chunk;
});
process.stdin.on("end", () => {
  const request = JSON.parse(input);
  if (request.targetType === "plugin" && request.source?.kind === "local-path") {
    process.stdout.write(
      JSON.stringify({
        protocolVersion: 1,
        decision: "block",
        reason: "local plugin paths are not approved on this host",
      }),
    );
    return;
  }
  process.stdout.write(JSON.stringify({ protocolVersion: 1, decision: "allow" }));
});
```

## Bundled skill allowlist

ParamField

  Optional allowlist for **bundled** skills only. When set, only bundled
  skills in the list are eligible; an empty list disables all bundled skills.
  Managed, agent-level, and workspace skills are unaffected.

## Per-skill entries (`skills.entries`)

Keys under `entries` match the skill `name` by default. If a skill defines
`metadata.openclaw.skillKey`, use that key instead. Quote hyphenated names
(JSON5 allows quoted keys).

ParamField
.enabled" type="boolean">
  `false` disables the skill even when bundled or installed. The
  `coding-agent` bundled skill is opt-in — set it to `true` and check that one of
  `claude`, `codex`, `opencode`, or another supported CLI is installed and
  authenticated.

ParamField
.apiKey" type='string | { source, provider, id }'>
  Convenience field for skills that declare `metadata.openclaw.primaryEnv`.
  Supports a plaintext string or a SecretRef: `{ source: "env", provider: "default", id: "VAR_NAME" }`.

ParamField
.env" type="Record<string, string>">
  Environment variables injected for the agent run. Only injected when the
  variable is not already set in the process.

ParamField
.config" type="object">
  Optional bag for custom per-skill configuration fields.

## Agent allowlists (`agents`)

Use agent config when you want the same machine/workspace skill roots but a
different visible skill set per agent.

```json5
{
  agents: {
    ownership: "explicit",
    defaults: {
      skills: ["github", "weather"], // shared baseline
      systemAgent: { agentId: "writer" },
      authInheritance: { agentId: "writer" },
    },
    entries: {
      writer: { workspace: "~/.openclaw/workspace" }, // inherits github, weather
      docs: { skills: ["docs-search"] }, // replaces defaults entirely
      "locked-down": { skills: [] }, // no skills
    },
  },
  talk: { agentId: "writer" },
}
```

ParamField

  Shared baseline allowlist inherited by agents that omit
  `agents.entries.*.skills`. Omit entirely to leave skills unrestricted by
  default.

ParamField

  Explicit final skill set for that agent. Explicit lists **replace**
  inherited defaults — they do not merge. Set to `[]` to expose no skills for
  that agent.

Warning

  Agent skill allowlists are a visibility and loading filter for OpenClaw
  skill discovery, prompts, slash-command discovery, sandbox sync, and skill
  snapshots. They are not a shell-time authorization boundary. If an agent
  can run host `exec`, that shell can still run external clients or read
  host files that are visible to the execution user, including MCP client
  registries such as `~/.openclaw/skills/config/mcporter.json`. For
  per-agent MCP isolation, combine skill allowlists with sandbox/OS-user
  isolation, deny or tightly allowlist host exec, and prefer per-agent
  credentials at the MCP server.

<a id="workshop-skills-workshop" />

## Workshop settings

Skill Workshop is a bundled plugin, so its settings live under
`plugins.entries.skill-workshop.config`. Older configs kept them in
`skills.workshop`; `openclaw doctor --fix` moves them, and `openclaw update`
runs that repair for you.

ParamField

  `auto` lets agents save and update Workshop skills: a background review runs
  after substantial work, learned skills unused for 30 days are archived, and
  one oversized learned skill a day is [dieted](/tools/skill-workshop#skill-diet).
  Review changes appear as a **Learned** row in the Control UI chat, separately
  from the assistant’s answer and collapsed **Worked** activity. Older plain-text
  review notices also stay separate. Every change can be undone. `propose` runs
  the background review but saves its changes as
  [drafts](/tools/skill-workshop#drafts) to review with `/learn drafts`; it does
  not archive or diet skills. `off` disables the background review,
  unused-skill cleanup, and the skill diet. User-prompted skill creation, `/learn`, and manual
  learning sessions work in every mode.

ParamField

  When `true`, background review notices are posted to channel conversations
  (except Slack) with an **Undo** button; the Control UI shows that message as
  plain text. When `false`, they appear only as the **Learned** row in the
  Control UI chat. Saying "undo" works either way.

See [Self-learning](/tools/self-learning) for eligibility, privacy, cost,
and troubleshooting.

ParamField

  Maximum `SKILL.md` size in bytes for Workshop skills (allowed range:
  1024-200000). Skill descriptions are capped at 1024 bytes separately; keep
  them near 160 bytes because they appear in discovery and listing output.

`openclaw doctor --fix` also migrates configs from the removed proposal queue:
it maps `skills.workshop.autonomous.enabled: true` to `mode: "propose"`
(`false` to `"off"`) and deletes `skills.workshop.approvalPolicy` and
`skills.workshop.maxPending` before moving the remaining settings.

See [Skill Workshop](/tools/skill-workshop) for the skill lifecycle, CLI
commands, agent tool parameters, and Gateway methods this config controls.

## Symlinked skill roots

By default, workspace, project-agent, extra-dir, and bundled skill roots are
containment boundaries. A symlinked skill folder under `<workspace>/skills`
that resolves outside the root is skipped with a log message.

To allow an intentional symlink layout, declare the trusted target:

```json5
{
  skills: {
    load: {
      extraDirs: ["~/path/to/skills"],
      allowSymlinkTargets: ["~/path/to/skills"],
    },
  },
}
```

With this config, `<workspace>/skills/manager -> ~/path/to/skills`
is accepted after realpath resolution. `extraDirs` scans the sibling repo
directly; `allowSymlinkTargets` preserves the symlinked path for existing
layouts.

Skill Workshop uses each agent's `<state-dir>/agents/<agentId>/agent/workshop-skills`
containment boundary. It does not use `allowSymlinkTargets`, and it rejects
symlinked skills that resolve outside that directory.

Managed `~/.openclaw/skills` and personal `~/.agents/skills` directories
already accept skill-directory symlinks unconditionally (per-skill
`SKILL.md` containment still applies) — `allowSymlinkTargets` is only needed
for workspace, extra-dir, and project-agent (`<workspace>/.agents/skills`)
roots.

## Sandboxed skills and env vars

Warning

  `skills.entries.<skill>.env` and `apiKey` apply to **host** runs only.
  Inside a sandbox they have no effect — a skill that depends on
  `GEMINI_API_KEY` will fail with `apiKey not configured` unless the sandbox
  is given the variable separately.

Pass secrets into a Docker sandbox with:

```json5
{
  agents: {
    defaults: {
      sandbox: {
        docker: {
          env: { GEMINI_API_KEY: "your-key-here" },
        },
      },
    },
  },
}
```

Note

  Users with Docker daemon access can inspect `sandbox.docker.env` values
  through Docker metadata. Use a mounted secret file, a custom image, or
  another delivery path when that exposure is not acceptable.

## Loading order reminder

See [Loading order](/tools/skills#loading-order) for source precedence, including
the per-agent Workshop tier, and [Snapshots and refresh](/tools/skills#snapshots-and-refresh)
for when changes become visible.

## Related

CardGroup

  
Skills reference

    What skills are, loading order, gating, and SKILL.md format.
  
  
Creating skills

    Authoring custom workspace skills.
  
  
Skill Workshop

    Agent-learned skills, change history, and undo.
  
  
Self-learning

    Automatic, undoable skill learning from completed work.
  
  
Slash commands

    Native slash-command catalog and chat directives.

---

