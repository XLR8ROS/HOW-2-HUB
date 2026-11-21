# XOS integration reference: OpenClaw, OpenAI Agents SDK, LiteLLM

Updated: 2026-11-20 (America/New_York). Informational documentation, not deployment or configuration authorization.

## Architecture distinction

OpenClaw has its own built-in agent runtime. It is not the OpenAI Agents SDK. An XOS design that uses both must define an explicit supported boundary. The existing XOS LiteLLM proxy is a separate LLM gateway and can serve both as an OpenAI-compatible endpoint. Do not assume OpenClaw agents, OpenAI SDK sessions, handoffs, authorization policies, or tool permissions automatically carry across that boundary.

## OpenClaw primary sources (local full copies)

- [OpenClaw architecture](reference/agent-runtime-architecture.md) | https://docs.openclaw.ai/agent-runtime-architecture
- [LiteLLM provider](reference/providers/litellm.md) | https://docs.openclaw.ai/providers/litellm
- [MCP client/server integrations](reference/tools/mcp.md) | https://docs.openclaw.ai/tools/mcp
- [A2A agents](reference/channels/a2a.md) | https://docs.openclaw.ai/channels/a2a
- [Gateway trust model](reference/gateway/security/trust-model.md) | https://docs.openclaw.ai/gateway/security/trust-model
- [Models](reference/concepts/models.md) | https://docs.openclaw.ai/concepts/models
- [Official complete documentation index](DOC_INDEX.md)

## Agents SDK primary sources (external, separate product)

- Models and OpenAI-compatible custom endpoints: https://openai.github.io/openai-agents-python/models/
- Model configuration: https://openai.github.io/openai-agents-python/config/
- SDK agents, tools and handoffs: https://openai.github.io/openai-agents-python/agents/
- Handoffs: https://openai.github.io/openai-agents-python/handoffs/
- Sessions: https://openai.github.io/openai-agents-python/sessions/
- SDK deterministic testing: https://openai.github.io/openai-agents-python/testing/

Use AsyncOpenAI(base_url=.../v1, api_key=virtual_key) and OpenAIChatCompletionsModel for an OpenAI-compatible LiteLLM proxy when the upstream Responses path is not verified. SDK LiteLLM adapter support is separate, best-effort/beta. Confirm tracing configuration for non-OpenAI providers, and preserve original XOS routing and model selection rules.

## LiteLLM primary sources (external, separate product)

- Proxy quickstart: https://docs.litellm.ai/docs/
- Model management: https://docs.litellm.ai/docs/proxy/model_management
- Client virtual keys and MCP: https://docs.litellm.ai/docs/proxy/client_setup/overview
- Router configuration, retries and fallbacks: https://docs.litellm.ai/docs/router/api_reference/configuration
- Native Responses passthrough: https://docs.litellm.ai/docs/response_api_native_passthrough

## Verification gates, not rollout instructions

1. Confirm the actual model alias and allowed provider in the LiteLLM model registry.
2. Confirm the actual proxy URL and virtual-key scope without placing credentials in documentation.
3. Exercise a non-destructive chat completion and verify an upstream result and recorded routing.
4. Test tool/function calling and structured output separately; protocol similarity is not feature parity.
5. Verify the Agents SDK uses the proxy for model calls and never silently reaches a different endpoint.
6. Test permission, session, message-channel, approval, and trace isolation as independent boundaries.
7. Verify no unapproved fallback or retry behavior. Do not weaken macOS security for convenience.
