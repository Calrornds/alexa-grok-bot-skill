# Diseño MVP — Alexa → Chief (+ Lingxis / Commie)

Cerrado con Carlos, 2026-11-05 Lima. Fork de `debs-obrien/alexa-grok-bot-skill`.

## Objetivo

Skill Alexa **personal** (Development, sin publicar). Despierta bots de Grok Bot por voz; la respuesta llega al chat y, si aplica, se lee en el Echo con Voice Monkey.

## Piezas

1. Skill Alexa (Amazon Developer) — invocación **Chief**.
2. Cloudflare Worker (este repo) — valida firma Alexa, enruta, wake webhook, ack hablado.
3. Routine webhook en cada bot (Chief, Lingxis, Commie).
4. Voice Monkey — TTS del resultado en el Echo.

## Activación (palabras de Amazon)

Tras «Alexa»: **abre**, **lanza**, **empieza**, **pregunta a**, **dile a**, **pídele a** + invocación **Chief**.  
«Despierta» no cuenta.

Ejemplos:

- `Alexa, dile a Chief qué hay para hoy` → Chief
- `Alexa, pregunta a Chief que Lingxis: qué hay para mergear` → Lingxis
- `Alexa, dile a Chief que Commie: resumen del radar` → Commie

## Routing

- Sin prefijo de bot → **Chief** (default).
- Dentro de la pregunta: `que Lingxis: <pedido>` o `que Commie: <pedido>`.
- Mapa bot → webhook URL + key (secretos del Worker; nunca en el repo).

## Respuestas

| Momento | Qué oye el Echo |
|---|---|
| Al wake (≤~8 s) | `Listo, <Bot> ya está en eso.` |
| Resultado (Voice Monkey) | Respuesta **completa** si es corta; si no, **resumen**. Detalle siempre en el chat del bot. |
| Temas sensibles (salud, plata, familia, HR) | Solo chat; en voz: indicar que quedó en el chat. |

Sin quiet hours (TTS siempre que haya resumen).

## Fuera del MVP

- Conversación continua por voz con el bot.
- Publicar la skill.
- YouTube Music / control del Echo como skill de Grok Bot.
- Enviar, comprar, borrar o pagar por voz.

## Checklist de build (siguiente)

1. Routine webhook en Chief, Lingxis y Commie (payload: query, source=alexa, requestId, timestamp; solo lectura salvo confirmación en chat).
2. Secrets Worker: skill ID, webhooks, Voice Monkey.
3. Interaction model: un intent + slot query; invocación Chief.
4. Deploy Worker + endpoint HTTPS en la skill (Development).
5. Probar: Chief solo → Lingxis → Commie → TTS.

## Decisiones registradas

- Paquete: wake + chat + TTS día 1 + multi-bot.
- Invocación: Chief; sin quiet hours.
- Bots: Chief + Lingxis + Commie.
- Enrutado: `que <Bot>: <pedido>`.
- Ack: `Listo, <Bot> ya está en eso.`
- TTS: completa si corta; si no, resumen.
