# 03. 常见报错与排坑速查表（Windows & macOS）

卡住时先别慌，按下面症状直接对号入座，90% 的问题 1 分钟内就能解决。

---

### Q1. 下载本地索引模型一直转圈 / 失败怎么办？
**原因**：校园网波动，或系统全局代理干扰了内置模型分发源连接。
**解决**：
1. 打开 Nowledge Mem -> **设置（Settings）-> AI 模型（AI models）**，点击重试下载。
2. 如果开着全局代理下载反而变慢或失败，尝试暂时关闭代理再试，或切手机热点测试。

---

### Q2. `[macOS / Windows]` 终端输入 `nmem` 提示 `zsh: command not found: nmem` 或「不是内部或外部命令」
**原因**：在 macOS 上，Nowledge Mem 首次启动会先把 `nmem` 安装在 `~/.local/bin/nmem`，还没写进默认的 `zsh` PATH；或者写入后没有重开终端窗口。
**解决**：
1. 打开 Nowledge Mem -> **设置（Settings）-> 通用（General）-> 开发者工具（Developer Tools）-> 命令行界面（Command Line Interface）**。
2. 点击卡片上的 **「写入 `~/.zshrc`」**（或 **「用管理员权限安装」** 安装到 `/usr/local/bin`）。
3. **彻底关闭当前所有的终端 / PowerShell 窗口**，新开一个窗口再试（macOS 也可直接执行 `source ~/.zshrc`）。
4. **临时救急**：在 macOS 终端里也可以直接用完整路径运行，例如：
   ```bash
   ~/.local/bin/nmem config mcp show --host workbuddy
   ```

---

### Q3. WorkBuddy 桌面端找不到「Plugins / 插件」，或者粘贴 MCP 配置报 `Invalid JSON format`
**解决**：
1. **正确入口**：WorkBuddy 桌面端不需要找单独的 Plugins 按钮，直接点左侧栏 **「专家·技能·连接器（Experts · Skills · Connectors）」-> 顶部「Connectors」-> 右上角「Custom connectors」-> `+ Add MCP`**。
2. **防止 JSON 格式报错**：
   - 打开的 `mcp.json` 里默认已经有一对最外层 `{ "mcpServers": { } }`；
   - 粘贴 `nmem config mcp show --host workbuddy` 的输出时，**要么整段替换整个文件里的全部内容，要么只把 `"nowledge-mem": { ... }` 粘到 `"mcpServers": { }` 的大括号里面**，注意检查不要多出或漏掉大括号 `{}`。
3. 保存弹出绿色 `Configuration saved successfully` 后，在 MCP 列表里确认 **`nowledge-mem` 右侧开关已打开（绿色）**。

---

### Q4. WorkBuddy 配置好了，但对话里没有调用记忆工具
**解决**（按顺序逐项检查）：
1. [ ] 确认 **Nowledge Mem 桌面端正在本机运行**（不能退出）。
2. [ ] 在 WorkBuddy 的 `MCP Server Management` 里确认 **`nowledge-mem` 开关为开启状态**。
3. [ ] 重启一次 WorkBuddy，并**新建一个空白对话**测试（旧对话可能不会加载新启用的 MCP 工具）。

---

### Q5. 在「服务商（Providers）」里填好了 DeepSeek API Key，但 AI Now 还是报错 / 读不到模型
**原因**：在「服务商」页只点保存，此时 Mem 仍停留在「本机内置模型」模式，系统会暂停已保存的云端服务商，导致 AI Now 无法调用。
**解决**：
1. 打开 **设置（Settings）-> AI 模型（AI models）**，切到顶部的 **「AI 模型（AI models）」** 标签页（左边那个，不是「服务商」）。
2. 找到 **「记忆优化模型（Memory processing model）」** 卡片，把下拉框从 **「本机内置模型（Built-in model on this device）」** 切换为你刚刚配好的 **DeepSeek**。
3. 切回 **AI Now**，**新建一个对话**再提问即可正常使用。

---

### Q6. 模型调用完工具后突然用英文回复怎么办？
**原因**：底层的 MCP 工具说明和系统提示词以英文为主，部分模型拿到工具结果后会顺着切到英文输出。
**解决**：
- **最快办法**：在提问末尾顺手加一句 **「请用中文回答」**。
- **一劳永逸**：打开 Nowledge Mem -> **设置（Settings）-> 个人资料（Profile）**，在自定义指令里写一句 `所有回复和记忆整理请始终使用简体中文` 并保存。

---

### Q7. `[Windows]` 或老款无独立 GPU 电脑，开了本地大模型很卡、风扇狂转
**原因**：没有 GPU 加速时，内置本地 LLM 只能靠 CPU 运行，内存和 CPU 占用高。
**解决**：
- **不需要卸载 Mem**！保留轻量的本地 **索引模型（Search Index Model）** 即可，不需要下载本地 LLM。
- 如需自动提炼记忆或使用 AI Now，按 [02. 接入 DeepSeek 等国产大模型](02-domestic-models.md) 配置云端 API，不占本机算力。

---

### Q8. 浏览器插件在 DeepSeek / 豆包网页版里连不上 Nowledge Mem
**解决**：
1. 确认 **Nowledge Mem 桌面端正在本机运行**。
2. 刷新一次 DeepSeek 网页标签页（装完插件后旧标签页需要刷新才能生效）。
3. 如果开启了系统全局代理，确认 `localhost` / `127.0.0.1` 在代理绕过列表（Bypass）中。

---

### Q9. 还是没解决？提问前请准备好这 3 条信息
向老师、助教或同学求助时，一次性发这 3 条能最快定位（**注意打码，绝对不要发自己的 API Key 或私密对话**）：
1. 你的电脑系统（例如：`Windows 11` 或 `macOS`）
2. 卡在哪一步 + 报错截图
3. 终端运行 `nmem doctor` 的输出截图
