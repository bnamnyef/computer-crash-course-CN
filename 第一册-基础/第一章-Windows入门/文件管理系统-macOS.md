# macOS 文件管理系统（零基础入门）

> 本篇是 [Windows 文件管理系统](./Windows-文件管理系统.md) 的 macOS 对应篇：概念（文件系统、用户账户、环境变量）完全相通，只是工具与写法换成了 macOS 的。**macOS 读者读本篇即可，不必再读 Windows 篇。**

### 本章学完你能做什么

- 你能说清楚 macOS 是什么，并列出它与 Windows、Linux 的主要区别；
- 你会理解「用户（账户）」与权限：为什么有时命令前要加 `sudo`；
- 你能解释环境变量是什么，知道 macOS 的环境变量写在哪里；
- 你能亲手添加一个环境变量（临时 `export` 与写入 `~/.zshrc` 永久生效两种方式），并用 `echo` 验证生效。

## 一、什么是 macOS？

macOS 是苹果（Apple）公司开发的电脑操作系统，只预装在 Mac 电脑上。按 Apple 官方《Mac 使用手册》的定位，它负责管理 Mac 的硬件与软件，并通过**访达（Finder）**组织文件。你可以从左上角的「苹果菜单」→「关于本机」查看 macOS 版本（如 macOS Sequoia 15、macOS Tahoe 26）与芯片信息。

与 Windows 最大的不同：**macOS 的内核基于 Unix**（Darwin），自带终端和大量 Unix 命令，文件系统默认为 APFS（Apple File System）。这也是本教程 macOS 路线不需要 WSL 的原因。

## 二、macOS 与 Windows、Linux 的区别

| 对比项 | macOS | Windows | Linux |
| --- | --- | --- | --- |
| 定位 | 苹果电脑专用，图形界面友好 | 面向普通用户、开箱即用 | 开源内核，多用于服务器与开发者 |
| 授权 | 商业闭源（仅随 Mac 硬件提供） | 商业闭源 | 开源免费（如 Ubuntu、Debian 等发行版） |
| 内核 | Unix（Darwin） | Windows NT | Linux |
| 文件系统 | APFS | NTFS | ext4 等 |
| 软件格式 | 以 `.app` / `.dmg` / `.pkg` 为主，命令行工具有 Homebrew | 以 `.exe` 安装包为主 | 以软件包管理器（apt 等）为主 |
| 命令行 | 自带「终端」（默认 shell 为 zsh） | cmd / PowerShell | bash 等 |
| 用户权限 | 管理员 / 普通用户，命令前加 `sudo`；root 默认禁用 | 管理员 / 标准用户账户 | root 与普通用户 |

**关键结论**：macOS 的命令行与 Linux 高度相似，所以本教程后面关于终端、Python、Git、Vim 的篇目你都可以直接使用；遇到路径、包管理器等差异，教程会单独标注。

## 三、什么是用户（User）与权限

Mac 同样用「账户」区分"谁在用这台电脑"：第一次开机设置时创建的账户就是**管理员账户**，可以在「系统设置 → 用户与群组」中添加其他用户（官方手册：[在 Mac 上添加用户或群组](https://support.apple.com/zh-cn/guide/mac-help/mchl3e281fc9/mac)）。各账户有独立的桌面、文稿文件夹与个人设置。

macOS 权限机制的几个要点：

- **日常操作不需要管理员权限**；只有安装系统级软件、修改系统设置等操作才需要；
- 终端里需要管理员权限时，在命令前加 **`sudo`**（superuser do），回车后输入**登录密码**——输入时屏幕不会显示任何字符，这是正常的安全设计；
- **root 超级用户账户默认是禁用状态**，日常不要启用它；
- 文件权限可以精细设置：在访达中选中文件 → 右键 →「显示简介」，底部「共享与权限」可设置读与写 / 只读等（官方手册：[在 Mac 上更改文件、文件夹或磁盘的权限](https://support.apple.com/zh-cn/guide/mac-help/mchlp1203/mac)）。

## 四、环境变量是什么

环境变量是系统记住的"全局设置"（如告诉系统去哪里找程序的 PATH、当前用户的主目录 HOME），概念与 Windows 完全一致，区别在于**写法与存放位置**：

| 对比项 | macOS | Windows |
| --- | --- | --- |
| 变量引用方式 | `$变量名`（如 `echo $PATH`） | `%变量名%`（如 `echo %PATH%`） |
| 用户变量的存放位置 | shell 配置文件，如 `~/.zshrc` | 图形界面「环境变量」窗口 |
| 永久设置方式 | 在配置文件中写 `export` | GUI 新建 / `setx` 命令 |
| 修改后生效时机 | 新开终端窗口；已打开的图形界面程序需重启 | 新开命令行窗口；已打开的程序需重启 |

macOS 默认 shell 是 **zsh**，用户级环境变量通常写在 **`~/.zshrc`** 这个文件里（`~` 是当前用户主目录 `/Users/你的用户名`）。官方 zsh 手册指出，`.zshrc` 会在每个交互式 shell 启动时读取（[zsh 启动文件文档](https://zsh.sourceforge.io/Doc/Release/Files.html)）。

> 注意：从图标双击打开的图形界面程序**不会读取** `~/.zshrc` 里的环境变量（它们由系统以另一套机制启动）。初学者只需记住：环境变量改完，重开终端窗口；图形界面程序则重启程序本身。

## 五、实操：添加一个环境变量

### 方法一：终端里临时添加（只对当前窗口生效）

打开「终端」（聚焦搜索 `Cmd+Space` 输入 Terminal / 终端），输入：

```bash
export MY_VAR=hello
echo $MY_VAR      # 输出 hello
```

关掉这个终端窗口再重开，`echo $MY_VAR` 就输出空行了——这就是"临时"。

### 方法二：写入 ~/.zshrc（永久生效，推荐）

```bash
echo 'export MY_VAR=hello' >> ~/.zshrc
source ~/.zshrc               # 让当前窗口立即生效
echo $MY_VAR                  # 输出 hello
```

以后每开一个新终端窗口都会自动生效。把程序目录加入 PATH 的写法同理：

```bash
echo 'export PATH="$PATH:$HOME/bin"' >> ~/.zshrc
source ~/.zshrc
```

### 注意事项

- 追加内容前先确认没有重复行，避免 `.zshrc` 越改越乱；
- `>>` 是「追加到文件末尾」，`>` 会覆盖整个文件，别写错；
- 修改后已打开的图形界面程序不会自动生效，重启程序即可（终端则是新开窗口或 `source`）。

## 小结与练习

**练习 1（动手）**：打开「终端」，运行 `echo $PATH` 和 `printenv | head`，观察系统里都有哪些环境变量。

**练习 2（动手）**：用 `export MY_TEST=Hello` 临时定义变量并验证，然后关闭窗口重开，看看它是否还在。

**练习 3（动手）**：把 `export MY_TEST=Hello` 写入 `~/.zshrc`（注意用 `>>` 追加），`source ~/.zshrc` 后验证；再新开一个终端窗口验证永久生效。

**练习 4（自查）**：macOS 默认的 shell 是什么？用户环境变量一般写在哪个文件里？变量引用符号与 Windows 有什么不同？`sudo` 是做什么的、为什么输密码时屏幕没有反应？

## 参考官方文档

- [Mac 使用手册 - 官方 Apple 支持](https://support.apple.com/zh-cn/guide/mac-help/welcome/mac)
- [在 Mac 上添加用户或群组 - 官方 Apple 支持](https://support.apple.com/zh-cn/guide/mac-help/mchl3e281fc9/mac)
- [在 Mac 上更改文件、文件夹或磁盘的权限 - 官方 Apple 支持](https://support.apple.com/zh-cn/guide/mac-help/mchlp1203/mac)
- [终端使用手册 - 官方 Apple 支持](https://support.apple.com/zh-cn/guide/terminal/welcome/mac)
- [zsh 启动文件（官方 zsh 手册）](https://zsh.sourceforge.io/Doc/Release/Files.html)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 操作系统 | Operating System（OS） | 管理电脑硬件与软件的底层系统，如 macOS |
| 内核 | Kernel | 操作系统的核心，macOS 基于 Unix（Darwin） |
| 文件系统 | File System | 组织和存储文件的规则，macOS 为 APFS |
| 用户 / 账户 | User / Account | "谁在用这台电脑"的身份凭证 |
| 管理员 | Administrator | 拥有系统管理权限的账户 |
| sudo | superuser do | 以管理员权限执行命令的前缀 |
| 环境变量 | Environment Variable | 保存搜索路径、主目录等系统信息 |
| 终端 | Terminal | macOS 自带的命令行工具 |
| zsh | Z shell | macOS 默认的命令行解释器（shell） |
| 配置文件 | dotfile / rc file | 以点开头的设置文件，如 `~/.zshrc` |
| 访达 | Finder | macOS 的文件管理器 |
