# XOS How-To Hub | Remote Desktop Commander, Mac Access & Agent MCP Integration

**Document type:** Operational How-To / architecture and implementation reference  
**Last reviewed:** November 9, 2026  
**Scope:** Desktop Commander local MCP; hosted Remote Desktop Commander; XOS Paperclip-agent access to the MacBook through an independently enrolled Tailscale service; multi-agent coordination; Google Drive/Stenographer prerequisites.  
**Status:** Documentation ready to file. **XOS Paperclip-agent Mac access is not accepted as production-complete.**  
**Source authority:** Vendor documentation for Desktop Commander and Tailscale; live Mac configuration and existing Paperclip issue evidence for XOS-specific facts; Global Memory Contract for memory rules. A How-To is not a substitute for the Constitution, SOP, Memory Contract, agent permissions, or Reg's approvals.

> **Important:** Desktop Commander is principally a **file, code, search, terminal and process** MCP. Do not describe its standard tool catalog as a graphical remote-control system with native keyboard, mouse and screen-view tools. Any separate computer-use/UI layer needs its own access model and exclusive-focus coordination.

---

## 1. What Desktop Commander actually does

Desktop Commander gives a supported MCP client access to operations performed **on a computer the user controls**, under the permissions of the account running the local device agent. It can inspect and change files, search a filesystem, run terminal commands, manage long-running processes and perform supported document operations. This is real host access, not ChatGPT's isolated working container.

There are **three distinct deployment patterns** in XOS:

| Pattern | Actual path | Purpose | Identity/trust boundary |
|---|---|---|---|
| **Local Desktop Commander MCP** | Local MCP client → stdio Desktop Commander server → Mac | Tools used by an MCP-compatible client running on the machine | Local user / client permissions |
| **Hosted Remote Desktop Commander** | ChatGPT/another MCP client → `https://mcp.desktopcommander.app/mcp` → paired device agent → local MCP engine | Existing external ChatGPT access to the Mac | Vendor OAuth/account, paired device and local OS permissions |
| **XOS dedicated tailnet MCP gateway** | Authenticated Paperclip issue-scoped agent → restricted Tailscale connection → XOS HTTP MCP gateway → local Desktop Commander stdio engine → Mac | Paperclip-native agents gain controlled Mac operations | Tailnet grant **plus** Paperclip own-agent/run/checkout and operation policy |

**Do not conflate these:** successful calls from the external ChatGPT Remote Desktop Commander connector do **not** establish that Paperclip Junior, Addie, Quan, or any other Paperclip agent can use the Mac. Likewise, an online Tailscale node does not prove the upstream MCP engine or native grants work.

## 2. Official documentation and software provenance

- [Desktop Commander Help Center](https://desktopcommander.app/help/)
- [Desktop Commander: overview and product](https://desktopcommander.app/)
- [Remote Desktop Commander official setup guide](https://github.com/desktop-commander/remote-desktop-commander/blob/main/docs/SETUP.md)
- [Remote Desktop Commander official README / tool families](https://github.com/desktop-commander/remote-desktop-commander)
- [Remote Desktop Commander hosted-service security policy](https://github.com/desktop-commander/remote-desktop-commander/blob/main/SECURITY.md)
- [Open-source local Desktop Commander MCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)
- [Local Remote Device explanation and session behavior](https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/main/src/remote-device/README.md)
- [Tailscale tsnet](https://tailscale.com/docs/features/tsnet) and [tsnet.Server API](https://tailscale.com/docs/reference/tsnet-server-api)
- [Tailscale grants and least privilege](https://tailscale.com/docs/features/access-control/grants)

**Vendor distinction:** the local `@wonderwhy-er/desktop-commander` MCP implementation is open source. The hosted relay service is proprietary; its repository publishes documentation and manifests, not the service implementation. Commands and tool schemas can change between versions; verify against the installed server and current official docs before execution.

## 3. Requirements and normal setup

### Hosted Remote Desktop Commander for ChatGPT or another remote MCP client

**Requirements:** the target Mac/PC/Linux host, Node.js 18 or newer for the vendor's `npx` agent, a Remote Desktop Commander account, and a compatible remote MCP client.

1. On a computer you control, install an approved Node.js version if necessary. In a terminal, start the remote device agent:

   ```bash
   npx @wonderwhy-er/desktop-commander@latest remote
   ```

2. The vendor's device authorization flow presents a code in the terminal and browser. **Only approve if both codes match**, then sign in to the intended Desktop Commander account.
3. In the remote MCP-capable client, connect to:

   ```text
   https://mcp.desktopcommander.app/mcp
   ```

   Complete the corresponding OAuth sign-in using the **same intended account**. Client-specific settings vary by platform and plan; prefer the current vendor setup guide rather than assuming menu labels.
4. Confirm that the correct device is online at [Remote Desktop Commander device management](https://mcp.desktopcommander.app/). Run a harmless file listing or system-information read on that device and inspect the returned result.
5. Keep the device agent available as required. Disconnecting the device process does not necessarily revoke prior credentials. Use the dashboard to revoke a device when access should end. `remote --logout` clears local stored authorization but, according to the vendor, is not itself server-side device revocation.

**Do not install a second remote service unnecessarily** if the intended Mac's agent is already paired and online; inventory the existing launchd entries first. Do not revoke a device or restart the Mac as a troubleshooting shortcut.

### Local Desktop Commander MCP

Local MCP clients generally launch the server via an `npx` stdio command:

```bash
npx -y @wonderwhy-er/desktop-commander@latest
```

Check the official local repository for setup syntax for each client. It uses the local OS account's permissions and is not automatically available to another XOS machine or agent merely because the package is installed.

## 4. Supported tool classes

The available catalog depends on the vendor version, client and allowed configuration. Common classes:

| Area | Examples | Operational consequence |
|---|---|---|
| Files | `read_file`, `read_multiple_files`, `write_file`, `move_file`, `create_directory`, `get_file_info` | Read/write actual host files; changes can affect other agents |
| Search | `start_search`, `get_more_search_results`, `stop_search`, active search listing | Potentially lengthy host I/O; collect results by search/session ID |
| Code edits | `edit_block` | Make targeted edits with matching context and readback |
| Terminal | `start_process`, `interact_with_process`, `read_process_output` | May execute real commands; process startup alone does not prove task completion |
| Sessions/processes | `list_sessions`, `list_processes`, `force_terminate`, `kill_process` | Can affect another agent's work; verify process owner and authorization |
| Documents | Supported PDF/file operations, where exposed | Respect file-type-specific creation/edit instructions |
| Account/device | `list_devices`, account/usage tools | Confirm account, online device and intended target |
| Configuration | `get_config`, `set_config_value` | Restrictions and behavior change for subsequent requests; controlled change only |
| Device shutdown | Remote agent shutdown/disconnect where exposed | **Never** confuse stopping remote access with stopping an individual task; requires explicit user direction |

Tool names, arguments and availability must be discovered from the installed client or the live MCP `tools/list` result; the examples above are not a promise that every client exposes all methods. Beware of tool results indicating a **process is still running**: use the returned PID/session to inspect actual output. If a remote MCP call has its own `call_id`, query its status instead of automatically repeating a potentially side-effecting call.

## 5. Current XOS MacBook implementation — observed November 9, 2026

These are **observations**, not blanket configuration instructions or proof of acceptance:

| Component | Live observed location / state | Interpretation |
|---|---|---|
| Hosted Remote Desktop Commander | `MacBookPro.lan` online, observed device `21df6463-89f4-44fc-8313-c00f6236df94`, agent app `0.3.1` | External ChatGPT Remote MCP route exists. Re-discover device IDs each session; older plan documents show a different device reference. |
| Existing remote-agent launch configurations | `~/Library/LaunchAgents/com.xos.desktop-commander-remote.plist` and `~/Library/LaunchAgents/com.xos.desktopcommander.remote.plist` | Two launch configurations are present. Do not merge, remove or restart without checking which is authoritative. |
| Local XOS MCP HTTP gateway | `~/.xos/xos-desktop-mcp-gateway/gateway.mjs` | Locally bound to `127.0.0.1:7876` and delegates to the stdio MCP engine. Read-only SHA-256 at inspection: `e0d7ed4fa04c91e3db0aa8e78249ed1eb9508b2e2eb44d4bc895d51f425e6b8e`. |
| Gateway health | `GET http://127.0.0.1:7876/health` returned HTTP 200 with `upstreamConnected:false` and `registeredTools:0` | **The listener is alive, but upstream MCP execution was not ready at the check. Do not claim agent tool access is working.** |
| Local `/mcp` | Unauthenticated/incorrect-method GET returned 404 | This is **not** a successful authorized MCP request or an indication that POST authorization works. |
| Dedicated tsnet service | `~/.xos/xos-desktop-tsnet/main.go`, binary and separate state directory | Source defines independent `xos-desktop-mcp` tsnet hostname, tailnet TLS `:443`, and reverse proxy to local gateway. |
| Tailscale visibility | `tailscale status --json`: main Tailscale `Running`; `xos-desktop-mcp` and `paperclip-xos` seen online as separate tailnet nodes | Node presence is confirmed. Tailnet grants, TLS accessibility from the approved agent runtime, authentication and tool results **not accepted**. |
| Paperclip CLI/server | Local Paperclip API `127.0.0.1:3100`, XOS run-scoped identity | Must validate actual agent, company, live run and issue checkout for each native operation. |
| Paperclip project work | XOS-144 plan, XOS-250 connector verification, Alpha Senior owner | Plan exists and local technical work started. XOS-250 is not a completed acceptance. |

**Existing Paperclip plan:** XOS-144 document `remote-desktop-tsnet-integration-plan-20261109`, revision `853e2980-2f60-4e63-8bb6-512c52dbdbbe`. Read its current revision before changing any code. **XOS-250** is the existing verification issue; do not duplicate it with another investigation. The gateway source or issue status can change later; update this section with fresh readback before relying on it.

### XOS-specific request flow

```text
Paperclip task and authenticated agent (own agentId + RUNNING runId + checkout)
           |
           v
Approved XOS MCP connection / access grant
           |
           v
Dedicated Tailscale node xos-desktop-mcp (TLS :443, tailnet grants)
           |
           v
Local XOS MCP HTTP gateway (127.0.0.1:7876 /mcp)
           |
           v
Original Desktop Commander local stdio MCP process
           |
           v
MacBook filesystem / shell / process result
           |
           v
One true issue-scoped Paperclip receipt and target readback
```

The current gateway source validates `GET /api/agents/me`, `GET /api/heartbeat-runs/{runId}`, a `RUNNING` run, the run's issue ID, issue assignee and `checkoutRunId`, an `in_progress` issue and configured operation grants. Those checks must be retained, not bypassed simply because the requesting network address belongs to the tailnet.

**Observed gap:** the local gateway reported no connected upstream tools. Also, the original plan's accepted remote/Tailscale/Paperclip-grant tests have not been demonstrated in an own-agent scope. Do not treat gateway health HTTP 200 or successful node enrollment as a completed implementation.

## 6. Paperclip identity, permissions and checkout

For every agent-originated Mac operation:

1. Use the existing legitimate Paperclip heartbeat for the agent's **own** identity. Confirm the target issue and company.
2. Verify run status is `running`; the task is assigned, checked out to that run and eligible. Do not borrow the Board account or Alpha Senior's identity for another agent.
3. Require a scoped MCP grant for that agent **and** the actual operation. A tailnet address is a network assertion, not a Paperclip identity or task authorization.
4. For mutating operations, establish explicit authority for the file, process, service or account affected. Respect Reg-only Board approvals for protected/high-risk changes.
5. Record tool name, resource, sanitized result, exact run ID, and authoritative effect readback. If the tool call was blocked before reaching the device, record it as **not executed**.
6. Never convert an HTTP 200, process exit 0 or command delivery into a claim that a build or runtime task was accepted.

Never paste API bearer tokens, OAuth refresh tokens, Keychain secrets, device pairing codes, or raw credential values into the How-To Hub, an issue comment, or the agent's prompt.

## 7. Multiple XOS agents on one Mac: concurrency contract

**Desktop Commander does not automatically supply the XOS cross-agent isolation needed for simultaneous Paperclip agents.** Standard vendor documentation describes tool execution, not an XOS-wide transactional lock manager. Concurrency below is an XOS implementation requirement, **not** a vendor feature claimed to be installed.

| Situation | Recommended coordination |
|---|---|
| Different agents read independent files | Permit concurrent reads, subject to system load and permissions. |
| Two agents write the **same file** | Exclusive resource lock, version/hash precondition, write/readback, then release. Avoid overwriting changes. |
| Two agents edit separate files in one codebase | Parallel work possible, but enforce Git working-tree/branch ownership and prevent conflicting commits or migrations. |
| Two agents operate the same service/database/process | Per-service lock with approved change window and deterministic owner. |
| One agent launches a long-running process | Return a process/session identifier; avoid killing or reusing another agent's process without authority. |
| Two agents use an additional graphical computer-use layer | Only one agent may own keyboard/mouse/application focus at a time. This is a rule for that separate UI layer, not a native guarantee of standard Desktop Commander. |
| Conflicting tasks arrive together | Queue; do not discard either task. Release resources on verified completion, cancellation or an expired/reconciled lease. |

**Coordinator design:** resource keys such as `device:MacBookPro`, `file:/canonical/path`, `repo:<repo>`, `service:<label>`, `database:<db>`, `ui:desktop`; shared-read/exclusive-write semantics; separate priority and fairness policy; lease owner `(agentId, runId, issueId)`, creation/expiry, and audit log. Include a safe stale-lease recovery that **first** checks whether the old operation had an effect. No automatic replay of an unverified write.

The coordinator should allow independent, safe reads in parallel. It should not hold a global Mac lock for the entire duration of an agent's reasoning or a Paperclip issue's `In Progress` status.

## 8. Operational read-only checks and commands

These commands are examples for the **correct, authorized host**; adjust the actual paths to current installation. Do not blindly run write/restart commands as health checks.

```bash
# Installed Node, vendor version, and current remote device (read only)
node --version
npx @wonderwhy-er/desktop-commander --version

# Check main tailnet and separate service nodes (read only)
tailscale status

# Check local gateway listener and its actual upstream readiness
curl --fail --silent --show-error http://127.0.0.1:7876/health

# Check config files without altering launchd services
plutil -p "$HOME/Library/LaunchAgents/com.xos.desktop-commander-remote.plist"
plutil -p "$HOME/Library/LaunchAgents/com.xos.desktopcommander.remote.plist"

# Inspect whether runtime processes are present (presence != successful MCP operation)
pgrep -af 'desktop-commander|xos-desktop-tsnet|xos-desktop-mcp-gateway'
```

**Warning:** `npx ... --version` may fetch a package depending on local installation/cache. For strictly offline inspection use the already installed executable/package metadata. Do not run install, uninstall, service restart, revoke, device logout, or permissions update as a mere diagnostic.

### Expected acceptance evidence (existing XOS-250)

1. Right Mac and dedicated tailnet node independently verified. Network access permitted only from approved source agents/devices, without Funnel/public Internet exposure.
2. Gateway's MCP upstream is connected and returns the real local Desktop Commander `tools/list` results. `upstreamConnected:true` with actual tool count is necessary but not sufficient.
3. Authorized Paperclip agent with a current, own-agent, issue-scoped checkout invokes **one harmless native READ** over the intended remote route; verify genuine returned data.
4. Authorized agent performs **one separately authorized controlled WRITE** to a scratch location and rereads the exact resulting bytes.
5. An authorized process invocation returns process output/exit evidence, not just a sent command.
6. Negative paths demonstrate wrong agent/run, stopped run, wrong issue checkout, unavailable tool grant and disallowed resource are denied.
7. A second agent can run an independent read while conflicting writes are serialized without corruption or starvation.
8. Service restart persistence is verified only when a separately authorized service change is actually required and permitted. Do not restart the Mac, Paperclip, or Desktop Commander solely to manufacture evidence.
9. Evidence is preserved on the existing XOS-250 source issue under the actual executing agent's own live run. Alpha Senior performs technical ownership; Reg accepts any separately gated final release decision.

## 9. Troubleshooting / safe recovery

| Symptom | Meaning to investigate | Next authorized action |
|---|---|---|
| Device offline in hosted dashboard | Remote device agent absent, disconnected, wrong account or pairing state | Confirm exact paired device and process; restore only the authorized agent service if permitted. |
| Wrong computer selected | Two similar device entries or old pairing references | Re-run `list_devices`, verify host/device identity; never hardcode historical device IDs. |
| ChatGPT permission approval prompt | Client-side approval for a particular tool invocation | Inspect action/account/resource and use platform controls; do not bypass client approval checks. |
| Local `/health` returns 200 but `upstreamConnected:false` | HTTP listener works but local MCP engine is not ready | Inspect the upstream stdio process and sanitized logs before declaring access available. |
| Tailscale node online but MCP call fails | Reachability, TLS, grants, path/method and Paperclip authorization are distinct | Check exact layer and denial result; do not expand grants speculatively. |
| HTTP 401/403 | Missing/invalid credential, wrong agent/run/checkout or denied operation | Confirm authentic identity and grant; no borrowed agent credential or Board impersonation. |
| HTTP 404 on GET `/mcp` | Wrong method/path or gateway routing; may be expected | Discover supported MCP transport/method; test through real authenticated MCP client. |
| Two agents edit same path | Race, lost update or Git conflict | Queue exclusive write; preserve all versions; reconcile actual outcome before retry. |
| Tool call still running / timed out | Process or remote tool may have performed an effect | Poll returned session/call ID; inspect authoritative state before retrying or canceling. |
| macOS permission denial | OS filesystem/privacy/security controls may restrict the daemon | Route precise, permitted permission request to owner; do not grant broad privileges as workaround. |
| Competing Mac-agent launch services | Risk of wrong device/reconnect/session overlap | Inspect launchd labels, ownership and current connection. Do not remove or restart blindly. |

Rollback must preserve working hosted remote access and the separate Paperclip tsnet service. Treat any authorization failure or unknown effect as a distinct incident; do not use generic status `Done`.

## 10. Dependency on Google Drive, Stenographer and the Global Memory Contract

**Reg's release sequencing, November 9, 2026:**

| Sequence | Work | Existing Paperclip issues | Placement |
|---|---|---|---|
| First | MacBook access for Paperclip agents through Remote Desktop Commander | XOS-144 plan; XOS-250 remaining integration/verification | Final V0.4.1 prerequisite |
| Next | Google OAuth scope/account groundwork; authorized Google Drive/Docs access | XOS-33, XOS-212, XOS-213, XOS-27, XOS-28, XOS-12 | Beginning of V0.5, **before Stenographer** |
| Then | Stenographer capture liveness, agent enrollment, input adapters and verification | XOS-155 plan; XOS-214 build; XOS-215 verify | Subsequent V0.5 work |
| Thereafter, under the existing contract | Weave/finalize live Daily Notes, complete episodic promotion, chunk/index and retrieval | Established Global Memory Contract, not new duplicate memory storage design | Contract-driven lifecycle |

**Why Google Drive goes first:** during the active day the live Daily Note is the agent's designated Google Doc in its Google Drive folder when available. `WDN` appends to that working Google Doc, **not** directly to the finalized repository Markdown or the Durable Memory corpus. Missing Drive authority should use a documented non-destructive fallback rather than silently changing the lifecycle.

### Two source-capture paths, one preservation contract

```text
Paperclip-managed agents                    External ChatGPT agents
  |                                           |
  | Paperclip tasks, comments, tool/run       | Authorized ChatGPT conversation,
  | activity, task-backed transcripts         | recoverable chat/project episodes,
  | and events with own run attribution       | external actions and tool results
  v                                           v
  Paperclip-side Stenographer intake         Separate authorized ChatGPT intake
                  \                         /
                   \                       /
                 Chronological verbatim source + provenance
                                  |
                       Live Google Doc Daily Note
                         (WDN while day open)
                                  |
                  Verbatim weave and verified day closure
                                  |
                 Canonical finalized repository Markdown
                                  |
                Complete Durable Memory episodic promotion
                                  |
                     Chunk / embed / index / retrieve
                         (source kept whole)
```

These are **distinct acquisition adapters, not distinct memory contracts**. The Stenographer issue explicitly calls for Paperclip capture independent of optional Mirror/model routing and a **separate authorized ChatGPT conversation-history adapter**. Current Stenographer config was observed with `chatgpt_source: mirror`, two configured agents, and a journal/event path, so dynamic enrollment and live external capture cannot be assumed complete. Any historical ticket marked Done is not proof of new end-to-end acceptance.

The authoritative **Global Memory Contract** requires preserving **every recoverable substantive episode**, including corrections, failed attempts, unimportant-looking details and tool outcomes. It does **not** promote only an LLM-selected subset. The daily workflow is:

1. Capture source records and operational WDN material while the day is open.
2. Weave all recoverable chronology into the live Google Doc, preserving source identity/time and media references.
3. Verify and finalize canonical Markdown in the agent repository.
4. Promote the full preserved source into Durable Memory; only exact technical duplicates may be suppressed without information loss.
5. Chunk, embed and index for search. Retrieval may be selective; preservation is not.

Do not use Desktop Commander as an invented memory repository or bypass the established canonical storage/retrieval rules. It supplies authorized **Mac access**, which the capture and promotion processes may need for local source files, services and maintenance.

## 11. Ownership and change protocol

- **Alpha Senior** owns XOS-144 technical planning and XOS-250 remaining Desktop Commander implementation/verification, with its own proper Paperclip agent identity/run.
- **Reg** owns actual Board approvals, scope-expanding permissions and final acceptance. User authorization for the task is not authorization to impersonate another agent or disable platform/security checks.
- Other agents may execute only their own delegated tasks under verified runs and grants. Keep Plan and Build distinct where the existing Paperclip workflow requires them; do not duplicate accepted plans or create extra review stages.
- **Coco** coordinates executive priority and Master/workbook alignment but does not claim Alpha Senior's Mac implementation as its own completed work.
- Preserve the original live installation, existing two hosted-agent launch files and tsnet states. No Mac reboot, shutdown, external account revoke, or destructive permission change without separate explicit consent.

## 12. Before marking production-ready

**Never accept the integration solely because** the vendor device is online, Tailscale sees `xos-desktop-mcp`, the gateway responds HTTP 200, a client sends a message, or a subprocess exits successfully.

Accept only with complete source-attributed evidence demonstrating agent permission enforcement, real authorized read/write/process execution, conflict-safe concurrency, recovery, and source issue readback. Apply Reg's own approval when the change falls under a Board gate. Update the How-To with final exact code revisions and owner-approved operational procedures when those gates are actually met.

---

## Reference index

1. Desktop Commander Help: https://desktopcommander.app/help/
2. Hosted Remote MCP setup: https://github.com/desktop-commander/remote-desktop-commander/blob/main/docs/SETUP.md
3. Remote MCP README: https://github.com/desktop-commander/remote-desktop-commander
4. Security policy: https://github.com/desktop-commander/remote-desktop-commander/blob/main/SECURITY.md
5. Local MCP repository: https://github.com/wonderwhy-er/DesktopCommanderMCP
6. Remote Device lifecycle: https://github.com/wonderwhy-er/DesktopCommanderMCP/blob/main/src/remote-device/README.md
7. Tailscale tsnet: https://tailscale.com/docs/features/tsnet
8. Tailscale grants: https://tailscale.com/docs/features/access-control/grants
9. Google Drive scopes: https://developers.google.com/workspace/drive/api/guides/api-specific-auth
10. Google OAuth server-side flow: https://developers.google.com/identity/protocols/oauth2/web-server
11. Google Drive changes: https://developers.google.com/workspace/drive/api/guides/manage-changes
12. XOS local canon: `~/XOS-GitHub/reginaldberry02-sys/CocoCore/Global Memory Contract.md` (also verify the matching XOS HQ authoritative canon and agent copies)
13. Paperclip: XOS-144 (`remote-desktop-tsnet-integration-plan-20261109`), XOS-250, XOS-33, XOS-12, XOS-27, XOS-155, XOS-214, XOS-215

*End of How-To. This Markdown is an original operational consolidation with source links, not a wholesale copy of proprietary documentation.*
