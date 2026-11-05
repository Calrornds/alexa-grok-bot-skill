# MVP design — Alexa → Chief (+ Lingxis / Commie)

Closed design. Carlos, 2026-11-05, Lima.

Fork of [debs-obrien/alexa-grok-bot-skill](https://github.com/debs-obrien/alexa-grok-bot-skill). This document does not change the Worker.

Spanish twin: [DISENO-MVP.md](./DISENO-MVP.md). Spoken examples stay in Spanish because that is what you say to Alexa.

## Pieces

- Alexa skill in **Development**. Invocation name: **Chief**.
- This Cloudflare Worker.
- Routines with a webhook (an automatic notice over the internet) in Chief, Lingxis, and Commie.
- Spoken aloud (TTS) with Voice Monkey: Alexa reads the result out loud.

## Launch phrases (Amazon)

`abre`, `lanza`, `empieza`, `pregunta a`, `dile a`, `pídele a` + Chief.

Do not use «despierta»: Amazon does not offer it as a launch phrase.

## Examples

- «Alexa, dile a Chief qué hay para hoy» → Chief
- «Alexa, pregunta a Chief que Lingxis: qué hay listo para revisar» → Lingxis
- «Alexa, dile a Chief que Commie: resumen del radar» → Commie

## Routing

Chief by default.

Inside the request:

- `que Lingxis: <request>` → Lingxis
- `que Commie: <request>` → Commie

Map from bot to webhook secrets. Secrets do not go in the repository.

## What you hear

Acknowledgement: `Listo, <Bot> ya está en eso.`

What you hear: the full text when it is short; otherwise a summary. The detail stays in the bot chat.

Sensitive topics (health, money, family, HR): chat only, without speaking aloud.

No quiet hours.

## Out of the MVP

- Ongoing voice conversation.
- Publishing the skill.
- YouTube Music.
- Sending, buying, or deleting by voice.

## Build checklist

1. Webhooks on the three bots.
2. Worker secrets.
3. Interaction model.
4. Publish the Worker on Cloudflare.
5. Test on the Echo: «Alexa, dile a Chief qué hay para hoy».
   You should hear: «Listo, Chief ya está en eso.» and then the spoken summary (or only the acknowledgement if the topic is sensitive).
