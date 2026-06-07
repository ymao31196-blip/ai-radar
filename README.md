# AI Radar — 可用 AI 资讯追踪

追踪最新的 AI 动态，**核心准则是：只看能落地的**。每一条记录都必须回答「这对我有什么用」。

## 七大追踪方向

| 方向 | 目录 | 关注点 |
|------|------|--------|
| 🆕 新模型 | [models/](models/) | 新模型发布、横向对比、关键指标 |
| 🔧 工具框架 | [tools/](tools/) | 框架更新、Breaking Changes、新工具 |
| 🏗️ Agent & MCP | [agents/](agents/) | Agent 架构演进、MCP 生态、设计模式 |
| 🧩 Skill & MCP | [skills-mcp/](skills-mcp/) | 官方/社区好用的 Skill 和 MCP Server |
| 📐 Prompt 实战 | [prompts/](prompts/) | 场景化 Prompt 模板、模型敏感度 |
| 🛍️ 产品拆解 | [products/](products/) | 成功 AI 产品拆解、商业化案例 |
| ⚖️ 成本优化 | [cost/](cost/) | API 定价变动、降本技巧、额度变化 |

## 记录规范

每条资讯使用统一模板：

```markdown
## [标题]

**日期**：YYYY-MM-DD
**来源**：[链接]
**可信度**：🟢 官方 / 🟡 可靠媒体 / 🟠 传闻

### 是什么
一句话概括

### 有什么用
对我实际可用的点（必填，不可写"无"）

### 关键数据
- 指标1：xxx
- 指标2：xxx

### 行动项
- [ ] 是否要跟进？怎么做？
```

## 日常操作

- **每周一刷**：快速扫一遍 `models/`、`tools/` 和 `skills-mcp/` 的新增
- **做项目前**：查 `prompts/` 和 `cost/`，确保选型不踩坑
- **思考方向时**：翻 `products/` 和 `agents/`，找可复用的模式
- **选工具时**：查 `skills-mcp/`，看有没有现成的 Skill 或 MCP 直接用
