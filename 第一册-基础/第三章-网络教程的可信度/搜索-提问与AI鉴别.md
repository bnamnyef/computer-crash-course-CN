# 搜索、提问与 AI 鉴别

> 本篇是[《网络教程的可信度》](./网络教程的可信度.md)的配套篇。学会甄别之后，还有两件事能大幅提升自学效率：**搜得准**（找到好答案）和**问得好**（让高手愿意回答你）。另外，2026 年的自学已经绕不开 AI——AI 给的内容也要过三关。

### 本章学完你能做什么

- 用报错信息原文构造搜索，几秒钟命中答案
- 用 `site:` 等搜索技巧过滤低质内容
- 看懂 Stack Overflow 答案的「投票 + 采纳 + 时间」三个信号
- 按规范提问（最小可复现示例），而不是"在线等，急"
- 交叉验证 AI 给出的答案与命令，不被"自信的胡说"带偏

## 一、搜索：报错信息就是最好的关键词

大多数搜索失败，是因为搜的是"问题描述"，而不是"问题本身"。

- **复制完整报错**：把报错原样粘进搜索框，去掉本机特有的信息（用户名、绝对路径）。例如搜 `E: Unable to locate package` 而不是"Ubuntu 装不了软件怎么办"。
- **关键词组合**：软件名 + 版本 + 关键词，例如 `conda PackagesNotFoundError`、`wsl 0x800701bc`。
- **限定来源**：在关键词前加 `site:域名`，例如 `site:learn.microsoft.com wsl install`、`site:stackoverflow.com pip externally-managed`——直接跳过低质转载站（Google 官方帮助里介绍了这类搜索技巧）。
- **配合附录**：本教程附录的《常见报错速查表》就是按"错误信息 → 原因 → 解决办法 → 官方链接"整理的，遇到报错先查表，再搜索。

## 二、Stack Overflow：高分答案怎么读

Stack Overflow 是全球最大的编程问答社区，答案质量整体很高，但也要会读：

1. **三个信号**：投票数（社区认可度）、被采纳答案（提问者打勾，通常最对症）、回答时间（晚于提问时间才可能是针对最新版本的）。
2. **版本意识**：答案下方的评论常藏着"这个方法已过时"的提示；回答里提到的软件版本要和你的一致。
3. **提问前先搜索**：绝大多数问题已经被问过，搜到直接看答案，别急着提问。

如果确实需要提问，Stack Overflow 官方给出了提问规范（how-to-ask），核心三条：

1. **描述问题而不是情绪**：贴出完整报错、你执行的命令、期待的结果；
2. **最小可复现示例（minimal reproducible example）**：别人能直接复制运行的最小代码，而不是一整个项目；
3. **说明你试过什么**：列出已尝试的方案和搜索结果，避免别人重复劳动。

> 记住：提问是把"你的问题"翻译成"别人能秒懂的问题"的过程。问题描述得越清楚，回答质量越高。

## 三、GitHub Issues：给开源项目提问题

用到的开源软件（WSL、conda、Cherry Studio、OpenCode 等）出了官方文档没写的错，最靠谱的渠道是项目仓库的 Issues：

- **先搜已有 issue**：用关键词 + 报错信息在 issues 里搜索，很多"疑难杂症"其实已有讨论和解决方案；
- **报告 bug 的规范**：附上软件版本、操作系统、完整报错、复现步骤，缺一不可——否则维护者无法定位，问题会被直接关闭。

## 四、AI 时代的鉴别：AI 说的也要过三关

AI（如 ChatGPT、DeepSeek、OpenCode）回答问题的能力很强，但它可能**自信地编造**——生成不存在的函数、过时的 API、编造的参数，这种"一本正经的胡说"叫**幻觉（hallucination）**。把 AI 的回答当成"一篇声称自己是对的教程"，就很好理解了。

三条对策：

1. **要求给来源**：让 AI"只基于官方文档回答，并附上链接"，然后逐个点开核实——这是最有效的防幻觉手段（提示词写法见第二章《AI-API 使用》）；
2. **命令照常过三关**：AI 给的命令按「版本匹配、命令安全、结果验证」处理，关键命令先去官方文档确认；
3. **交叉验证**：让两个不同的 AI 回答同一问题做对比，或用 AI 的答案对照官方文档；两处说法一致才可信。

> 定位：AI 是"检索加速器"，不是"事实来源"。它的价值是帮你快速找到方向、解释概念，最终判断权在你手里——这和三关验证的原则完全一致。

## 小结与练习

1. **练习**：用你最近遇到的一个报错信息做搜索，分别试"完整报错原文"和"问题描述"两种搜法，对比结果质量。
2. **练习**：打开 Stack Overflow，找一个你关心的编程问题，指出它的"三个信号"分别是什么。
3. **练习**：让 AI 给你一段安装某个软件的步骤，然后用三关逐条检查它给的命令，找出至少一个需要核实的地方。
4. **自查**：为什么提问时要提供"最小可复现示例"？如果你收到一条只有"报错"没有"报错信息"的问题，你能回答吗？

## 参考官方文档

- [Refine web searches - Google 搜索帮助（含 site: 等搜索技巧）](https://support.google.com/websearch/answer/2466433)
- [How do I ask a good question? - Stack Overflow Help Center](https://stackoverflow.com/help/how-to-ask)
- [How to create a Minimal, Reproducible Example - Stack Overflow Help Center](https://stackoverflow.com/help/minimal-reproducible-example)
- [Searching issues and pull requests - GitHub 官方文档（中文）](https://docs.github.com/zh/search-github/searching-on-github/searching-issues-and-pull-requests)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 搜索运算符 | Search Operator | 限定搜索范围的语法，如 `site:域名` |
| 最小可复现示例 | Minimal Reproducible Example | 别人能直接运行的最小问题代码 |
| 采纳答案 | Accepted Answer | 提问者标记为已解决问题的回答 |
| 幻觉 | Hallucination | AI 生成看似合理但并非事实的内容 |
| 交叉验证 | Cross-validation | 用多个来源互相对照，确认信息一致 |
| 议题 | Issue | GitHub 上提问、报告 bug、讨论功能的入口 |
