---
name: lint
description: Revisa la salud de la wiki según el flujo de lint de AGENTS.md. Solo reporta, no corrige.
disable-model-invocation: true
---

Haz lint de la wiki según el "Flujo de lint" de AGENTS.md. **Solo reporta, no corrijas nada.**

Entrega una tabla por cada tipo de hallazgo (contradicciones, páginas huérfanas, conceptos sin página, afirmaciones sin cita, confidence: low, duplicados, páginas de más de 2.500 palabras), con la ruta del archivo y el detalle. Si un tipo no tiene hallazgos, dilo.

Termina preguntando si quiero guardar el reporte en wiki/_pending/lint-<fecha>.md.
