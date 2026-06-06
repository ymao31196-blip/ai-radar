# Dynamic Workflows — 大规模并行 Agent 执行模式

**日期**：2026-05-28
**来源**：https://www.anthropic.com/news/claude-opus-4-8
**可信度**：🟢 官方

### 核心思路
Claude Code 新增 **Dynamic Workflows** 能力：Agent 先分析任务制定计划，然后根据计划并行启动数百个子 Agent（fan-out），各子 Agent 独立执行子任务，最后汇总验证结果。模式：**Plan → Fan-out → Parallel Execute → Verify**。

### 架构图

```
用户需求（如：迁移整个代码库）
        ↓
    Planner Agent
    （分析任务，拆分子任务，生成执行计划）
        ↓
   ┌────┼────────┬────────┐
   ↓    ↓        ↓        ↓
 子Agent 1  子Agent 2  ... 子Agent N
 (模块A)   (模块B)       (模块N)
   ↓    ↓        ↓        ↓
   └────┼────────┴────────┘
        ↓
    Verifier Agent
    （检查结果一致性，汇总报告）
        ↓
      用户
```

### 解决了什么问题
- **痛点**：单个 Agent 受限于上下文窗口和推理能力，无法独立完成数十万行代码的重构或迁移
- **之前怎么做**：人工将大任务拆分为多个小任务，多次手动调用 Agent，中间状态靠人维护
- **现在怎么做**：一个 Planner Agent 自动拆分任务，自动扇出并行执行，自动验证

### 关键设计决策
- **Plan-first**：必须先规划再执行，避免子 Agent 间冲突
- **Parallel fan-out**：数百个子 Agent 并行，时间成本接近单个子任务
- **Verify gate**：所有子任务完成后必须通过验证阶段，确保一致性
- **Effort Control 联动**：根据任务复杂度可调节每个子 Agent 的思考深度

### 适用场景
- ✅ 适合：全库级代码迁移（框架升级、API 重构）、大型代码库审查、批量测试生成
- ❌ 不适合：小型单文件修改（过度设计）、需要实时交互的任务

### 代码示例
```bash
# Claude Code 中使用 Dynamic Workflows
> 将整个项目从 React 18 迁移到 React 19，包括：
  1. 更新所有组件语法
  2. 迁移废弃的 API
  3. 更新类型定义
  4. 确保所有测试通过
```

### 行动项
- [ ] 是否在我们的项目中采用？→ 如果有框架升级/全库重构需求，优先试用
- [ ] 对比 OpenAI Codex Multi-Agent v2 的同类能力
