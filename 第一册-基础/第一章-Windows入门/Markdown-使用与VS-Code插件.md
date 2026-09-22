# Markdown 使用与 VS Code 插件

> 本篇两平台通用。文中的 VS Code 快捷键以 Windows 写法给出，macOS 用户把 `Ctrl` 换成 `Cmd` 即可（如 `Ctrl+Shift+V` → `Cmd+Shift+V`）。

### 本章学完你能做什么

- 你能说清楚 Markdown 是什么，以及 CommonMark、GFM 这两个规范是什么关系；
- 你会写标题、加粗、列表、表格、代码块、链接等常用语法；
- 你能在 VS Code 里实时预览 Markdown（`Ctrl+Shift+V` / `Ctrl+K V`），并用大纲快速跳转；
- 你会安装并配置 5 个推荐插件，提升写作效率；
- 你会用命令面板、路径补全等技巧，边写边预览出排版良好的文档。

## 一、Markdown 是什么？

Markdown 是一种**轻量级标记语言**：用纯文本编写，通过简单的符号（如 `#`、`*`）表示格式，保存为 `.md` 文件。你正在看的这份教程的所有章节都是 Markdown 写的。它的语法标准是 CommonMark（官方规范，最新版本 0.31.2），GitHub 等平台还扩展了表格、任务列表等语法（GitHub Flavored Markdown，简称 GFM）。

## 二、常用语法速查（官方规范）

````markdown
# 一级标题          （## 二级、### 三级……最多 6 级）
**加粗**  *斜体*  ~~删除线~~
- 无序列表         1. 有序列表
- [ ] 待办事项      - [x] 已完成（任务列表，GFM 语法）
> 引用文本
行内代码用 `反引号` 括起来
```python
# 三个反引号包住代码块，可指定语言（python/js/bash…）实现高亮
print("Hello")
```
[链接文字](https://example.com)
![图片说明](images/截图.png)
| 列1 | 列2 |        （表格：用竖线分隔，第二行写 | --- |）
| --- | --- |
| 内容 | 内容 |
---                 （三个短横线做分隔线）
脚注示例[^1]；[^1]: 脚注内容
````

以上大部分语法参考 GitHub 官方文档《基本写作和格式语法》与 CommonMark 规范。

## 三、VS Code 中写 Markdown（官方内置能力）

VS Code 对 Markdown 有开箱即用的支持（官方文档 "Markdown and Visual Studio Code"）：

- **实时预览**：`Ctrl+Shift+V` 打开预览标签页，`Ctrl+K V` 并排预览（左侧编辑、右侧渲染，实时同步）；
- **大纲视图**：侧边栏"大纲"（Outline）按标题层级展示文档结构，`Ctrl+Shift+O` 快速跳转标题；
- **规范遵循**：官方文档说明 VS Code 遵循 **CommonMark** 规范（基于 markdown-it 库），内置支持 Mermaid 图表和 KaTeX 数学公式渲染；
- **插入图片**：可从资源管理器拖拽图片进文档（按住 Shift 放置），也可直接粘贴图片/文件/URL；命令面板运行 `Markdown: Insert Image from Workspace` 可选图插入；
- **路径补全**：输入 `/`（相对工作区根目录）、`./`（相对当前文件）、`#`（文件内标题）自动补全。

用之前学过的 `code .`（见 [软件安装-VSCode](./软件安装-VSCode.md)）打开本教程文件夹，双击任一 `.md` 文件即可边写边预览。

## 四、推荐插件（Marketplace 核实，2026-08 安装量）

1. **Markdown All in One** —— 编辑增强：快捷键（Ctrl+B 加粗、Ctrl+I 斜体）、一键生成目录（TOC）、列表自动编号、表格格式化（约 1425 万安装）；
2. **markdownlint** —— 语法规范检查：违反规范处显示波浪线，支持一键修复（约 1193 万安装）；
3. **Markdown Preview Enhanced** —— 增强预览：滚动同步、数学公式、Mermaid/PlantUML 图、导出 PDF/HTML（约 1003 万安装）；
4. **Paste Image** —— 剪贴板图片一键粘贴：`Ctrl+Alt+V` 截图直接粘贴为图片文件并插入相对路径（约 72 万安装）；
5. **Path Autocomplete** —— 路径补全增强：写图片/链接时自动提示文件路径（约 245 万安装）。

**安装方法**：左侧扩展面板（`Ctrl+Shift+X`）搜索插件名安装；或命令行执行 `code --install-extension yzhang.markdown-all-in-one`（插件 ID）。

## 小结与练习

**练习 1（动手）**：在 VS Code 中新建 `practice.md`，用第二节的语法写一篇小文档，至少包含标题、加粗、列表、表格和一段代码块。

**练习 2（动手）**：按 `Ctrl+Shift+V` 预览你的 `practice.md`，再按 `Ctrl+K V` 试试并排预览，观察两侧实时同步。

**练习 3（动手）**：安装 Markdown All in One 插件，选中一段文字按 `Ctrl+B` 加粗，再试试"一键生成目录"功能。

**练习 4（自查）**：CommonMark 和 GFM 有什么区别？本教程里的表格、任务列表属于哪种规范的语法？

## 参考官方文档

- [CommonMark 规范（最新 0.31.2）](https://spec.commonmark.org/)
- [基本写作和格式语法 - GitHub 官方文档（中文）](https://docs.github.com/zh/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Markdown and Visual Studio Code - VS Code 官方文档](https://code.visualstudio.com/docs/languages/markdown)
- [Markdown All in One - Marketplace](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
- [markdownlint - Marketplace](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
- [Markdown Preview Enhanced - Marketplace](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)
- [Paste Image - Marketplace](https://marketplace.visualstudio.com/items?itemName=mushan.vscode-paste-image)
- [Path Autocomplete - Marketplace](https://marketplace.visualstudio.com/items?itemName=ionutvmi.path-autocomplete)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 标记语言 | Markup Language | 用符号标记格式的语言 |
| Markdown | Markdown | 轻量级标记语言，文件后缀为 .md |
| CommonMark | CommonMark | Markdown 的官方标准规范 |
| GFM | GitHub Flavored Markdown | GitHub 在 CommonMark 上扩展的语法（表格、任务列表等） |
| 预览 | Preview | 查看渲染效果的方式 |
| 大纲 | Outline | 按标题层级展示文档结构的侧边栏视图 |
| 目录 | Table of Contents（TOC） | 由标题自动生成的文档导航列表 |
| 代码块 | Code Block | 用三个反引号包裹的代码区域 |
| 相对路径 | Relative Path | 相对当前文件或工作区根目录的路径 |
| 扩展 / 插件 | Extension | 为 VS Code 增加功能的组件 |
