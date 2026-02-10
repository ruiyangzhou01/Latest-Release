# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md) | [日本語 README](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_ja.md)

Latest Release is a command-line Python tool that checks the latest GitHub releases for a list of repositories and downloads their assets to your machine. It stores the current release tag in `config.yaml` and updates it after each download to track what is installed.

## Features

- Uses the GitHub Releases API to compare the stored tag with the latest release
- Downloads all assets or a single asset matching a keyword
- Updates `config.yaml` with the newest tag after downloading
- Optional archive extraction for `.gz`, `.tar`, `.zip`, and `.rar` files, with optional cleanup
- Optional HTTP/HTTPS proxy for API calls and downloads
- Reloads `config.yaml` on every command so edits take effect immediately

## Requirements

- Python 3 and pip (when running from source)
- `requests`, `ruamel.yaml`, `tqdm`, `pyyaml`
- `rarfile` (only required to extract `.rar` archives)

## Installation

Choose one of the following options.

### Option 1: Run the Windows executable

Windows only.

1. Go to the [GitHub Releases page](https://github.com/ruiyangzhou01/Latest-Release/releases) and expand **Assets** for the latest release.
2. Download **Latest Release.zip** and unzip it.
3. Make sure a `config.yaml` file exists and configure it (see [Usage](#usage)).
4. Open Command Prompt or PowerShell in the folder and run the executable.

### Option 2: Run from Python

Requires Python 3 and pip.

1. Go to the [GitHub Releases page](https://github.com/ruiyangzhou01/Latest-Release/releases) and download **Source code (zip)**.
2. Unzip the archive and create a `config.yaml` file (see [Usage](#usage)).
3. Install dependencies:

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

   Optional for `.rar` extraction:

   ```bash
   pip install rarfile
   ```

4. Run the script:

   ```bash
   python main.py
   ```

## Usage

Start the executable or script. If `config.yaml` does not exist, a template file is created in the current directory. Update it with your repositories, then run the commands below. The file is reloaded on every command.

### Commands

```
Command[<args>]        : Usage
list/ls                : List configured repositories and stored tags
status/st              : Show status and compare against the latest release
update/up              : Download latest release assets for all repositories
config/cf              : Open config.yaml in VS Code or Notepad
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
| `path` | `str` | - | Default download root. When `target` is empty, files are stored under `path\\<name>\\<tag>\\` |
| `proxy` | `dict` | - | Optional HTTP/HTTPS proxy settings passed to requests |
| `repos` | `list` | - | List of repositories to manage |

#### `repos` entries

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `author` | `str` | - | Repository owner |
| `name` | `str` | - | Repository name |
| `tag` | `str` | - | Last downloaded release tag; leave empty to download the latest release |
| `key` | `str` | `"all"` | Asset name filter (`all` or empty means all assets; otherwise the first filename containing the key is downloaded) |
| `target` | `str` | `path` | Download destination path; leave empty to use `path` |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | Archive extraction settings (applies to `.gz`, `.tar`, `.zip`, `.rar`) |

#### `setting` fields

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` extracts next to the archive, a non-empty value extracts to that folder, and an empty value extracts to `<file_name>_files` |
| `clean` | `bool` | `true` | Remove the archive after extraction |

Non-archive assets are left in place without extraction.

## License

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
