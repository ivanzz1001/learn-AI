# AI编程工具(202608)

目前比较值得关注的主力基本是`Cursor`、`Claude Code`、`Codex`、`GitHub Copilot`、`Windsurf`，另外还有 Aider 这种偏终端/Git 的工具。近期的实际开发者比较和研究也基本集中在这些工具上。

#### 我的推荐排序

| 工具                 | 我认为最适合           | Agent能力 | 大型代码库 | IDE体验 |    终端 |       推荐度 |
| ------------------ | ---------------- | ------: | ----: | ----: | ----: | --------: |
| **Cursor**         | 日常主力开发           |   ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |  ⭐⭐⭐⭐ | **★★★★★** |
| **Claude Code**    | 复杂问题/重构/Debug    |   ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |   ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | **★★★★★** |
| **Codex**          | 长任务、复杂工程、代码审查    |   ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |  ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | **★★★★★** |
| **GitHub Copilot** | IDE补全、企业开发       |    ⭐⭐⭐⭐ |  ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |  ⭐⭐⭐⭐ | **★★★★☆** |
| **Windsurf**       | Agent IDE、快速开发   |   ⭐⭐⭐⭐⭐ |  ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |   ⭐⭐⭐ | **★★★★☆** |
| **Aider**          | Git/CLI/开源/自定义模型 |    ⭐⭐⭐⭐ |  ⭐⭐⭐⭐ |    ⭐⭐ | ⭐⭐⭐⭐⭐ | **★★★★☆** |

## 1. Cursor —— 如果只选一个，我最推荐

Cursor官方网站: https://cursor.com/

如果你已经在用 Cursor，我其实不建议因为现在 AI 编程工具变多了就马上换掉。

Cursor 现在已经不只是“AI 版 VS Code”，而是越来越偏向：

```text
Cursor
 ├── Chat
 ├── Agent
 ├── Codebase understanding
 ├── Multi-file editing
 ├── Terminal
 ├── CLI Agent
 └── Cloud Agent
```
官方现在也把 Cursor 定位成 coding agent，可以从 IDE、CLI 等多个入口使用 Agent。

## 2. Claude Code —— 非常强的“工程师 Agent”

Claude Code 官方介绍: https://www.anthropic.com/claude-code

如果 Cursor 是：“AI IDE”; 那么 Claude Code 更像：“坐在你终端旁边的高级工程师”.

典型使用方式：
```text
cd my-project
claude
```
然后：
```text
分析这个项目的网络请求路径
找出为什么高并发下 CPU 利用率不均
不要修改代码，先给我分析
```
它会主动：
```text
find
grep
git
cat
go test
go build
运行程序
分析错误
修改代码
再次测试
```
Anthropic 官方也明确把 Claude Code 定位成 terminal/repo 中的 agentic coding tool，并支持项目级规则、skills、plugins、subagents 等。

## 3. Codex —— 现在非常值得认真考虑

OpenAI Codex: https://openai.com/codex

这个其实我特别建议你关注。

现在的 Codex 已经不是以前那个“生成代码的模型”概念了，而是完整的 coding agent。

官方目前支持：
```text
ChatGPT
IDE
Terminal
Cloud
GitHub / PR
```
而且可以进行：
```text
Feature development
Bug fixing
Refactoring
Migration
Testing
Code review
```
并且支持多个 Agent 并行处理任务。

例如你可以给 Codex：
```text
分析这个 Go 项目。

要求：
1. 不要修改代码
2. 分析启动流程
3. 找出所有 goroutine
4. 找出可能的 data race
5. 分析 CPU hotspot
6. 最后给出修改建议
```
它特别适合**长任务**。
