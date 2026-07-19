# Rclone GUI — Interfaz gráfica para rclone

![screenshot](https://github.com/mggons93/rclone_gui/blob/main/img/captura1.PNG?raw=true)

## Descripción

Rclone GUI es una interfaz gráfica (GUI) y herramienta auxiliar para gestionar y ejecutar operaciones con `rclone`. Permite configurar remotos, lanzar sincronizaciones y copias, y visualizar el estado y los logs de las transferencias sin necesidad de utilizar únicamente la línea de comandos.

## Badges

- Versión: v2.0 (ver `version_info.txt`)
- Licencia: MIT (o la que el proyecto use)

## Tabla de contenidos

- [Descripción](#descripción)
- [Características](#características)
- [Integración con rclone](#integración-con-rclone)
- [Interfaz y flujo de uso](#interfaz-y-flujo-de-uso)
- [Uso por línea de comandos](#uso-por-línea-de-comandos)
- [Instalación](#instalación)
- [Configuración](#configuración)
- [Empaquetado y distribución](#empaquetado-y-distribución)
- [Ejemplos prácticos](#ejemplos-prácticos)
- [Resolución de problemas](#resolución-de-problemas)
- [Contribuir](#contribuir)
- [Changelog](#changelog)
- [Licencia y autores](#licencia-y-autores)
- [Contacto](#contacto)

## Características

- Interfaz gráfica para crear y editar remotos de `rclone`.
- Ejecutar operaciones comunes: `sync`, `copy`, `move`, `mount`, `ls`, `check`.
- Guardado y gestión de configuraciones locales (`rclone.conf`, `rclone_gui_config.json`).
- Logs y panel de estado para ver transferencias en tiempo real.
- Interfaz ligera y multiplataforma (usa `rclone` como backend).

## Integración con rclone

El programa actúa como frontend para `rclone`, invocando el binario de `rclone` con los parámetros adecuados. Algunas integraciones importantes:

- Usa `rclone.conf` para leer y escribir remotos.
- Ejecuta comandos como `rclone sync`, `rclone copy`, `rclone ls`, `rclone mount`.
- Interpreta códigos de salida y captura stdout/stderr para mostrar logs en la GUI.

Ejemplo de invocación (interno de la aplicación):

```bash
rclone copy "C:/Mi/Carpeta" "remote:backup/Carpeta" --progress --config "./rclone.conf"
```

## Interfaz y flujo de uso

1. Abrir la aplicación (`Rclone_GUI_2.0.py` o el ejecutable generado).
2. Configurar remotos desde el panel de configuración o importar `rclone.conf`.
3. Seleccionar origen y destino en la pantalla principal.
4. Elegir operación (`sync`, `copy`, `check`) y opciones avanzadas.
5. Ejecutar y seguir el progreso en el panel de logs.

![screenshot](docs/screenshot.png)

## Uso por línea de comandos

Aunque la intención principal es la GUI, la aplicación incluye utilidades y scripts que pueden ejecutarse por CLI.

Ejemplos:

```bash
# Ejecutar la GUI (Python)
python Rclone_GUI_2.0.py
```

## Instalación

Requisitos previos:

- Python 3.8+ (recomendado 3.10+)
- rclone (instalado y accesible en PATH)

Instalación en Windows (rápida):

```powershell
# Instala dependencias si el proyecto incluye requirements.txt
python -m pip install -r requirements.txt

# Ejecuta la GUI
python Rclone_GUI_2.0.py
```

Linux / macOS:

```bash
python3 -m pip install -r requirements.txt
python3 Rclone_GUI_2.0.py
```

Usar los scripts de build (Windows):

```powershell
.\build_debug.bat      # empaqueta en modo debug para pruebas
.\build_rclone_gui.bat # empaqueta la GUI para distribución
```

## Configuración

Archivos de configuración importantes:

- `rclone.conf` — Configuración de remotos de `rclone`.
- `rclone_gui_config.json` — Preferencias de la GUI (UI, rutas por defecto, opciones guardadas).

Ejemplo mínimo `rclone.conf`:

```conf
[remote]
type = s3
provider = AWS
env_auth = false
access_key_id = TU_ACCESS_KEY
secret_access_key = TU_SECRET_KEY
region = us-east-1
endpoint = 
```

Ejemplo `rclone_gui_config.json`:

```json
{
  "last_source": "C:/Mi/Carpeta",
  "last_destination": "remote:backup/Carpeta",
  "rclone_path": "rclone",
  "log_level": "INFO"
}
```

Nota: No incluyas credenciales en repositorios públicos. Usa variables de entorno o archivos ignorados por git.

## Empaquetado y distribución

El repo incluye archivos `.spec` (posiblemente para PyInstaller). Los artefactos generados aparecen en `build/`.

Pasos generales para crear un ejecutable (ejemplo genérico):

```bash
pyinstaller --onefile --name "Rclone GUI V2.0" Rclone_GUI_2.0.py
```

O usar los scripts incluidos en Windows: `build_debug.bat` y `build_rclone_gui.bat`.

## Ejemplos prácticos y casos de uso

- Copia local a remoto:

```bash
rclone copy "C:/Fotos" "remote:backup/fotos" --progress
```

- Sincronizar carpetas remotas:

```bash
rclone sync "remoteA:carpeta/" "remoteB:carpeta/" --transfers=8 --checksum
```

## Resolución de problemas

- rclone no encontrado: asegúrate de que `rclone` esté en el `PATH` o configura `rclone_path` en `rclone_gui_config.json`.
- Errores de permisos: revisa credenciales en `rclone.conf` y la configuración del proveedor.
- Logs: revisa la salida en el panel de logs de la GUI o ejecuta el comando con `--log-level DEBUG`.

## Contribuir

1. Fork del repositorio.
2. Crea una rama para tu feature: `git checkout -b feature/nombre`.
3. Añade tests si aplica.
4. Haz commit con mensajes claros y crea un PR.

Normas de estilo: sigue la convención de Python del proyecto y añade cambios en la documentación.

## Changelog

Consulta `version_info.txt` para la versión actual. Ejemplo de entradas de changelog:

- v2.0 — Interfaz gráfica renovada, soporte de logs, mejoras de empaquetado.

## Licencia y autores

Indica la licencia del proyecto (por ejemplo MIT). Autores:

- Nombre del autor / mantenedor — correo@ejemplo.com

## Contacto

Abre un issue en el repositorio GitHub o envía un email a correo@ejemplo.com para soporte.

---

Notas finales:

-- Reemplaza marcadores y ejemplos de credenciales por valores reales antes de desplegar.
-- Añade capturas de pantalla en `docs/` y actualiza la sección de badges con enlaces reales.

## Cambios de versión

- v2.0 — Interfaz gráfica renovada; mejoras en gestión de remotos y soporte de logs.
- v1.0 — Primera versión pública: integración básica con `rclone`, operaciones `copy` y `sync`.

Plantilla para nuevas entradas de versión:

```markdown
- vX.Y — Resumen breve. (YYYY-MM-DD)
  - Cambios destacados:
    - Punto 1
    - Punto 2
```

Actualiza `version_info.txt` y esta sección al publicar nuevas versiones.
