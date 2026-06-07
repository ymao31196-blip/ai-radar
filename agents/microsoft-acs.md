# Microsoft Agent Control Specification (ACS) — 跨框架 Agent 治理标准

**日期**：2026-06-02
**来源**：https://techcrunch.com/2026/06/02/microsoft-offers-devs-a-better-way-to-control-ai-agent-behavior/
**可信度**：🟢 官方

### 核心思路
Microsoft 发布开源的 **Agent Control Specification (ACS)**，一个跨框架的 AI Agent 行为治理标准。核心理念：**策略文件跟随 Agent**——用可移植的策略文件定义 Agent 能做什么、不能做什么、何时需要人类审批、什么必须被记录。策略在多个「拦截点」被检查：输入前、工具调用前、工具返回后、最终响应前。

### 架构图

```
用户输入
    ↓
[拦截点 1: 输入前检查] ← ACS 策略文件
    ↓
LLM 推理
    ↓
[拦截点 2: 工具调用前检查] ← ACS 策略文件
    ↓
工具执行
    ↓
[拦截点 3: 工具返回后检查] ← ACS 策略文件
    ↓
[拦截点 4: 最终响应前检查] ← ACS 策略文件
    ↓
输出 + 审计日志
```

### 解决了什么问题
- **痛点**：每个 Agent 框架（LangChain、OpenAI Agents SDK、Anthropic Agents SDK、AutoGen、CrewAI、Semantic Kernel、MCP）各有自己的安全机制，不存在统一的治理标准。Agent 行为失控（越权操作、数据泄露）是阻碍企业级部署的头号障碍
- **之前怎么做**：每个框架单独配置安全规则，切换框架需要重写所有治理逻辑
- **现在怎么做**：一份 ACS 策略文件，跨所有主流框架生效；Agent 无论在哪里运行都携带相同的行为契约

### 关键设计决策
- **策略文件跟随 Agent**：治理逻辑从基础设施中解耦，Agent 去哪里策略跟到哪里
- **多层拦截**：4 个拦截点形成纵深防御（输入/工具前/工具后/输出），单一拦截点被绕过也不致命
- **分类器 + LLM-as-judge + 人工审批**：三层递进的判断机制，兼顾速度和准确性
- **已支持框架**：LangChain、OpenAI Agents SDK、Anthropic Agents SDK、AutoGen、CrewAI、Semantic Kernel、MCP 工具
- **开源**：Strategy 文件格式开放，SDK 提供插件式集成

### 适用场景
- ✅ 适合：多 Agent 系统、跨框架部署、企业级 Agent 治理、合规审计
- ✅ 适合：需要统一安全策略的大型组织
- ❌ 不适合：单 Agent 原型验证阶段（过度设计）

### 行动项
- [ ] 评估 ACS 作为内部 Agent 治理层的可行性
- [ ] 参考 ACS 的四层拦截点设计，审查现有 Agent 系统的安全边界
- [ ] 关注 ACS 与 MCP Skills 实验的整合进展（两个标准互补）
