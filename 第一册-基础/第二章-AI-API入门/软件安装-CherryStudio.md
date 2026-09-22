# 软件安装：Cherry Studio 入门

### 本章学完你能做什么

- 你能说清楚 Cherry Studio 是什么、它能帮你做什么；
- 你会从官网和 GitHub Releases 认准官方渠道下载安装包并完成安装；
- 你能在"设置 → 模型服务"里添加服务商、填入 API Key 并测试连接；
- 你会获取模型列表、勾选常用模型，并在对话界面切换使用；
- 你会知道没有 API Key 时的替代方案（CherryAI 免费体验）。

## 一、Cherry Studio 是什么？

Cherry Studio 是一款开源的 AI 桌面客户端（官方 GitHub 仓库：CherryHQ/cherry-studio），支持 Windows、macOS、Linux。它的核心价值是把各家大模型"装进"一个软件统一使用：

- 内置 **60+ 模型服务商模板**：OpenAI、Google Gemini、Anthropic、DeepSeek、智谱、硅基流动等，按官方文档只需填入 API Key 即可连接；
- 支持多 API Key 轮换、知识库、MCP 等进阶能力，社区版为 AGPL-3.0 开源协议。

## 二、官方下载与安装

### 1. 下载（务必认准官方渠道）

- **官网下载页**：https://cherryai.com.cn/download/v2 （官方安装指南指定的入口），按系统和芯片架构（如 Windows x64）选择安装包；
- **GitHub Releases**：https://github.com/CherryHQ/cherry-studio/releases （最新版 v2.0.5 于 2026-08-13 发布，提供 Windows x64 安装版/便携版等 22 个安装资产）。

> 提示：避免从第三方下载站获取安装包，防止捆绑软件。

### 2. 安装（Windows 为例）

1. 双击下载的安装包（形如 `Cherry-Studio-...-x64-setup.exe`）；
2. 按向导点击"下一步 → 安装"，等待进度完成；
3. 打开 Cherry Studio，能正常进入主界面即安装成功（官方安装指南的判断标准）。

## 三、基础使用：添加模型服务

按照官方"模型服务"文档的标准流程：

1. 打开软件，进入 **设置 → 模型服务**（Settings → Model Services）；
2. 在内置提供商列表中找到目标服务商（如 OpenAI、DeepSeek），点击进入详情页；
3. 填入 **API Key**（在对应服务商官网的开发者平台申请，申请方法见 [AI-API 使用](./AI-API-使用.md)），API 地址保持默认即可；
4. 点击 **获取模型列表**，勾选你常用的对话模型；
5. 点 **测试** 验证连接，成功后在对话界面选择该模型即可开始使用。

没有自己的 API Key 也没关系：官方还提供免费的 CherryAI 服务可供体验。

## 小结与练习

**练习 1（动手）**：从官网下载页按你的系统和芯片架构选择安装包并安装，打开后能正常进入主界面即算成功。

**练习 2（动手）**：在"设置 → 模型服务"中添加一个服务商（如 DeepSeek），填入自己的 API Key，点"测试"验证连接是否成功。

**练习 3（动手）**：成功连接后，获取模型列表并勾选一个常用对话模型，然后在对话界面选它聊一句试试。

**练习 4（自查）**：为什么官方反复提醒要从官网或 GitHub Releases 下载安装包？没有 API Key 时，还有哪种方式可以用上 Cherry Studio？

## 参考官方文档

- [Cherry Studio 官网](https://cherry-ai.com)（国内可访问 https://www.cherryai.com.cn/）
- [下载和安装指南 - Cherry Studio 官方文档](https://docs.cherryai.com.cn/docs/en-us/cherry-studio/installation)
- [模型服务教程 - Cherry Studio 官方文档](https://docs.cherryai.com.cn/docs/en-us/pre-basic/providers)
- [CherryHQ/cherry-studio - GitHub 仓库与发布页](https://github.com/CherryHQ/cherry-studio/releases)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 开源 | Open Source | 源代码公开、可自由查看和使用的软件 |
| 桌面客户端 | Desktop Client | 安装并运行在电脑上的应用程序 |
| 模型服务商 | Model Provider | 提供大模型 API 的公司或平台 |
| API 密钥 | API Key | 连接模型服务商的身份凭证 |
| 模型列表 | Model List | 服务商提供的一组可用模型 |
| 安装包 | Installer | 用于安装软件的安装程序文件 |
| 便携版 | Portable | 免安装、解压即可运行的版本 |
| 轮换 | Rotation | 多个 API Key 轮流使用 |
| 知识库 | Knowledge Base | 供模型检索参考的资料库 |
