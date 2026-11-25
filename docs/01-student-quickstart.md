# 01. 学生上手指南（Windows & macOS 双系统版）

> **目标**：15 分钟内完成 Nowledge Mem 安装、本地搜索就绪，并成功接入 **WorkBuddy**，亲眼看到 AI 跨对话「记住你」。
> **原则**：严格按顺序做完每一步的「验收标准」，不要跳步；遇到任何报错直接翻到 [03. 常见报错与排坑速查表](03-faq-troubleshooting.md)。

---

## 第一步：安装 Nowledge Mem 桌面端（3 分钟）

前往官方下载页下载对应系统的安装包：https://mem.nowledge.co/download

### `[Windows]` 安装要点
1. 下载 `.exe` 安装包并双击运行。
2. 如果弹出 **Windows 已保护你的电脑（SmartScreen）**，点击 **「更多信息」->「仍要运行」**。
3. 建议使用默认安装路径，**避免安装到带中文或空格的自定义路径**。
4. 安装完成后打开 Nowledge Mem，**后续操作期间请保持它在后台运行，不要退出**。

### `[macOS]` 安装要点
1. 确认自己的 Mac 芯片：点击左上角苹果图标 ->「关于本机」，M1/M2/M3/M4 选 **Apple Silicon**，旧款 Intel 芯片选 **Intel**。
2. 双击 `.dmg` 文件后，**务必将 Nowledge Mem 图标拖进 `Applications（应用程序）` 文件夹**，再从「应用程序」里打开（不要直接在 dmg 挂载盘里运行）。
3. 首次打开如提示「来自未知开发者/从互联网下载」，点击「打开」即可。

> **验收标准**：能看到 Nowledge Mem 主界面正常打开。

---

## 第二步：确认本地索引模型就绪（3 分钟）

Nowledge Mem 内置了模型分发源，**不需要手动切换下载源，也不需要代理**，按下面检查即可：

1. 打开 Nowledge Mem 左侧的 **设置（Settings）-> AI 模型（AI models）**。
2. 确认本地 **索引模型（Search Index Model）** 已下载并处于就绪状态（如果还没下载，展开下方模型管理区点击下载即可）。
3. **关于「本地 LLM（Local LLM）」的双系统建议**：
   - **`[Windows]` / 老款 Intel Mac**：如果没有可用的 GPU 加速，界面也会提示「本地 LLM 只能靠 CPU 运行，后台提炼会非常慢且容易发热」。**这一步不需要下载本地 LLM**，只保留索引模型即可；需要记忆提炼或 AI Now 时，可在 [02. 接入国产大模型](02-domestic-models.md) 里切到「服务商（Providers）」接入 DeepSeek API（几块钱够用一学期）。
   - **`[macOS]`（Apple Silicon M 系列）**：有 GPU 加速，本地体验较顺畅，也可以按需切到 DeepSeek API。

> **验收标准**：在 Mem 主界面手动新建一条测试记忆（例如：`我是一名计算机专业学生，本学期正在修《智能体》课程，打算用 Nowledge Mem 做长期记忆实验。`），在顶部搜索框输入 `智能体`，能够立刻搜到这条记忆。

---

## 第三步：确认 `nmem` 命令行工具可用（2 分钟）

WorkBuddy 的自动捕获功能依赖本机的 `nmem` CLI。Nowledge Mem 桌面端会自动配置它，**不需要自己装 Python**：

1. 打开 **设置（Settings）-> 通用（General）**，往下滑找到 **开发者工具（Developer Tools）-> 命令行界面（Command Line Interface）**。
2. 看卡片右侧状态：
   - 如果显示绿色 **已验证（Verified）**，说明已经就绪；
   - 如果显示 **还不能用（Not working yet）**，或顶部栏提示 **CLI 设置（CLI setup）**，按卡片上的按钮完成安装/写入 PATH（macOS 若弹出管理员授权请点允许）。
3. 在终端里做一次最终验证：
   - **`[Windows]`**：**新开**一个 **PowerShell**（或「命令提示符 / 终端」），输入并回车：
     ```powershell
     nmem doctor
     ```
   - **`[macOS]`**：新开一个 **「终端（Terminal）」** 应用，输入并回车：
     ```bash
     nmem doctor
     ```

> **验收标准**：终端输出显示连接本地 Mem 服务正常（没有报错 `command not found` 或 `不是内部或外部命令`）。
> *注意：如果安装前就已经开着终端窗口，**必须关掉重开一个新窗口**，环境变量才会生效。*

---

## 第四步：接入 WorkBuddy（课堂核心实战，6 分钟）

### 4.1 添加插件市场并安装
1. 打开 **WorkBuddy 桌面端**。
2. 进入 **Plugins（插件）-> 点击 `+` 号**（添加插件市场）。
3. **完整复制并粘贴**下面这行地址（**一个字符都不要少，不要只填仓库名**）：
   ```text
   https://raw.githubusercontent.com/nowledge-co/community/main/.workbuddy-plugin/marketplace.json
   ```
   > **为什么必须填完整地址？** 社区仓库同时包含 CodeBuddy 和 WorkBuddy 插件，只填仓库名可能会误装成 CodeBuddy 版本。
4. 在出现的 **nowledge-community** 列表中找到 **Nowledge Mem**，点击 **Install（安装）**。

*(如果校园网访问 `raw.githubusercontent.com` 超时，请直接看 [03. 常见报错与排坑速查表](03-faq-troubleshooting.md#q3-workbuddy-添加插件地址一直转圈或报错)。)*

### 4.2 重启并手动授权 Trust（最容易漏的一步！）
1. 安装完成后，确认插件和 Skill 均处于 **开启（Enabled）** 状态。
2. **完全退出并重新打开 WorkBuddy**（或点击 Reload）。
3. 打开 WorkBuddy 的 **Connections / MCP（连接与 MCP）** 设置页面，找到 `nowledge-mem`。
4. 如果看到信任提示，**手动点击 Trust（信任）**。
   > 安全说明：MCP 连接授权必须由用户本人确认，不会自动静默开启。

### 4.3 课堂验收小实验（亲眼看到 AI 记住你）
1. 在 WorkBuddy 里**新建一个空白对话**。
2. 输入下面这句话并发送：
   ```text
   请用 nowledge-mem 查一下我现在的上下文和关于「智能体课程」的记忆。
   ```
3. 观察现象：
   - WorkBuddy 会调用 `nowledge-mem` 的 MCP 工具进行检索；
   - 它会准确说出你在第二步里存下的「计算机专业 / 《智能体》课程」信息。
4. 再验证自动归档：和它随便聊两句后，回到终端执行：
   ```bash
   nmem t list --source workbuddy -n 5
   ```
   或者直接回到 Nowledge Mem 的 **Threads（对话）** 页面，可以看到刚才的 WorkBuddy 对话已经同步进来。

> **恭喜通关！** 到这里你已经完成了课堂主线全部要求。
> 接下来强烈推荐花 5 分钟完成 [02. 接入 DeepSeek 等国产大模型](02-domestic-models.md)，把你平时免费用的 DeepSeek / 豆包 / Kimi 也连到同一个记忆库里。
