# 02. 接入 DeepSeek 等国产大模型（网页插件 + API 进阶）

很多同学第一次接触时会把两件事混在一起，这里先帮你一眼分清：

| 方案 | 适合谁 | 要不要花钱 | 解决什么问题 |
| --- | --- | --- | --- |
| **方案 A：浏览器插件（强烈推荐所有人做）** | 平时用 **DeepSeek / 豆包 / Kimi / 元宝 / 千问** 网页版写作业、查资料的同学 | **完全免费** | 把网页版 AI 的对话一键存进 nmem，或把已有记忆带进新对话 |
| **方案 B：配置 DeepSeek API（选修进阶）** | 想让 nmem 自动提炼记忆、用内置 AI Now，或 Windows 轻薄本不想本地跑大模型 | 极低（充 5～10 元够用一学期） | 给 nmem 内部提供高速、低价的云端推理大脑 |
| **方案 C：Cherry Studio / 自建 Agent（课程彩蛋）** | 做《智能体》大作业想用自己的代码或图形客户端连长期记忆 | 视所选模型而定 | 通过标准 MCP 协议把 nmem 变成任意 Agent 的记忆后端 |

---

## 方案 A：零成本接入 DeepSeek / 豆包 / Kimi 等网页版（5 分钟）

> **配套视频**：*[此处插入 短视频 3：DeepSeek 网页版与 WorkBuddy 联动（约 60 秒）]*

Nowledge Mem 的官方浏览器插件原生支持主流国产网页端 AI，包括：
- **DeepSeek**（`chat.deepseek.com`）
- **Kimi**、**豆包**、**通义千问**、**腾讯元宝**、**智谱清言**、**MiniMax**
- 同时也支持 ChatGPT、Claude、Gemini、NotebookLM、Perplexity 等。

### 安装步骤（双系统通用）
1. 确认 **Nowledge Mem 桌面端正在运行**。
2. 安装浏览器插件（Nowledge Mem Exchange）：
   - **`[Windows]`**：如果你平时用系统自带的 **Edge 浏览器**，**不需要专门去下载 Chrome**——Edge 可以直接安装 Chrome 扩展（也可以在扩展页面开启「允许来自其他应用商店的扩展」或按官方下载页指引加载）。
   - **`[macOS]`**：Chrome 或 Edge 浏览器均可直接安装。
3. 安装后把插件图标**固定（Pin）在浏览器右上角工具栏**，点开确认显示已连接到本地 Nowledge Mem。

### 跨工具联动小实验（最直观的体验）
1. 打开 **DeepSeek 网页版**（`https://chat.deepseek.com`），和它讨论一个课程大作业选题（例如：「帮我设计一个带长期记忆的校园答疑智能体，核心模块有哪些？」）。
2. 点开浏览器右侧/右上角的 **Nowledge Mem 插件**，点击保存当前对话（Save / Sync），并提炼或保存一条关键结论到记忆库。
3. 切回 **WorkBuddy**，新开一个对话问它：
   ```text
   帮我查一下我刚才在 DeepSeek 里讨论的校园答疑智能体方案。
   ```
4. 你会看到 WorkBuddy 直接读出了你在 DeepSeek 网页版里聊过的内容——这就是**跨平台 Agent 共享记忆**的真实效果。

---

## 方案 B（选修）：在 nmem 内部配置 DeepSeek API

> **什么时候需要配这个？**
> 当你想使用 nmem 内置的 **AI Now**、**自动从长对话中提炼记忆（Distillation）**、或 **Smart Feed**，但电脑跑本地小模型太慢/发烫时（特别是 Windows 轻薄本），配一个 DeepSeek API 体验会立刻起飞。

### 1. 获取 DeepSeek API Key
1. 访问 DeepSeek 开放平台：`https://platform.deepseek.com` 并注册/登录。
2. 充值极少余额即可（例如 5～10 元，日常学习提炼记忆通常能用整个学期）。
3. 在左侧 **API Keys** 页面点击「创建 API Key」，**立刻复制保存**（关闭弹窗后无法再次查看完整 Key）。

> **安全提醒**：API Key 相当于你的钱包密码，**绝对不要截图发到课程群、不要提交到 GitHub 仓库**！

### 2. 在 Nowledge Mem 中填入配置
1. 打开 Nowledge Mem -> **Settings（设置）-> Providers（模型供应商）**。
2. 选择添加 **DeepSeek**（或选择 **OpenAI Compatible / 自定义 OpenAI 兼容接口**），按如下信息填写：
   - **Base URL**：`https://api.deepseek.com`（若界面要求带版本路径可填 `https://api.deepseek.com/v1`）
   - **API Key**：粘贴你刚才复制的 Key
   - **推荐模型**：`deepseek-chat`（性价比高、响应快，适合日常记忆提炼与问答）
3. 点击测试连接（Test），通过后回到 **Settings -> Models / LLM Provider**，将远程 LLM 切换为刚刚配置好的 DeepSeek。

*(同理，通义千问 DashScope、硅基流动 SiliconFlow、智谱 GLM、Kimi Moonshot 等只要提供 OpenAI 兼容接口的国产平台，都可以用完全相同的方法接入。)*

---

## 方案 C（《智能体》课程大作业彩蛋）

如果你在课后想进一步把 Nowledge Mem 用到自己的课程项目或大作业里：

1. **用 Cherry Studio + DeepSeek API**：
   - Cherry Studio（2.1.8 及以上版本）已经内置了 Nowledge Mem 的 MCP 预设，直接在 MCP 设置里启用即可让 DeepSeek API 对话读写你的本地记忆库。
2. **用 Python / LangGraph 自己写 Agent**：
   - Nowledge Mem 提供标准 **MCP Server** 和 **本地 HTTP/CLI 接口**，社区仓库 `nowledge-co/community` 中已有 `nowledge-mem-langgraph` 等集成参考，可以直接把你的课程大作业升级成「带持久化记忆图谱的智能体」。
