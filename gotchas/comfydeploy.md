# Gotchas conocidos: ComfyDeploy

Problemas reales que el autor (PMS) enfrentó deployando workflows a ComfyDeploy. Cada uno con su fix probado.

## libGL.so.1 missing

**Síntoma**: `ImportError: libGL.so.1: cannot open shared object file`

**Causa**: el container Docker base de ComfyDeploy no incluye librerías gráficas que algunos nodos asumen presentes (típicamente OpenCV, mediapipe, ultralytics).

**Fix**: agregar al Dockerfile de ComfyDeploy o al setup script:
```bash
apt-get update && apt-get install -y libgl1 libglib2.0-0
```

Si no podés modificar el Dockerfile, usar la versión `-headless` del paquete Python:
```bash
pip install opencv-python-headless
# en vez de
pip install opencv-python
```

## mediapipe build failure

**Síntoma**: error compilando `mediapipe` durante `pip install`, mensaje sobre `bazel` o `protobuf`.

**Causa**: mediapipe requiere C++ build chain que no siempre está en el container.

**Fix**: usar versión pre-buildeada:
```bash
pip install mediapipe-silicon  # si Mac M1/M2
pip install mediapipe==0.10.14  # versión estable conocida
```

## snapshot.json desactualizado

**Síntoma**: el deploy reporta `Failed to import` para nodos que SÍ existen en el repo del custom node.

**Causa**: ComfyDeploy usa `snapshot.json` para reproducir el environment. Si el snapshot apunta a un commit viejo del custom node, intenta importar la versión vieja.

**Fix**:
1. En tu ComfyUI local, asegurate de tener la versión actualizada del custom node:
```bash
cd ComfyUI/custom_nodes/<paquete>
git pull
```
2. Regenerar snapshot:
   - En ComfyUI Manager: "Snapshot Manager" → "Save snapshot"
   - O manualmente: editar `snapshot.json` y poner el commit SHA correcto
3. Re-subir snapshot.json a ComfyDeploy

## Seed value overflow

**Síntoma**: error tipo `OverflowError: int too large to convert to C long` o KSampler tirando seed inválido.

**Causa**: ComfyDeploy serializa seeds como int32 mientras que ComfyUI local usa int64. Seeds grandes (>2^31) tronan al pasar por la API.

**Fix**: limitar seeds en tu workflow a `2147483647` máximo. En el `KSampler`:
```
seed: 2147483647 (en vez de algo tipo 368238446106056)
```

## Custom node solo en local

**Síntoma**: el deploy falla porque un nodo no existe en cloud.

**Causa**: instalaste un custom node desde un .zip o git clone manual que NO está en Comfy Registry.

**Fix**: o bien
- Publicar el custom node al registry (si es tuyo)
- O desinstalarlo y reemplazarlo por uno equivalente del registry
- O usar deploy con custom Docker image
