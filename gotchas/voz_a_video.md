# Gotcha: Workflows de voz+video sobrecargados

Patrón común en pipelines de TTS + generación de video: el usuario duplica el bloque de generación N veces (uno por escena) en vez de usar batching.

## Síntoma

Workflow `.json` con N copias de:
- `Qwen3VoiceClone` (o cualquier TTS)
- `CLIPTextEncode` (positive)
- `KSampler` + `VAE Decode`
- `VHS_VideoCombine`

Más nodos de routing tipo `Any Switch (rgthree)` para alternar entre escenas. Para 4 escenas: ~30 nodos. Para 10: ~70 nodos. Imposible de mantener.

## Diagnóstico rápido

Indicadores en el JSON:
- `"type": "Qwen3VoiceClone"` aparece 3+ veces
- `"type": "VHS_VideoCombine"` aparece 3+ veces
- `"type": "Any Switch (rgthree)"` aparece 5+ veces
- IDs de nodos muy altos (workflow viejo con muchas modificaciones)

## Fix recomendado

Reemplazar TODO el patrón duplicado por 2 nodos del paquete `promptmodels` (sub-módulo `BatchEscenas`):

1. **`PMS_DualPromptListBatch`** (fan-out con `OUTPUT_IS_LIST`)
   - 2 textareas paralelos: voice_prompts y visual_prompts separados por `---`
   - Emite listas — ComfyUI ejecuta el workflow downstream 1 vez por escena automáticamente

2. **`PMS_VideoBatchConcat`** (fan-in con `INPUT_IS_LIST`)
   - Recibe las N salidas de IMAGE y AUDIO como listas
   - Concatena en 1 IMAGE batch + 1 AUDIO continuo
   - Cierra el batch

Conexión:
```
PMS_DualPromptListBatch
    |-- voice_prompt[i]  --> Qwen3VoiceClone --> AUDIO[i]
    |-- visual_prompt[i] --> CLIPTextEncode  --> KSampler --> VAE Decode --> IMAGE[i]
                                                                  |
                                         +------------------------+
                                         |
                           PMS_VideoBatchConcat
                                         |
                           VHS_VideoCombine (final, 1 sola vez)
                                         |
                                   video_completo.mp4
```

## Resultado

- ~30 nodos → ~8 nodos
- Mismo comportamiento, código ejecutado N veces internamente
- Fácil de escalar de 3 a 10 escenas (solo cambiás el textarea)

## Tope recomendado

`max_scenes=5` por default. Más allá de eso, considerar:
- Generar en batches de 5 y hacer postproceso para concatenar
- Migrar a un workflow externo con script Python
- Limitar duración de cada escena a 4-8 segundos (LTX-2.3 sweet spot)

## Cuándo NO aplicar este fix

- Si el usuario quiere control total sobre cada escena (cada una con seed distinto, modelo distinto, etc.)
- Si el workflow es solo de 2 escenas (no vale la pena)
- Si el usuario nunca usó el paquete `promptmodels` (le pediría instalarlo primero)
