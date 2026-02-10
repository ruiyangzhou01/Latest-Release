# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md)

Latest Release is a Python tool that automatically downloads and deploys GitHub Release assets. It helps you keep applications up to date with minimal manual effort.

## Features

### Automated workflow

- Checks for new GitHub Release versions and downloads assets
- Supports automatic extraction and cleanup of archives
- Automatic installation support is under development

### Simple, reusable configuration

- One configuration file can be reused across runs
- Hot reload support for configuration files

## Installation

Choose one of the following options.

### Option 1: Run the Windows executable

Windows only.

1. Go to the [GitHub Releases page](https://github.com/ruiyangzhou01/Latest-Release/releases) and expand **Assets** for the latest release.
2. Download **Latest Release.zip** and unzip it.
3. Create a `config.yaml` file and configure it (see [Usage](#usage)).
4. Open Command Prompt or PowerShell in the folder and run the executable.

### Option 2: Run from Python

Requires Python 3 and pip.

1. Go to the [GitHub Releases page](https://github.com/ruiyangzhou01/Latest-Release/releases) and download **Source code (zip)**.
2. Unzip the archive and create a `config.yaml` file (see [Usage](#usage)).
3. Install dependencies:

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

4. Run the script:

   ```bash
   python main.py
   ```

## Usage

### Commands

After starting the executable or script, enter `help` in the command window to see the available commands.

```
Command[<args>]        : Usage
list/ls                : List installed apps
status/st              : Show status and check for new app versions
update/up              : Update all apps
config/cf              : Open config file to add an app or modify settings
exit/et                : Exit the shell
```

### Configure `config.yaml`

A minimal `config.yaml` file looks like this:

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

#### Top-level fields

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `path` | `str` | - | Default storage path used when `target` is not specified |
| `proxy` | `dict` | - | Optional HTTP/HTTPS proxy settings |
| `repos` | `list` | - | List of repositories to manage |

#### `repos` entries

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `author` | `str` | - | Repository owner |
| `name` | `str` | - | Repository name |
| `tag` | `str` | - | Current release tag; leave empty to download the latest release |
| `key` | `str` | `"all"` | Asset name to download (`all` or empty means all assets) |
| `target` | `str` | `path` | Download destination path |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | Decompression settings |

#### `setting` fields

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` extracts next to the archive, a non-empty value extracts to that folder, and an empty value extracts to `<file_name>_files` |
| `clean` | `bool` | `true` | Remove the archive after extraction |

## Roadmap

- A WinUI3 GUI client is planned.
- More functions and configuration options are planned.

## License

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
