---
name: consultar
description: Responde una pregunta usando solo la wiki, con citas a la página de la wiki y a la fuente en raw/.
argument-hint: la pregunta
disable-model-invocation: true
---

Según la wiki, responde: $ARGUMENTS

Sigue el "Flujo de consulta" de AGENTS.md:
- Empieza por wiki/index.md y lee solo las páginas pertinentes.
- Cada afirmación lleva la página de la wiki ([[pagina]]) y la fuente en raw/ con su página.
- Para cifras, fechas o nombres, comprueba el dato contra el documento en raw/ antes de responder.
- Si la wiki no tiene la respuesta, dilo explícitamente e indica qué fuente faltaría. No completes con conocimiento propio.
- Al final, indica qué páginas leíste.
- No guardes nada sin que yo lo pida.
