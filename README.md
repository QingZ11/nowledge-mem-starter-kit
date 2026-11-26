# Nowledge Mem 新手上手指南（学生与课程版）

> 花 **15 分钟**，给你的 AI 装上「长期记忆」。
> 不管你是用 **WorkBuddy** 写代码，还是在网页上免费用 **DeepSeek / 豆包 / Kimi / 腾讯元宝 / 通义千问** 写作业、查论文，都可以共用同一个本地记忆库，不用每次新开对话都重新交代背景。

---

## 一、跟着 4 段短视频直接上手（每段不到 1 分钟，点击即可在线播放）

<details open>
<summary><strong>01. 首次启动：下载本地索引模型 + 创建第一条记忆（50 秒）</strong></summary>

https://github.com/user-attachments/assets/d7ffa7a9-8872-4198-a6ee-4c0e7cfbafb2

</details>

<details>
<summary><strong>02. WorkBuddy 通过 MCP 接入 Nowledge Mem 并召回记忆（71 秒）</strong></summary>

https://github.com/user-attachments/assets/70b9f9ac-be49-4dce-b9d6-6d21c92d5bcb

</details>

<details>
<summary><strong>03. 在 Nowledge Mem 配置 DeepSeek 模型 + AI Now 中文问答（47 秒）</strong></summary>

https://github.com/user-attachments/assets/2d55a66a-8c2a-403d-bcc7-4d0ef69d94bd

</details>

<details>
<summary><strong>04. DeepSeek 网页版插件同步/提炼 → WorkBuddy 跨工具召回（64 秒）</strong></summary>

https://github.com/user-attachments/assets/4f148223-bf3d-4459-9f43-f45ede9225a9

</details>

---

## 二、图文手册导航

| 你的需求 | 点这里开始 | 预计耗时 |
| --- | --- | --- |
| **第一次安装与上手（必看）** | [01. 15 分钟上手指南（Windows & macOS 双系统）](docs/01-student-quickstart.md) | 15 分钟 |
| **想连 DeepSeek / 豆包 / Kimi 等国产 AI** | [02. 接入 DeepSeek 等国产大模型（免费插件 + API 进阶）](docs/02-domestic-models.md) | 5～10 分钟 |
| **安装或使用时遇到报错** | [03. 常见报错与排坑速查表](docs/03-faq-troubleshooting.md) | 随查随用 |
| **老师 / 助教课堂演示参考** | [04. 课堂 15 分钟演示脚本与课前检查清单](docs/04-instructor-demo-script.md) | 课前 5 分钟 |

---

## 三、30 秒看懂：Nowledge Mem 是什么？

在智能体（AI Agent）架构中，一个完整的 Agent 通常由三个核心部分组成：

```text
┌──────────────────────────────────────────────────────────┐
│                       AI Agent                           │
│                                                          │
│   ┌──────────┐      ┌───────────────┐      ┌──────────┐  │
│   │   LLM    │ ───▶ │ Tools / MCP   │ ───▶ │  Memory  │  │
│   │  (大脑)   │ ◀─── │   (手脚协议)   │ ◀─── │ (海马体)  │  │
│   └──────────┘      └───────────────┘      └──────────┘  │
│                                            Nowledge Mem  │
└──────────────────────────────────────────────────────────┘
```

大语言模型本身有两个天然限制：**上下文窗口有限**、**新开对话即失忆**；更常见的是，你在 DeepSeek 里聊出来的项目思路，切到 WorkBuddy 写代码时它完全不知道。

**Nowledge Mem** 就是你的 **AI 长期记忆层**：
- **本地优先**：你的课程笔记、论文摘录、项目决策和历史对话保存在本地，随时可搜索、可追溯。
- **跨工具共享**：通过 **MCP 协议** 和 **浏览器插件**，让 WorkBuddy、DeepSeek、Kimi、豆包、Cherry Studio 甚至你自己写的 Agent 共用同一份记忆。
- **自动沉淀**：连接好插件后，对话记录会自动归档，告别手动复制粘贴。

---

## 四、常用官方链接

- 软件下载（Windows / macOS）：https://mem.nowledge.co/download
- 官方文档：https://mem.nowledge.co/docs
- 社区集成与插件：https://github.com/nowledge-co/community
