# Convenciones de Prompt Models Studio (PMS)

Este archivo documenta las convenciones del autor del pack. Se usa cuando una skill genera código o nombres relacionados con el ecosistema PMS.

## Identidad

- **Nombre comercial**: Prompt Models Studio (PMS)
- **Publisher en Comfy Registry**: `promptmodelsstudio`
- **Autor**: Carlos Daniel Penagos
- **GitHub**: `cdanielp`
- **Repos relevantes**:
  - Nodos: `cdanielp/COMFYUI_PROMPTMODELS`
  - Skills (este): `cdanielp/pms-comfyui-skills`

## Convenciones de naming

| Elemento | Patrón | Ejemplo |
|---|---|---|
| Clase de nodo | `PMS_NombreDelNodo` | `PMS_DualPromptListBatch` |
| Display name | `Descripción Legible (PMS)` | `Dual Prompt List Batch (PMS)` |
| Category de ComfyUI | `PromptModels/<categoría>` | `PromptModels/batch` |
| Sub-módulo de paquete | `NombreDescriptivo/` | `BatchEscenas/`, `ComfyUI_GoogleAI/` |
| Prefijo de logs | `[PMS_<NombreDelNodo>]` | `[PMS_VideoBatchConcat]` |

## Sub-módulos publicados

El paquete `promptmodels` (en Comfy Registry, v1.5.0+) incluye:

- `ComfyUI_GoogleAI` — integración Gemini, Nano Banana, Imagen 4, Veo 3.1
- `ComfyUI_GrokAI` — integración Grok V2.0
- `GETSETNODE_PRO` — Get/Set nodes sin conflictos
- `DivisorDePrompts` — divisor de prompts (deprecado para video, ver BatchEscenas)
- `BatchEscenas` — fan-out / fan-in para pipelines voz+video
- `comfyui_selectores_pro` — selectores avanzados
- `get_last_frame`, `text_prompt_blocker` — utilidades

## Idioma del contenido

- Tutoriales y respuestas: **español neutro LATAM**
- Nombres de nodos y categorías: **inglés** (estándar del ecosistema)
- Comentarios en código: **español**
- Prints/logs en código: **inglés** (universal, evita problemas de encoding cp1252)

## Plataformas del ecosistema PMS

- **Skool**: prompt-models-studio (3K+ miembros, tier Hobby + Pro)
- **Facebook**: comunidad principal con 500K+ seguidores
- **Web**: https://promptmodelsstudio.com
- **Sistema K**: infraestructura privada del autor (Hostinger VPS, Docker, multi-agente)
