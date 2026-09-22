# VS Code 安装与使用：「项目管理」式开发

VS Code（Visual Studio Code）是微软出品的免费代码编辑器。本课安装它，重点学会**以项目（文件夹）为单位管理代码，而不是零散地打开单个文件**。Windows 用户会把它与 WSL 配合使用；macOS 用户直接在本机使用（见文中「macOS 用户」小节）。

### 本章学完你能做什么

- 你会下载安装 VS Code：Windows 正确勾选 **Add to PATH**，macOS 用 `.dmg` 拖入「应用程序」并安装 `code` 命令；
- 你会安装 WSL 扩展，从 WSL 终端用 `code .` 打开项目文件夹（Windows 用户）；
- 你能以"项目管理"方式使用工作区、资源管理器和内置终端，而不是零散打开单个文件；
- 你会安装常用插件（中文语言包、Python、GitLens 等），并会用命令行 `code --install-extension` 安装；
- Windows 用户会确认 VS Code 已连接 WSL 环境（左下角显示「WSL: Ubuntu」）；macOS 用户会确认 `code` 命令可用。

## 一、安装 VS Code（Windows 用户）

1. 到官网 `https://code.visualstudio.com/download` 下载 Windows 安装包并安装。
2. **重要**：安装时在「选择附加任务」界面勾选 **Add to PATH**（这样才可以在 WSL 终端里用 `code` 命令）。
3. 打开 VS Code，点击左侧「扩展」图标（或按 `Ctrl+Shift+X`），搜索安装 **WSL** 扩展（发布者为 Microsoft）。它能让 VS Code 直接以 WSL 作为开发环境，在 Windows 界面里编辑 Linux 里的文件。

### macOS 用户：安装 VS Code

1. 到官网 `https://code.visualstudio.com/download` 下载 macOS 版（Universal 通用版，或按芯片选 Apple Silicon / Intel），得到 `.dmg` 文件；
2. 双击打开 `.dmg`，把 **Visual Studio Code.app** 拖入「应用程序」文件夹；
3. 打开 VS Code，按 `Cmd+Shift+P` 打开命令面板，输入 `shell command`，运行 **Shell Command: Install 'code' command in PATH**，这样终端里就能用 `code` 命令；
4. 如果之后终端里提示找不到 `code`，重启终端窗口再试。macOS 用户**不需要安装 WSL 扩展**，VS Code 直接在本机运行。

> 官方步骤（含手动配置 PATH 的方法）：[Installing Visual Studio Code on macOS](https://code.visualstudio.com/docs/setup/mac)。

## 二、从终端打开项目文件夹

**Windows（WSL）**：打开 WSL 终端，进入项目目录后输入：

```bash
cd ~/my-project
code .
```

首次运行会自动在 WSL 内安装 VS Code Server（仅需一次）。稍等片刻后新窗口出现，**左下角显示「WSL: Ubuntu」标识**，说明当前已连接到 WSL 环境——此时 VS Code 里的所有操作（编辑、运行、终端）都发生在 Linux 中。

**macOS**：打开「终端」，进入项目目录后输入同样的命令（`cd ~/my-project`、`code .`）；VS Code 直接在本机打开该文件夹，没有「WSL: Ubuntu」标识，属正常现象。

## 三、以「项目管理」方式使用 VS Code

很多初学者习惯「双击打开单个文件」，但开发中更高效的方式是**把整个项目文件夹作为工作区打开**。VS Code 官方文档指出：工作区（Workspace）是打开在窗口中的一个或多个文件夹的集合，打开文件夹后 VS Code 会自动记住你的布局、记录工作区级配置。

**1. 打开文件夹（而不是单个文件）**

- 菜单：**文件 → 打开文件夹…**（File → Open Folder…）。
- 或终端命令：`code .`（打开当前目录）。
- 进阶：多根工作区可用「文件 → 将文件夹添加到工作区」，保存为 `.code-workspace` 文件，方便同时管理多个项目。

**2. 用好资源管理器（Explorer）**

左侧的**资源管理器**（Explorer）会按文件夹树展示项目全部文件：可以新建/重命名/删除文件与文件夹、拖拽移动文件、右键在集成终端中打开。项目结构一目了然，这比在系统文件管理器里翻找高效得多。

**3. 使用内置终端**

按 `Ctrl + \``（反引号）打开集成终端（macOS 为 `Cmd + \``）。Windows 上由于已连接 WSL，**终端自动运行在 Linux 中**；macOS 上终端直接运行在本机。两者都可以直接执行 `python`、`pip`、`opencode` 等命令，无需切换窗口。

**4. 安装扩展**

按 `Ctrl+Shift+X`（macOS 为 `Cmd+Shift+X`）打开扩展面板安装所需扩展（如 Python、中文语言包等）。Windows 连接 WSL 后，扩展会自动安装到 WSL 侧，确保运行环境一致；macOS 则安装在本机。

## 四、后续课程会用到的常用插件

> 以下插件均已在 VS Code Marketplace 核实（2026 年 8 月），安装量数据来自官方页面。
>
> 快捷键在 macOS 上为 `Cmd` 组合（如 `Cmd+Shift+P`、`Cmd+Shift+X`），与 Windows 的 `Ctrl` 一一对应，下文不再重复标注。

### 中文环境

- **Chinese (Simplified) Language Pack** —— VS Code 中文（简体）界面语言包（微软官方，约 5444 万安装）。安装后按 `Ctrl+Shift+P` 输入 "Configure Display Language" 选择「中文(简体)」并重启即可。

### WSL 与远程开发

- **WSL** —— 让 VS Code 直接连接 WSL 里的 Linux 环境，所有命令、终端、扩展都在 Linux 侧运行（微软官方，约 4029 万安装）。装好后在 WSL 终端输入 `code .` 即可打开项目。**仅 Windows 用户需要安装**，macOS 用户跳过本节。

### Python 开发

- **Python** —— Python 开发核心扩展：代码补全、调试、代码检查、格式化、单元测试与环境切换（微软官方，约 2.32 亿安装）。**安装时无需单独装 Pylance**：官方说明 Pylance（高性能语言服务器）与 Python Debugger 会由 Python 扩展自动安装，还新增了 Python Environments 环境管理扩展。
- **Jupyter** —— 在 VS Code 中打开和运行 Jupyter Notebook（.ipynb），支持单元格运行、图表渲染，后续学数据分析/机器学习会用到（微软官方，约 1.08 亿安装）。需要先在终端里装好 `jupyter` 包（`mamba install jupyter` 或 `conda install jupyter`）。

### Git 协作

- **GitLens** —— Git 增强神器：代码行级 blame 注解、提交图（Commit Graph）、分支对比、自动生成提交信息等（GitKraken 出品，约 5198 万安装；社区版免费开源）。
- **Git Graph** —— 在标签页中以图形化方式查看 Git 提交历史，右键即可完成分支、合并、回退等操作（mhutchie，约 1503 万安装）。提示：它和 GitLens 的提交图功能重叠，装一个即可。

### 代码质量

- **Prettier - Code formatter** —— 一键统一代码格式（JS/TS/HTML/CSS/Markdown 等），保存时自动格式化，杜绝「格式之争」（Prettier 官方，约 7078 万安装）。
- **Error Lens** —— 把错误和警告直接内联显示在出错的代码行末尾并高亮整行，不用打开「问题」面板就能看到问题（Alexander 出品，约 960 万安装）。

### 运行与调试

- **Code Runner** —— 一键运行当前文件或选中的代码片段（支持 Python、JS、C++ 等 60+ 语言），快捷键 `Ctrl+Alt+N`，适合快速测试小段代码（Jun Han，约 4137 万安装）。

### Web 预览

- **Live Server** —— 在本地起一个开发服务器并实时刷新网页，写 HTML 时改完代码浏览器立即更新（Ritwick Dey，约 8127 万安装）。⚠️ 该扩展**自 2019 年起未再更新**（功能稳定仍可用），作者在官方页面推荐测试版替代品 **Live Server++**；遇到问题可换用它，或直接用 Python 内置服务器：`python -m http.server 8000`。

### 安装提示

- **方式一（推荐）**：打开 VS Code，按 `Ctrl+Shift+X` 打开扩展面板，直接搜索插件名称安装。
- **方式二（命令行）**：在终端中执行 `code --install-extension 插件ID`（Windows 用户在 WSL 终端执行即安装到 WSL 环境；macOS 用户在自带终端执行），例如：

```bash
code --install-extension ms-python.python
code --install-extension ms-vscode-remote.remote-wsl
code --install-extension ms-ceintl.vscode-language-pack-zh-hans
```

## 小结与练习

**练习 1（动手）**：打开终端，进入你的项目目录（如 `cd ~/my-project`），运行 `code .`：Windows 用户确认新窗口左下角显示「WSL: Ubuntu」标识；macOS 用户确认 VS Code 打开的是本机目录。

**练习 2（动手）**：用「文件 → 打开文件夹…」打开本教程所在的文件夹，在资源管理器中练习新建、重命名、拖拽移动文件，并双击任一 `.md` 文件试试打开效果（Markdown 写法见 [Markdown 使用与 VS Code 插件](./Markdown-使用与VS-Code插件.md)）。

**练习 3（动手）**：按 **Ctrl + 反引号键**（macOS：**Cmd + 反引号键**）打开内置终端，运行 `python` 或 `pip` 试试；Windows 用户可同时确认命令在 Linux（WSL）环境中执行。

**练习 4（自查）**：（Windows）安装 VS Code 时为什么要勾选 **Add to PATH**？（macOS）为什么要运行 "Install 'code' command in PATH"？再用 `code --install-extension ms-python.python` 命令行方式安装一次 Python 扩展，说说它和"扩展面板搜索安装"有什么差别。

## 参考官方文档

- [VS Code 下载页](https://code.visualstudio.com/download)
- [在 macOS 上安装 VS Code（官方文档，含 code 命令配置）](https://code.visualstudio.com/docs/setup/mac)
- [在 WSL 中开发（VS Code 官方文档）](https://code.visualstudio.com/docs/remote/wsl)
- [什么是 VS Code 工作区（官方文档）](https://code.visualstudio.com/docs/editing/workspaces/workspaces)
- [VS Code 用户界面与资源管理器（官方文档）](https://code.visualstudio.com/docs/editing/userinterface)
- [Python 扩展（Microsoft）](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
- [WSL 扩展（Microsoft）](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)
- [中文（简体）语言包（Microsoft）](https://marketplace.visualstudio.com/items?itemName=ms-ceintl.vscode-language-pack-zh-hans)
- [Live Server（含 Live Server++ 替代说明）](https://marketplace.visualstudio.com/items?itemName=ritwickdey.liveserver)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 代码编辑器 | Code Editor | 用于编写和编辑代码的软件，如 VS Code |
| WSL | Windows Subsystem for Linux | Windows 上运行 Linux 环境的子系统 |
| 工作区 | Workspace | 打开在窗口中的一个或多个文件夹的集合 |
| 资源管理器 | Explorer | VS Code 左侧按树形展示项目文件的面板 |
| 集成终端 | Integrated Terminal | 内嵌在 VS Code 窗口里的终端 |
| 扩展 | Extension | 为 VS Code 增加功能的插件 |
| 路径 | PATH | 系统查找可执行程序的位置列表 |
| 语言服务器 | Language Server | 提供代码补全、检查等能力的后台服务 |
| 格式化 | Formatting | 自动统一代码风格的机制 |
| 调试 | Debug | 定位并修复代码错误的过程 |
