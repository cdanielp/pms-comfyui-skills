# Stack ComfyUI deprecado (abril 2026)

Tecnologías que aparecen mucho en tutoriales viejos pero que **NO debés recomendar** para workflows nuevos. Cada entrada incluye su reemplazo moderno.

## Generación de video

| Deprecado | Por qué | Reemplazo 2026 |
|---|---|---|
| AnimateDiff (todas las variantes) | Calidad inferior, modelos desentrenados | LTX-2.3, WAN 2.2, Hunyuan |
| Stable Video Diffusion (SVD) | Discontinuado, sin updates | LTX-2.3 distilled |
| ModelScope T2V | Calidad muy baja vs alternativas | Cualquiera de los modernos |

## Adapters e identidad

| Deprecado | Por qué | Reemplazo 2026 |
|---|---|---|
| IPAdapter clásico | Reemplazado por Plus | IPAdapter Plus, Flux Redux |
| Reactor (face swap clásico) | Mantenimiento errático | PuLID, InstantID |
| Roop / FaceSwap | Sin updates | InstantID, PuLID |

## Control y guidance

| Deprecado | Por qué | Reemplazo 2026 |
|---|---|---|
| ControlNet v1.0 (SD1.5) | Modelos viejos, calidad inferior | SDXL ControlNet Union, Flux ControlNet |
| T2I Adapter clásico | Superado por ControlNet moderno | Flux ControlNet, SDXL Union |

## Modelos base

| Deprecado | Por qué | Reemplazo 2026 |
|---|---|---|
| SD 1.5 (workflows nuevos) | Calidad muy inferior, ecosistema en sunset | SDXL Lightning, Flux Schnell, Flux Dev |
| SD 2.0 / 2.1 | Nunca alcanzó adopción | Saltarse a SDXL o Flux |

## Upscaling

| Deprecado | Por qué | Reemplazo 2026 |
|---|---|---|
| ESRGAN solo (estándar) | Resultados artificiales en rostros | SUPIR + tile, CCSR, SeeSR |
| Real-ESRGAN x4 (uso único) | Bien como primer pase, no como final | Combinar con SUPIR refine |

## Workflow tools

| Deprecado | Por qué | Reemplazo 2026 |
|---|---|---|
| ComfyUI-Manager (como instalador principal) | Reemplazado por Comfy Registry | `comfy node install <pkg>` desde registry.comfy.org |
| Custom nodes con `requirements.txt` informal | Pre-Registry era | Usar `pyproject.toml` + Comfy Registry |

## Cómo usar este archivo

Antes de recomendar cualquier nodo o técnica, verificar contra esta lista. Si lo que el usuario pide está acá:

1. Avisar al usuario brevemente: "Este enfoque está deprecado, te conviene X"
2. Mostrar la alternativa moderna
3. Si el usuario insiste en lo deprecado (caso válido: workflow legacy que no puede migrar), ayudar pero mencionar el riesgo
