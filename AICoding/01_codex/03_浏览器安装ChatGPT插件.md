# 浏览器安装ChatGPT插件


按下面的顺序检查：

1. **打开并更新 ChatGPT 桌面应用**
   - 打开电脑上安装的 ChatGPT 应用。
   - 在应用菜单中查找“检查更新”；如果没有该选项，通过你安装应用的官方渠道检查更新。
   - 更新完成后，退出并重新打开应用。

2. **查找浏览器设置**
   - 打开 ChatGPT 的 **Settings（设置）**。
   - 查找 **Computer Use（计算机使用）**。
   - 如果能进入，查找 **Google Chrome**；浏览器没有直接显示时，展开 **More browsers（更多浏览器）**。官方文档给出的配置路径是桌面端的这个入口。[learn.chatgpt.com](https://learn.chatgpt.com/docs/chrome-extension?utm_source=chatgpt.com)

3. **安装并连接官方扩展**
   - 选择 Chrome，按提示安装所需插件。
   - 点击 Chrome 旁边的 **Install（安装）**，从它打开的扩展商店页面安装 ChatGPT 扩展。
   - 回到 ChatGPT 的 Computer Use 设置，确认 Chrome 旁边显示 **Manage（管理）**。
   - 打开 Chrome 对应的开关，使它出现在聊天的 `@` 菜单中。[learn.chatgpt.com](https://learn.chatgpt.com/docs/chrome-extension?utm_source=chatgpt.com)

4. **确认使用同一个 Chrome 用户配置**
   - 如果 Chrome 右上角有多个个人资料，确保扩展安装在你登录公司 GitLab 的那个配置中。
   - 重启 Chrome，然后从工具栏的扩展菜单打开 ChatGPT，检查侧边聊天能否正常加载。[learn.chatgpt.com](https://learn.chatgpt.com/docs/chrome-extension?utm_source=chatgpt.com)

5. **从聊天选择浏览器**
   - 新建一个 **ChatGPT Work 或 Codex** 聊天。
   - 输入 `@`，在菜单中选择 **Chrome**，或者选择已经打开的 MR 标签页。
   - 提交任务，并按提示允许访问 `gitlab.sensecore.cn`。[learn.chatgpt.com](https://learn.chatgpt.com/docs/chrome-extension?utm_source=chatgpt.com)

如果仍然找不到入口，可以按下面区分：

| 你看到的情况 | 下一步 |
|---|---|
| 整个 **Computer Use** 都没有 | 更新后仍缺失，可能受功能开放范围或工作区设置限制；当前官方说明没有提供一个通用的“强制开启”方法 |
| 有 Computer Use，没有 Chrome | 展开 **More browsers**，确认本机已安装 Chrome |
| Chrome 显示 **Install** | 连接尚未完成，重新走设置里的安装流程 |
| Chrome 显示 **Manage**，但 `@` 菜单没有 Chrome | 开启 Chrome 对应开关，再新建 Work 或 Codex 聊天 |
| 能选 Chrome，但连接失败 | 检查扩展所在的 Chrome 配置、网站是否被阻止，再重启浏览器和桌面应用 |

这些排查项来自[官方浏览器扩展说明](https://learn.chatgpt.com/docs/chrome-extension)。功能可用性确实可能受开放进度和工作区设置影响。[learn.chatgpt.com](https://learn.chatgpt.com/docs/chrome-extension?utm_source=chatgpt.com)
