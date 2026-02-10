# Latest Release

<p>
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/Latest-Release?&color=blue&logo=hack-the-box)" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-9f62a5?style=flat&logo=python&logoColor=white" />
<!--    <img alt="C#" src="https://img.shields.io/badge/-C_Sharp-9f62a5?style=flat&logo=csharp&logoColor=white" />
    <img alt="WinUI_3" src="https://img.shields.io/badge/-WinUI_3-9f62a5?style=flat&logo=windows&logoColor=white" />-->
</p>

[English Readme](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README.md) | [中文自述文件](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_zh.md) | [Deutsche Anleitung](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_de.md) | [Guía en Español](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_es.md) | [Guide en Français](https://github.com/ruiyangzhou01/Latest-Release/blob/main/README_fr.md)

Latest Release 是一个 Python 工具，可自动下载并部署 GitHub Release 资源，帮助你以最少的手动操作保持应用更新。

## 特点

### 自动化流程

- 检查 GitHub Release 新版本并下载资源
- 支持自动解压与清理归档文件
- 自动安装功能正在开发中

### 简单可复用的配置

- 一个配置文件可在多次运行中复用
- 支持配置文件热更新

## 安装

请选择以下任意一种方式。

### 方式一：运行 Windows 可执行文件

仅适用于 Windows。

1. 访问 [GitHub Releases 页面](https://github.com/ruiyangzhou01/Latest-Release/releases)，展开最新版本的 **Assets**。
2. 下载 **Latest Release.zip** 并解压。
3. 创建 `config.yaml` 文件并进行配置（见 [使用说明](#使用)）。
4. 在该文件夹中打开命令提示符或 PowerShell，然后运行可执行文件。

### 方式二：使用 Python 运行

需要 Python 3 和 pip。

1. 访问 [GitHub Releases 页面](https://github.com/ruiyangzhou01/Latest-Release/releases) 并下载 **Source code (zip)**。
2. 解压后创建 `config.yaml` 文件（见 [使用说明](#使用)）。
3. 安装依赖：

   ```bash
   pip install requests ruamel.yaml tqdm pyyaml
   ```

4. 运行脚本：

   ```bash
   python main.py
   ```

## 使用

### 命令

启动可执行文件或脚本后，在命令窗口中输入 `help` 查看可用命令。

```
Command[<args>]        : Usage
list/ls                : 列出已安装的应用
status/st              : 查看状态并检查新版本
update/up              : 更新所有应用
config/cf              : 打开配置文件以添加应用或修改设置
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
| `path` | `str` | - | 未指定 `target` 时使用的默认存储路径 |
| `proxy` | `dict` | - | 可选的 HTTP/HTTPS 代理设置 |
| `repos` | `list` | - | 需要管理的仓库列表 |

#### `repos` 条目

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `author` | `str` | - | 仓库所有者 |
| `name` | `str` | - | 仓库名称 |
| `tag` | `str` | - | 当前发行版标签；留空则下载最新版本 |
| `key` | `str` | `"all"` | 要下载的资源名称（`all` 或留空表示全部资源） |
| `target` | `str` | `path` | 下载目标路径 |
| `setting` | `dict` | `{ decompress: auto, clean: true }` | 解压设置 |

#### `setting` 字段

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `decompress` | `str` | - | `auto` 表示解压到归档所在目录，非空值表示解压到指定文件夹，空值解压到 `<file_name>_files` |
| `clean` | `bool` | `true` | 解压后自动删除归档文件 |

## 路线图

- 计划推出基于 WinUI3 的 GUI 客户端。
- 计划支持更多功能与配置选项。

## 许可证

[GPL-3.0 License](https://github.com/ruiyangzhou01/Latest-Release/blob/main/LICENSE) © ruiyangzhou01
