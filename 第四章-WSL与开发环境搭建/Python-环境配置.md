# Python 环境配置（WSL + Miniforge + 国内镜像）

### 本章学完你能做什么

- 在 WSL 中安装 Miniforge（Python 环境管理器）
- 用 conda 为每个项目创建互相隔离的 Python 环境
- 配置清华 TUNA 国内镜像源，让 conda/pip 下载速度提升数十倍
- 验证 Python 环境与镜像配置是否生效

## 一、为什么用 conda 管 Python？

在 WSL（Ubuntu）中直接 `apt install python3` 虽然简单，但 AI 项目常需要不同 Python 版本和依赖包，混装容易冲突。**Miniforge**（conda-forge 官方轻量版，默认只含 python 和 conda）通过"环境"为每个项目隔离一套独立的软件包。官方定义：环境是"自包含的隔离空间，可以安装特定版本的软件包、依赖库和 Python 版本"。

## 二、安装 Miniforge（官方指南）

在 WSL 终端执行（x86_64 架构）：

```bash
curl -L -O https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
bash ~/Miniforge3-Linux-x86_64.sh
```

交互过程：按回车查看许可协议 → 输入 `yes` 同意 → 回车接受默认安装位置（`/home/你的用户名/miniforge3`）→ 询问是否初始化时输入 `yes`。完成后刷新终端：`source ~/.bashrc`，提示符出现 `(base)` 即成功。

> 国内下载安装包慢的话，可从清华镜像下载：`https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniforge/`（TUNA 官方帮助页提供）。

## 三、conda 环境管理（官方文档）

```bash
conda create -n myenv python=3.11 numpy   # 创建环境（官方建议一次性装齐所需包）
conda activate myenv                      # 激活环境
conda deactivate                          # 退出环境
conda info --envs                         # 查看所有环境
conda list                                # 查看当前环境已装包
conda env export > environment.yml       # 导出环境配置（分享/备份）
conda env create -f environment.yml      # 从配置文件重建环境
conda remove -n myenv --all               # 删除环境
```

## 四、配置国内镜像源（重点）

官方源服务器在境外，国内直连常超时。改为国内镜像后，下载速度可提升数十倍。

**国内主流镜像源**：
- **清华 TUNA 镜像站**：清华大学信息化技术中心维护，同步速度快、更新及时，是国内最常用的开源软件镜像源之一，适用于 conda 和 pip。
- **阿里云镜像站**：阿里云提供的公共镜像服务，稳定性高，适合对网络质量要求较高的用户，主要用于 pip。

### 1. conda 镜像（清华 TUNA，按官方帮助页）

编辑 `~/.condarc`（Linux 下该文件位于用户主目录）：

```yaml
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

然后清除索引缓存并测试：`conda clean -i` 后执行 `conda create -n myenv numpy`。

### 2. pip 镜像（清华 TUNA / 阿里云）

```bash
# 使用清华 TUNA 镜像（推荐）
pip config set global.index-url https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple

# 或使用阿里云镜像
# pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/

# 临时使用（不写入配置）：
pip install -i https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple 包名
```

注意：URL 中的 `simple` 不能少，且必须用 https。清华源更新频率高，阿里云源网络稳定性好，可根据实际情况选择。

## 五、Python 为什么适合 AI + 验证

PyTorch 等主流框架以 Python 为第一语言（官方安装页要求 Python 3.10+，`pip3 install torch torchvision torchaudio` 即可装）。完成以上步骤后验证：

```bash
conda --version && python --version   # 显示 conda 与 Python 版本
conda list                             # 显示已安装包列表
pip install numpy                      # 测试 pip 镜像是否生效（速度快即为成功）
```

## 小结与练习

1. 在 WSL 中安装 Miniforge，并确认提示符出现 `(base)`。
2. 创建名为 `ai-env` 的环境（Python 3.11），激活后安装 `numpy`，观察安装速度。
3. 按本章方法配置 conda 与 pip 的清华镜像，重跑练习 2 对比下载速度。
4. 用 `conda env export > environment.yml` 导出你的环境，再用 `conda env remove -n ai-env --all` 删除后重建，验证配置文件能否复现环境。

## 参考官方文档

- [Installing Miniforge（Linux 安装指南）- conda-forge 官方文档](https://github.com/conda-forge/miniforge/releases)
- [Environments（conda 环境管理）- Anaconda 官方文档](https://www.anaconda.com/docs/getting-started/working-with-conda/environments)
- [Anaconda 软件仓库帮助 - 清华 TUNA 镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)
- [PyPI 软件仓库帮助 - 清华 TUNA 镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/)
- [阿里云 PyPI 镜像源](https://mirrors.aliyun.com/pypi/simple/)
- [PyTorch 官网（Python 版本要求与安装命令）](https://pytorch.org/)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
|---|---|---|
| 环境管理器 | Environment Manager | 管理互相隔离的软件包集合的工具 |
| 虚拟环境 | Virtual Environment | 独立、可随时删除重建的 Python 环境 |
| 软件源/渠道 | Channel | conda 获取软件包的仓库来源 |
| 镜像站 | Mirror | 官方源的国内加速副本 |
| 索引地址 | Index URL | pip 下载包的地址（如清华 PyPI 镜像） |
| 依赖 | Dependency | 软件运行所需的其他包 |
