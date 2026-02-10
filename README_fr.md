# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md) | [日本語 README](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_ja.md)

Latest Release est un outil en ligne de commande Python qui interroge les dernières GitHub Releases d'une liste de dépôts et télécharge leurs ressources sur votre machine. Il enregistre le tag de release actuel dans `config.yaml` et le met à jour après chaque téléchargement pour suivre ce qui est installé.

## Fonctionnalités

- Utilise l'API GitHub Releases pour comparer le tag enregistré avec la dernière release
- Télécharge toutes les ressources ou une ressource unique correspondant à un mot-clé
- Met à jour `config.yaml` avec le tag le plus récent après le téléchargement
- Extrait automatiquement les fichiers `.gz`, `.tar`, `.zip` et `.rar` et nettoie les archives téléchargées (sans option de désactivation)
- Proxy HTTP/HTTPS facultatif pour les appels API et les téléchargements
- `config.yaml` est rechargé à chaque commande afin que les modifications soient immédiates

## Prérequis

- Python 3 et pip (si vous exécutez depuis le code source)
- `requests`, `ruamel.yaml`, `tqdm`, `pyyaml`
- `rarfile` (uniquement requis pour extraire les archives `.rar`)

## Installation

Choisissez l'une des options suivantes.

### Option 1 : Exécuter l'exécutable Windows

Windows uniquement.

1. Rendez-vous sur la [page des GitHub Releases](https://github.com/ruiyangzhou01/Latest-Release/releases) et développez **Assets** pour la dernière version.
2. Téléchargez **Latest Release.zip** et décompressez-le.
3. Assurez-vous qu'un fichier `config.yaml` existe et configurez-le (voir [Utilisation](#utilisation)).
4. Ouvrez l'invite de commandes ou PowerShell dans le dossier et lancez l'exécutable.

### Option 2 : Exécuter avec Python

Nécessite Python 3 et pip.

1. Rendez-vous sur la [page des GitHub Releases](https://github.com/ruiyangzhou01/Latest-Release/releases) et téléchargez **Source code (zip)**.
2. Décompressez l'archive et créez `config.yaml` (voir [Utilisation](#utilisation)).
3. Installez les dépendances :

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

   Optionnel pour extraire `.rar` :

   ```bash
   pip install rarfile
   ```

4. Lancez le script :

   ```bash
   python main.py
   ```

## Utilisation

Démarrez l'exécutable ou le script. Si `config.yaml` n'existe pas, un modèle est créé dans le répertoire courant. Mettez à jour vos dépôts puis exécutez les commandes ci-dessous ; le fichier est rechargé à chaque commande.

### Commandes

```
Command[<args>]        : Usage
list/ls                : Lister les applications installées
status/st              : Afficher l'état et vérifier les nouvelles versions des applications
update/up              : Mettre à jour toutes les applications
config/cf              : Ouvrir le fichier de configuration pour ajouter une application ou modifier les réglages
exit/et                : Quitter le shell
```

### Configurer `config.yaml`

Un `config.yaml` minimal ressemble à ceci :

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

#### Champs de niveau supérieur

| Paramètre | Type | Valeur par défaut | Description |
| --- | --- | --- | --- |
| `path` | `str` | - | Racine de téléchargement par défaut. Quand `target` est vide, les fichiers sont stockés dans `path\\<name>\\<tag>\\` |
| `proxy` | `dict` | - | Paramètres de proxy HTTP/HTTPS facultatifs transmis à requests |
| `repos` | `list` | - | Liste des dépôts à gérer |

#### Entrées `repos`

| Paramètre | Type | Valeur par défaut | Description |
| --- | --- | --- | --- |
| `author` | `str` | - | Propriétaire du dépôt |
| `name` | `str` | - | Nom du dépôt |
| `tag` | `str` | - | Tag de la dernière release téléchargée ; laissez vide pour récupérer la dernière release |
| `key` | `str` | `"all"` | Filtre d'asset (`all` ou vide pour tout télécharger ; sinon le premier fichier contenant la clé est téléchargé) |
| `target` | `str` | `path` | Chemin de destination des téléchargements ; laissez vide pour utiliser `path` |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | Paramètres d'extraction (toujours appliqués à `.gz`, `.tar`, `.zip`, `.rar`) |

#### Champs `setting`

| Paramètre | Type | Valeur par défaut | Description |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` extrait à côté de l'archive, une valeur non vide extrait dans ce dossier, une valeur vide extrait dans `<file_name>_files` |
| `clean` | `bool` | `true` | Supprime l'archive après extraction (actuellement toujours activé) |

Les ressources non archivées sont conservées telles quelles, sans extraction.

## Licence

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
