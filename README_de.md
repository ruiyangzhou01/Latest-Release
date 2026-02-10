# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md) | [日本語 README](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_ja.md)

Latest Release ist ein Kommandozeilen-Tool in Python, das die neuesten GitHub-Releases für eine Liste von Repositories prüft und deren Assets auf deinen Rechner herunterlädt. Es speichert den aktuellen Release-Tag in `config.yaml` und aktualisiert ihn nach jedem Download, um installierte Versionen nachzuverfolgen.

## Funktionen

- Verwendet die GitHub-Releases-API, um den gespeicherten Tag mit dem neuesten Release zu vergleichen
- Lädt alle Assets oder ein einzelnes Asset mit einem passenden Schlüsselwort herunter
- Aktualisiert `config.yaml` nach dem Download mit dem neuesten Tag
- Optionale Entpackung von `.gz`, `.tar`, `.zip` und `.rar` inklusive optionaler Bereinigung
- Optionale HTTP/HTTPS-Proxys für API-Aufrufe und Downloads
- `config.yaml` wird bei jedem Befehl neu geladen, sodass Änderungen sofort greifen

## Voraussetzungen

- Python 3 und pip (wenn aus dem Quellcode ausgeführt)
- `requests`, `ruamel.yaml`, `tqdm`, `pyyaml`
- `rarfile` (nur erforderlich zum Entpacken von `.rar`-Archiven)

## Installation

Wähle eine der folgenden Optionen.

### Option 1: Windows-Executable ausführen

Nur für Windows.

1. Gehe zur [GitHub-Releases-Seite](https://github.com/ruiyangzhou01/Latest-Release/releases) und klappe **Assets** beim neuesten Release aus.
2. Lade **Latest Release.zip** herunter und entpacke es.
3. Stelle sicher, dass eine `config.yaml`-Datei vorhanden ist und konfiguriere sie (siehe [Verwendung](#verwendung)).
4. Öffne die Eingabeaufforderung oder PowerShell im Ordner und starte die ausführbare Datei.

### Option 2: Mit Python ausführen

Erfordert Python 3 und pip.

1. Gehe zur [GitHub-Releases-Seite](https://github.com/ruiyangzhou01/Latest-Release/releases) und lade **Source code (zip)** herunter.
2. Entpacke das Archiv und erstelle eine `config.yaml`-Datei (siehe [Verwendung](#verwendung)).
3. Installiere die Abhängigkeiten:

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

   Optional für `.rar`-Entpackung:

   ```bash
   pip install rarfile
   ```

4. Starte das Skript:

   ```bash
   python main.py
   ```

## Verwendung

Starte die ausführbare Datei oder das Skript. Wenn `config.yaml` fehlt, wird im aktuellen Verzeichnis eine Vorlage erstellt. Aktualisiere die Repositories und führe anschließend die Befehle aus; die Datei wird bei jedem Befehl neu geladen.

### Befehle

```
Command[<args>]        : Usage
list/ls                : Konfigurierte Repositories und gespeicherte Tags auflisten
status/st              : Status anzeigen und mit dem neuesten Release vergleichen
update/up              : Aktuelle Release-Assets für alle Repositories herunterladen
config/cf              : config.yaml in VS Code oder Notepad öffnen
exit/et                : Die Shell beenden
```

### `config.yaml` konfigurieren

Eine minimale `config.yaml` sieht so aus:

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

#### Felder auf oberster Ebene

| Parameter | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `path` | `str` | - | Standard-Download-Stamm. Wenn `target` leer ist, werden Dateien unter `path\\<name>\\<tag>\\` gespeichert |
| `proxy` | `dict` | - | Optionale HTTP/HTTPS-Proxy-Einstellungen für requests |
| `repos` | `list` | - | Liste der zu verwaltenden Repositories |

#### `repos`-Einträge

| Parameter | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `author` | `str` | - | Repository-Eigentümer |
| `name` | `str` | - | Repository-Name |
| `tag` | `str` | - | Zuletzt heruntergeladener Release-Tag; leer lassen, um das neueste Release zu laden |
| `key` | `str` | `"all"` | Asset-Filter (`all` oder leer bedeutet alle Assets; ansonsten wird die erste Datei mit dem Schlüsselwort geladen) |
| `target` | `str` | `path` | Zielpfad für Downloads; leer lassen, um `path` zu verwenden |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | Entpackeinstellungen (gilt für `.gz`, `.tar`, `.zip`, `.rar`) |

#### `setting`-Felder

| Parameter | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` entpackt neben dem Archiv, ein nicht leerer Wert entpackt in diesen Ordner, ein leerer Wert in `<file_name>_files` |
| `clean` | `bool` | `true` | Archiv nach dem Entpacken löschen |

Nicht-Archive bleiben unverändert, ohne Entpacken.

## Lizenz

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
