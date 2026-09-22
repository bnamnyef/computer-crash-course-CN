# Windows 文件管理系统（零基础入门）

### 本章学完你能做什么

- 你能说清楚 Windows 是什么、负责做什么，并列出它与 Linux 的主要区别；
- 你会理解"用户（账户）"的作用，知道管理员与标准用户的差别；
- 你能解释环境变量是什么，区分用户环境变量与系统环境变量；
- 你能亲手添加一个环境变量（图形界面或 setx 命令两种方式），并用 `echo` 验证生效。

## 一、什么是 Windows？

Windows 是微软（Microsoft）开发的电脑操作系统，目前主流版本是 Windows 10 和 Windows 11。按 Microsoft 官方定位，Windows 11 是"客户端操作系统"，负责管理电脑硬件、运行应用软件、组织文件（如 NTFS 文件系统），并为每个使用者提供独立的账户环境。你开机后看到的桌面、开始菜单、"此电脑"里的 C 盘、D 盘和文件文件夹，都是 Windows 管理文件系统的体现。

## 二、Windows 与 Linux 的区别

| 对比项 | Windows | Linux |
| --- | --- | --- |
| 定位 | 面向普通用户、开箱即用 | 开源内核，多用于服务器与开发者 |
| 授权 | 商业闭源 | 开源免费（如 Ubuntu、Debian 等发行版） |
| 软件格式 | 以 `.exe` 安装包为主 | 以软件包管理器（apt 等）为主 |
| 操作习惯 | 图形界面为主，可配命令行（cmd/PowerShell） | 命令行（终端）更常用 |
| 用户权限 | 管理员 / 标准用户账户 | root 与普通用户 |

两者都能管理文件，只是操作方式不同；本教程以 Windows 为例。

## 三、什么是用户（User）

微软官方文档指出：本地用户和系统帐户是"用于管理用户和系统对设备上资源的访问的安全主体"，并且"这些帐户仅对该设备拥有权限"。简单说：**用户（账户）就是"谁在用这台电脑"的身份凭证**。每台 Windows 电脑可以建多个账户（管理员、标准用户、来宾），各账户有自己独立的桌面、文档文件夹和软件设置。管理员可完全控制设备；日常使用建议用标准账户，需要装软件等管理操作时再用"以管理员身份运行"。

## 四、环境变量是什么

微软官方文档定义：环境变量"指定文件搜索路径、临时文件的目录、特定于应用程序的选项"等信息，分为**用户环境变量**（仅对当前用户生效）和**系统环境变量**（对整台电脑生效）两类。常见的有 `%PATH%`（告诉系统去哪里找程序）、`%TEMP%`（临时文件目录）。注意：修改后已打开的程序不会自动生效，需重启程序或命令行窗口。

## 五、实操：添加一个环境变量

### 方法一：图形界面（推荐新手）

1. 按 Win 键，输入"环境变量"，点击"编辑系统环境变量"（等价于：控制面板 → 系统 → 高级系统设置 → 环境变量）。
2. 上半区"用户变量"只对你生效；下半区"系统变量"对所有人生效。
3. 点"新建"，填变量名和值，确定后重启命令行验证：`echo %变量名%`。

### 方法二：setx 命令

微软官方说明：setx 用于"在用户或系统环境中创建或修改环境变量"，是永久设置系统环境变量的命令行方式。

```cmd
setx MY_VAR hello        :: 设置用户变量
setx MY_VAR hello /m     :: /m 表示系统变量（需管理员权限）
echo %MY_VAR%
```

注意：setx 设置的变量只在**将来的**命令窗口生效（当前窗口不变），且值限制 1024 个字符。

## 小结与练习

**练习 1（动手）**：按 Win 键输入"环境变量"打开设置窗口，观察上半区"用户变量"和下半区"系统变量"里都有哪些变量（如 `Path`、`TEMP`）。

**练习 2（动手）**：用图形界面新建一个用户变量 `MY_TEST`，值填 `Hello`，然后**重启**命令行窗口，运行 `echo %MY_TEST%` 验证是否输出了 `Hello`。

**练习 3（动手）**：再用 setx 命令完成同样的操作：`setx MY_TEST Hello`，对比一下两种方式的操作步骤差异。

**练习 4（自查）**：为什么修改环境变量后，已经打开的程序不生效？想让系统变量生效，setx 命令需要加什么参数、需要什么权限？

## 参考官方文档

- [环境变量 - Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/win32/procthread/environment-variables)
- [用户环境变量 - Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/win32/shell/user-environment-variables)
- [setx 命令 - Microsoft Learn](https://learn.microsoft.com/zh-cn/windows-server/administration/windows-commands/setx)
- [本地帐户 - Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/security/identity-protection/access-control/local-accounts)
- [Windows 11 概述 - Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/whats-new/windows-11-overview)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 操作系统 | Operating System（OS） | 管理电脑硬件与软件的底层系统，如 Windows 11 |
| 文件系统 | File System | 组织和存储文件的规则，如 NTFS |
| 路径 | Path | 文件或程序在系统中的位置描述 |
| 用户 / 账户 | User / Account | "谁在用这台电脑"的身份凭证 |
| 管理员 | Administrator | 拥有完全控制权限的账户 |
| 标准用户 | Standard User | 日常使用、权限受限的账户 |
| 环境变量 | Environment Variable | 保存搜索路径、临时目录等系统信息 |
| 命令提示符 | Command Prompt（cmd） | Windows 自带的命令行工具 |
| PowerShell | PowerShell | 微软推出的更强大的命令行与脚本工具 |
| setx | setx | 永久设置环境变量的命令行命令 |
