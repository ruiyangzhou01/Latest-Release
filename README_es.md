# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md) | [日本語 README](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_ja.md)

Latest Release es una herramienta de línea de comandos en Python que consulta las últimas releases de GitHub para una lista de repositorios y descarga sus recursos en tu equipo. Guarda la etiqueta de release actual en `config.yaml` y la actualiza después de cada descarga para hacer seguimiento de lo instalado.

## Funcionalidades

- Usa la API de GitHub Releases para comparar la etiqueta guardada con la última versión
- Descarga todos los recursos o un único recurso que coincida con una palabra clave
- Actualiza `config.yaml` con la etiqueta más reciente después de descargar
- Extracción opcional de `.gz`, `.tar`, `.zip` y `.rar` con limpieza opcional
- Proxy HTTP/HTTPS opcional para llamadas a la API y descargas
- `config.yaml` se recarga en cada comando para que los cambios surtan efecto de inmediato

## Requisitos

- Python 3 y pip (si se ejecuta desde el código fuente)
- `requests`, `ruamel.yaml`, `tqdm`, `pyyaml`
- `rarfile` (solo necesario para extraer archivos `.rar`)

## Instalación

Elige una de las siguientes opciones.

### Opción 1: Ejecutar el ejecutable de Windows

Solo para Windows.

1. Ve a la [página de GitHub Releases](https://github.com/ruiyangzhou01/Latest-Release/releases) y expande **Assets** en la versión más reciente.
2. Descarga **Latest Release.zip** y descomprímelo.
3. Asegúrate de que exista un archivo `config.yaml` y configúralo (consulta [Uso](#uso)).
4. Abre Símbolo del sistema o PowerShell en la carpeta y ejecuta el archivo ejecutable.

### Opción 2: Ejecutar con Python

Requiere Python 3 y pip.

1. Ve a la [página de GitHub Releases](https://github.com/ruiyangzhou01/Latest-Release/releases) y descarga **Source code (zip)**.
2. Descomprime el archivo y crea `config.yaml` (consulta [Uso](#uso)).
3. Instala las dependencias:

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

   Opcional para extraer `.rar`:

   ```bash
   pip install rarfile
   ```

4. Ejecuta el script:

   ```bash
   python main.py
   ```

## Uso

Inicia el ejecutable o el script. Si `config.yaml` no existe, se crea una plantilla en el directorio actual. Actualiza tus repositorios y ejecuta los comandos siguientes; el archivo se recarga en cada comando.

### Comandos

```
Command[<args>]        : Usage
list/ls                : Listar repositorios configurados y etiquetas guardadas
status/st              : Mostrar estado y comparar con la última release
update/up              : Descargar recursos de la última release para todos los repositorios
config/cf              : Abrir config.yaml en VS Code o Notepad
exit/et                : Salir de la consola
```

### Configurar `config.yaml`

Un `config.yaml` mínimo se ve así:

```yaml
path: download
proxy:
  http: http://127.0.0.1:7890
  https: http://127.0.0.1:7890
repos:
  - author: ruiyangzhou01
    name: Liquid
    tag:
    key: Liquid.zip
    target:
    setting: { decompress: auto, clean: true }
```

#### Campos de nivel superior

| Parámetro | Tipo | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| `path` | `str` | - | Raíz de descarga por defecto. Cuando `target` está vacío, los archivos se guardan en `path\\<name>\\<tag>\\` |
| `proxy` | `dict` | - | Configuración opcional de proxy HTTP/HTTPS pasada a requests |
| `repos` | `list` | - | Lista de repositorios que se gestionarán |

#### Entradas `repos`

| Parámetro | Tipo | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| `author` | `str` | - | Propietario del repositorio |
| `name` | `str` | - | Nombre del repositorio |
| `tag` | `str` | - | Etiqueta de la última release descargada; déjalo vacío para descargar la última versión |
| `key` | `str` | `"all"` | Filtro de recursos (`all` o vacío descarga todos; si no, se descarga el primer archivo que contenga la clave) |
| `target` | `str` | `path` | Ruta de destino para las descargas; déjalo vacío para usar `path` |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | Ajustes de extracción (aplica a `.gz`, `.tar`, `.zip`, `.rar`) |

#### Campos `setting`

| Parámetro | Tipo | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` extrae junto al archivo, un valor no vacío extrae en esa carpeta, un valor vacío extrae en `<file_name>_files` |
| `clean` | `bool` | `true` | Elimina el archivo después de extraer |

Los recursos que no son archivos comprimidos se dejan tal cual, sin extraer.

## Licencia

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
