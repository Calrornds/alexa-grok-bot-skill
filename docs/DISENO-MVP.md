# Diseño MVP — Alexa → Chief (+ Lingxis / Commie)

Diseño cerrado. Carlos, 2026-11-05, Lima.

Fork de [debs-obrien/alexa-grok-bot-skill](https://github.com/debs-obrien/alexa-grok-bot-skill). Este documento no cambia el Worker.

## Piezas

- Skill de Alexa en **Development**. Invocación: **Chief**.
- Este Cloudflare Worker.
- Rutinas con webhook en Chief, Lingxis y Commie.
- TTS con Voice Monkey.

## Frases de lanzamiento (Amazon)

`abre`, `lanza`, `empieza`, `pregunta a`, `dile a`, `pídele a` + Chief.

No usar «despierta»: Amazon no la ofrece como frase de lanzamiento.

## Ejemplos

- «Alexa, dile a Chief qué hay para hoy» → Chief
- «Alexa, pregunta a Chief que Lingxis: qué hay para mergear» → Lingxis
- «Alexa, dile a Chief que Commie: resumen del radar» → Commie

## Enrutado

Por defecto, Chief.

Dentro de la consulta:

- `que Lingxis: <pedido>` → Lingxis
- `que Commie: <pedido>` → Commie

Mapa bot → secretos del webhook. Los secretos no van al repositorio.

## Lo hablado

Acuse: `Listo, <Bot> ya está en eso.`

TTS del resultado: el texto completo si es corto; si no, un resumen. El detalle queda en el chat del bot.

Temas sensibles (salud, dinero, familia, RR. HH.): solo chat, sin TTS.

Sin horas de silencio.

## Fuera del MVP

- Conversación de voz continua.
- Publicar la skill.
- YouTube Music.
- Enviar, comprar o borrar por voz.

## Checklist de construcción

1. Webhooks en los tres bots.
2. Secretos del Worker.
3. Modelo de interacción.
4. Deploy.
5. Prueba.
