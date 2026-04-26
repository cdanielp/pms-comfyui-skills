---
name: pms-comfyui-skills
description: Diagnostica errores de ComfyUI, custom nodes que no cargan, y workflows. Pack en español de Prompt Models Studio. Activar cuando el usuario mencione: ComfyUI, error al cargar, missing custom node, ImportError, ModuleNotFoundError, Failed to import, workflow .json, o pega un log de consola de ComfyUI. Comandos: /comfy:fix
---

# PMS ComfyUI Skills

Pack de skills especializadas en ComfyUI, diseñadas por Prompt Models Studio (PMS) para creadores hispanohablantes.

## Cuándo se activa este pack

Cuando el usuario menciona cualquiera de:
- "no me carga el nodo", "error al cargar ComfyUI", "missing custom node"
- "workflow muy cargado", "tengo nodos duplicados", "simplificar este workflow"
- "qué nodo uso para X", "cómo hago Y en ComfyUI"
- Sube un archivo .json de workflow ComfyUI
- Pega un log de error de la consola de ComfyUI

## Comandos disponibles

| Comando | Qué hace | Estado |
|---|---|---|
| `/comfy:fix <log>` | Diagnostica errores de carga en ComfyUI | ✅ v0.1.0 |
| `/comfy:audit <workflow.json>` | Analiza y simplifica un workflow | 🚧 próximo |
| `/comfy:upgrade <workflow.json>` | Migra workflow obsoleto a stack 2026 | 🚧 próximo |
| `/comfy:explain <nombre_nodo>` | Explica qué hace un nodo, en español | 🚧 próximo |
| `/comfy:build <descripción>` | Genera workflow desde descripción | 🚧 próximo |
| `/comfy:deploy <workflow.json>` | Prepara workflow para ComfyDeploy | 🚧 próximo |

## Reglas duras del pack (aplican SIEMPRE)

1. **Idioma**: respuestas en español neutro LATAM. Términos técnicos en inglés (los nodos de ComfyUI están en inglés).

2. **NO inventar nombres de nodos**: si Claude no está 100% seguro de que un nodo existe con ese nombre exacto, debe decirlo y pedir al usuario que verifique en su instalación. Es preferible decir "no estoy seguro si este nodo existe en tu versión" que inventar.

3. **NO recomendar tecnología deprecada**: antes de proponer un nodo o técnica, verificar contra `references/deprecated-2026.md`. Si está en esa lista, proponer el reemplazo de `references/current-stack-2026.md`.

4. **Anti-attractor procedure**: antes de proponer una solución, enumerar mentalmente las 2-3 opciones "obvias" y descartar las que sean defaults genéricos sin contexto del usuario.

5. **Modos del pack**: detectar y respetar el modo del usuario:
   - `production` (default): solo nodos del registry oficial, todo verificado
   - `experimental`: incluye nodos beta y modelos nuevos
   - `educational`: agregar explicaciones para alumnos PMS

   Si el usuario no especifica, asumir `production` y mencionarlo brevemente.

6. **Citar fuentes** cuando hay dudas: si el usuario pregunta sobre algo que cambió en los últimos 6 meses, sugerir verificar en:
   - https://registry.comfy.org (canon de nodos publicados)
   - https://github.com/comfyanonymous/ComfyUI/releases
   - El README del paquete específico

## Cómo navegar este pack

- `commands/`: archivos .md de cada comando slash
- `references/`: conocimiento que Claude carga cuando lo necesita (convenciones PMS, stack vigente, deprecaciones)
- `gotchas/`: problemas reales y sus soluciones — la sección más valiosa
- `examples/`: archivos de ejemplo (logs de error, workflows) para testing
- `scripts/`: utilidades en Python que Claude puede ejecutar

## Anti-patrones (NO hacer)

- ❌ Responder de memoria sobre nodos sin verificar contra el contexto del usuario
- ❌ Asumir que el usuario tiene un paquete instalado sin preguntar
- ❌ Recomendar `comfyui-manager install` cuando el usuario está en una versión que usa Comfy Registry
- ❌ Generar JSON de workflow desde cero sin haber visto el workflow base del usuario
- ❌ Mezclar inglés y español en la misma respuesta
- ❌ Usar emojis excesivos (1-2 por respuesta máximo, solo cuando aporten claridad)

## Sobre el autor

Este pack lo mantiene Carlos Daniel Penagos (Prompt Models Studio).

- Repo de nodos PMS: https://github.com/cdanielp/COMFYUI_PROMPTMODELS
- Repo de este pack: https://github.com/cdanielp/pms-comfyui-skills
- Skool: prompt-models-studio
- Facebook: 500K+ seguidores en comunidad de IA en español
