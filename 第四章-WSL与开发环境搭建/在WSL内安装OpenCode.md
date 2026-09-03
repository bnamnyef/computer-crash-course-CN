# 在 WSL 内安装 OpenCode

### 本章学完你能做什么

- 你会用官方安装脚本在 WSL 里装好 OpenCode，并用 `opencode --version` 验证成功。
- 你能进入任意项目启动 OpenCode，并用 `/init` 生成项目的 `AGENTS.md` 说明文件。
- 你能通过 `/mnt/c` 等路径在 OpenCode 中访问 Windows 盘上的项目文件。
- 你会通过 `/connect` 配置 AI 提供商和 API 密钥，再用 `/models` 挑选合适的模型。
- 你能用 Plan 模式先出方案、Build 模式动手改代码，不满意时用 `/undo` 回退。
- 你会清楚 OpenCode 擅长什么、不擅长什么，知道哪些环节需要自己把关。

## 一、OpenCode 是什么

OpenCode 是一款**开源的 AI 编程代理（AI coding agent）**。根据官方文档（opencode.ai/docs），它提供终端界面（TUI）、桌面应用和 IDE 扩展三种形态，核心使用方式是：在终端里用自然语言描述需求，OpenCode 自主完成读代码、改代码、运行命令、搜索文件等操作，以「代理模式」替你干活，而不是只做被动问答。它基于 AI SDK 支持 **75+ 家模型提供商**（OpenAI、Anthropic、DeepSeek 等），配合 Plan 模式（先规划再动手）、`/undo` 撤销、MCP 外部工具集成等能力，是当前最受关注的开源编码代理之一。

官方文档明确建议：**Windows 用户使用 WSL 获得最佳体验**——性能更好、兼容性最完整。本节就来完成安装与 AI 配置。

## 二、安装 OpenCode

打开 WSL 的 Ubuntu 终端，运行官方安装脚本：

```bash
curl -fsSL https://opencode.ai/install | bash
```

> 其他安装方式（官方文档提供）：Node.js 用户可运行 `npm install -g opencode-ai`；macOS/Linux 可用 `brew install anomalyco/tap/opencode`。

安装完成后验证：

```bash
opencode --version
```

## 三、访问 Windows 文件系统（/mnt/c）

WSL 把 Windows 的磁盘「挂载」在 `/mnt/` 目录下：C 盘是 `/mnt/c`，D 盘是 `/mnt/d`，依此类推。因此在 WSL 终端（以及 OpenCode 内部执行的命令）里，可以直接用 Linux 路径访问 Windows 上的文件和项目：

```bash
cd /mnt/c/Users/你的用户名/Documents   # 进入 Windows 的「文档」目录
ls /mnt/d/学习资料                      # 列出 D 盘内容
```

打开位于 Windows 盘上的项目，再启动 OpenCode：

```bash
cd /mnt/c/Projects/my-project
opencode
```

几点建议（微软官方 WSL 文件系统文档）：

- **性能**：跨系统读写（如 `/mnt/c/...`）比 Linux 原生文件系统慢，正式项目建议放在 Linux 侧（如 `~/projects/...`）；需要与 Windows 软件共享的少量文件再走 `/mnt/c`。
- **路径书写**：在 OpenCode 对话中引用 Windows 文件时，一律写 `/mnt/c/...` 这样的 Linux 路径，不要写 `C:\...`。
- **反向访问**：在 Windows 资源管理器地址栏输入 `\\wsl$` 可反向查看 WSL 里的文件（完整路径知识见第一章的 [《文件路径》](../第一章-Windows入门/文件路径.md)）。

## 四、进入项目并初始化

在 WSL 中进入你的项目文件夹（没有项目就新建一个），然后启动 OpenCode：

```bash
cd ~/my-project
opencode
```

首次使用时，在 OpenCode 里输入 `/init`，它会分析项目并生成一个 `AGENTS.md` 文件（记录项目结构和编码约定），以后每次对话它都会参考这份说明。

## 五、配置 AI 模型提供商

OpenCode 支持 **75+ 家 LLM 提供商**（OpenAI、Anthropic、DeepSeek 等）。配置分两步：

**第 1 步：添加 API 密钥**

在 OpenCode 中运行 `/connect`，选择你的提供商（如 Anthropic、OpenAI、DeepSeek），然后把从该平台申请的 API 密钥粘贴进去即可（如何申请 API 密钥可回顾第二章的 [《AI-API 使用》](../第二章-AI-API入门/AI-API-使用.md)）。密钥会被安全保存在 `~/.local/share/opencode/auth.json`。

> 入门建议：官方推荐 **OpenCode Zen**——由 OpenCode 团队测试验证过的模型集合。在 `/connect` 中选择 OpenCode Zen，按提示到 opencode.ai/auth 登录并复制 API 密钥即可，之后用 `/models` 挑选模型。

**第 2 步：选择模型**

在 OpenCode 中运行：

```
/models
```

从列表中选择一个模型（例如 DeepSeek、Claude 或 GPT 系列），回车即可开始对话。

**进阶：配置文件方式**

也可以在项目根目录创建 `opencode.json` 自定义提供商（如修改 API 地址）：

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "anthropic": {
      "options": { "baseURL": "https://api.anthropic.com/v1" }
    }
  }
}
```

## 六、开始使用

进入 OpenCode 后，像和同事聊天一样用中文或英文描述需求即可：

- **提问**：`这个项目的登录逻辑是怎么实现的？`（可用 `@` 键快速搜索文件加入上下文）。
- **写功能**：按 `Tab` 键切换到 Plan 模式先让它出方案，确认后再按 `Tab` 切回 Build 模式执行。
- **撤销修改**：不满意时运行 `/undo` 回退改动。

## 七、能力边界：它能做什么、不能做什么

### 擅长（官方文档明确支持的能力）

- **代码生成与修改**：通过内置 `write`（新建/覆写文件）、`edit`（精确字符串替换）、`apply_patch`（应用补丁）工具改代码，可进行跨多文件的重构。
- **自主执行命令**：`bash` 工具可运行 `npm install`、`git status`、测试等任意 shell 命令。
- **代码理解与搜索**：`grep`（正则搜索）、`glob`（文件名匹配）、`read`（读取指定行范围），并可通过 LSP 语言服务器获得跳转定义、查找引用等代码智能。
- **外部工具集成**：支持 MCP（Model Context Protocol）服务器，接入数据库、GitHub、Sentry 等第三方服务；支持 `webfetch`/`websearch` 联网查资料。
- **多代理协作**：内置 Build（默认，全工具）、Plan（只规划不改代码）、Explore（只读搜索）等 Agent 模式，可用 `permission` 精确控制每个工具的 allow/ask/deny。

### 需要注意（官方文档提及的边界）

- **依赖模型能力**：实际效果取决于所选模型的推理能力与上下文窗口；官方文档提醒，启用大量 MCP 工具会快速消耗上下文，甚至超出上下文上限。
- **改动需要人工审查**：官方设计 Plan 模式与权限审批（默认编辑、执行命令需确认）就是为了防止意外改动；LSP 文档也指出语言服务器可能不同步、占用内存、拖慢流程，关键验证建议交给 lint/typecheck 等命令。
- **可能出错**：它生成的代码仍可能含 bug，官方文档明确强调要用 `/undo` 回退不满意的改动，并自行运行测试验证。
- **不是全自动无人值守**：它需要你在关键节点确认、提供反馈（内置 `question` 工具会在执行中向你提问），才能保证结果符合预期。
- **需要 API Key 与费用**：使用各提供商模型需要申请并配置 API 密钥，按 token 计费。

## 同类型产品：当前主流的 AI 编程工具

同类工具大致可分为三类：**终端型 CLI 代理**、**IDE 型工具**、**云端全自动代理**。

### 终端型 CLI 代理（与 OpenCode 同类）

- **Claude Code**（Anthropic）—— 终端原生执行代理，深度自主重构能力强，闭源 CLI（SDK 开源），支持 VS Code/JetBrains 等 IDE 插件（VS Code 的安装与使用见第一章的 [《软件安装-VSCode》](../第一章-Windows入门/软件安装-VSCode.md)）。
- **OpenAI Codex CLI** —— OpenAI 的终端代理，开源（Apache 2.0），在 CI 与云端执行上支持完善。
- **Gemini CLI**（Google）—— 开源终端代理，以超长上下文和慷慨的免费额度著称（注意：Google 已将其迁移至新的 Antigravity CLI，个人免费版停止服务）。
- **Aider** —— 最老牌的开源 CLI 结对编程工具（2023 年问世），git 原生工作流（每次修改即提交），可接入几乎所有模型。
- **Qwen Code**（阿里巴巴）—— 开源终端编码代理，支持 OpenAI/Anthropic/Gemini/Qwen 协议，另有桌面版与 IDE 插件。
- **Goose**（Block）—— 开源终端 AI agent。

### IDE 型工具

- **Cursor**（Anysphere）—— 基于 VS Code 分支的 AI IDE，以 Tab 补全与 Composer/Agent 多文件编辑著称。
- **Windsurf**（Codeium）—— 独立 AI IDE，核心是 Cascade 代理式工作流，价格低于 Cursor。
- **Cline** —— 开源 VS Code 扩展型编码代理，可自带模型（BYOM），安装量巨大。
- **GitHub Copilot** —— 安装基数最大的 IDE 插件，已从代码补全进化出 Agent 模式，可自动提交 PR。

### 云端全自动代理

- **Devin**（Cognition）—— 「派单式」云端全自动代理，给它一个任务单，数小时后返回可审查的 PR，企业级定价。

**选择建议**：追求终端内自由切换多模型、数据可控 → OpenCode / Aider / Qwen Code；追求深度自主重构 → Claude Code / Codex CLI；习惯图形界面 → Cursor / Windsurf；完全托管自动出 PR → Devin。

## 小结与练习

- **练习**：在 WSL 终端运行 `curl -fsSL https://opencode.ai/install | bash` 安装 OpenCode，再用 `opencode --version` 确认安装成功。
- **练习**：进入一个测试项目运行 `opencode`，输入 `/init`，打开生成的 `AGENTS.md` 看看里面记录了什么。
- **自查**：`/connect` 和 `/models` 分别解决什么问题？API 密钥保存在哪个文件里？
- **自查**：Plan 模式和 Build 模式的区别是什么？什么情况下应该先用 Plan 模式？

## 参考官方文档

- [OpenCode 官方文档（安装与入门）](https://opencode.ai/docs/)
- [OpenCode 模型提供商配置（Providers）](https://opencode.ai/docs/providers)
- [OpenCode 在 Windows / WSL 的使用说明](https://opencode.ai/docs/windows-wsl)
- [OpenCode 内置工具与权限控制（Tools）](https://opencode.ai/docs/tools/)
- [OpenCode Agent 模式与能力限制（Agents）](https://opencode.ai/docs/agents/)
- [OpenCode MCP 外部工具集成（MCP Servers）](https://opencode.ai/docs/mcp-servers/)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 编程代理 | Coding Agent | 能自主读代码、改代码、运行命令的 AI 程序 |
| API 密钥 | API Key | 调用模型服务时用来证明身份的一串凭证 |
| 提供商 | Provider | 提供 AI 模型的服务厂商，如 OpenAI、DeepSeek |
| 模型 | Model | 提供推理能力的 AI 程序，如 GPT、Claude |
| 终端界面 | TUI（Text User Interface） | 只在终端里运行的文字界面 |
| 上下文窗口 | Context Window | 模型单次对话能处理的信息量上限 |
| 撤销 | Undo | 把上一步不满意的代码修改回退掉 |
| 补丁 | Patch | 以差异文件形式应用的代码修改 |
| 计划模式 | Plan Mode | 只输出方案、不改代码的工作模式 |
| 权限审批 | Permission Approval | 工具执行前先征求你同意的机制 |
