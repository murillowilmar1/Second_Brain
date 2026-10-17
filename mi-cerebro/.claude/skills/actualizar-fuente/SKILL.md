---
name: actualizar-fuente
description: Cuando un archivo de raw/ tiene una versión nueva, identifica las páginas de la wiki desactualizadas y propone cambios sin editar.
argument-hint: raw/nombre-del-archivo.pdf
disable-model-invocation: true
---

$ARGUMENTS es una versión nueva. Sigue el "Flujo de actualización de fuente" de AGENTS.md:

1. Busca todas las páginas de wiki/ que citan ese archivo (campo sources: y citas [archivo: raw/...]).
2. Compara lo que dicen esas páginas con el documento actual y lista, por página, qué datos cambiaron (valor anterior → valor nuevo, con su cita).
3. **No edites nada todavía.** Espera mi aprobación.
