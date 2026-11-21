# Text-to-speech field reference
Source: https://docs.openclaw.ai/tools/tts/field-reference

## Field reference

Provider `apiKey` fields, including `personas.<id>.providers.<provider>.apiKey`,
can be raw strings or SecretRefs in global, per-agent, and Discord voice TTS config.
During cold Gateway startup, an unavailable TTS SecretRef marks the built-in TTS capability
configured-unavailable instead of stopping the Gateway. `tts.speak` then returns
`UNAVAILABLE` with reason `SECRET_SURFACE_UNAVAILABLE`, and no provider request is
sent. Status and doctor list the degraded TTS owner and its config paths. The
explicit refs remain in the runtime snapshot, so environment or profile
credentials cannot silently select a different account. Reloads and config-write
preflight apply the owner-aware degradation policy: an unchanged eligible TTS
owner may keep its last-known-good credentials as stale, while a new or changed
failure becomes cold without blocking healthy owners. Structurally invalid refs
and resolved values still fail startup or reject the update.

AccordionGroup

  
Top-level tts.*

    
ParamField

      Auto-TTS mode. `inbound` only sends audio after an inbound voice message; `tagged` only sends audio when the reply includes `[[tts:...]]` directives or a `[[tts:text]]` block.
    
    
ParamField

      Legacy toggle. `openclaw doctor --fix` migrates this to `auto`.
    
    
ParamField

      `"all"` includes tool/block replies in addition to final replies.
    
    
ParamField

      Speech provider id. When unset, OpenClaw uses the first configured provider in registry auto-select order. Legacy `provider: "edge"` is rewritten to `"microsoft"` by `openclaw doctor --fix`.
    
    
ParamField

      Active persona id from `personas`. Normalized to lowercase.
    
    
ParamField
" type="object">
      Stable spoken identity. Fields: `label`, `description`, `provider`, `fallbackPolicy`, `providers.<provider>`. See [Personas](/tools/tts/personas#personas).
    
    
ParamField

      Cheap model for auto-summary; defaults to `agents.defaults.model.primary`. Accepts `provider/model` or a configured model alias.
    
    
ParamField

      Allow the model to emit TTS directives. `enabled` defaults to `true`; `allowProvider` defaults to `false`.
    
    
ParamField
" type="object">
      Provider-owned settings keyed by speech provider id. Legacy direct blocks (`tts.openai`, `.elevenlabs`, `.microsoft`, `.edge`) are rewritten by `openclaw doctor --fix`; commit only `tts.providers.<id>`.
    
    
ParamField

      Hard cap for TTS input characters. `/tts audio`, `tts.convert`, and `tts.speak` fail if exceeded.
    
    
ParamField

      Request timeout in milliseconds. A per-call `timeoutMs` (agent tool, gateway) wins when set; otherwise an explicitly configured `tts.timeoutMs` wins over any plugin-authored provider default. When neither is set, DeepInfra and OpenRouter default to `120000` because hosted Kokoro synthesis can exceed 30 seconds.
    
  
  
Azure Speech

    
ParamField
Env: `AZURE_SPEECH_KEY`, `AZURE_SPEECH_API_KEY`, or `SPEECH_KEY`.
    
ParamField
Azure Speech region (e.g. `eastus`). Env: `AZURE_SPEECH_REGION` or `SPEECH_REGION`.
    
ParamField
Optional Azure Speech endpoint override (alias `baseUrl`).
    
ParamField
Azure voice ShortName. Default `en-US-JennyNeural`. Legacy alias: `voice`.
    
ParamField
SSML language code. Default `en-US`.
    
ParamField
Azure `X-Microsoft-OutputFormat` for standard audio. Default `audio-24khz-48kbitrate-mono-mp3`.
    
ParamField
Azure `X-Microsoft-OutputFormat` for voice-note output. Default `ogg-24khz-16bit-mono-opus`.
  

  
ElevenLabs

    
ParamField
Falls back to `ELEVENLABS_API_KEY` or `XI_API_KEY`.
    
ParamField
Model id. Default `eleven_multilingual_v2`; set `modelId: "eleven_v3"` for v3. The config key `model` is ignored. Legacy ids `eleven_turbo_v2_5`/`eleven_turbo_v2` are normalized to the matching `flash` model.
    
ParamField
ElevenLabs voice id. Default `pMsXgVXv3BLzUgSXRplE`. Legacy alias: `voiceId`.
    
ParamField

      `stability`, `similarityBoost`, `style` (each `0..1`, defaults `0.5`/`0.75`/`0`), `useSpeakerBoost` (`true|false`, default `true`), `speed` (`0.5..2.0`, default `1.0`).
    
    
ParamField
Text normalization mode.
    
ParamField
2-letter ISO 639-1 (e.g. `en`, `de`).
    
ParamField
Integer `0..4294967295` for best-effort determinism.
    
ParamField
Override ElevenLabs API base URL.
  

  
Google Gemini

    
ParamField
Falls back to `GEMINI_API_KEY` / `GOOGLE_API_KEY`. If omitted, TTS can reuse `models.providers.google.apiKey` before env fallback.
    
ParamField
Gemini TTS model. Default `gemini-3.1-flash-tts-preview`. Set `gemini-3.8-flash-tts` or `gemini-3.8-flash-lite-tts` to opt in to Gemini 3.8, which OpenClaw sends through the Interactions API. `gemini-2.5-flash-preview-tts` and `gemini-2.5-pro-preview-tts` also work.
    
ParamField
Gemini prebuilt voice name. Default `Kore`. Legacy aliases: `voiceName`, `voice`.
    
ParamField
Natural-language delivery style. Gemini 3.8 sends it as `speech_metadata.style`. Gemini 3.1 and 2.5 preview models prepend it to the spoken text.
    
ParamField
Optional speaker label. Gemini 3.8 sends it as the structured `speech_metadata.speaker` label alongside the single configured voice. Older preview models prepend `Speaker name:` before the spoken text.
    
ParamField
Exactly two `{ speaker, voice, style? }` entries. On Gemini 3.8, lines that start with one of the two configured names and a colon (with or without a following space) become conversational turns and the name is not spoken; any other line, including other `Word: text` prose, stays inside the current turn. Transcripts without configured labels stay single-voice.
    
ParamField
On Gemini 3.1 and 2.5 preview models, wrap active persona fields in a fixed prompt format. On Gemini 3.8, `personaPrompt` is sent as `speech_metadata.style` and is not read aloud; the persona label is not sent.
    
ParamField
Google-specific persona direction. Gemini 3.8 sends it as style metadata. Older preview models append it to the audio-profile template's Director's Notes.
    
ParamField
Only `https://generativelanguage.googleapis.com` is accepted.
  

  
Gradium

    
ParamField
Env: `GRADIUM_API_KEY`.
    
ParamField
HTTPS Gradium API URL on `api.gradium.ai`. Default `https://api.gradium.ai`.
    
ParamField
Default Emma (`YTpq7expH9539ERJ`). Legacy alias: `voiceId`.
  

  
Inworld

    <a id="inworld-primary" />

    
ParamField
Env: `INWORLD_API_KEY`.
    
ParamField
Default `https://api.inworld.ai`.
    
ParamField
Default `inworld-tts-1.5-max`. Also: `inworld-tts-1.5-mini`, `inworld-tts-1-max`, `inworld-tts-1`, `inworld-tts-2`, `inworld-tts-2-flash`.
    
ParamField
Default `Sarah`. Legacy alias: `voiceId`.
    
ParamField
Sampling temperature `0..2` (exclusive of 0). Ignored by `inworld-tts-2`, which uses `deliveryMode` instead.
    
ParamField
Speaking rate `0.5..1.5`; `1.0` is the voice's native speed. Sent as `audioConfig.speakingRate`.
    
ParamField
Delivery preset. Honored only by `inworld-tts-2` (where it replaces `temperature`); OpenClaw does not send it to other models, including `inworld-tts-2-flash`.

  

  
Local CLI (tts-local-cli)

    
ParamField
Local executable or command string for CLI TTS.
    
ParamField
Command arguments. Supports `{{Text}}`, `{{OutputPath}}`, `{{OutputDir}}`, `{{OutputBase}}` placeholders.
    
ParamField
Expected CLI output format. Default `mp3` for audio attachments.
    
ParamField
Command timeout in milliseconds. Overrides the resolved TTS request timeout when set. When omitted, follows the request timeout; the plugin default is `120000`.
    
ParamField
Optional command working directory.
    
ParamField
">Optional environment overrides for the command.

    Command stdout and generated or converted audio are limited to 50 MiB. Diagnostic stderr is limited to 1 MiB. OpenClaw terminates the command and fails synthesis when either limit is exceeded.

  

  
Microsoft (no API key)

    
ParamField
Allow Microsoft speech usage.
    
ParamField
Microsoft neural voice name (e.g. `en-US-MichelleNeural`). Legacy alias: `voice`. If the default English voice is in effect and reply text is CJK-dominant, OpenClaw auto-switches to `zh-CN-XiaoxiaoNeural`.
    
ParamField
Language code (e.g. `en-US`).
    
ParamField
Microsoft output format. Default `audio-24khz-48kbitrate-mono-mp3`. Not all formats are supported by the bundled Edge-backed transport.
    
ParamField
Percent strings (e.g. `+10%`, `-5%`).
    
ParamField
Write JSON subtitles alongside the audio file.
    
ParamField
Proxy URL for Microsoft speech requests.
    
ParamField
Request timeout override (ms).
    
ParamField
Legacy alias. Run `openclaw doctor --fix` to rewrite persisted config to `providers.microsoft`.
  

  
MiniMax

    
ParamField
Falls back to `MINIMAX_API_KEY`. Token Plan auth via `MINIMAX_OAUTH_TOKEN`, `MINIMAX_CODE_PLAN_KEY`, or `MINIMAX_CODING_API_KEY`.
    
ParamField
Default `https://api.minimax.io`. Env: `MINIMAX_API_HOST`.
    
ParamField
Default `speech-2.8-hd`. Env: `MINIMAX_TTS_MODEL`.
    
ParamField
Default `English_expressive_narrator`. Env: `MINIMAX_TTS_VOICE_ID`. Legacy alias: `voiceId`.
    
ParamField
`0.5..2.0`. Default `1.0`.
    
ParamField
`(0, 10]`. Default `1.0`.
    
ParamField
Integer `-12..12`. Default `0`. Fractional values are truncated before the request.
  

  
OpenAI

    
ParamField
Falls back to `OPENAI_API_KEY`.
    
ParamField
OpenAI TTS model id. Default `gpt-4o-mini-tts`.
    
ParamField
Voice name (e.g. `alloy`, `cedar`). Default `coral`. Legacy alias: `voice`.
    
ParamField
Explicit OpenAI `instructions` field. When set, persona prompt fields are **not** auto-mapped.
    
ParamField
Explicit response format. When omitted, OpenClaw selects Opus for voice-note targets and MP3 otherwise. Use `wav` for compatible local endpoints that do not encode compressed audio.
    
ParamField
">Extra JSON fields merged into `/audio/speech` request bodies after generated OpenAI TTS fields. Use this for OpenAI-compatible endpoints such as Kokoro that require provider-specific keys like `lang`; unsafe prototype keys are ignored.
    
ParamField

      Override the OpenAI TTS endpoint. Resolution order: config → `OPENAI_TTS_BASE_URL` → `https://api.openai.com/v1`. Non-default values are treated as OpenAI-compatible TTS endpoints, so custom model and voice names are accepted, and `speed` loses its `0.25..4.0` range check.
    
  

  
OpenRouter

    
ParamField
Env: `OPENROUTER_API_KEY`. Can reuse `models.providers.openrouter.apiKey`.
    
ParamField
Default `https://openrouter.ai/api/v1`. Legacy `https://openrouter.ai/v1` is normalized.
    
ParamField
Default `hexgrad/kokoro-82m`. Alias: `modelId`.
    
ParamField
Default `af_alloy`. Legacy aliases: `voice`, `voiceId`.
    
ParamField
Default `mp3`.
    
ParamField
Provider-native speed override.
  

  
Volcengine (BytePlus Seed Speech)

    
ParamField
Env: `VOLCENGINE_TTS_API_KEY` or `BYTEPLUS_SEED_SPEECH_API_KEY`.
    
ParamField
Default `seed-tts-1.0`. Env: `VOLCENGINE_TTS_RESOURCE_ID`. Use `seed-tts-2.0` when your project has TTS 2.0 entitlement.
    
ParamField
App key header. Default `aGjiRDfUWi`. Env: `VOLCENGINE_TTS_APP_KEY`.
    
ParamField
Override the Seed Speech TTS HTTP endpoint. Env: `VOLCENGINE_TTS_BASE_URL`.
    
ParamField
Voice type. Default `en_female_anna_mars_bigtts`. Env: `VOLCENGINE_TTS_VOICE`. Legacy alias: `voice`.
    
ParamField
Provider-native speed ratio, `0.2..3`.
    
ParamField
Provider-native emotion tag.
    
ParamField
Legacy Volcengine Speech Console fields. Env: `VOLCENGINE_TTS_APPID`, `VOLCENGINE_TTS_TOKEN`, `VOLCENGINE_TTS_CLUSTER` (default `volcano_tts`).
  

  
xAI

    
ParamField
Env: `XAI_API_KEY`.
    
ParamField
Default `https://api.x.ai/v1`. Env: `XAI_BASE_URL`.
    
ParamField
Default `eve`. With auth, `openclaw infer tts voices --provider xai` fetches the current built-in catalog; without auth it lists offline fallbacks `ara`, `eve`, `leo`, `rex`, and `sal`. Account custom voice IDs are forwarded even when absent from the built-in list. Legacy alias: `voiceId`.
    
ParamField
BCP-47 language code or `auto`. Default `en`.
    
ParamField
Default `mp3`.
    
ParamField
Provider-native speed override, `0.7..1.5`.
  

  
Xiaomi MiMo

    
ParamField
Env: `XIAOMI_API_KEY`.
    
ParamField
Default `https://api.xiaomimimo.com/v1`. Env: `XIAOMI_BASE_URL`.
    
ParamField
Default `mimo-v2.5-tts`. Env: `XIAOMI_TTS_MODEL`. Also supports `mimo-v2.5-tts-voicedesign`.
    
ParamField
Default `mimo_default` for preset-voice models. Env: `XIAOMI_TTS_VOICE`. Legacy alias: `voice`. Not sent for `mimo-v2.5-tts-voicedesign`.
    
ParamField
Default `mp3`. Env: `XIAOMI_TTS_FORMAT`.
    
ParamField
Optional natural-language style instruction sent as the user message; not spoken. For `mimo-v2.5-tts-voicedesign`, this is the voice-design prompt; OpenClaw supplies a default when omitted.

---

