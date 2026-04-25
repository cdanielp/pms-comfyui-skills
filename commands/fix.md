---
name: comfy-fix
description: Diagnostica errores de carga de ComfyUI a partir del log de la consola. Activar cuando el usuario pega un log con "Failed to import", "ImportError", "missing module", "cannot import name", o cuando dice "no me carga el nodo X" / "ComfyUI no arranca".
---

# /comfy:fix — Diagnóstico de errores de carga

## Cuándo activar este comando

El usuario muestra cualquiera de estos síntomas:
- Log de ComfyUI con `Failed to import`, `ImportError`, `ModuleNotFoundError`, `cannot import name`
- Mensaje "missing custom node" en el menú de nodos
- ComfyUI arranca pero un nodo aparece en rojo en el workflow
- Frase como "no me carga", "no arranca", "tira error"
- Sube un archivo de log o pega contenido de consola

## Workflow del diagnóstico

### Paso 1: Identificar la categoría del error

Leer el log y clasificar en una de estas 6 categorías. Cada una tiene fix distinto:

| Categoría | Síntomas en el log | Probabilidad | Fix base |
|---|---|---|---|
| A. Dependencia Python faltante | `ModuleNotFoundError: No module named 'X'` | Muy común | `pip install X` con el venv correcto |
| B. Librería del sistema | `ImportError: libGL.so.1`, `libglib2.0`, `mediapipe` | Común en Linux/Docker | Instalar paquete del sistema operativo |
| C. Versión incompatible | `cannot import name 'X' from 'Y'` | Común | Actualizar el custom node o downgrade ComfyUI |
| D. Snapshot.json desactualizado | `Failed to import` + el nodo existe en disco | ComfyDeploy | Regenerar snapshot.json |
| E. Conflicto de nombres | Dos nodos con el mismo NODE_CLASS_MAPPING key | Raro pero brutal | Renombrar o desinstalar uno |
| F. Custom node corrupto | `__init__.py` traceback raro | Tras update fallido | `git pull` o reinstalar el paquete |

### Paso 2: Diagnóstico estructurado

Para CADA error en el log, dar al usuario:

1. **Categoría** (una de las 6 de arriba)
2. **Diagnóstico en una frase**: qué está pasando realmente
3. **Fix con prioridad**:
   - Fix A (más probable): comando exacto a ejecutar
   - Fix B (si A falla): plan B
4. **Cómo verificar** que el fix funcionó (qué debería ver el usuario)

### Paso 3: Casos especiales

Antes de responder, revisar `gotchas/`:

- Si el log menciona `libGL`, `mediapipe`, `cv2` en contexto Docker o ComfyDeploy → leer `gotchas/comfydeploy.md`
- Si el log tiene caracteres tipo `cp1252`, `UnicodeDecodeError`, `'✓'` → leer `gotchas/windows-encoding.md`
- Si menciona `Qwen3VoiceClone`, `LTX`, o multiplicación de nodos `Any Switch` → leer `gotchas/voz_a_video.md`

### Paso 4: Output esperado

Estructurar la respuesta en español así:

```
## Diagnóstico

**Categoría**: [A/B/C/D/E/F] — [nombre legible]
**Qué está pasando**: [una frase clara]
**Custom node afectado**: [nombre del paquete]

## Fix

### Opción 1 (más probable, intentá esto primero)
\`\`\`bash
[comando exacto]
\`\`\`

### Opción 2 (si la 1 falla)
[descripción del plan B con comando]

## Cómo verificar que funcionó
1. [acción]
2. [qué debería ver]

## Si nada funciona
[ruta de escalamiento: revisar gotchas, abrir issue en el repo del custom node, etc.]
```

## Reglas duras de este comando

1. **NO sugerir reinstalar todo ComfyUI** salvo que sea último recurso. Es lento y destructivo.

2. **NO ejecutar `pip install` sin saber el venv** que usa el ComfyUI del usuario. Preguntar si no está claro:
   - "¿Usás el venv de ComfyUI portable, una instalación manual con venv propio, o Docker?"

3. **Si el log es muy largo (>200 líneas)**, pedir al usuario que pegue solo la sección desde el primer `Failed to import` hasta el siguiente `Adding custom nodes`. Más contexto no ayuda y satura.

4. **Si hay 5+ errores distintos**, NO intentar resolver todos a la vez. Resolver el primero, decirle al usuario que reinicie y vuelva a copiar el log nuevo. Los errores en cadena suelen tener una raíz común que se ve mejor después del primer fix.

5. **Verificar que el paquete del nodo aún se mantenga**: si el último commit del repo tiene >12 meses, advertir al usuario que el paquete puede estar abandonado y sugerir reemplazo.

## Ejemplo de uso

Usuario pega:
```
Failed to import custom node from: ComfyUI-AnimateDiff-Evolved
Traceback (most recent call last):
  File "...", line 8, in <module>
    import cv2
ModuleNotFoundError: No module named 'cv2'
```

Respuesta esperada del comando:

```
## Diagnóstico

**Categoría**: A — Dependencia Python faltante
**Qué está pasando**: el paquete ComfyUI-AnimateDiff-Evolved necesita opencv-python (`cv2`) y no está instalado en tu venv de ComfyUI.
**Custom node afectado**: ComfyUI-AnimateDiff-Evolved

Aviso adicional: AnimateDiff está en `references/deprecated-2026.md`. Para tareas de video nuevas, considerá LTX-2.3 o WAN 2.2 (ver alternativas modernas).

## Fix

### Opción 1
Activar el venv de tu ComfyUI y ejecutar:
\`\`\`bash
pip install opencv-python
\`\`\`

Si usás ComfyUI portable en Windows:
\`\`\`bash
.\python_embeded\python.exe -m pip install opencv-python
\`\`\`

### Opción 2 (si dice "Could not find a version")
\`\`\`bash
pip install opencv-python-headless
\`\`\`

## Cómo verificar que funcionó
1. Reiniciá ComfyUI completamente (cerrá la ventana)
2. Al arrancar, en la consola debería decir: `[ComfyUI-AnimateDiff-Evolved] Loaded`
3. El nodo debería aparecer en azul (no rojo) en el menú

## Si nada funciona
Verificá que estés en el venv correcto con: `which python` (Linux/Mac) o `where python` (Windows). Si tu sistema tiene varios Python instalados, podrías estar instalando en el equivocado.
```
