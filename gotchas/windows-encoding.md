# Gotchas conocidos: Encoding en Windows

## Símbolos Unicode revientan en consola Windows

**Síntoma**: error tipo `'charmap' codec can't encode character '✓'` o el comando se queda colgado sin imprimir nada.

**Causa**: la consola PowerShell/CMD de Windows usa codepage `cp1252` por default, que no incluye emojis ni símbolos como checkmark, advertencia, etc.

**Fix temporal** (para esta sesión):
```powershell
$env:PYTHONUTF8="1"
python tu_script.py
```

**Fix permanente** (variable de sistema):
1. Win+R → `sysdm.cpl` → pestaña "Avanzado" → "Variables de entorno"
2. Agregar nueva variable de usuario: `PYTHONUTF8 = 1`
3. Reiniciar PowerShell

**Para custom nodes que vas a publicar**: NUNCA uses emojis en `print()` dentro del código del nodo. Usa prefijos ASCII:
```python
# Mal
print("[Mi Nodo] OK - Cargado correctamente")

# Bien
print("[Mi Nodo] OK - Cargado correctamente")
```

## Path con espacios

**Síntoma**: `comfy node publish` o cualquier comando con paths reporta "file not found" cuando el path tiene espacios.

**Fix**: siempre usar comillas dobles:
```powershell
Set-Location "C:\Users\PC\Desktop\COMFYUI_PROMPTMODELS"
# en vez de
Set-Location C:\Users\PC\Desktop\COMFYUI_PROMPTMODELS
```

## Git pide credenciales en cada push

**Síntoma**: cada `git push` te pide usuario y contraseña, incluso después de haberlos puesto.

**Causa**: GitHub deprecó password auth en 2021. Necesitás Personal Access Token o GitHub CLI.

**Fix**:
```powershell
gh auth login
# seguir el flow web, autenticar con tu cuenta
gh auth setup-git
```
