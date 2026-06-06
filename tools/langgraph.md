# LangGraph

**类型**：Agent 编排框架
**官网**：https://langchain.com/langgraph
**GitHub**：https://github.com/langchain-ai/langgraph

---

## 更新记录

### v1.2.x + SDK v0.4.0 — 2026-05-21 ~ 06-02

**来源**：https://github.com/langchain-ai/langgraph/releases
**可信度**：🟢 官方

#### 变化了什么
- **SDK v0.4.0（重大发布）**：
  - v3 streaming primitives（新的流式架构）
  - WebSocket stream transport
  - SSE transport
  - Scoped subgraph handles
  - Messages/tool call projections
- **LangGraph v1.2.1~1.2.4**：
  - `before_builtins` opt-in stream transformers
  - 工具结果不再进入 v3 messages（减少上下文污染）
  - RemoteGraph v3 streaming + interleave
  - `lc_agent_name`：命名工具调度的子 Agent
  - Deep Agents（高层 Agent 封装）：Agent 可规划、使用子 Agent、利用文件系统

#### 有什么用
- **v3 Streaming 架构**：更高效的远程图执行，对 LangGraph Cloud 用户直接受益
- **子 Agent 命名**：`lc_agent_name` 让多 Agent 日志和追踪更清晰
- **Deep Agents**：开箱即用的复杂 Agent 封装，减少手写编排代码
- **Scoped subgraph**：子图隔离，一个子图失败不污染父图状态

#### 迁移成本
- langgraph>=1.2.4 已成为 langchain 主包的强制依赖
- SDK v0.4.0 涉及 streaming API 变更，需检查自定义 streaming handler

#### 行动项
- [ ] 如果使用 LangGraph Cloud，评估 SDK v0.4.0 迁移收益
- [ ] 试用 Deep Agents：能否替代手写的多 Agent 编排？
- [ ] 关注 `lc_agent_name` 在 tracing 中的应用
