# Deepgram
Source: https://docs.openclaw.ai/providers/deepgram

Deepgram is a speech-to-text API. OpenClaw uses it for inbound audio/voice-note
transcription through `tools.media.audio` and for Voice Call streaming STT
through `plugins.entries.voice-call.config.streaming`.

Batch transcription uploads the complete audio file to Deepgram. Flux models
use Deepgram's one-shot WebSocket instead. Both paths inject the transcript
into the reply pipeline (`{{Transcript}}` + `[Audio]` block).
Voice Call streaming forwards live G.711 u-law frames over Deepgram's
WebSocket `listen` endpoint and emits partial/final transcripts as Deepgram
returns them.

| Detail        | Value                                                      |
| ------------- | ---------------------------------------------------------- |
| Docs          | [developers.deepgram.com](https://developers.deepgram.com) |
| Auth          | `DEEPGRAM_API_KEY`                                         |
| Default model | `nova-3`                                                   |

## Getting started

Steps

  
Set your API key

    ```bash
    export DEEPGRAM_API_KEY=dg_...
    ```
  
  
Enable the audio provider

    ```json5
    {
      tools: {
        media: {
          models: [{ provider: "deepgram", model: "nova-3", capabilities: ["audio"] }],
          audio: {
            enabled: true,
          },
        },
      },
    }
    ```
  
  
Send a voice note

    Send an audio message through any connected channel. OpenClaw transcribes it
    via Deepgram and injects the transcript into the reply pipeline.
  

## Configuration options

| Option     | Path                            | Description                           |
| ---------- | ------------------------------- | ------------------------------------- |
| `model`    | `tools.media.models[].model`    | Deepgram model id (default: `nova-3`) |
| `language` | `tools.media.models[].language` | Language hint (optional)              |

`providerOptions.deepgram` merges extra query params directly into the
Deepgram `/listen` request, so any Deepgram-supported param name works
(for example `detect_language`, `punctuate`, `smart_format`).

Array values are sent as repeated query parameters in both batch and Flux
requests. For example, set `providerOptions` on the audio config or a model entry
to send each `keyterm` separately instead of a comma-separated list:

```json validate=false
{
  "providerOptions": {
    "deepgram": {
      "keyterm": ["OpenClaw", "Deepgram"]
    }
  }
}
```

Tabs

  
With language hint

    ```json5
    {
      tools: {
        media: {
          models: [
            { provider: "deepgram", model: "nova-3", language: "en", capabilities: ["audio"] },
          ],
          audio: {
            enabled: true,
          },
        },
      },
    }
    ```
  
  
With Deepgram options

    ```json5
    {
      tools: {
        media: {
          models: [{ provider: "deepgram", model: "nova-3", capabilities: ["audio"] }],
          audio: {
            enabled: true,
            providerOptions: {
              deepgram: {
                detect_language: true,
                punctuate: true,
                smart_format: true,
              },
            },
          },
        },
      },
    }
    ```
  

### Flux models

Use `flux-general-en` or `flux-general-multi` for Deepgram Flux. OpenClaw
converts the voice note to 16 kHz mono linear16 audio with `ffmpeg`, then sends
it to Deepgram's `/v2/listen` WebSocket endpoint.
Set `tools.media.models[].model` to either Flux model in the getting-started
configuration above.

Voice-note conversion processes the complete audio file, including notes longer
than 20 minutes. Decoded audio uses a private temporary file, which is removed
after the transcription attempt. The configured input-size and request-timeout
limits still apply; failed conversion or upload does not return a partial transcript.

Flux supports `eager_eot_threshold`, `eot_threshold`, `eot_timeout_ms`,
`keyterm`, `language_hint`, `mip_opt_out`, `numerals`, `profanity_filter`,
`redact`, and `tag` in `providerOptions.deepgram`. OpenClaw ignores batch-only
options such as `detect_language`, `punctuate`, and `smart_format` on Flux.
Language hints apply only to `flux-general-multi`: OpenClaw maps the model entry's
`language` setting to `language_hint`, with an explicit provider option taking
precedence. Both settings are ignored for the English-only `flux-general-en` model.

## Voice Call streaming STT

The bundled `deepgram` plugin also registers a realtime transcription provider
for the Voice Call plugin.

Realtime transcription WebSockets honor the Gateway's `HTTPS_PROXY` / `https_proxy`
and `NO_PROXY` / `no_proxy` settings, including CIDR bypasses. Configured debug
capture proxies take precedence; TLS certificate verification remains enabled.

| Setting         | Config path                                                             | Default                                                                |
| --------------- | ----------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| API key         | `plugins.entries.voice-call.config.streaming.providers.deepgram.apiKey` | Falls back to `DEEPGRAM_API_KEY`, then a saved `deepgram` auth profile |
| Base URL        | `...deepgram.baseUrl`                                                   | `DEEPGRAM_BASE_URL` or Deepgram's public API                           |
| Model           | `...deepgram.model`                                                     | `nova-3`                                                               |
| Language        | `...deepgram.language`                                                  | (unset)                                                                |
| Encoding        | `...deepgram.encoding`                                                  | `mulaw`                                                                |
| Sample rate     | `...deepgram.sampleRate`                                                | `8000`                                                                 |
| Endpointing     | `...deepgram.endpointingMs`                                             | `800`                                                                  |
| Interim results | `...deepgram.interimResults`                                            | `true`                                                                 |

The saved auth profile is used only when Deepgram is the named provider, for example
`streaming.provider: "deepgram"`. Automatic selection counts only the config and
environment keys.

With interim results enabled and endpointing at most 5000 ms, a provider-detected
word gap also completes confirmed speech when background noise prevents endpointing.
The gap is at least 1000 ms and follows `endpointingMs` above that minimum. A long
pause can therefore split a thought into separate turns; provisional text is never committed.

```json5
{
  plugins: {
    entries: {
      "voice-call": {
        config: {
          streaming: {
            enabled: true,
            provider: "deepgram",
            providers: {
              deepgram: {
                apiKey: "${DEEPGRAM_API_KEY}",
                model: "nova-3",
                endpointingMs: 800,
                language: "en-US",
              },
            },
          },
        },
      },
    },
  },
}
```

For a [Deepgram custom endpoint](https://developers.deepgram.com/reference/custom-endpoints),
set `baseUrl` to the endpoint root, including any base path but not `/listen`.
Realtime endpoints accept `http://`, `https://`, `ws://`, and `wss://`. HTTP
maps to WS, HTTPS maps to WSS, and explicit WebSocket schemes stay unchanged.
Malformed URLs and other schemes fail during session setup.

Note

Voice Call receives telephony audio as 8 kHz G.711 u-law. The Deepgram
streaming provider defaults to `encoding: "mulaw"` and `sampleRate: 8000`, so
Twilio media frames can be forwarded directly.

## Notes

AccordionGroup

  
Authentication

    Authentication follows the standard provider auth order. `DEEPGRAM_API_KEY` is
    the simplest path.
  
  
Proxy and custom endpoints

    Override endpoints or headers on the Deepgram `tools.media.models[]` entry when using a proxy.
  
  
Output behavior

    Output follows the same audio rules as other providers (size caps, timeouts,
    transcript injection).
  
  
Flux requires ffmpeg

    Install `ffmpeg` with the gateway host's package manager before selecting a
    Flux model.
  

## Related

CardGroup

  
Media tools

    Audio, image, and video processing pipeline overview.
  
  
Configuration

    Full config reference including media tool settings.
  
  
Troubleshooting

    Common issues and debugging steps.
  
  
FAQ

    Frequently asked questions about OpenClaw setup.

---

