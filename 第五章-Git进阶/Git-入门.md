# Git 入门

> 本章属于「计算机使用速成」第五章。学完本章，你将能用 Git 记录代码历史、自由回退。想学分支、连接 GitHub 等进阶操作，接着看[《Git 进阶》](./Git-进阶.md)。

### 本章学完你能做什么

- 在 WSL 中安装 Git 并完成首次配置
- 用 `add`/`commit` 记录每次改动，用 `log`/`diff` 查看历史
- 用 `restore`/`reset` 回退错误的改动
- 知道下一步可以学什么（分支、连接 GitHub 等进阶内容）

> 进阶内容（分支、远程仓库、.gitignore、用 OpenCode 操作 Git）在[《Git 进阶》](./Git-进阶.md)，看完本篇接着学。

## 一、Git 是什么？

Git 是一个**分布式版本控制系统**（Distributed Version Control System）。通俗地说，它是一个"时光机 + 保险柜"：

- **历史记录**：每一次改动都留下快照（提交 commit），随时可以查看"这个文件以前长什么样"。
- **回退**：改坏了？一条命令回到之前的版本。
- **协作**：多人同时改一个项目，Git 负责合并各自的修改，谁改了什么一目了然。

它是当前程序员最离不开的工具之一——几乎每个开源项目都用它（Pro Git 官方手册定义："Git 是一个免费的、开源的分布式版本控制系统"）。

## 二、在 WSL 中安装

在 WSL（Ubuntu）终端里用系统包管理器安装，一条命令搞定：

```bash
sudo apt update
sudo apt install git
git --version   # 看到版本号即安装成功
```

## 三、首次配置

安装后先告诉 Git"你是谁"，提交记录才会带上署名（把引号里的内容换成你自己的）：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱@example.com"
```

`--global` 表示对这台机器上所有仓库生效，只需配置一次。

## 四、基本流程

1. **初始化**：进入项目文件夹，`git init` 创建仓库（会出现隐藏的 `.git` 目录）。
2. **暂存**：`git add 文件名`（或 `git add .` 全部）把改动放进"暂存区"。
3. **提交**：`git commit -m "说明这次改了什么"` 拍下快照。
4. **查看**：

```bash
git status            # 当前仓库状态：哪些文件被改了
git log --oneline     # 提交历史（一行一个）
git diff              # 查看尚未暂存的具体改动内容
```

日常工作流就是"改代码 → add → commit"循环，越频繁越好。

## 五、版本回退

- **丢弃未提交的修改**（文件还没 add/commit）：

```bash
git restore 文件名
```

- **回退上一个提交**（已提交，谨慎！）：

```bash
git reset --hard HEAD~1
```

`HEAD` 指向当前版本，`HEAD~1` 是上一个版本。**警告**：`--hard` 会彻底丢弃改动且难以找回，新手请先 `git log` 确认再操作。

## 六、下一步：Git 进阶

至此你已经掌握 Git 最核心的日常流程：记录历史、查看改动、回退错误。接下来可以学：

- **分支**：另开一条开发线做实验，互不干扰；
- **连接 GitHub**：把项目备份到远程，支持多人协作；
- **.gitignore**：让密钥、依赖等文件不进版本库；
- **用 OpenCode 操作 Git**：让 AI 帮你执行 Git 命令。

以上内容见[《Git 进阶》](./Git-进阶.md)。

## 小结与练习

1. 在 WSL 中安装 Git 并配置用户名邮箱，运行 `git config --list` 确认生效。
2. 新建一个项目文件夹，`git init` 后创建文件、`git add .`、`git commit -m "first commit"`，用 `git log --oneline` 查看。
3. 修改文件后用 `git restore` 丢弃改动，观察 `git status` 的变化。
4. 上面的流程已经顺手了吗？继续学[《Git 进阶》](./Git-进阶.md)：分支、连接 GitHub、.gitignore、用 OpenCode 操作 Git。

## 参考官方文档

- Pro Git 中文版（git-scm.com 官方书籍）：[git-scm.com/book/zh](https://git-scm.com/book/zh/v2)
  - [1.5 安装 Git](https://git-scm.com/book/zh/v2/%e8%b5%b7%e6%ad%a5-%e5%ae%89%e8%a3%85-Git)、[1.6 初次运行 Git 前的配置](https://git-scm.com/book/zh/v2/%e8%b5%b7%e6%ad%a5-%e5%88%9d%e6%ac%a1%e8%bf%90%e8%a1%8c-Git-%e5%89%8d%e7%9a%84%e9%85%8d%e7%bd%ae)
  - [2.2 记录每次更新到仓库](https://git-scm.com/book/zh/v2/Git-%e5%9f%ba%e7%a1%80-%e8%ae%b0%e5%bd%95%e6%af%8f%e6%ac%a1%e6%9b%b4%e6%96%b0%e5%88%b0%e4%bb%93%e5%ba%93)、[2.3 查看提交历史](https://git-scm.com/book/zh/v2/Git-%e5%9f%ba%e7%a1%80-%e6%9f%a5%e7%9c%8b%e6%8f%90%e4%ba%a4%e5%8e%86%e5%8f%b2)、[2.4 撤消操作](https://git-scm.com/book/zh/v2/Git-%e5%9f%ba%e7%a1%80-%e6%92%a4%e6%b6%88%e6%93%8d%e4%bd%9c)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
|---|---|---|
| 版本控制系统 | Version Control System | 记录文件历史、支持回退与协作的系统 |
| 仓库 | Repository | 项目 + 它的全部历史记录 |
| 提交 | Commit | 一次改动拍下的快照 |
| 暂存区 | Staging Area | 提交前临时存放改动的区域 |
