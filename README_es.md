# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md)

Latest Release es una herramienta en Python que descarga y despliega automáticamente los recursos de GitHub Releases. Ayuda a mantener las aplicaciones actualizadas con un esfuerzo manual mínimo.

## Funcionalidades

### Flujo de trabajo automatizado

- Comprueba nuevas versiones de GitHub Releases y descarga recursos
- Soporta extracción automática y limpieza de archivos
- La instalación automática está en desarrollo

### Configuración sencilla y reutilizable

- Un solo archivo de configuración puede reutilizarse en múltiples ejecuciones
- Admite recarga en caliente de los archivos de configuración

## Instalación

Elige una de las siguientes opciones.

### Opción 1: Ejecutar el ejecutable de Windows

Solo para Windows.

1. Ve a la [página de GitHub Releases](https://github.com/ruiyangzhou01/Latest-Release/releases) y expande **Assets** en la versión más reciente.
2. Descarga **Latest Release.zip** y descomprímelo.
3. Crea un archivo `config.yaml` y configúralo (consulta [Uso](#uso)).
4. Abre Símbolo del sistema o PowerShell en la carpeta y ejecuta el archivo ejecutable.

### Opción 2: Ejecutar con Python

Requiere Python 3 y pip.

1. Ve a la [página de GitHub Releases](https://github.com/ruiyangzhou01/Latest-Release/releases) y descarga **Source code (zip)**.
2. Descomprime el archivo y crea `config.yaml` (consulta [Uso](#uso)).
3. Instala las dependencias:

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

4. Ejecuta el script:

   ```bash
   python main.py
   ```

## Uso

### Comandos

Después de iniciar el ejecutable o el script, escribe `help` en la ventana de comandos para ver los comandos disponibles.

```
Command[<args>]        : Usage
list/ls                : Listar aplicaciones instaladas
status/st              : Mostrar estado y comprobar nuevas versiones
update/up              : Actualizar todas las aplicaciones
config/cf              : Abrir el archivo de configuración para añadir apps o modificar ajustes
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
| `path` | `str` | - | Ruta de almacenamiento por defecto cuando no se especifica `target` |
| `proxy` | `dict` | - | Configuración opcional de proxy HTTP/HTTPS |
| `repos` | `list` | - | Lista de repositorios que se gestionarán |

#### Entradas `repos`

| Parámetro | Tipo | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| `author` | `str` | - | Propietario del repositorio |
| `name` | `str` | - | Nombre del repositorio |
| `tag` | `str` | - | Etiqueta de la versión actual; déjalo vacío para descargar la última versión |
| `key` | `str` | `"all"` | Nombre del recurso a descargar (`all` o vacío significa todos los recursos) |
| `target` | `str` | `path` | Ruta de destino para las descargas |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | Ajustes de descompresión |

#### Campos `setting`

| Parámetro | Tipo | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` extrae junto al archivo, un valor no vacío extrae en esa carpeta, un valor vacío extrae en `<file_name>_files` |
| `clean` | `bool` | `true` | Elimina el archivo después de extraer |

## Roadmap

- Se planea un cliente GUI con WinUI3.
- Se planean más funciones y opciones de configuración.

## Licencia

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
