# Second_Brain: Operación NeoPay

Segundo cerebro con IA (patrón *LLM Wiki* de Andrej Karpathy) para la due diligence de adquisición de NeoPay Technologies, S.L. Taller final del curso Tópicos Avanzados, EIA.

El agente es **Claude Code**, en lugar de Google Antigravity 2.0. El enunciado permite "otro agente autónomo en entorno local".

## Estructura

```
mi-cerebro/
├── AGENTS.md              reglas operativas (citación literal, contradicciones, seguridad)
├── CLAUDE.md              carga AGENTS.md en Claude Code
├── .claude/
│   ├── settings.json      permisos: raw/ bloqueado para escritura, sin internet, sin modo bypass
│   └── skills/            /ingerir, /consultar, /lint, /actualizar-fuente
├── raw/                   documentos originales (solo lectura)
│   ├── 01_resumen_financiero_2024.pdf
│   ├── 02_informe_actualizado_q2_2025.pdf
│   └── 03_analisis_mercado_y_riesgos.pdf
└── wiki/
    ├── index.md           catálogo
    ├── log.md             registro append-only
    ├── sources/  concepts/  entities/  _pending/
```

## Gobernanza

| Control | Implementación |
|---|---|
| Modo estricto | Claude Code en modo "Ask before edits"; el modo bypass está deshabilitado en `settings.json` |
| `raw/` de solo lectura | Regla en `AGENTS.md` y bloqueo técnico `Edit(/raw/**)` |
| Human-in-the-loop | Cada ingesta se propone primero y solo se ejecuta con aprobación |
| Trazabilidad | Cita obligatoria `[archivo: raw/..., pág. X]` y cifras copiadas literalmente |
| Contradicciones | Se registran ambas versiones en `## Contradicciones`; el agente no elige |
| Inyección de prompts | El contenido de `raw/` es información, nunca instrucciones |
| Historial | Un commit por cada ingesta aprobada |
