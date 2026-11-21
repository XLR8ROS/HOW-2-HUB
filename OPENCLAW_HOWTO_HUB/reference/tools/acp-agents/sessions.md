# ACP agents sessions
Source: https://docs.openclaw.ai/tools/acp-agents/sessions

## Start ACP sessions

Two ways to start an ACP session:

Tabs

  
From sessions_spawn

    Use `runtime: "acp"` to start an ACP session from an agent turn or tool
    call.

    ```json
    {
      "task": "Open the repo and summarize failing tests",
      "runtime": "acp",
      "agentId": "codex",
      "thread": true,
      "mode": "session"
    }
    ```

    
Note

    `runtime` defaults to `subagent`, so set `runtime: "acp"` explicitly for
    ACP sessions. If `agentId` is omitted, OpenClaw uses `acp.defaultAgent`
    when configured. `mode: "session"` requires `thread: true` to keep a
    persistent bound conversation.
    

  
  
From /acp command

    Use `/acp spawn` for explicit operator control from chat.

    ```text
    /acp spawn codex --mode persistent --thread auto
    /acp spawn codex --mode oneshot --thread off
    /acp spawn codex --bind here
    /acp spawn codex --thread here
    ```

    Key flags:

    - `--mode persistent|oneshot`
    - `--bind here|off`
    - `--thread auto|here|off`
    - `--cwd <absolute-path>`
    - `--label <name>`

    See [Slash commands](/tools/slash-commands).

  

### `sessions_spawn` parameters

ParamField

  An admitted participant's requester_profile.id. Omit to keep the execution's original requester. Explicit selection uses that person's authority and authenticated requester facts; it does not establish their intent or approval.

ParamField

  Initial prompt sent to the ACP session.

ParamField

  Must be `"acp"` for ACP sessions.

ParamField

  ACP target harness id or configured ACP agent alias. Falls back to
  `acp.defaultAgent` if set. Raw harnesses create children under the requesting
  OpenClaw agent; configured aliases own their children. The harness remains
  the ACP runtime identity in either case.
  For cross-agent aliases, thread binding and inline delivery use the owner's bound channel account.
  A raw harness keeps the requesting agent's active inbound account.

ParamField

  Request thread binding flow where supported.

ParamField

  `"run"` is one-shot; `"session"` is persistent. If `thread: true` and
  `mode` is omitted, OpenClaw may default to persistent behaviour per
  runtime path. `mode: "session"` requires `thread: true`.

ParamField

  Requested runtime working directory (validated by backend/runtime policy).
  If omitted, ACP spawn inherits the OpenClaw owner's workspace when configured;
  missing inherited paths fall back to backend defaults, while real access
  errors are returned.

ParamField

  Operator-facing label used in session/banner text.

ParamField

  Resume an existing ACP session instead of creating a new one. The agent
  replays its conversation history via `session/load`. Requires
  `runtime: "acp"`. The ID must be recorded for the selected backend and harness and belong
  to the requester (the requester itself or a session it spawned or parented).
  Unknown IDs are rejected without enumerating the agent's sessions.
  Historical harness-owned records remain eligible under the same checks;
  spawning does not move or rewrite their histories. OpenClaw checks ownership
  again before initializing the resumed runtime.

ParamField

  `"parent"` streams initial ACP run progress summaries back to the requester
  session as system events. OpenClaw records the full relay history in the
  child agent's SQLite state and removes it with the child session. Parent
  progress streams show assistant commentary and ACP status progress by default unless
  `streaming.progress.commentary=false`. Discord parent progress requires an
  explicit `streaming.mode: "progress"`; unset Discord streaming stays quiet.
  Status progress still honors `acp.stream.tagVisibility`, so tags such as
  `plan` remain hidden unless explicitly enabled.

ACP `sessions_spawn` runs use `agents.defaults.subagents.runTimeoutSeconds`
for their default child turn limit. The tool does not accept per-call
timeout overrides (`runTimeoutSeconds`/`timeoutSeconds` are rejected with a
config-the-default error).

ParamField

  Explicit model override for the ACP child session. Codex ACP spawns
  normalize OpenAI refs such as `openai/gpt-5.4` to Codex ACP startup config
  before `session/new`; slash forms such as `openai/gpt-5.4/high` also set
  Codex ACP reasoning effort. When omitted, `sessions_spawn({ runtime: "acp" })`
  uses the target agent's `subagents.model`, then `agents.defaults.subagents.model`,
  then the target agent's explicit `model.primary`. If none is configured, it lets
  the ACP harness use its own default model. Native subagent spawns do not inherit
  an ACP agent's harness primary; they use native subagent settings or the native
  default instead. Other harnesses must advertise ACP model
  controls for an explicit selection. Without those controls, an explicit
  selection fails; an inherited default may be omitted so the harness can use
  its own default.

ParamField

  Explicit thinking/reasoning effort. For Codex ACP, `minimal` maps to low
  effort, `low`/`medium`/`high`/`xhigh` map directly, and `off` omits the
  reasoning-effort startup override. An explicit value takes precedence over
  a reasoning suffix in `model`, including `off`. When omitted, ACP spawns use existing
  subagent thinking defaults, the configured target agent's `thinkingDefault`, and per-model
  `params.thinking` for the selected model. The target agent's
  `agents.entries.<agent>.models["provider/model"]` setting overrides the shared
  `agents.defaults.models["provider/model"]` setting.

## Spawn bind and thread modes

Tabs

  
--bind here|off

    | Mode   | Behavior                                                               |
    | ------ | ----------------------------------------------------------------------- |
    | `here` | Bind the current active conversation in place; fail if none is active. |
    | `off`  | Do not create a current-conversation binding.                          |

    Notes:

    - `--bind here` is the simplest operator path for "make this channel or chat Codex-backed."
    - `--bind here` does not create a child thread.
    - `--bind here` is only available on channels that expose current-conversation binding support.
    - `--bind` and `--thread` cannot be combined in the same `/acp spawn` call.

  
  
--thread auto|here|off

    | Mode   | Behavior                                                                                            |
    | ------ | ------------------------------------------------------------------------------------------------- |
    | `auto` | In an active thread: bind that thread. Outside a thread: create/bind a child thread when supported. |
    | `here` | Require current active thread; fail if not in one.                                                  |
    | `off`  | No binding. Session starts unbound.                                                                 |

    Notes:

    - On non-thread binding surfaces, default behavior is effectively `off`.
    - Thread-bound spawn requires channel policy support:
      - Discord/Telegram: `session.threadBindings.spawnSessions=true`
    - Use `--bind here` when you want to pin the current conversation without creating a child thread.

---

