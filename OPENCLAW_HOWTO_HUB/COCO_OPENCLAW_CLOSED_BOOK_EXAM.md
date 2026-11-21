XOS | COCO: OPENCLAW DEEP OPERATIONS CERTIFICATION
CLOSED BOOK | OFFICIAL DOCUMENTATION SNAPSHOT: 2026-11-20
100 questions | 100 possible points

RULES
- Do not consult documentation, search engines, assistants, source code or the answer key while taking the test.
- Do not run commands against the XOS Mac, Paperclip or production infrastructure.
- Answer in your own words. Pseudocode is permitted where requested.
- “I don't know” is better than fabricating an answer.
- Give exact commands, settings or boundaries when requested.
- Each answer is worth 1 point; half-credit for substantially correct but incomplete answers.
- Passing: 90/100, with no dangerous security or authorization recommendation.
- Questions marked [CRITICAL] require a correct safe answer.

SECTION I | INSTALLATION AND BOOTSTRAP (1-12)

1. Give the minimum supported Node 24 and Node 26 versions for the current OpenClaw CLI.
2. Which Node major versions are explicitly unsupported, and is Node 27 categorically rejected?
3. Name the more secure recommended Node patch floors and explain why the minimum-versus-recommended distinction matters.
4. Give the documented macOS/Linux installer command and its no-onboarding variant.
5. With npx openclaw@latest, what changes when the operator accepts versus declines “Keep OpenClaw running in the background”?
6. Name the CLI commands to install and start the persistent Gateway service and to verify it actually responds.
7. Is pnpm required for an ordinary packaged installation? When is it needed?
8. During LiteLLM-specific onboarding, what is the default proxy location and how is the first model chosen?
9. Distinguish the default OpenClaw state/config directory from the default agent workspace. Why does the distinction matter?
10. Is the macOS menu-bar app identical to the Gateway runtime? Explain the roles of each.
11. On macOS versus Linux, what Node line does the installer provision when Node is missing?
12. [CRITICAL] You discover a partially configured XOS installation. Give a safe inspection-and-preservation sequence before changing anything.

SECTION II | OPENAI AGENTS SDK INTEGRATION (13-23)

13. [CRITICAL] Does installing OpenClaw install or switch it to the OpenAI Agents SDK execution loop? Explain the runtime boundary.
14. Sketch the smallest viable Python Agents SDK model configuration that sends calls to an existing LiteLLM proxy, not directly to OpenAI.
15. Which API shape does the Agents SDK default to, and what should you do when an OpenAI-compatible provider lacks it?
16. Name the three supported scopes for overriding/selecting model providers in the Agents SDK.
17. Explain the difference between the SDK's beta LiteLLM adapter and pointing the SDK's OpenAI-compatible client at an existing LiteLLM proxy.
18. The model call succeeds but the SDK emits an OpenAI tracing 401. Identify the separate subsystem and two supported fixes.
19. Distinguish a handoff from using a specialist Agent.as_tool(); who owns the conversation after each?
20. Can a single SDK run use a client-managed session simultaneously with conversation_id or previous_response_id continuation?
21. [CRITICAL] Do SDK handoffs, tool guardrails or approval callbacks automatically enforce OpenClaw Gateway permissions and XOS Paperclip authorization?
22. What actual integration tests prove model text generation is not being mistaken for tool calling and structured-output compatibility?
23. How would you prove that EVERY model invocation in an SDK workflow reached the approved LiteLLM gateway, including delegated calls?

SECTION III | LITELLM GATEWAY AND ROUTING (24-36)

24. Explain model_list.model_name versus litellm_params.model in a LiteLLM configuration.
25. Give the OpenClaw-side provider name/API shape normally documented for connecting to the LiteLLM proxy.
26. Give the documented OpenClaw LiteLLM onboarding auth-choice and the purpose of model discovery.
27. What does GET /v1/models prove, and what further test must succeed before you claim the model works?
28. Distinguish an upstream model-provider API credential from a LiteLLM virtual key used by clients.
29. What must change when LiteLLM is on a remote host instead of localhost? Address transport and key handling.
30. [CRITICAL] XOS prohibits unapproved automatic model fallbacks. Which layers must be inspected to ensure a supposedly pinned request cannot silently change models?
31. Distinguish a retry to the SAME model from a fallback to another model. Why does the distinction matter operationally?
32. Where do LiteLLM router retry, load-balancing and fallback settings belong in proxy configuration?
33. Why is exposing /v1/responses not enough to assume native Responses feature parity for every backend?
34. What can virtual keys enforce besides simple authentication, and why should different agents avoid sharing the admin key?
35. Name the LiteLLM diagnostic route for inspecting the transformed upstream request.
36. An API response displays the requested model alias. Does that alone prove which upstream deployment actually served it? What would?

SECTION IV | CONNECTORS, TOOLS, CHANNELS AND CAPABILITIES (37-56)

37. Distinguish a tool, a skill and a plugin in OpenClaw.
38. Where are third-party MCP server definitions registered?
39. Name three MCP transport options supported by OpenClaw.
40. Does connecting an MCP server automatically bypass agent tool-policy restrictions?
41. What OpenClaw command exposes OpenClaw capabilities TO an external MCP client rather than importing external MCP tools?
42. What unusual size limit applies to MCP server initialization guidance placed into the embedded agent prompt?
43. Why must a newly installed plugin's capabilities and provenance be reviewed instead of assuming installation equals consent?
44. Name six distinct messaging platforms OpenClaw can connect, without counting different accounts on the same platform.
45. What are DM pairing, sender allowlists and group mention gating intended to control?
46. How do OpenClaw's default direct-message and group session-scoping behaviors differ?
47. In a multi-agent roster with no unambiguous owner, may the system safely pick an arbitrary agent to receive a message?
48. [CRITICAL] Is BlueBubbles still the supported native OpenClaw iMessage connector? Describe the current supported path.
49. What additional macOS security tradeoff is documented for enabling advanced imsg private-API actions?
50. With imsg, which two different macOS permission categories govern reading the Messages database and sending through Messages?
51. OpenClaw's A2A channel supports which inbound payload types, and which transport/media capabilities does it explicitly lack?
52. Why should an A2A sender not assume that a leading slash command such as /reset will execute?
53. Does a paired node automatically have authority to execute every requested device command or capability?
54. Is the default OpenClaw browser profile the operator's existing personal browser profile?
55. Can an agent with message-tool access potentially send across providers/conversations unless explicitly restricted?
56. Choose the correct surface for each: external HTTP trigger, session-reset event, every-tool-call interception.

SECTION V | TROUBLESHOOTING AND RECOVERY (57-70)

57. Give a safe first-line diagnostic sequence for a Gateway that appears running but cannot serve RPCs.
58. A scheduled job never fires. Name four things to inspect before rewriting it.
59. The proxy's model list works, but the SDK gets HTTP 404 for a model call. Give two protocol/routing causes.
60. The SDK's LLM responses work but the tracing exporter returns 401. What should be changed, and what should not be changed blindly?
61. An MCP server appears in Settings but exposes no usable tools. Give four checks that do not weaken security controls.
62. A Telegram/Discord DM gets no reply while the Gateway is healthy. Which identity and channel policies would you inspect?
63. [CRITICAL] The exec tool is denied by policy. Will /exec or elevated mode legitimately override that hard denial?
64. A tool can see the workspace directory. Does this prove it cannot reach arbitrary absolute host paths?
65. A node is paired and online but an action is denied. Distinguish transport pairing from execution/capability approval.
66. The browser tool cannot attach to a browser. Give a safe diagnosis that does not expose debugging ports to the Internet.
67. iMessage history reads succeed but sends fail with AppleEvents -1743. Which permission path is suspect?
68. A one-shot schedule using kind=at is rejected when a condition trigger is included. Explain the valid correction.
69. Separate OpenClaw agents can read each other's sessions unexpectedly. What defaults and controls should be investigated?
70. After an update, a previously working Gateway breaks. Give a reversible diagnostic sequence; no Mac reboot allowed.

SECTION VI | DEEP OPENCLAW CAPABILITIES, SECURITY AND HARD LIMITS (71-100)

71. [CRITICAL] What trust boundary does one OpenClaw Gateway assume?
72. Is a single Gateway a supported hostile multi-tenant security boundary for mutually adversarial users?
73. What authority risk exists when multiple untrusted people can message the same tool-enabled agent?
74. What tools.profile posture does local onboarding commonly choose, and why is that security-relevant?
75. What are the documented trusted single-operator host exec approval defaults?
76. Define the separate purposes of sandbox, tool policy and elevated access.
77. Why is setting an agent workspace NOT equivalent to sandboxing that agent?
78. Which workspaceAccess choices restrict sandbox access to workspace files?
79. [CRITICAL] What are the documented defaults for tools.sessions.visibility and tools.agentToAgent.enabled, and why do they matter?
80. How can you permit narrow send-only delegation without giving unrestricted cross-agent session access?
81. What communication boundary must be configured to keep an agent from sending across channel providers?
82. What is the difference between openclaw security audit, --deep and --fix?
83. List two things security audit --fix intentionally does NOT guarantee.
84. Explain OpenClaw's defensive order: identity first, scope second, model last.
85. How do standing orders differ from automations?
86. What four fields make a well-scoped standing order?
87. Does openclaw agent exec necessarily omit preexisting AGENTS.md instructions?
88. What configuration suppresses automatic workspace-context injection in the embedded runtime?
89. Name at least four default workspace bootstrap files that can be injected into a session.
90. Are arbitrary Markdown files in nested workspace folders auto-injected merely because they exist?
91. What does the openclaw cron CLI now represent relative to openclaw automations?
92. What happened to legacy heartbeat monitoring in the current automation architecture?
93. Were inferred conversational commitments and their maintenance CLI retained after OpenClaw 2.0?
94. What is Lobster, and does every OpenClaw install have it enabled by default?
95. Name a former OpenClaw task/orchestration feature explicitly removed from the current automation architecture.
96. What tool restrictions apply to sub-agents by default?
97. Distinguish durable memory files/indexed recall from a model magically retaining everything it once saw.
98. Why should control of a paired remote node be treated as consequential operator authority?
99. What security problem does published npm-shrinkwrap.json help with, and what problem does it NOT solve?
100. [CRITICAL] Design the tightest PRACTICAL XOS setup for five cooperating agents: specify Gateway trust separation, session isolation, tool permissions, remote nodes, messaging, credentials, approval boundaries, LiteLLM routing, tracing and verification. Mention at least one feature you would deliberately leave disabled.

END OF EXAM. ANSWER KEY MUST NOT ACCOMPANY THE CANDIDATE COPY.