# OpenCode Go
Source: https://docs.openclaw.ai/providers/opencode-go

OpenCode Go is a separate paid subscription inside [OpenCode](/providers/opencode).
It uses the same `OPENCODE_API_KEY` credential infrastructure as Zen, but a Zen
key does not automatically include Go entitlement. Go keeps its own runtime
provider id (`opencode-go`) so upstream per-model routing stays correct.
OpenCode Go is bundled in the OpenClaw package, so onboarding
and configuration are sufficient; no separate plugin install is required.

| Property         | Value                                              |
| ---------------- | -------------------------------------------------- |
| Runtime provider | `opencode-go`                                      |
| Plugin           | Bundled (`opencode-go`)                            |
| Auth             | `OPENCODE_API_KEY` (alias: `OPENCODE_ZEN_API_KEY`) |
| Parent setup     | [OpenCode](/providers/opencode)                    |

## Getting started

OpenCode Go is already included with OpenClaw. Continue with
interactive onboarding or pass the shared OpenCode API key directly.

Tabs

  
Interactive

    
Steps

      
Run onboarding

        ```bash
        openclaw onboard --auth-choice opencode-go
        ```
      
      
Set a Go model as default

        ```bash
        openclaw config set agents.defaults.model.primary "opencode-go/kimi-k3"
        ```
      
      
Verify models are available

        ```bash
        openclaw models list --provider opencode-go
        ```
      
    
  

  
Non-interactive

    
Steps

      
Pass the key directly

        ```bash
        openclaw onboard --opencode-go-api-key "$OPENCODE_API_KEY"
        ```
      
      
Verify models are available

        ```bash
        openclaw models list --provider opencode-go
        ```
      
    
  

## Config example

```json5
{
  env: { vars: { OPENCODE_API_KEY: "YOUR_API_KEY_HERE" } }, // pragma: allowlist secret
  agents: { defaults: { model: { primary: "opencode-go/kimi-k3" } } },
}
```

## Catalog

Run `openclaw models list --provider opencode-go` for the current model list.
OpenClaw shows every model ID Go's model list advertises and enriches it with
metadata from `https://models.opencode.ai/api.json`, so new models appear without
an OpenClaw update. IDs the metadata does not describe yet use Go's
OpenAI-compatible route with default limits. OpenClaw also identifies itself with
its `openclaw/<version>` User-Agent on model-list requests. The upstream catalog is downloaded and
cached only when OpenCode Zen or Go is configured or explicitly selected with
OpenCode credentials; it is never fetched at startup or while using unrelated
providers.

Example refs include `opencode-go/deepseek-v4.1-flash`, `opencode-go/kimi-k3`, and
`opencode-go/qwen3.8-max`. Use the CLI for the current lineup rather than treating
these examples as an inventory. OpenClaw excludes deprecated rows from active
discovery and applies refreshed lifecycle status to its offline fallback.
Bundled preview rows stay hidden until accepted upstream metadata supplies them.
Existing explicit refs in the bundled seed remain resolvable.

The Go model-list endpoint is a general inventory, not an account-entitlement
check. A successful listing does not grant access: inference still requires an
active Go subscription, including for promotional models.

DeepSeek V4 models apply the same thinking controls in agent turns and standalone
completions. Explicit `off` disables native thinking and removes reasoning from
replayed history; enabled thinking preserves the reasoning needed for follow-up turns.
Both paths also omit unsupported controls for MiniMax models with fixed reasoning
and remove Kimi K2 reasoning replay fields.

## Endpoint outages

A 403 response containing `Upstream request failed: Endpoint is unavailable.` is
treated as a service failure, so configured fallbacks can run and the shared API
key stays available to other models. Genuine authentication refusals still follow
the normal sign-in and credential-cooldown behavior.

## Privacy

Retention and training policies vary by model. Review the current
[OpenCode Go privacy table](https://opencode.ai/docs/go/#privacy) before using a
model, because provider policy can change independently of OpenClaw.

## Advanced configuration

AccordionGroup

  
Routing behavior

    OpenClaw selects each model’s API family and endpoint automatically; no extra
    provider config is required. Chat Completions and Responses use
    `https://opencode.ai/inference/go/openai/v1`, Anthropic Messages uses
    `https://opencode.ai/inference/go/anthropic` (the transport appends `/v1/messages`),
    and Gemini uses `https://opencode.ai/inference/go/google/v1beta`.

    Model discovery uses the separate
    `https://opencode.ai/inference/go/v1/models` inventory endpoint, not the
    inference base plus `/models`. Saved native Go URLs are normalized by each
    model’s API family; custom proxy URLs are left unchanged.

  

  
Runtime ref convention

    Runtime refs stay explicit: `opencode/...` for Zen, `opencode-go/...` for
    Go. This keeps upstream per-model routing correct across both catalogs.
  

  
Shared credentials

    The same `OPENCODE_API_KEY` can authenticate both runtime providers, so
    setup may store both profiles. Go access still requires a separate paid
    subscription in the OpenCode console.
  

Tip

See [OpenCode](/providers/opencode) for the shared onboarding overview and the full
Zen + Go catalog reference.

## Related

CardGroup

  
OpenCode (parent)

    Shared onboarding, catalog overview, and advanced notes.
  
  
Model selection

    Choosing providers, model refs, and failover behavior.

---

