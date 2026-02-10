# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md)

Latest Release est un outil Python qui télécharge et déploie automatiquement les ressources des GitHub Releases. Il aide à garder les applications à jour avec un minimum d'efforts manuels.

## Fonctionnalités

### Flux de travail automatisé

- Vérifie les nouvelles versions des GitHub Releases et télécharge les ressources
- Prend en charge l'extraction automatique et le nettoyage des archives
- L'installation automatique est en cours de développement

### Configuration simple et réutilisable

- Un seul fichier de configuration peut être réutilisé sur plusieurs exécutions
- Prise en charge du rechargement à chaud des fichiers de configuration

## Installation

Choisissez l'une des options suivantes.

### Option 1 : Exécuter l'exécutable Windows

Windows uniquement.

1. Rendez-vous sur la [page des GitHub Releases](https://github.com/ruiyangzhou01/Latest-Release/releases) et développez **Assets** pour la dernière version.
2. Téléchargez **Latest Release.zip** et décompressez-le.
3. Créez un fichier `config.yaml` et configurez-le (voir [Utilisation](#utilisation)).
4. Ouvrez l'invite de commandes ou PowerShell dans le dossier et lancez l'exécutable.

### Option 2 : Exécuter avec Python

Nécessite Python 3 et pip.

1. Rendez-vous sur la [page des GitHub Releases](https://github.com/ruiyangzhou01/Latest-Release/releases) et téléchargez **Source code (zip)**.
2. Décompressez l'archive et créez `config.yaml` (voir [Utilisation](#utilisation)).
3. Installez les dépendances :

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

4. Lancez le script :

   ```bash
   python main.py
   ```

## Utilisation

### Commandes

Après avoir démarré l'exécutable ou le script, saisissez `help` dans la fenêtre de commande pour afficher les commandes disponibles.

```
Command[<args>]        : Usage
list/ls                : Lister les applications installées
status/st              : Afficher l'état et vérifier les nouvelles versions
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
| `path` | `str` | - | Chemin de stockage par défaut quand `target` n'est pas défini |
| `proxy` | `dict` | - | Paramètres de proxy HTTP/HTTPS facultatifs |
| `repos` | `list` | - | Liste des dépôts à gérer |

#### Entrées `repos`

| Paramètre | Type | Valeur par défaut | Description |
| --- | --- | --- | --- |
| `author` | `str` | - | Propriétaire du dépôt |
| `name` | `str` | - | Nom du dépôt |
| `tag` | `str` | - | Tag de release actuel ; laissez vide pour télécharger la dernière version |
| `key` | `str` | `"all"` | Nom de la ressource à télécharger (`all` ou vide signifie toutes les ressources) |
| `target` | `str` | `path` | Chemin de destination des téléchargements |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | Paramètres d'extraction |

#### Champs `setting`

| Paramètre | Type | Valeur par défaut | Description |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` extrait à côté de l'archive, une valeur non vide extrait dans ce dossier, une valeur vide extrait dans `<file_name>_files` |
| `clean` | `bool` | `true` | Supprime l'archive après extraction |

## Roadmap

- Un client GUI WinUI3 est prévu.
- D'autres fonctionnalités et options de configuration sont prévues.

## Licence

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
