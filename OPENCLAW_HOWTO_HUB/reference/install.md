# Install
Source: https://docs.openclaw.ai/install

## System requirements

- **Node 24.16.0+ on 24.x, or 26.1.0+** (24.22.1+/26.12.1+ strongly recommended for security) - Node 26 is recommended; the installer provisions Node 26 on macOS and Node 24 LTS on Linux when Node is missing (see [Node.js compatibility](/install/node-compatibility)).
- **macOS, Linux, or Windows** - Windows users can start with the native Windows Hub app, the PowerShell CLI installer, or a WSL2 Gateway. See [Windows](/platforms/windows).
- `pnpm` is only needed if you build from source.

## Download the desktop app

Prefer a normal app download over the CLI? OpenClaw ships desktop companions:

- **Windows (recommended)**: the native [Windows Hub](/platforms/windows#recommended-windows-hub) companion app — a signed installer you download and run like any Windows app, with setup, tray status, chat, and node mode:
  - [OpenClawCompanion-Setup-x64.exe](https://github.com/openclaw/openclaw-windows-node/releases/latest/download/OpenClawCompanion-Setup-x64.exe)
  - [OpenClawCompanion-Setup-arm64.exe](https://github.com/openclaw/openclaw-windows-node/releases/latest/download/OpenClawCompanion-Setup-arm64.exe)
  - All Hub releases: [Windows Hub releases page](https://github.com/openclaw/openclaw-windows-node/releases/latest)
- **macOS**: the [macOS menu bar app](/platforms/macos) — download the `OpenClaw-<version>.dmg` (preferred) or `.zip` asset from [OpenClaw GitHub releases](https://github.com/openclaw/openclaw/releases), then install and launch **OpenClaw.app**. See the [macOS app page](/platforms/macos) for details, including what to do when the newest release ships no macOS asset.

On Windows, the cross-platform [Tauri desktop app](/platforms/windows#backup-tauri-desktop-app)
is the backup option. Its `OpenClaw-<version>-windows-x86_64.exe` installer ships
in regular [OpenClaw releases](https://github.com/openclaw/openclaw/releases)
and can set up a local Windows Gateway with bundled Bun or connect remotely.

Both native desktop apps can provision a local Gateway during first-run setup, or connect to an existing remote Gateway.

## Recommended: installer script

The fastest way to install. It detects your OS, installs Node if needed, installs OpenClaw, and launches onboarding.

Note

For Windows desktop setup, we recommend the native [Windows Hub](/platforms/windows#recommended-windows-hub) companion app, which includes setup, tray status, chat, node mode, and local MCP mode.

Tabs

  
macOS / Linux / WSL2

    ```bash
    curl -fsSL https://openclaw.ai/install.sh | bash
    ```
  
  
Windows (PowerShell)

    ```powershell
    iwr -useb https://openclaw.ai/install.ps1 | iex
    ```
  

To install without running onboarding:

Tabs

  
macOS / Linux / WSL2

    ```bash
    curl -fsSL https://openclaw.ai/install.sh | bash -s -- --no-onboard
    ```
  
  
Windows (PowerShell)

    ```powershell
    & ([scriptblock]::Create((iwr -useb https://openclaw.ai/install.ps1))) -NoOnboard
    ```
  

For all flags and CI/automation options, see [Installer internals](/install/installer).

## Alternative install methods

### Local prefix installer (`install-cli.sh`)

Use this when you want OpenClaw and Node kept under a local prefix such as
`~/.openclaw`, without depending on a system-wide Node install:

```bash
curl -fsSL https://openclaw.ai/install-cli.sh | bash
```

It supports npm installs by default, plus git-checkout installs under the same
prefix flow. Full reference: [Installer internals](/install/installer#install-clish).

Already installed? Switch between package and git installs with
`openclaw update --channel dev` and `openclaw update --channel stable`. See
[Updating](/install/updating#switch-between-npm-and-git-installs).

### npm, pnpm, or bun

If you already manage Node yourself:

Tabs

  
npm

    On npm 12 or npm 11.16+:

    ```bash
    npm install -g openclaw@latest --allow-scripts=openclaw
    openclaw onboard --install-daemon
    ```

    On npm 11.15 and earlier, use the same command without
    `--allow-scripts=openclaw`.

    
Note

    npm 12 blocks unapproved package lifecycle scripts by default. The
    `--allow-scripts=openclaw` option explicitly allows OpenClaw's `preinstall`
    and `postinstall` steps; without it, npm reports them as `blocked because
    they are not covered by allowScripts`.

    npm 11.16 accepts the option but otherwise only warns that the scripts are
    `not yet covered by allowScripts` and still runs them. npm 11.15 and earlier
    have neither the policy nor the option, so their command must be unflagged.
    The `npm approve-scripts openclaw`
    command suggested by npm 11.16 does not work for a global install — it fails
    with `ENOMATCH  No installed packages match: openclaw`.
    

    
Note

    The hosted installer clears npm freshness filters such as `min-release-age`
    for the OpenClaw package install. If you install manually with npm, your own
    npm policy still applies.
    

  
  
pnpm

    ```bash
    pnpm add -g --allow-build=openclaw openclaw@latest
    openclaw onboard --install-daemon
    ```

    
Note

    pnpm requires explicit approval for packages with build scripts. `approve-builds -g` is not supported for global installs, so pass `--allow-build=openclaw` on the `pnpm add -g` command instead.
    

  
  
bun

    ```bash
    bun add -g --trust openclaw@latest
    bun run --bun openclaw onboard --install-daemon --daemon-runtime bun
    ```

    
Note

    `--trust` allows OpenClaw's package lifecycle scripts for this install. Bun
    1.4.4 or newer can also run OpenClaw's CLI, local agent, and Gateway. Node
    remains the primary runtime, so the plain `openclaw` executable keeps its
    Node shebang. `bun run --bun` forces the Bun runtime, while
    `--daemon-runtime bun` installs the managed Gateway under Bun.
    

  

### From source

For contributors or anyone who wants to run from a local checkout:

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
corepack enable
pnpm install && pnpm build && pnpm ui:build
pnpm add --global "openclaw@link:$PWD"
openclaw onboard --install-daemon
```

`pnpm add --global "openclaw@link:$PWD"` links the CLI to this checkout without changing its package files. If pnpm reports that its global bin directory is not on `PATH`, run `pnpm setup`, reopen your shell, and retry.

For a server checkout that only runs OpenClaw, use `pnpm build:runtime` to build
the JavaScript, plugins, Control UI, and metadata without TypeScript declarations.
Use `pnpm build` for development or packaging that needs declarations and their
validation; CI typechecks still apply to runtime-only builds.

Corepack selects the exact pnpm version from `package.json` (currently pnpm 12).
If Corepack is unavailable, read that version from the checkout and install it explicitly:

```bash
pnpm_spec=$(node -p "require('./package.json').packageManager.split('+')[0]")
npm install -g "$pnpm_spec" --allow-scripts="$pnpm_spec"
```

The `+` suffix records Corepack's integrity hash and is not part of the npm package specifier.
Keep npm install scripts and optional dependencies enabled so pnpm can provision its native executable.

Or skip the global install and use `pnpm openclaw ...` from inside the repo. See [Setup](/start/setup) for full development workflows.

### Standalone builds

For application packaging or a deployment without a separate Node or Bun
installation, build an executable and companion runtime directory from source.
See [Standalone builds](/install/standalone) for modes, output files, signing,
and the update boundary.

### Install from the GitHub main checkout

```bash
curl -fsSL --proto '=https' --tlsv1.2 https://openclaw.ai/install.sh | bash -s -- --install-method git --version main
```

### Containers and package managers

CardGroup

  
Ansible

    Automated fleet provisioning.
  
  
Bun

    Optional dependency installer and package-script runner.
  
  
Docker

    Containerized or headless deployments.
  
  
Nix

    Declarative install via Nix flake.
  
  
Podman

    Rootless container alternative to Docker.
  

## Verify the install

```bash
openclaw --version      # confirm the CLI is available
openclaw doctor         # check for config issues
openclaw gateway status # verify the Gateway is running
```

If you want managed startup after install:

- macOS: LaunchAgent via `openclaw onboard --install-daemon` or `openclaw gateway install`
- Linux/WSL2: systemd user service via the same commands
- Native Windows: Scheduled Task first, with a per-user Startup-folder login item fallback if task creation is denied

## Next: run onboarding and connect a channel

CardGroup

  
Getting started

    Run onboarding, install the Gateway service, and open the dashboard.
  
  
Connect a channel

    Message your agent from Telegram, Discord, Slack, WhatsApp, and more.
  

## Hosting and deployment

Deploy OpenClaw on a cloud server or VPS. See [Linux server](/vps) for the full
provider picker (DigitalOcean, Hetzner, Hostinger, Fly.io, GCP, Azure, Railway,
Northflank, Oracle Cloud, Raspberry Pi, and more), deploy declaratively on
[Render](/install/render), or try the experimental [Cloudflare Containers](/install/cloudflare)
template.

CardGroup

  
Cloudflare

    Experimental Worker + Container deployment.
  
  
Docker VM

    Shared Docker steps.
  
  
Kubernetes

    K8s deployment.
  
  
macOS VM

    Isolated local or hosted macOS deployment.
  
  
Upstash Box

    Managed Linux host with SSH-tunneled access.
  
  
VPS

    Pick a provider.
  

## Back up, update, migrate, or uninstall

CardGroup

  
Backups

    Create, verify, and restore state archives.
  
  
Updating

    Keep OpenClaw up to date.
  
  
Migrating

    Move to a new machine.
  
  
Uninstall

    Remove OpenClaw completely.
  

## Troubleshooting: `openclaw` not found

Almost always a PATH issue: npm's global bin directory isn't on your shell's `PATH`. See [Node.js troubleshooting](/install/node#troubleshooting) for the full fix, including the Windows path.

```bash
node -v           # Node installed?
npm prefix -g     # Where are global packages?
echo "$PATH"      # Is the global bin dir in PATH?
```

---

