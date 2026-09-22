# AI-API 使用：从聊天对话框到程序调用

### 本章学完你能做什么

- 你能说清楚 API 和 API Key 是什么，明白"为什么还要学 API"；
- 你会在 DeepSeek 与硅基流动两个平台完成注册、实名认证并创建自己的 API Key；
- 你能看懂并运行调用大模型的 Python 示例代码（填 Key、选模型、发请求）；
- 你会查看用量与余额、控制费用，并认识 401 / 402 / 429 等常见错误码；
- 你能按提示词工程的基本原则，写出更具体、更有效的提示词。

## 一、为什么还要学 API？

网页版和 App 里的 AI 适合人手动对话，而 **API（应用程序编程接口）** 让程序直接调用大模型：批量翻译、自动写周报、给自己的应用接入聊天机器人。它用 API Key 认证、按用量计费，本质是"把 AI 能力变成一行代码就能调用的服务"。

## 二、API Key：AI 服务的"钥匙"

API Key 是一串密钥，用来证明"你是谁、用了多少量"。以 OpenAI 为例，官方帮助中心说明：在 API 平台的项目设置中，进入"API 密钥"页面，点击 **Create new secret key** 即可创建；密钥在创建时完整显示一次，**出于安全原因之后无法再次查看**，丢失只能重新生成。两点安全须知：

- Key 相当于密码，不要发给别人，更不要提交到 GitHub 等公开仓库；
- 一旦泄露，立即到平台吊销并重新生成。

## 三、最简单的调用示例（思路）

流程三步：**拿 Key → 选模型 → 发请求收回复**。用 Python 的示意代码如下（具体参数以官方文档为准）：

```python
from openai import OpenAI
client = OpenAI(api_key="sk-你的Key")     # 1. 填入 API Key
resp = client.chat.completions.create(      # 2. 调用对话接口
    model="gpt-4o-mini",                    # 3. 指定模型
    messages=[{"role": "user", "content": "用一句话介绍你自己"}],
)
print(resp.choices[0].message.content)      # 4. 取出回复内容
```

不写代码也行：本章稍后会介绍的 [Cherry Studio](./软件安装-CherryStudio.md) 等桌面客户端，填入同一把 Key 就能以图形界面调用这批模型。

## 四、DeepSeek 开放平台（platform.deepseek.com）

### 1. 注册与创建 API Key

1. 打开官网 platform.deepseek.com，注册并登录账号。
2. 进入 API 密钥页：https://platform.deepseek.com/api_keys （官方文档指定的申请入口），创建并复制你的 API Key，妥善保管。

### 2. 调用方式（官方文档）

- **API 地址**：OpenAI 格式 base_url 为 `https://api.deepseek.com`，Anthropic 格式为 `https://api.deepseek.com/anthropic`。
- **兼容性**：官方明确说明"DeepSeek API 使用与 OpenAI/Anthropic 兼容的 API 格式，通过修改配置即可用 OpenAI/Anthropic SDK 访问"。Python 示例（官方）：

```python
from openai import OpenAI
client = OpenAI(api_key="你的Key", base_url="https://api.deepseek.com")
resp = client.chat.completions.create(
    model="deepseek-v4-pro",
    messages=[{"role": "user", "content": "你好"}],
)
print(resp.choices[0].message.content)
```

- **模型**：当前官方调用名为 `deepseek-v4-flash`（轻量快速）与 `deepseek-v4-pro`（更强推理），具体以官方"模型 & 价格"页为准（早期版本曾用 deepseek-chat / deepseek-reasoner 命名，已随版本更新）。

### 3. 费用与用量查看

- **用量页**：登录平台后打开 https://platform.deepseek.com/usage （需登录访问），页面显示 Token 用量与费用明细；也可从返回结果的 `usage` 字段查看单次消耗。
- **余额**：官方提供查询余额接口 `GET /user/balance`（返回充值余额、赠送余额与总余额）。
- **计费**：按百万 tokens 计费，费用 = token 消耗量 × 模型单价，从充值余额或赠送余额中扣减，赠送余额优先（官方扣费规则）。

## 五、硅基流动（SiliconFlow，cloud.siliconflow.cn）

### 1. 注册与创建 API Key

1. 打开 https://cloud.siliconflow.cn ，点右上角"登录"，支持短信、邮箱登录（官方文档）。
2. **实名认证**：官方要求按法规完成实名认证（用户中心 → 实名认证，个人认证用支付宝刷脸）；不认证将无法充值与开发票。
3. 进入 API 密钥页 https://cloud.siliconflow.cn/account/ak ，点击"新建API密钥"创建。

### 2. 调用方式（官方文档）

- **API 地址**：`https://api.siliconflow.cn/v1`。
- **兼容性**：大语言模型支持以 OpenAI 库调用（`pip install --upgrade openai`），官方示例：

```python
from openai import OpenAI
client = OpenAI(api_key="你的Key", base_url="https://api.siliconflow.cn/v1")
response = client.chat.completions.create(
    model="Qwen/Qwen2.5-72B-Instruct",
    messages=[{"role": "user", "content": "你好"}],
)
print(response.choices[0].message.content)
```

### 3. 模型、免费额度与费用

- **免费模型**：官方产品简介明确"Qwen2.5（7B）等多个大模型 API 免费使用"，可在**模型广场**（https://cloud.siliconflow.cn/models ，登录后访问）查看模型列表、价格与限速，支持筛选免费模型。
- **费用查看**：登录控制台，点左侧边栏"**费用账单**"（https://cloud.siliconflow.cn/bills ）查看用量账单，需要开发票也在此申请。
- **充值**：完成实名认证后，左侧边栏"**余额充值**"（https://cloud.siliconflow.cn/expensebill ）即可充值。

## 六、API 使用注意事项

### 1. API Key 安全

- Key 等同于密码：不要写进代码、发给别人或提交到 GitHub 等公开仓库。
- 一旦怀疑泄露，立即到平台（如 DeepSeek 的 API 密钥页、硅基流动的 API 密钥页）吊销并重新生成新 Key。

### 2. 费用控制

- 按量计费按 token 计算：DeepSeek 官方换算约 1 个中文字符 ≈ 0.6 token，每次请求消耗可在返回结果的 `usage` 字段看到。
- 先小额充值、勤查余额：DeepSeek 用量页 https://platform.deepseek.com/usage ；硅基流动控制台左侧"费用账单"（https://cloud.siliconflow.cn/bills ）。
- 关注扣费顺序与优惠：DeepSeek 官方说明费用从充值余额或赠送余额扣减、优先扣赠送余额；有缓存命中的输入价格更低。
- 注意限流：请求速率达到上限会返回 **429**（官方错误码），程序应降低频率或错峰请求。

### 3. 常见问题（对照官方错误码）

- **401 认证失败**：API Key 错误或未创建，检查密钥是否正确。
- **402 余额不足**：账号余额不足，前往平台充值页面充值。
- **429 请求速率达上限**：合理规划请求速率，稍后重试。
- **免费模型的限制**：硅基流动免费模型（如 Qwen2.5-7B）通常有速率/用量限制，具体以模型广场标注为准，避免用于高并发场景。
- **网络与地区**：海外平台（如 OpenAI）对部分地区访问受限；国内用户可优先选择 DeepSeek、硅基流动等国内平台直接访问。硅基流动还需注意：未完成实名认证无法充值和开发票，付费前先完成认证。

## 七、提示词工程：基本原则

OpenAI 官方定义：提示工程是"**为模型编写有效指令的过程**，旨在使其持续生成符合需求的内容"。官方指南的核心策略：

1. **写出清晰指令**：给模型设定角色、用分隔符划分内容、提供示例、规定输出格式；
2. **提供参考文本**：让模型基于你给的资料回答；
3. **复杂任务拆成子任务**：一步步来，别一次堆太多要求；
4. **给模型时间"思考"**：要求它先列步骤再给结论；
5. **善用外部工具**（联网搜索、代码执行等）；
6. **系统地测试变更**：改提示后对比结果再决定。

此外，OpenAI 帮助中心还建议：提示要**清晰具体、避免歧义**，可指定语气（正式/友好/专业），并**迭代优化**——先试一版，看输出再改。

## 八、简单示例：改写前后对比

> 差的提示：`写个自我介绍。`

> 好的提示：
>
> ```text
> 你是一名资深简历顾问。请为一名计算机专业应届生写一段 100 字以内的自我介绍：
> 1. 突出编程能力和项目经验；
> 2. 语气专业友好；
> 3. 不使用空话套话。
> ```

同样的模型，提示越具体、越结构化，输出质量越高——这就是提示词工程的日常用法。

## 小结与练习

**练习 1（动手）**：到 https://platform.deepseek.com/api_keys 创建一个 API Key，创建时立即复制并妥善保存（密钥只完整显示一次）。

**练习 2（动手）**：把第三节示例代码中的 `api_key` 和 `base_url` 换成你自己的，运行一次调用，看看返回了什么。

**练习 3（自查）**：401、402、429 三个错误码分别代表什么问题？分别应该怎么处理？

**练习 4（动手）**：用"写个自我介绍。"和第八节的结构化提示词分别问同一个模型，对比两次输出的质量差异。

## 参考官方文档

- [ChatGPT 提示工程最佳实践 - OpenAI 帮助中心（中文）](https://help.openai.com/zh-hans-cn/articles/10032626-prompt-engineering-best-practices-for-chatgpt)
- [Prompt engineering - OpenAI 官方指南](https://developers.openai.com/api/docs/guides/prompt-engineering)
- [在 API 平台中管理项目（含 API 密钥说明）- OpenAI 帮助中心（中文）](https://help.openai.com/zh-hans-cn/articles/9186755-managing-your-api-keys-and-project-api-keys)
- [DeepSeek 首次调用 API（快速开始）](https://api-docs.deepseek.com/zh-cn/)
- [DeepSeek 模型 & 价格](https://api-docs.deepseek.com/zh-cn/quick_start/pricing)
- [DeepSeek 查询余额接口](https://api-docs.deepseek.com/zh-cn/api/get-user-balance/)
- [DeepSeek 错误码](https://api-docs.deepseek.com/zh-cn/quick_start/error_codes)
- [硅基流动快速上手](https://docs.siliconflow.cn/cn/userguide/quickstart)
- [硅基流动产品简介（含免费模型说明）](https://docs.siliconflow.cn/cn/userguide/introduction)
- [硅基流动财务问题（充值/费用账单）](https://docs.siliconflow.cn/cn/faqs/misc_finance)

## 术语中英对照

| 中文 | 英文 | 一句话说明 |
| --- | --- | --- |
| 应用程序编程接口 | API | 让程序之间互相调用的接口 |
| API 密钥 | API Key | 证明"你是谁、用了多少量"的密钥 |
| 大语言模型 | Large Language Model（LLM） | 能理解并生成自然语言的 AI 模型 |
| Token | Token | 模型计费与用量的基本单位 |
| 兼容 | Compatible | 接口格式与 OpenAI/Anthropic 一致，可直接换库调用 |
| 提示词工程 | Prompt Engineering | 为模型编写有效指令的过程 |
| 限流 / 速率限制 | Rate Limit | 单位时间内的请求次数上限，超限返回 429 |
| 错误码 | Error Code | 接口返回的错误编号，如 401、402、429 |
| 余额 | Balance | 账户中可用于扣费的金额 |
| 实名认证 | Real-name Verification | 平台按法规要求验证用户真实身份 |
