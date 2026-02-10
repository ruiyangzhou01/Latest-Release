# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md)

Latest Release ist ein Python-Tool, das GitHub-Release-Assets automatisch herunterlädt und bereitstellt. Es hilft, Anwendungen mit minimalem manuellen Aufwand aktuell zu halten.

## Funktionen

### Automatisierter Ablauf

- Prüft GitHub Releases auf neue Versionen und lädt Assets herunter
- Unterstützt automatisches Entpacken und Aufräumen von Archiven
- Automatische Installation ist in Entwicklung

### Einfache, wiederverwendbare Konfiguration

- Eine Konfigurationsdatei kann für mehrere Läufe genutzt werden
- Unterstützt Hot Reload von Konfigurationsdateien

## Installation

Wähle eine der folgenden Optionen.

### Option 1: Windows-Executable ausführen

Nur für Windows.

1. Gehe zur [GitHub-Releases-Seite](https://github.com/ruiyangzhou01/Latest-Release/releases) und klappe **Assets** beim neuesten Release aus.
2. Lade **Latest Release.zip** herunter und entpacke es.
3. Erstelle eine `config.yaml`-Datei und konfiguriere sie (siehe [Verwendung](#verwendung)).
4. Öffne die Eingabeaufforderung oder PowerShell im Ordner und starte die ausführbare Datei.

### Option 2: Mit Python ausführen

Erfordert Python 3 und pip.

1. Gehe zur [GitHub-Releases-Seite](https://github.com/ruiyangzhou01/Latest-Release/releases) und lade **Source code (zip)** herunter.
2. Entpacke das Archiv und erstelle eine `config.yaml`-Datei (siehe [Verwendung](#verwendung)).
3. Installiere die Abhängigkeiten:

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

4. Starte das Skript:

   ```bash
   python main.py
   ```

## Verwendung

### Befehle

Nach dem Start der ausführbaren Datei oder des Skripts kannst du mit `help` im Befehlsfenster die verfügbaren Befehle anzeigen.

```
Command[<args>]        : Usage
list/ls                : Installierte Apps auflisten
status/st              : Status anzeigen und neue Versionen prüfen
update/up              : Alle Apps aktualisieren
config/cf              : Konfigurationsdatei öffnen, um Apps hinzuzufügen oder Einstellungen zu ändern
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
| `path` | `str` | - | Standard-Speicherpfad, wenn `target` nicht angegeben ist |
| `proxy` | `dict` | - | Optionale HTTP/HTTPS-Proxy-Einstellungen |
| `repos` | `list` | - | Liste der zu verwaltenden Repositories |

#### `repos`-Einträge

| Parameter | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `author` | `str` | - | Repository-Eigentümer |
| `name` | `str` | - | Repository-Name |
| `tag` | `str` | - | Aktueller Release-Tag; leer lassen, um das neueste Release zu laden |
| `key` | `str` | `"all"` | Name des herunterzuladenden Assets (`all` oder leer bedeutet alle Assets) |
| `target` | `str` | `path` | Zielpfad für Downloads |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | Entpackeinstellungen |

#### `setting`-Felder

| Parameter | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` entpackt neben dem Archiv, ein nicht leerer Wert entpackt in diesen Ordner, ein leerer Wert in `<file_name>_files` |
| `clean` | `bool` | `true` | Archiv nach dem Entpacken löschen |

## Roadmap

- Ein WinUI3-GUI-Client ist geplant.
- Weitere Funktionen und Konfigurationsoptionen sind geplant.

## Lizenz

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
