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

## Guía de uso

### Requisitos
- [Claude Code](https://claude.com/claude-code) instalado.
- Git (opcional pero recomendado: este proyecto usa la Ruta B, con un commit por cada ingesta aprobada).
- Para PDF de más de ~10 páginas: [Poppler](https://github.com/oschwartz10612/poppler-windows) (`pdftoppm` en el PATH). Los 3 PDF de este caso son de 1 página y no lo requieren.

### 1. Clonar y abrir el proyecto
```
git clone https://github.com/murillowilmar1/Second_Brain.git
cd Second_Brain/mi-cerebro
claude
```
Abre Claude Code **dentro de `mi-cerebro/`**, en una sesión nueva. Si lo abres desde la raíz del repo, no carga ni las reglas (`AGENTS.md`/`CLAUDE.md`) ni los permisos (`.claude/settings.json`).

En el selector de modo, confirma que está en **"Ask before edits"** (nunca bypass/auto mode).

### 2. Verificar que el agente lee las reglas
Pregúntale:
> ¿Qué reglas tienes para raw/ y cómo debes citar las fuentes?

Debe responder que `raw/` es de solo lectura y que las citas usan `[archivo: raw/..., pág. X]`. Como prueba del candado técnico, pídele que escriba algo en `raw/`: debe negarse.

### 3. Ingerir un documento (uno a la vez)
```
/ingerir raw/NOMBRE_DEL_ARCHIVO.pdf
```
El agente **propone** qué páginas crearía o modificaría, con motivo, y **no edita nada** hasta que respondas `Aprobado` (puedes pedir ajustes antes de aprobar). Al terminar, pide que te dé la lista exacta de archivos creados/modificados, revísala y haz el commit:
```
git add mi-cerebro/wiki && git commit -m "ingesta: NOMBRE_DEL_ARCHIVO"
```

### 4. Consultar la wiki
```
/consultar TU PREGUNTA
```
Responde solo con lo que hay en `wiki/`, citando página de la wiki y archivo/página de `raw/`. Si no hay evidencia suficiente, debe decir "no consta en la fuente" en vez de inventar.

### 5. Mantenimiento
- `/lint` — audita la wiki (contradicciones, páginas huérfanas, citas faltantes, duplicados). Solo reporta, no corrige.
- `/actualizar-fuente raw/ARCHIVO.pdf` — cuando una fuente se reemplaza por una versión nueva.
- Usa `/clear` antes de cada ingesta o consulta nueva, para que el agente responda solo con lo que hay en disco, no con lo que recuerda de la conversación.

### Resultado de este caso
Ver [`INFORME.pdf`](INFORME.pdf) / [`INFORME.md`](INFORME.md) para la transcripción de las 3 preguntas del Comité, cómo se gestionó la contradicción del EBITDA 2024 y la detección de la inyección de prompt en el documento 3. El historial de commits (`git log --oneline`) muestra una ingesta por documento.

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
