# 文件路径（macOS 版）：给文件一个「地址」

> 本篇是 [文件路径](./文件路径.md) 的 macOS 对应篇。**macOS 读者读本篇即可**；Windows 与 WSL 的文件互访（`/mnt/c`、`\\wsl$`）是 Windows 专属内容，本篇不涉及。

### 本章学完你能做什么

- 说清楚什么是路径，区分绝对路径与相对路径（含 `.` 和 `..` 的含义）；
- 看懂 macOS 的路径风格（`/Users/...`），并与 Windows、Linux 对比；
- 在访达（Finder）与终端之间互相定位文件；
- 通过 PATH 环境变量，让程序"敲名字就能运行"。

## 一、什么是路径

路径就是文件在电脑中的「地址」，它告诉系统文件存放在哪个文件夹里。在访达中选中一个文件，按 `Cmd+Option+P` 或点菜单「显示 → 显示路径栏」，窗口底部就会显示它的路径，例如 `/Users/xiaoming/Documents/report.docx`。学会看路径，是理解文件系统与命令行操作的第一步。

## 二、绝对路径与相对路径

- **绝对路径**：从根目录 `/` 开始写全，无论当前在哪都能准确定位。macOS 如 `/Users/xiaoming/Documents/report.docx`。
- **相对路径**：相对「当前所在目录」来描述位置，结果随当前位置变化。
- **`.` 与 `..`**：单个句点 `.` 代表当前目录，双句点 `..` 代表父目录。例如 `cd ..` 表示「回到上一级目录」，`mv file .` 表示「把文件移到当前目录」。

| 写法 | 含义 |
|---|---|
| `/Users/xiaoming/Documents/report.docx` | 绝对路径 |
| `Documents/report.docx` | 相对当前目录 |
| `.` | 当前目录 |
| `..` | 上一级（父）目录 |
| `~` | 当前用户的主目录（`/Users/用户名`） |

## 三、macOS 与 Windows、Linux 路径风格对比

| 项目 | macOS | Windows | Linux（含 WSL） |
|---|---|---|---|
| 示例 | `/Users/me/Project` | `C:\Users\me\Project` | `/home/me/Project` |
| 分隔符 | 正斜杠 `/` | 反斜杠 `\` | 正斜杠 `/` |
| 盘符 | 无盘符；外部磁盘挂在 `/Volumes` 下 | 每个盘一个字母（C:、D:） | 无盘符，所有磁盘统一挂载在根 `/` 下 |
| 根目录 | 唯一的根 `/` | 每盘一个根（`C:\`） | 唯一的根 `/` |
| 大小写 | 默认不区分（APFS 默认不区分大小写，但写路径时建议保持原样） | 不区分（`Foo.txt` 与 `foo.txt` 视为同一文件） | 区分（两者是不同的文件） |
| 主目录 | `/Users/用户名`（即 `~`） | `C:\Users\用户名` | `/home/用户名` |

> 也就是说：**macOS 的路径风格和 Linux 基本一致**，只把 `/home/用户名` 换成了 `/Users/用户名`。以后你看到 Linux 教程里的路径，可以直接类推。

## 四、在访达与终端之间互相定位

- **在终端打开当前目录的访达窗口**：输入 `open .` 回车；
- **把访达中的文件夹拖进终端**：路径会自动填充，省去手打（官方说明：[将项目拖移到"终端"窗口中](https://support.apple.com/zh-cn/guide/terminal/trml106/mac)）；
- **在访达中前往指定路径**：按 `Cmd+Shift+G`，输入路径后回车；
- **显示隐藏文件**：在访达中按 `Cmd+Shift+.`（句点）切换；
- **外部磁盘**：插入 U 盘、移动硬盘后，会出现在 `/Volumes/磁盘名`；
- **用默认程序打开文件**：`open report.docx`；用指定程序打开：`open -a "Visual Studio Code" .`。

## 五、PATH 实操：敲名字就能运行程序

系统靠一个叫 PATH 的环境变量记住「程序放在哪些文件夹」。当程序所在目录已加入 PATH，命令行里直接敲程序名即可运行，无需写完整路径：

1. 查看当前搜索路径：`echo $PATH`（各路径之间用冒号 `:` 分隔）；
2. **临时添加**（只对当前窗口生效）：`export PATH="$PATH:$HOME/bin"`；
3. **永久添加**（推荐）：把同一行 `export PATH="$PATH:$HOME/bin"` 追加到 `~/.zshrc`，然后 `source ~/.zshrc`（详见 [macOS 文件管理系统](./文件管理系统-macOS.md) 第五节）。

这也是后面 VS Code 安装时要把 `code` 命令加入 PATH 的原因。

## 六、常用路径命令速查

| 命令 | 作用 | Finder 对应 |
|---|---|---|
| `pwd` | 显示当前所在路径 | 底部路径栏 |
| `cd 路径` | 切换目录 | 双击进入文件夹 |
| `cd ~` | 回到主目录 | 侧边栏「个人」文件夹 |
| `ls` / `ls -la` | 列出文件（-a 含隐藏文件） | 图标视图 |
| `mkdir 目录名` | 新建文件夹 | 右键 → 新建文件夹 |
| `open .` | 用访达打开当前目录 | — |

## 小结与练习

1. 打开终端，用 `pwd` 查看当前路径，再用 `cd ~` 回到主目录，`cd ..` 回到上一级，体会绝对与相对路径的区别。
2. 用 `cd /Users/你的用户名/Documents` 进入「文稿」文件夹（可先用 `ls` 查看有哪些内容），再运行 `open .` 用访达打开对照。
3. 在访达中按 `Cmd+Shift+G`，输入 `/Users/你的用户名` 回车，看看能不能进入你的主目录。
4. 执行 `mkdir -p ~/bin`，把 `export PATH="$PATH:$HOME/bin"` 加入 `~/.zshrc` 并 `source`，重启终端后 `echo $PATH` 验证。
5. 自查：`.` 和 `..` 分别代表什么？macOS 与 Windows 的路径分隔符、盘符、主目录分别有何区别？

## 参考官方文档

- [在"访达"中整理文件 - 官方 Apple 支持](https://support.apple.com/zh-cn/guide/mac-help/mchlp2605/mac)
- [指定文件和文件夹（终端使用手册）- 官方 Apple 支持](https://support.apple.com/zh-cn/guide/terminal/apd3cf6fe02-3ec8-48f1-951f-866e52955fc8/mac)
- [执行命令和运行工具（终端使用手册）- 官方 Apple 支持](https://support.apple.com/zh-cn/guide/terminal/apdb66b5242-0d18-49fc-9c47-a2498b7c91d5/mac)
- [将项目拖移到"终端"窗口中 - 官方 Apple 支持](https://support.apple.com/zh-cn/guide/terminal/trml106/mac)
- [zsh 启动文件（官方 zsh 手册）](https://zsh.sourceforge.io/Doc/Release/Files.html)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
|---|---|---|
| 路径 | Path | 文件在电脑中的"地址" |
| 绝对路径 | Absolute Path | 从根目录 `/` 写起的完整地址 |
| 相对路径 | Relative Path | 相对当前目录的地址 |
| 根目录 | Root Directory | 路径的最顶层（macOS 唯一 `/`） |
| 父目录 | Parent Directory | 上一级目录（`..`） |
| 主目录 | Home Directory | 当前用户的家（macOS 为 `/Users/用户名`，即 `~`） |
| 访达 | Finder | macOS 的文件管理器 |
| 路径栏 | Path Bar | 访达窗口底部显示路径的栏位 |
| 挂载 | Mount | 把磁盘/目录接入文件系统的过程（如 `/Volumes`） |
| 环境变量 | Environment Variable | 系统级设置项，PATH 是其中最常见的一个 |
