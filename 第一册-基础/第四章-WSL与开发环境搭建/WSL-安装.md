# WSL 安装：给 Windows 装一个「轻量 Linux」

> **本篇为 Windows 用户专属**。macOS 用户请跳过，改读[《终端与 Homebrew（macOS 版）》](./终端与Homebrew-macOS.md)。

本课带你完成 WSL（Windows Subsystem for Linux）的安装。安装完成后，你就能在 Windows 里直接使用 Ubuntu 等 Linux 系统，为后续学习编程和 AI 工具打好基础。

### 本章学完你能做什么

- 你能检查自己电脑的 CPU 虚拟化是否开启，并在需要时进 BIOS 把它打开。
- 你会安装 Windows Terminal，并学会在 PowerShell 与 WSL 之间切换。
- 你能用一条命令 `wsl --install` 装好 Ubuntu，并完成首次启动的配置。
- 你会用 `wsl -l -v` 验证安装结果，并说出 WSL 比传统虚拟机快在哪。

## 一、虚拟系统是什么？为什么用它？

虚拟机（Virtual Machine）是用软件在电脑里「模拟」出另一台电脑。它的优势很明显：

- **隔离安全**：Linux 系统独立运行，弄坏了删掉重来，不影响 Windows。
- **随装随用**：不用重装系统、不用双系统切换。
- **环境统一**：开发环境（软件版本、配置）可以保持一致，团队协作不踩坑。

## 二、第一步：检查 CPU 虚拟化是否开启

WSL 依赖硬件虚拟化技术（Intel 的 VT-x 或 AMD 的 AMD-V）。检查方法：

1. 按 `Ctrl + Shift + Esc` 打开**任务管理器**。
2. 点击「性能」选项卡，左侧选中「CPU」。
3. 查看右下角「虚拟化」一栏：显示**「已启用」**即可继续；若显示「已禁用」，需要进 BIOS 开启。

> 提示：也可以在命令行运行 `systeminfo.exe`，查看「Hyper-V 要求」部分是否全部为「是」。

## 三、第二步：在 BIOS 中开启虚拟化

如果虚拟化未启用，重启电脑并在开机时按提示按键（常见为 `F2`、`Del`、`F10`）进入 BIOS/UEFI 设置：

1. 找到虚拟化选项：Intel 平台通常是 **Intel Virtualization Technology (VT-x)** 或 **Intel (VMX) Virtualization Technology**；AMD 平台是 **SVM Mode** 或 **AMD-V**。
2. 将其改为 **Enabled**，保存并退出（通常按 `F10`）。
3. 进入系统后，再到任务管理器确认「虚拟化：已启用」。

微软官方说明：许多新电脑默认已开启虚拟化，无需任何操作；不同品牌电脑的 BIOS 选项位置不同，详见电脑厂商手册。

## 四、第三步：安装 Windows Terminal（推荐）

Windows Terminal 是微软的新式终端应用，支持多标签页、分屏、自定义主题，能统一运行 PowerShell 和 WSL。安装方式：

- 打开 Microsoft Store，搜索 **Windows Terminal** 并安装；或访问微软官方安装链接 `https://aka.ms/terminal`。

常用操作：

- `Ctrl + Shift + T`：新建标签页；`Ctrl + Shift + W`：关闭标签页。
- 点击标题栏下拉箭头，可在 PowerShell 与 WSL 之间切换。

## 五、第四步：一条命令安装 WSL

1. 右键点击「开始」菜单，选择 **终端（管理员）** 或 **PowerShell（管理员）**。
2. 输入以下命令并回车（默认安装 Ubuntu）：

```powershell
wsl --install
```

3. **重启电脑**，重启后 Ubuntu 会自动完成安装，首次启动时设置 Linux 用户名和密码即可。
4. 验证安装结果：

```powershell
wsl -l -v
```

## 六、WSL 的优势：简单快捷的 Linux

据微软官方文档，WSL 让你**无需单独的虚拟机或双启动**即可在 Windows 上运行 Linux 环境，其优势包括：

- **启动快**：安装完成后几乎秒开，比传统虚拟机轻量得多。
- **完整 Linux 内核**：WSL 2 通过轻量虚拟机运行真实 Linux 内核，系统调用兼容性完整。
- **文件互通**：可在 WSL 中直接访问 Windows 文件（如 `/mnt/c`），也能用 `explorer.exe .` 打开资源管理器（Windows 的文件管理操作可回顾第一章的 [《Windows 文件管理系统》](../第一章-Windows入门/Windows-文件管理系统.md)）。
- **支持 GPU 加速**：可用于机器学习等重负载场景。
- **生态齐全**：Ubuntu 的软件源、Python、Node.js 等开发工具开箱即用。

## 小结与练习

- **自查**：任务管理器的「性能 → CPU」里，「虚拟化」一栏显示什么，才说明可以继续安装 WSL？
- **练习**：在管理员终端运行 `wsl --install`，重启后完成 Ubuntu 的用户名和密码设置。
- **自查**：`wsl -l -v` 的输出里，你安装的发行版名称和版本号是什么？
- **练习**：在 WSL 里运行 `explorer.exe .`，看看弹出的 Windows 资源管理器打开的是哪个目录。

## 参考官方文档

- [WSL 安装文档（Microsoft Learn）](https://learn.microsoft.com/zh-cn/windows/wsl/install)
- [WSL 是什么与 WSL 2 概述（Microsoft Learn）](https://learn.microsoft.com/zh-cn/windows/wsl/about)
- [在 Windows 上启用虚拟化（Microsoft 支持）](https://support.microsoft.com/zh-cn/windows/experience/enable-virtualization-on-windows)
- [Windows Terminal 官方文档（Microsoft Learn）](https://learn.microsoft.com/zh-cn/windows/terminal/)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 虚拟机 | Virtual Machine | 用软件模拟出的另一台完整电脑 |
| 虚拟化 | Virtualization | 把一台电脑的硬件资源划分给多个独立系统使用的技术 |
| 内核 | Kernel | 操作系统的核心，负责管理硬件和运行程序 |
| 发行版 | Distribution | 内核加上软件包组成的完整 Linux 系统，如 Ubuntu |
| 子系统 | Subsystem | 运行在 Windows 内部的 Linux 兼容环境 |
| 双启动 | Dual Boot | 一台电脑装两个系统、开机时手动选择 |
| 终端 | Terminal | 用来输入命令、显示结果的文字窗口 |
| 标签页 | Tab | 终端里可随时切换的多个会话页面 |
