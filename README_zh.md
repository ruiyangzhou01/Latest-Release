# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md) | [日本語 README](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_ja.md)

Latest Release 是一个命令行 Python 工具，会检查多个仓库的最新 GitHub Release 并下载资源到本地。它会在 `config.yaml` 中记录当前的 release 标签，并在每次下载后更新，以便跟踪已安装版本。

## 特点

- 使用 GitHub Releases API 比较已记录的标签与最新版本
- 可下载全部资源或匹配关键字的单个资源
- 下载后自动更新 `config.yaml` 中的最新标签
- 可选自动解压 `.gz`、`.tar`、`.zip`、`.rar`，并可在完成后清理归档
- 支持为 API 调用和下载配置 HTTP/HTTPS 代理
- 每次命令都会重新读取 `config.yaml`，修改后立即生效

## 环境要求

- 运行源码需要 Python 3 和 pip
- `requests`、`ruamel.yaml`、`tqdm`、`pyyaml`
- `rarfile`（仅在需要解压 `.rar` 时）

## 安装

请选择以下任意一种方式。

### 方式一：运行 Windows 可执行文件

仅适用于 Windows。

1. 访问 [GitHub Releases 页面](https://github.com/ruiyangzhou01/Latest-Release/releases)，展开最新版本的 **Assets**。
2. 下载 **Latest Release.zip** 并解压。
3. 确保存在 `config.yaml` 文件并进行配置（见 [使用说明](#使用)）。
4. 在该文件夹中打开命令提示符或 PowerShell，然后运行可执行文件。

### 方式二：使用 Python 运行

需要 Python 3 和 pip。

1. 访问 [GitHub Releases 页面](https://github.com/ruiyangzhou01/Latest-Release/releases) 并下载 **Source code (zip)**。
2. 解压后创建 `config.yaml` 文件（见 [使用说明](#使用)）。
3. 安装依赖：

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

   如需解压 `.rar`：

   ```bash
   pip install rarfile
   ```

4. 运行脚本：

   ```bash
   python main.py
   ```

## 使用

启动可执行文件或脚本。如果 `config.yaml` 不存在，会在当前目录创建模板文件。更新仓库配置后再执行下列命令，且每次命令都会重新加载该文件。

### 命令

```
Command[<args>]        : Usage
list/ls                : 列出已配置的仓库与标签
status/st              : 显示状态并与最新版本比较
update/up              : 下载所有仓库的最新 Release 资源
config/cf              : 用 VS Code 或记事本打开 config.yaml
exit/et                : 退出命令行
```

### 配置 `config.yaml`

最小化的 `config.yaml` 示例：

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

#### 顶层字段

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `path` | `str` | - | 默认下载根目录。当 `target` 为空时，文件保存到 `path\\<name>\\<tag>\\` |
| `proxy` | `dict` | - | 可选的 HTTP/HTTPS 代理设置（传递给 requests） |
| `repos` | `list` | - | 需要管理的仓库列表 |

#### `repos` 条目

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `author` | `str` | - | 仓库所有者 |
| `name` | `str` | - | 仓库名称 |
| `tag` | `str` | - | 上次下载的 release 标签；留空则下载最新版本 |
| `key` | `str` | `"all"` | 资源名称过滤（`all` 或空表示全部资源；否则下载文件名包含该关键字的第一个资源） |
| `target` | `str` | `path` | 下载目标路径；留空使用 `path` |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | 解压设置（仅对 `.gz`、`.tar`、`.zip`、`.rar` 生效） |

#### `setting` 字段

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` 表示解压到归档所在目录，非空值表示解压到指定文件夹，空值解压到 `<file_name>_files` |
| `clean` | `bool` | `true` | 解压后删除归档文件 |

非归档资源会保持原样，不会解压。

## 许可证

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
