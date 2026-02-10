# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md) | [日本語 README](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_ja.md)

Latest Release は、複数のリポジトリの最新 GitHub Release を確認してアセットをローカルにダウンロードする Python 製のコマンドラインツールです。現在のリリースタグを `config.yaml` に保存し、ダウンロード後に更新してインストール済みの状態を追跡します。

## 特長

- GitHub Releases API で保存済みタグと最新リリースを比較
- すべてのアセット、またはキーワードに一致する単一アセットをダウンロード
- ダウンロード後に `config.yaml` のタグを最新に更新
- `.gz`、`.tar`、`.zip`、`.rar` の展開（任意）と後片付け（任意）
- API 呼び出しとダウンロード用の HTTP/HTTPS プロキシに対応
- `config.yaml` は各コマンドで再読み込みされ、変更がすぐ反映される

## 要件

- Python 3 と pip（ソースから実行する場合）
- `requests`、`ruamel.yaml`、`tqdm`、`pyyaml`
- `rarfile`（`.rar` の展開が必要な場合のみ）

## インストール

以下のいずれかの方法を選択してください。

### 方法 1: Windows 実行ファイルを利用

Windows のみ。

1. [GitHub Releases ページ](https://github.com/ruiyangzhou01/Latest-Release/releases)で最新リリースの **Assets** を開きます。
2. **Latest Release.zip** をダウンロードして展開します。
3. `config.yaml` が存在することを確認し、設定します（[使い方](#使い方)を参照）。
4. フォルダーでコマンドプロンプトまたは PowerShell を開き、実行ファイルを起動します。

### 方法 2: Python から実行

Python 3 と pip が必要です。

1. [GitHub Releases ページ](https://github.com/ruiyangzhou01/Latest-Release/releases)から **Source code (zip)** をダウンロードします。
2. アーカイブを展開し、`config.yaml` を作成します（[使い方](#使い方)を参照）。
3. 依存関係をインストールします。

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

   `.rar` を展開する場合は追加で:

   ```bash
   pip install rarfile
   ```

4. スクリプトを実行します。

   ```bash
   python main.py
   ```

## 使い方

実行ファイルまたはスクリプトを起動します。`config.yaml` がない場合は、現在のディレクトリにテンプレートが作成されます。リポジトリ設定を更新したら、以下のコマンドを実行してください。ファイルは各コマンドで再読み込みされます。

### コマンド

```
Command[<args>]        : Usage
list/ls                : 設定済みリポジトリとタグを一覧表示
status/st              : 状態を表示し最新リリースと比較
update/up              : すべてのリポジトリの最新 Release アセットをダウンロード
config/cf              : config.yaml を VS Code またはメモ帳で開く
exit/et                : シェルを終了
```

### `config.yaml` の設定

最小構成の `config.yaml` は次のとおりです。

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

#### 最上位の項目

| 項目 | 型 | 既定値 | 説明 |
| --- | --- | --- | --- |
| `path` | `str` | - | 既定のダウンロードルート。`target` が空の場合は `path\\<name>\\<tag>\\` に保存されます |
| `proxy` | `dict` | - | requests に渡す HTTP/HTTPS プロキシ（任意） |
| `repos` | `list` | - | 管理するリポジトリの一覧 |

#### `repos` の項目

| 項目 | 型 | 既定値 | 説明 |
| --- | --- | --- | --- |
| `author` | `str` | - | リポジトリ所有者 |
| `name` | `str` | - | リポジトリ名 |
| `tag` | `str` | - | 前回ダウンロードした release タグ。空欄で最新リリースを取得 |
| `key` | `str` | `"all"` | アセット名フィルタ（`all` または空欄で全件。指定すると名前にキーが含まれる最初のファイルを取得） |
| `target` | `str` | `path` | ダウンロード先。空欄なら `path` を使用 |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | 展開設定（`.gz`、`.tar`、`.zip`、`.rar` に適用） |

#### `setting` の項目

| 項目 | 型 | 既定値 | 説明 |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` はアーカイブの隣に展開し、空でない値はそのフォルダーに展開、空欄は `<file_name>_files` に展開 |
| `clean` | `bool` | `true` | 展開後にアーカイブを削除 |

アーカイブ以外のアセットは展開せずに保存されます。

## ライセンス

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
