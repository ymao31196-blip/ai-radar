# 多 Agent 框架对比 — 2026年6月选型指南

**日期**：2026-06-05
**来源**：GitHub 各框架仓库 + 官方发布公告
**可信度**：🟢 官方

### 核心思路
近两周三个主流多 Agent 框架均有重大更新，且市场格局发生显著变化：**AutoGen 退役 → Microsoft Agent Framework 接班**。当前存活的三条路径各有侧重。

### 架构对比

| 维度 | LangGraph + Deep Agents | Microsoft Agent Framework | CrewAI |
|------|------------------------|--------------------------|--------|
| **Star** | 34k | 11.1k | 52.9k |
| **定位** | 底层编排 + 高层封装 | 企业级多 Agent 平台 | 角色驱动 + 事件工作流 |
| **编排模式** | 图驱动（Subgraph） | 顺序/并发/交接/群组 | Crews（自治团队）+ Flows（事件驱动） |
| **Agent 模式** | Deep Agents（规划→子Agent→文件系统） | 图驱动 + checkpointing + 时间回溯 | 角色协作 + 精确事件流 |
| **持久化** | ✅ Durable execution（从故障恢复） | ✅ Checkpointing + 时间回溯 | ⚠️ 有限 |
| **人机协作** | ✅ | ✅ | ✅ |
| **跨语言** | Python | Python + C#/.NET | Python |
| **A2A/MCP** | MCP | A2A + MCP | 有限 |
| **声称性能** | — | — | 比 LangGraph 快 5.76×（特定 QA 任务） |
| **企业就绪** | ✅ LangSmith 可观测性 | ✅ Foundry Hosted Agents + DevUI | ✅ AMP Suite 控制面板 |
| **子 Agent 扇出** | ✅ Deep Agents | ✅ 并发/群组 | ✅ Flows |

### 解决了什么问题
- **痛点**：AutoGen 退役后，多 Agent 框架进入三国时代（LangGraph / MAF / CrewAI），三者 API 风格、部署模式、价格模型完全不同，选错框架的迁移成本极高
- **之前怎么做**：AutoGen 是默认选择，社区统一，无需纠结
- **现在怎么做**：根据团队技术栈和项目阶段决策：Python 深度定制 → LangGraph；企业级 + .NET → MAF；快速原型 + 角色驱动 → CrewAI

### 关键设计决策
- **LangGraph**：选择了「底层图编排 + 高层 Deep Agents」双层架构，灵活性最高但学习曲线最陡
- **MAF**：继承了 AutoGen 的生态但重新设计了 API，从研究驱动转向产品驱动
- **CrewAI**：坚持「角色驱动」这个差异化，声称速度优势作为卖点

### 适用场景
- ✅ **选 LangGraph**：需要最大灵活性、已有 LangChain 生态投资、自定义 Agent 编排逻辑
- ✅ **选 MAF**：企业级部署（.NET 团队、Foundry 基础设施）、需要跨语言、AutoGen 迁移用户
- ✅ **选 CrewAI**：快速原型、中小团队、角色驱动协作场景匹配
- ❌ **不选 AutoGen**：已维护模式，不再接受新功能

### 行动项
- [ ] 如果当前在用 AutoGen，立即制定向 MAF 或 LangGraph 的迁移计划
- [ ] 新项目根据团队技术栈选择：Python 团队优先 LangGraph / CrewAI；.NET 团队优先 MAF
- [ ] 关注 Deep Agents、MAF Skills、CrewAI 对话流这三个新能力的实际表现
