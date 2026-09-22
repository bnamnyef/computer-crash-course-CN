# 终端与 Homebrew（macOS 版）：开发环境准备

> 本篇对应 Windows 路线的 [《WSL 安装》](./WSL-安装.md) 与 [《WSL 使用》](./WSL-使用.md)：macOS 自带 Unix 终端，只需认识终端并装好包管理器 Homebrew，就完成了同样的准备工作。**macOS 读者读本篇即可**，不必安装 WSL。

### 本章学完你能做什么

- 打开 macOS 自带的「终端」，说清楚它与 WSL 的关系（macOS 不需要 WSL）；
- 认识 zsh 与命令提示符，会在终端与访达之间切换；
- 安装包管理器 Homebrew，并用 `brew` 安装、升级、卸载软件；
- 理解 Homebrew 与 WSL 里 `apt` 的对应关系。

## 一、macOS 自带终端，不需要 WSL

macOS 基于 Unix，自带「终端」（Terminal）App，命令与 Linux 高度一致——这正是 Windows 用户安装 WSL 想获得的环境。所以你**不需要安装任何"Linux 子系统"**，直接使用系统自带的终端即可。

打开方式（任选）：聚焦搜索 `Cmd+Space` 输入「终端」或 Terminal；或「应用程序 → 实用工具 → 终端」。官方手册见[终端使用手册](https://support.apple.com/zh-cn/guide/terminal/welcome/mac)。

打开后你会看到类似这样的窗口：

```
你的用户名@MacBook-Pro ~ %
```

- `%` 之前是提示符；`~` 表示当前位于用户主目录（`/Users/你的用户名`）；
- macOS 默认的 shell 是 **zsh**，用法与 Ubuntu 默认的 bash 基本一致（[《终端与命令行基础》](./终端与命令行基础.md)里的命令两平台通用）；
- 输入 `exit` 回车或直接关闭窗口即可退出。

> 想更好用一点可以安装 iTerm2 等第三方终端，但初学阶段系统自带终端完全足够。

## 二、安装 Homebrew（macOS 的「apt」）

WSL 里用 `apt` 安装软件；macOS 对应的工具是 **Homebrew**（简称 brew）。按 Homebrew 官方的说法，它负责为你安装需要的命令行工具与应用。安装步骤如下：

1. 打开终端，粘贴并执行官网的安装命令：

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. 脚本会先说明它要做什么（Apple 芯片默认装到 `/opt/homebrew`，Intel 芯片为 `/usr/local`），阅读后按回车确认；过程中可能要求输入开机密码；
3. 如果系统提示缺少命令行开发工具，按提示安装 Xcode Command Line Tools（也可手动执行 `xcode-select --install`，这是官方要求的前置条件）；
4. **按屏幕提示把 brew 加入 PATH**（关键一步，否则终端里找不到 `brew`）。Apple 芯片一般是在 `~/.zprofile` 中追加：

   ```bash
   echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
   eval "$(/opt/homebrew/bin/brew shellenv)"
   ```

   Intel 芯片把路径换成 `/usr/local/bin/brew`。然后新开一个终端窗口，运行 `brew --version` 验证。

> 国内网络从 GitHub 拉取安装脚本或执行更新可能较慢，可查阅官方文档 [Installation](https://docs.brew.sh/Installation) 的 "Git remote mirroring" 一节了解镜像配置方式。

## 三、brew 常用命令

| 命令 | 作用 | apt 对应（WSL） |
|---|---|---|
| `brew install 软件名` | 安装命令行工具 | `sudo apt install 软件名` |
| `brew install --cask 软件名` | 安装图形界面应用（如 VS Code、Cherry Studio） | —（图形应用用安装包） |
| `brew search 关键词` | 搜索软件 | `apt search 关键词` |
| `brew list` | 查看已安装列表 | `apt list --installed` |
| `brew upgrade` | 升级全部软件 | `sudo apt upgrade` |
| `brew uninstall 软件名` | 卸载软件 | `sudo apt remove 软件名` |
| `brew info 软件名` | 查看软件信息 | `apt show 软件名` |
| `brew cleanup` | 清理旧版本缓存 | `sudo apt autoremove` |
| `brew doctor` | 体检并给出修复建议 | — |

示例：

```bash
brew install git                        # 后面《Git 入门》需要
brew install --cask visual-studio-code  # 安装 VS Code（也可用官方 .dmg）
```

> 与 `apt` 不同：brew 安装软件**不需要加 `sudo`**，也**不建议加**（官方 FAQ 明确指出用 sudo 会带来权限问题）。

## 四、下一步：配置 Python 环境

接着学：[Python 环境配置（macOS 版）](./Python-环境配置-macOS.md)。

## 小结与练习

1. 用 `Cmd+Space` 打开终端，运行 `pwd`、`ls`，确认自己在主目录。
2. 安装 Homebrew，按提示把 brew 加入 PATH，用 `brew --version` 验证。
3. 用 `brew install git` 安装 Git，`git --version` 验证；再运行 `brew info git` 看看软件信息。
4. 自查：macOS 为什么不需要 WSL？macOS 默认 shell 是什么？brew 与 apt 的对应关系是什么？为什么 brew 不建议加 `sudo`？

## 参考官方文档

- [终端使用手册 - 官方 Apple 支持](https://support.apple.com/zh-cn/guide/terminal/welcome/mac)
- [Homebrew 官网（含安装命令）](https://brew.sh/)
- [Homebrew Installation（官方安装文档）](https://docs.brew.sh/Installation)
- [Homebrew FAQ（含 sudo 与卸载说明）](https://docs.brew.sh/FAQ)
- [Homebrew Troubleshooting（官方排障）](https://docs.brew.sh/Troubleshooting)
- [Homebrew Packages 搜索页](https://formulae.brew.sh/)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
|---|---|---|
| 终端 | Terminal | macOS 自带的命令行窗口 |
| shell | Shell | 解释并执行命令的程序，macOS 默认 zsh |
| 提示符 | Prompt | 终端里等待输入的命令提示 |
| 包管理器 | Package Manager | 安装/升级/卸载软件的工具（macOS 为 Homebrew） |
| formula | Formula | Homebrew 中命令行软件包的打包定义 |
| cask | Cask | Homebrew 中图形界面应用的打包定义 |
| 命令行工具 | Command Line Tools（CLT） | Xcode 附带的开发工具集，Homebrew 的前置依赖 |
| 路径前缀 | Prefix | Homebrew 的安装位置（Apple 芯片 `/opt/homebrew`，Intel `/usr/local`） |
