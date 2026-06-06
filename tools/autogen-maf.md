# AutoGen → Microsoft Agent Framework

**类型**：Agent 框架
**官网**：https://github.com/microsoft/autogen（→ 迁移至 https://github.com/microsoft/agent-framework）
**GitHub**：https://github.com/microsoft/agent-framework（11.1k ⭐）

---

## ⚠️ 重要：AutoGen 进入维护模式

AutoGen 已不再接受新功能开发。微软将 Agent 框架重心迁移至 **Microsoft Agent Framework (MAF)**。现有 AutoGen 用户应评估迁移路径。

---

## 更新记录

### AutoGen Python v0.6.0 — 2026-06-05（最后一个大版本）

**来源**：https://github.com/microsoft/autogen/releases/tag/python-v0.6.0
**可信度**：🟢 官方

#### 变化了什么
- 新功能：
  - **GraphFlow 并发 Agent 支持**：fan-out-fan-in 模式
  - 可调用边条件
  - **OpenAIAgent**：基于 OpenAI Responses API 的原生集成
  - MCP Streamable HTTP 传输
  - Qwen3 支持
  - `tool_choice` 参数
- Breaking Change：无（但这是最后一个大版本）

#### 有什么用
- GraphFlow 并发是 AutoGen 最强新功能，适合需要并行 Agent 的场景
- 但如果要长期使用，建议直接迁移到 MAF

#### 迁移成本
- 从 AutoGen v0.5.x 升级：无 Breaking Change，但此为最终大版本，后续无新功能
- 如需长期维护，建议制定向 MAF 的迁移计划

#### 行动项
- [ ] 存量 AutoGen 项目：升级到 v0.6.0 作为过渡版本
- [ ] 制定向 MAF 迁移的时间表和评估计划

---

### Microsoft Agent Framework v1.8.0 — 2026-06-04

**来源**：https://github.com/microsoft/agent-framework/releases
**可信度**：🟢 官方

#### 变化了什么
- **Foundry Hosted Agents**：2 行代码部署到微软 Foundry 基础设施
- **Agent Skills 支持**
- **DevUI**：交互式 Agent 开发和调试 UI
- 支持模式：顺序、并发、交接（handoff）、群组协作
- 跨语言：Python + C#/.NET 统一 API
- 标准支持：A2A（Agent-to-Agent）+ MCP 互操作
- 图驱动工作流 + checkpointing + 人机协作 + 时间回溯

#### 有什么用
- **生产级 Agent 框架**：checkpointing 和时间回溯解决 Agent 编排中的故障恢复问题
- **跨语言**：Python 和 .NET 团队可用同一套抽象
- **DevUI**：降低 Agent 调试门槛，可视化查看 Agent 状态和执行轨迹
- **A2A 互操作**：不同框架的 Agent 可通过标准协议通信

#### 迁移成本
- 从 AutoGen 迁移：API 不同，需重写 Agent 定义和工作流
- 建议先在新项目试用 MAF，存量 AutoGen 项目暂维持不动

#### 迁移成本
- 从 AutoGen 迁移到 MAF：API 不同，需重写 Agent 定义和工作流
- 建议先在新项目试用 MAF，存量 AutoGen 项目暂维持 AutoGen v0.6.0

#### 行动项
- [ ] 新 Agent 项目直接用 MAF 而非 AutoGen
- [ ] 评估 MAF Foundry Hosted Agents 是否适合企业部署
- [ ] 存量 AutoGen 项目制定迁移时间表（AutoGen 仅维护模式，无新功能）
