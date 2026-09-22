# Git 进阶：分支与远程协作

> 本章属于「计算机使用速成」第五章（进阶），是[《Git 入门》](./Git-入门.md)的续篇。学完本篇，你将能用分支大胆实验、把项目备份到 GitHub，并学会让 OpenCode 帮你操作 Git。

### 本章学完你能做什么

- 用分支做实验并合并回主线，解决合并冲突
- 把项目推送到 GitHub 备份，用 token 或 SSH 完成认证
- 用 `.gitignore` 让不该进版本库的文件自动被忽略
- 用 OpenCode 帮你执行 Git 命令（分批提交、软回退等）

## 一、分支（branch）

分支就像"平行世界"：在主分支上稳定开发，另开一个分支大胆实验，做好后再合并回来。

```bash
git branch           # 查看所有分支（* 表示当前所在）
git checkout -b 新功能  # 创建并切换到新分支（-b 表示新建）
git merge 新功能        # 在主线分支上把新功能合并进来
```

合并出现冲突时，Git 会提示哪些文件两边都改了，手动选择保留哪份即可（详见 Pro Git 第 3 章"分支的新建与合并"）。

## 二、连接 GitHub（可跳过）

> **本节可跳过**：如果只想在本地用 Git 记录历史、暂时不需要把项目备份到 GitHub，直接跳到第三节即可，不影响前面学的内容。需要协作或远程备份时再回来看本节。

在 GitHub 网页上新建空仓库后，把本地仓库"绑定"到远程并推送：

```bash
git remote add origin https://github.com/你的用户名/仓库名.git
git push -u origin main        # 首次推送，-u 记住关联
git pull                       # 以后拉取远程最新改动
```

认证方式二选一（GitHub 官方推荐 HTTPS）：

1. **HTTPS + 个人访问令牌（token）**：在 GitHub「设置 → 开发者设置」生成 token，当密码输入即可；密码认证已被 GitHub 移除。
2. **SSH 密钥**：`ssh-keygen` 生成密钥对，把公钥粘贴到 GitHub「Settings → SSH and GPG keys」。之后推送无需输密码。

## 三、.gitignore 忽略文件

有些文件不该进版本库——比如 `node_modules`（依赖包，可随时重新下载）、密钥、日志。在仓库根目录建一个 `.gitignore` 文件：

```gitignore
node_modules/
.env
*.log
```

Git 就会自动无视这些文件，保证仓库干净、不泄露秘密。

## 四、用 OpenCode 帮你操作 Git（提示词示例）

OpenCode 等 AI 编程代理（见第四章的 [《在 WSL 内安装 OpenCode》](../../第一册-基础/第四章-WSL与开发环境搭建/在WSL内安装OpenCode.md)）内置 bash 工具，可以直接替你执行 Git 命令。在 OpenCode 对话里粘贴下面的提示词即可，它会先列出要执行的命令征求你同意。

### 1. 初始化仓库并首次提交

> 帮我初始化 Git 仓库：运行 `git init`，创建一份合理的 `.gitignore`（忽略 `.env`、`node_modules`、`__pycache__`、`*.log`），然后 `git add .` 并提交，提交信息写 "init: 项目初始化"。

### 2. 按功能分批提交（推荐）

> 分析当前工作区的所有改动，按功能/模块把它们分成几批，每批执行一次 `git add` 和 `git commit`，提交信息用简短中文写明每批改了什么。先把分批方案列给我确认，再执行。

### 3. 只提交指定文件

> 只提交 `src/utils.py` 和 `tests/test_utils.py`，提交信息写 "feat: 添加工具函数及测试"，其余改动先不要提交。

### 4. 查看改动并生成提交信息

> 运行 `git status` 和 `git diff` 看看现在的改动，帮我总结成一条规范的提交信息（先不提交）。

### 5. 回退到上一个版本（保留改动）

> 我提交错了，运行 `git log --oneline` 让我看历史，然后帮我软回退最后一次提交（保留文件改动）。

### 使用要点

- **先看命令再放行**：涉及 `git reset --hard`、`git push` 等不可逆操作时，OpenCode 默认会征求确认——放行前仔细看它要执行的命令。
- **分批提交先要方案**：让 AI 先列出分批计划再执行，避免提交历史混乱。
- **提交信息规范**：常用 "feat: 新功能 / fix: 修复 / docs: 文档 / refactor: 重构" 前缀，AI 可以帮你自动生成。

## 小结与练习

1. 建一个分支 `git checkout -b test` 改点东西再 `git merge test` 合并回主线，看看 `git log --oneline` 的变化。
2. 在 GitHub 新建空仓库，把本地仓库推上去（token 或 SSH 任选），再 `git pull` 一次。
3. 给仓库加一份 `.gitignore`，把 `.env`、`*.log` 加进去，用 `git status` 验证它们不再出现。
4. 用 OpenCode 的"按功能分批提交"提示词，把你近期的一堆改动整理成干净的提交历史。

## 参考官方文档

- Pro Git 中文版（git-scm.com 官方书籍）：[git-scm.com/book/zh](https://git-scm.com/book/zh/v2)
  - [3.2 分支的新建与合并](https://git-scm.com/book/zh/v2/Git-%e5%88%86%e6%94%af-%e5%88%86%e6%94%af%e7%9a%84%e6%96%b0%e5%bb%ba%e4%b8%8e%e5%90%88%e5%b9%b6)、[4.3 生成 SSH 公钥](https://git-scm.com/book/zh/v2/%e6%9c%8d%e5%8a%a1%e5%99%a8%e4%b8%8a%e7%9a%84-Git-%e7%94%9f%e6%88%90-SSH-%e5%85%ac%e9%92%a5)
- GitHub 官方中文文档（docs.github.com/zh）
  - [管理远程存储库](https://docs.github.com/zh/get-started/git-basics/managing-remote-repositories)、[关于远程仓库](https://docs.github.com/zh/get-started/git-basics/about-remote-repositories)
  - [推送提交到远程](https://docs.github.com/zh/get-started/using-git/pushing-commits-to-a-remote-repository)、[从远程获取更改](https://docs.github.com/zh/get-started/using-git/getting-changes-from-a-remote-repository)
  - [使用 SSH 连接到 GitHub](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh)、[管理个人访问令牌](https://docs.github.com/zh/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
  - [忽略文件](https://docs.github.com/zh/get-started/git-basics/ignoring-files)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
|---|---|---|
| 分支 | Branch | 独立的开发线（"平行世界"） |
| 合并 | Merge | 把一个分支的改动合入另一个分支 |
| 远程仓库 | Remote | 托管在 GitHub 等服务器上的仓库 |
| 忽略文件 | .gitignore | 声明哪些文件不进版本库 |
| 个人访问令牌 | Personal Access Token | GitHub 上生成的替代密码的访问凭证 |
