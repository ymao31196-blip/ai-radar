# MCP 生态 — 近两周动态汇总

**日期**：2026-05-22 ~ 06-05
**来源**：GitHub modelcontextprotocol 组织 + 各 SDK 仓库
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
