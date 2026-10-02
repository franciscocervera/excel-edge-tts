# Excel Edge TTS

Genera archivos MP3 en lote a partir de un catálogo de textos en Excel mediante `edge-tts`. La utilidad incluye control de voz, velocidad, volumen, tono, concurrencia, reintentos y protección contra sobrescritura accidental.

El repositorio incluye `catalogo_audios.xlsx` con datos de ejemplo, por lo que puede ejecutarse inmediatamente después de instalar las dependencias.

## Requisitos

- Python 3.10 o superior.
- Conexión a Internet durante la generación de audio.
- Un archivo `.xlsx` con las columnas `Audio_ID` y `Texto`.

## Instalación

Clona o descarga el repositorio y abre una terminal dentro de la carpeta `excel-edge-tts`. Después crea un entorno virtual:

```bash
python -m venv .venv
```

Actívalo en Windows:

```powershell
.venv\Scripts\Activate.ps1
```

O en macOS/Linux:

```bash
source .venv/bin/activate
```

Instala las dependencias:

```bash
pip install -r requirements.txt
```

## Uso rápido

Con el catálogo incluido y la configuración predeterminada:

```bash
python generar_audios_edge_tts.py
```

Los archivos se guardan en la carpeta `audio/`. Cada MP3 toma su nombre de la columna `Audio_ID`.

### Opciones principales

| Opción | Predeterminado | Función |
| --- | --- | --- |
| `excel` | `catalogo_audios.xlsx` | Archivo Excel de entrada. |
| `--sheet` | `Audios_TTS` | Hoja que contiene el catálogo. |
| `--output` | `audio` | Carpeta donde se guardan los MP3. |
| `--voice` | `es-MX-DaliaNeural` | Voz utilizada por Edge TTS. |
| `--rate` | `+0%` | Ajuste de velocidad. |
| `--volume` | `+0%` | Ajuste de volumen. |
| `--pitch` | `+0Hz` | Ajuste de tono. |
| `--concurrency` | `3` | Cantidad de solicitudes simultáneas. |
| `--retries` | `3` | Reintentos máximos por audio. |
| `--overwrite` | Desactivado | Regenera archivos MP3 que ya existen. |

## Cambiar la voz

`edge-tts` permite consultar las voces disponibles desde su propia herramienta de línea de comandos:

```bash
edge-tts --list-voices
```

Después utiliza el nombre de la voz con `--voice`:

```bash
python generar_audios_edge_tts.py --voice es-MX-JorgeNeural
```

## Regenerar archivos existentes

Por seguridad, un MP3 existente no se reemplaza. Para forzar su regeneración:

```bash
python generar_audios_edge_tts.py --overwrite
```

## Usar otro catálogo

Puedes indicar otro archivo como primer argumento:

```bash
python generar_audios_edge_tts.py datos/mis_audios.xlsx
```

Y, si la hoja tiene otro nombre:

```bash
python generar_audios_edge_tts.py datos/mis_audios.xlsx --sheet Textos
```
