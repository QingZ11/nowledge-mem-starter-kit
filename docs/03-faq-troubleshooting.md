# 03. 常见报错与排坑速查表（Windows & macOS）

卡住时先别慌，按下面症状直接对号入座，90% 的问题 1 分钟内就能解决。

---

### Q1. 下载本地索引模型一直转圈 / 失败怎么办？
**原因**：默认源在校园网环境下可能受限或速度极慢。
**解决**：
1. 打开 Nowledge Mem -> **Settings -> Models**。
2. 将 **Model Repository（模型下载源）** 切换为 **ModelScope（魔搭）**。
3. 点击重试下载。如果开着全局代理反而下载慢，可以尝试暂时关闭代理再试。

---

### Q2. 终端输入 `nmem doctor` 提示 `command not found` 或「不是内部或外部命令」
**原因**：没有安装内置 CLI，或者安装后没有重开终端导致环境变量（PATH）没刷新。
**解决**：
1. 回到 Nowledge Mem -> **Settings -> Preferences -> Developer Tools**，重新点击一次 **Install bundled CLI**，确认弹出成功提示。
2. **彻底关闭当前所有的终端/PowerShell 窗口**，重新打开一个新窗口再输入 `nmem doctor`。
3. `[Windows]` 如果仍提示找不到，检查是否安装了杀毒软件拦截了脚本执行，或重启一次电脑让用户环境变量生效。

---

### Q3. WorkBuddy 添加插件地址一直转圈或报错
**原因**：常见有两种——填错了地址，或者校园网访问 `raw.githubusercontent.com` 超时。
**解决**：
1. 先核对粘贴的地址是否**一字不差**：
   ```text
   https://raw.githubusercontent.com/nowledge-co/community/main/.workbuddy-plugin/marketplace.json
   ```
   注意：不要只填 `nowledge-co/community`，否则可能误装成 CodeBuddy 插件。
2. 如果确认地址无误但报网络超时：
   - 切换手机热点试一次（插件很小，只耗几百 KB 流量，装完切回校园网即可）。
   - 或者在课上直接向助教/老师获取离线 Skill 包 + 本地 MCP 配置块作为临时备选。

---

### Q4. WorkBuddy 插件显示安装成功了，但对话里完全不调用记忆工具
**原因**：**90% 是漏了「重启 + 点 Trust」这两步**，或者 Mem 桌面端被关掉了。
**解决**（按顺序逐项打勾）：
1. [ ] 确认 **Nowledge Mem 桌面端正在运行**（不能退出）。
2. [ ] 完全退出并**重启 WorkBuddy**。
3. [ ] 打开 WorkBuddy 的 **Plugins**，确认 Nowledge Mem 插件和 Skill 都是 **Enabled**。
4. [ ] 打开 WorkBuddy 的 **Connections / MCP**，确认 `nowledge-mem` 已点击 **Trust（信任）**。
5. [ ] **新建一个空白对话**测试（旧对话可能不会加载新启用的 MCP 工具）。

---

### Q5. `[Windows]` 开了本地大模型后电脑很卡、风扇狂转
**原因**：Windows 笔记本默认使用 CPU 跑本地大语言模型，内存和 CPU 占用高。
**解决**：
- **不需要卸载 Mem**！只需把本地大模型关掉/切回仅使用本地索引模型（索引模型非常轻量，不影响日常使用）。
- 如果需要 AI 提炼记忆或 AI Now，改用 [02. 接入 DeepSeek API](02-domestic-models.md#方案-b选修在-nmem-内部配置-deepseek-api) 即可，不占本机算力。

---

### Q6. 浏览器插件在 DeepSeek / 豆包网页版里连不上 Nowledge Mem
**解决**：
1. 确认 **Nowledge Mem 桌面端正在本机运行**。
2. 刷新一次 DeepSeek 网页标签页（装完插件后旧标签页需要刷新才能注入）。
3. 如果开启了系统全局代理，确认 `localhost` / `127.0.0.1` 在代理的绕过列表（Bypass）中，避免本地请求被发到代理服务器。

---

### Q7. 还是没解决？提问前请先准备好这 3 条信息
向老师、助教或同学求助时，一次性发这 3 条能最快定位（**注意打码，不要发自己的 API Key 或私密对话内容**）：
1. 你的电脑系统（例如：`Windows 11` 或 `macOS Apple Silicon`）
2. 卡在哪一步 + 报错截图
3. 终端运行 `nmem doctor` 的输出截图
