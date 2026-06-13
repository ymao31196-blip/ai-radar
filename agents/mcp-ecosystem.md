# MCP 生态 — 近两周动态汇总

**日期**：2026-05-22 ~ 06-11
**来源**：GitHub modelcontextprotocol 组织 + 各 SDK 仓库 + GitHub Changelog
**可信度**：🟢 官方

---

## MCP Registry — 生产就绪的 Server 注册中心

**日期**：2026-05-12（v1.7.9）
**来源**：https://github.com/modelcontextprotocol/registry
**可信度**：🟢 官方

### 核心思路
MCP Registry 是 MCP Server 的"应用商店"，已进入 **API freeze (v0.1)**。开发者可通过 GitHub OAuth/OIDC/DNS 验证发布自己的 MCP Server，让 Claude Code、ChatGPT、Cursor、VS Code 等客户端直接发现和使用。

### 解决了什么问题
- **痛点**：MCP Server 分散在各个 GitHub 仓库，用户需要手动 clone 和配置
- **现在怎么做**：统一注册中心，一键安装和配置

### 适用场景
- ✅ 适合：希望发布自己工具的 MCP Server 开发者
- ✅ 适合：寻找现成 MCP 工具的 Agent 开发者

---

## MCP Skills 实验

**日期**：2026-06-05（活跃开发中）
**来源**：https://github.com/modelcontextprotocol/experimental-ext-skills
**可信度**：🟢 官方实验

### 核心思路
探索通过 MCP 原语（primitives）进行 **Skills 分发与发现** 的标准化机制。目标是让 Agent 技能可以跨平台复用——一次定义，任何 MCP 客户端都能用。

### 解决了什么问题
- **痛点**：每个 Agent 平台（Claude Code、Cursor、Codex）有自己的 skill/plugin 格式，不互通。开发者为同一个工具需要维护多套 skill 定义
- **之前怎么做**：为每个平台单独编写 skill/plugin 配置
- **现在怎么做**：通过 MCP 原语统一 Skills 定义标准，一次编写，多平台复用

### 关键设计决策
- 基于现有 MCP primitives 扩展，而非定义全新协议
- 实验阶段，API 可能变化

### 适用场景
- ✅ 适合：希望在多个 Agent 平台分发自己工具的开发者
- ❌ 不适合：生产环境（仍为实验阶段）

### 行动项
- [ ] 指派 1 人在 1 周内跟踪 MCP Skills 实验进展，判断是否值得为内部工具编写 MCP Skills 适配

---

## MCP 生态数据（截至 2026-06-06）

| 项目 | 状态 | Star 数 |
|------|------|---------|
| MCP Servers 仓库 | 活跃 | 86.8k ⭐ |
| MCP Inspector | 可视化测试工具 | 10k ⭐ |
| 官方 SDK | 10 种语言（TS/Python/Java/Kotlin/C#/Go/PHP/Ruby/Rust/Swift） | — |
| 规范版本 | 2026-07-28 RC（非最终版） | — |

### 关键设计决策
- **多语言 SDK 全覆盖**：降低不同技术栈的接入门槛
- **RC 非最终版**：规范仍在迭代，生产环境建议等正式版

### 行动项
- [ ] 指派 1 人在 1 周内扫描 MCP Registry，列出 3-5 个对我们项目可复用的 MCP Server
- [ ] 评估是否需要将我们的工具封装为 MCP Server 发布到 Registry
- [ ] 订阅 MCP 规范更新，在正式版发布后 2 周内完成 Server 适配评估

---

## Anthropic Claude Partner Hub — MCP 连接器实战

**日期**：2026-06-03
**来源**：https://www.anthropic.com/news/services-track-partner-hub
**可信度**：🟢 官方

### 核心思路
Anthropic 在 Claude Partner Network 中推出了 **Partner Hub MCP 连接器**：合作伙伴通过 MCP 将业务数据（认证人数、生产部署数、案例引用数）连接到 Claude，用自然语言查询合作伙伴状态（「我离下一级还有多远？」「某笔注册交易的状态如何？」）。分级每天刷新，晋升每半年处理一次。

### 解决了什么问题
- **MCP 连接业务数据的模板**：这是 Anthropic 官方首次展示 MCP 在企业内部系统中的应用——不是连接外部工具，而是连接内部业务数据库
- **可复用的模式**：结构化业务数据 → MCP Server → Claude 对话查询，这个三步走模式对任何企业内部 Agent 场景都适用

### 关键设计决策
- 分级标准透明化：认证从业者数量、生产部署数量、公开引用——这三个维度定义了「Claude-ready」的含义
- 每日刷新：MCP 连接的不是静态数据，是实时运营数据

### 行动项
- [ ] 参考 Partner Hub MCP 模式，设计内部运营数据的 Agent 查询接口
- [ ] 评估关键业务指标是否适合通过 MCP 暴露给 Agent

---

## GitHub 第三方编码 Agent 的自动安全验证

**日期**：2026-06-09
**来源**：https://github.blog/changelog/2026-06-09-security-validation-for-third-party-coding-agents/
**可信度**：🟢 官方

### 核心思路
GitHub 已把第三方 coding agents（包括 Claude 和 OpenAI Codex）生成的代码纳入自动安全验证，处理方式与 GitHub Copilot cloud agent 对齐。

### 解决了什么问题
- **痛点**：第三方 agent 写出的代码可能把漏洞、脆弱依赖或密钥泄露带进 PR。
- **之前怎么做**：需要额外手工串接扫描和验证流程。
- **现在怎么做**：GitHub 会在 PR 完成前自动用 CodeQL、GitHub Advisory Database 和 secret scanning 检查 agent 生成的代码，并在发现问题时尝试修复。

### 可用状态
- **状态**：一般可用（GA）
- **默认行为**：默认开启，并遵循仓库的 Copilot 验证设置
- **许可证要求**：不需要 GitHub Advanced Security license

### 归档方向
- 适合放在 `agents/`：这是 GitHub 平台级 agent 安全治理，不是可安装的 Skill 或 MCP Server
- 不适合放在 `skills-mcp/`：它不是 skill 或 MCP 资源目录

### 限制 & 注意
- 适用于 GitHub 已支持的第三方 coding agents 和对应仓库设置

### 行动项
- [ ] 如果团队依赖第三方 coding agents，核对仓库 Copilot 安全验证是否已经开启

---

## Streamable HTTP 的 tools/list 刷新问题（issue 观察）

**日期**：2026-06-11
**来源**：https://github.com/modelcontextprotocol/modelcontextprotocol/issues/2904
**可信度**：🟡 官方 issue（待验证）

### 核心思路
根据 issue #2904 的报告，在 **Streamable HTTP** 场景下，Claude.ai 可能不会在新会话中重新调用 `tools/list`，从而让工具清单更新难以及时下发。这里记录的是 issue 反馈，不是 MCP 规范已经确认的缓存机制。

### 解决了什么问题
- **痛点**：如果这类行为复现，工具定义更新后，客户端可能暂时看不到新 schema。
- **之前怎么做**：默认假设新会话一定会再次调用 `tools/list`。
- **现在怎么做**：对 stateless / Streamable HTTP MCP server，先按“可能存在刷新延迟”来设计 schema 版本和失效策略，但不要把 issue 当成已确认的协议事实。

### 适用场景
- ✅ 适合：维护 Streamable HTTP MCP server、需要频繁迭代 tool schema 的团队
- ❌ 不适合：把当前实现直接解释成“官方已确认的全局缓存机制”

### 限制 & 注意
- 这是官方仓库 issue，仍处于 Open 状态，尚无规范修复结论
- 目前不能据此断言 Claude.ai 或 MCP 协议层已经存在固定缓存实现

### 行动项
- [ ] 继续跟踪 issue #2904 的后续回复、关联 PR / SEP
