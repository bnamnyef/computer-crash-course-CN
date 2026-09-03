# WSL 使用：进入终端与更新软件源

### 本章学完你能做什么

- 随时进入和退出 WSL 的 Ubuntu 终端
- 用 `apt` 更新软件源、升级并安装软件
- 知道安装完 Miniconda 后，如何配置 Python 环境（下一步指向）

## 一、进入 WSL 终端

在 Windows Terminal 中点击标题栏下拉箭头，选择 **Ubuntu**；或在 PowerShell 中直接输入：

```powershell
wsl
```

看到类似 `user@host:~$` 的提示符，说明已进入 Linux 环境。

## 二、apt update：更新软件源

Ubuntu 用 **apt**（Advanced Packaging Tool）管理软件。`apt update` 的作用是**从软件源更新软件包索引**，让系统知道有哪些新版本可用——这是安装任何软件前的第一步。

```bash
sudo apt update
sudo apt upgrade
```

- `sudo`：以管理员权限执行（会要求输入密码，输入时不显示字符属正常现象）。
- `apt update`：更新软件包列表；`apt upgrade`：升级已安装的软件。

之后安装软件就用：

```bash
sudo apt install 软件包名
```

## 三、下一步：配置 Python 环境

Python 环境（Miniconda 安装、conda 环境管理、国内镜像源加速）已整理为独立章节，接着往下学：

- [Python 环境配置（WSL + Miniconda + 国内镜像）](./Python-环境配置.md)

## 小结与练习

1. 进入 WSL 终端，用 `pwd` 和 `ls` 看看你当前在哪、有什么文件。
2. 执行 `sudo apt update` 并观察输出，说说 `apt update` 和 `apt upgrade` 的区别。
3. 用 `sudo apt install htop` 安装一个小工具，运行 `htop` 看看系统状态（按 `q` 退出）。
4. 思考：为什么安装任何软件前都要先 `apt update`？

## 参考官方文档

- [Ubuntu 软件包管理（ubuntu.com 官方文档）](https://ubuntu.com/server/docs/how-to/software/package-management/)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
|---|---|---|
| 软件源 | Software Repository | 存放软件包的服务器仓库 |
| 软件包 | Package | 可安装的软件单元 |
| 软件包管理器 | Package Manager | 负责安装/升级/卸载软件的工具（如 apt） |
| 管理员权限 | Root/Superuser | 对系统做修改所需的最高权限（sudo 临时获取） |
| 终端 | Terminal | 敲命令与系统交互的窗口 |
