# Stack ComfyUI vigente (abril 2026)

Tecnologías recomendadas para workflows nuevos. Esta lista se actualiza cada mes.

## Modelos base de imagen

| Modelo | Cuándo usarlo | Velocidad | Calidad |
|---|---|---|---|
| Flux Dev | Default para calidad | Media | Muy alta |
| Flux Schnell | Cuando velocidad importa | Rápida | Alta |
| SDXL Lightning | Workflows con ControlNet abundante | Rápida | Alta |
| Z Image | Estilo artístico específico | Media | Alta |

## Modelos base de video

| Modelo | Cuándo usarlo | Hardware mínimo |
|---|---|---|
| LTX-2.3 22B distilled | Default para video corto (4-8s) | 24GB VRAM |
| WAN 2.1 / 2.2 | Video con prompt complejo | 24GB VRAM |
| Hunyuan Video | Calidad cinematográfica | 24GB+ VRAM |
| Mochi 1 | Estilo experimental | 24GB+ VRAM |

## Adapters e identidad

| Tecnología | Para qué |
|---|---|
| Flux Redux | Style transfer + identidad con Flux |
| IPAdapter Plus | Identidad con SDXL |
| InstantID | Face swap con preservación de identidad |
| PuLID | Alternativa moderna a Reactor |

## Control y guidance

| Tecnología | Para qué |
|---|---|
| Flux ControlNet Union | Control universal con Flux |
| SDXL ControlNet Union | Control universal con SDXL |
| Depth Anything v2 | Profundidad de alta calidad |

## Upscaling

| Tecnología | Para qué |
|---|---|
| SUPIR | Upscale artístico con detalle |
| CCSR | Upscale fiel al input |
| SeeSR | Upscale con prompt guidance |

## TTS / Voz

| Tecnología | Idioma |
|---|---|
| Qwen3VoiceClone | Multi-idioma incluido español |
| F5-TTS | Inglés primario |
| OpenVoice v2 | Multi-idioma con cloning |

## Workflow tools

| Tecnología | Para qué |
|---|---|
| Comfy Registry (`comfy node install`) | Instalación oficial de custom nodes |
| ComfyDeploy | Hosting de workflows en cloud |
| KJNodes | Utilidades (VRAM_Debug, Math Expression, etc.) |
| rgthree | Power Lora Loader, switches |
| Impact Pack | Nodos avanzados de detección |
| WAS Node Suite | Utilidades misceláneas |
