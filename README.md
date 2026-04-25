# PMS ComfyUI Skills

> Pack de skills para Claude Code orientadas a ComfyUI, en español.

[![Comfy Registry](https://img.shields.io/badge/Comfy_Registry-promptmodels-purple)](https://registry.comfy.org/nodes/promptmodels)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Mantenido por [Prompt Models Studio (PMS)](https://promptmodelsstudio.com), comunidad LATAM de IA generativa con 500K+ seguidores.

## Qué es esto

Un pack de skills para Claude Code (también compatibles con Cursor, Gemini CLI y otros agentes con soporte SKILL.md) que ayudan a usuarios hispanohablantes de ComfyUI a:

- Diagnosticar errores de carga de custom nodes
- Simplificar workflows sobrecargados
- Migrar workflows con tecnología obsoleta al stack 2026
- Construir workflows nuevos siguiendo las mejores prácticas vigentes

Todo en español neutro LATAM, con conocimiento del stack ComfyUI **al día de abril 2026**.

## Comandos disponibles

| Comando | Qué hace | Estado |
|---|---|---|
| `/comfy:fix` | Diagnostica errores de carga | disponible |
| `/comfy:audit` | Audita y simplifica un workflow | próximo |
| `/comfy:upgrade` | Migra workflow a stack 2026 | próximo |
| `/comfy:explain` | Explica un nodo en español | próximo |
| `/comfy:build` | Genera workflow desde descripción | próximo |
| `/comfy:deploy` | Prepara workflow para ComfyDeploy | próximo |

## Instalación

### Opción 1: Clonar a tu carpeta de skills (Claude Code)

```bash
git clone https://github.com/cdanielp/pms-comfyui-skills.git ~/.claude/skills/pms-comfyui-skills
```

Después reiniciá Claude Code. El pack se carga automáticamente.

### Opción 2: Via plugin marketplace (cuando esté disponible)

```bash
/plugin marketplace add cdanielp/pms-comfyui-skills
```

## Uso

Una vez instalado, simplemente describí tu problema. Claude detecta cuándo activar las skills.

**Ejemplo 1 — Error de carga:**

```
Pegá tu log:

Failed to import custom node from: ComfyUI-AnimateDiff-Evolved
ImportError: libGL.so.1: cannot open shared object file
```

Claude responderá con diagnóstico estructurado, fix con prioridad y verificación.

**Ejemplo 2 — Invocación explícita:**

```
/comfy:fix
[pegás el log]
```

## Estructura del pack

```
pms-comfyui-skills/
├── SKILL.md              <- skill maestra (router del pack)
├── commands/             <- cada comando slash
├── references/           <- stack vigente, deprecaciones, convenciones
├── gotchas/              <- problemas reales y sus fixes
├── examples/             <- logs y workflows de ejemplo
└── scripts/              <- utilidades Python (futuro)
```

## Filosofía

Este pack se construyó observando que:

1. **Las IAs alucinan con ComfyUI** porque su training tiene info de 2-3 años atrás. IPAdapter clásico, AnimateDiff y SD 1.5 dominan los rankings de Google pero ya no son la respuesta correcta en 2026.

2. **El contenido en español falta**: el 90% de los tutoriales de ComfyUI son en inglés. Los hispanohablantes traducen mentalmente y pierden contexto.

3. **Los workflows reales son caóticos**: se acumulan duplicaciones, nodos deprecados y rutas de routing complejas. Hay patrones repetidos de simplificación.

Estas skills atacan los 3 problemas con knowledge curado, español primero y patrones probados en producción.

## Contribuir

Bienvenidos PRs con:
- Nuevos `gotchas/` (problemas reales con sus fixes)
- Actualizaciones a `references/` cuando salgan modelos nuevos
- Comandos nuevos siguiendo el patrón de `commands/fix.md`
- Traducciones a otras variantes del español (rioplatense, castellano, etc.)

## Licencia

MIT — usá, modificá, redistribuí libremente.

## Autor

**Carlos Daniel Penagos** (Prompt Models Studio)

- Web: [promptmodelsstudio.com](https://promptmodelsstudio.com)
- GitHub: [@cdanielp](https://github.com/cdanielp)
- Comfy Registry: [promptmodels](https://registry.comfy.org/nodes/promptmodels)
- Skool: [Prompt Models Studio](https://www.skool.com/prompt-models-studio)
- Facebook: comunidad de IA en español con 500K+ seguidores

---

Si este pack te ahorra tiempo, dejá una estrella. Si te ayudó a resolver un problema concreto, contámelo en un issue.
