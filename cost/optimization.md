# 降本技巧

> 更新日期：2026-06-11
> 来源：各厂商官方文档 + Anthropic / DeepSeek / OpenAI 官方公告 + Linux Foundation / FinOps Foundation 官方资料
> 可信度：🟢 官方

---

## 1. 上下文缓存 (Context Caching)

**原理**：对重复使用的系统提示、知识库上下文进行缓存。只有首次命中按正常费率，后续自动使用缓存价。

**各厂商缓存对比**：

| 厂商 | 缓存命中价 | 节省幅度 |
|------|-----------|---------|
| DeepSeek V4 Flash | $0.0028/M input | **98%** 于常规价 |
| OpenAI GPT-5.5 | $0.50/M input | **90%** 于常规价 |
| Anthropic Claude | Prompt Caching 支持 | 60-90% |

**最佳实践**：
- 将不变的 System Prompt 放在最前面（首批被缓存）
- Anthropic 支持在 messages[] 中更新 System Prompt 而不破坏缓存（Opus 4.8 新增）
- 划分「热」前缀（频繁复用）和「冷」后缀（每次变化）

**预期节省**：长上下文重复请求可降 **60-98%** 输入费用。

---

## 2. Effort Control / 推理深度调节

**原理**：降低模型推理努力程度，减少输出 tokens。不适用于所有模型。

**可用模型**：
| 模型 | Effort 档位 | 节省幅度 |
|------|------------|---------|
| Claude Opus 4.8 | low/medium/high/extra/max（默认 high） | low effort 减少 30-60% 输出 tokens |
| DeepSeek V4 | reasoning_effort: "high"/"max" | 使用非 thinking 模式可大幅降低 |

**最佳实践**：
- 简单问答 → low effort
- 一般编码/分析 → high（默认）
- 复杂推理/数学 → max
- 非推理任务直接使用 DeepSeek V4 非 thinking 模式

**预期节省**：**15-50%**（取决于任务复杂度分布）。

---

## 3. 模型路由 (Model Routing)

**原理**：根据任务复杂度自动选择合适模型。简单任务用小模型，复杂任务用大模型。

**路由策略示例**：

```
if 任务 == "翻译/摘要/简单问答":
    使用 DeepSeek V4 Flash ($0.14/$0.28)
elif 任务 == "代码生成/Agent":
    使用 DeepSeek V4 Pro ($0.435/$0.87) 或 GPT-5.4 mini ($0.75/$4.50)
elif 任务 == "复杂推理/安全审查":
    使用 Claude Opus 4.8 ($5/$25) 或 GPT-5.5 ($5/$30)
```

**价格差距**：Flash 与 Opus 4.8 输入价差 **35x+**。

**预期节省**：**40-80%** 总成本（取决于流量中简单任务占比）。

---

## 4. 批处理 (Batch API)

**原理**：非实时场景下将多个请求合并发送，享受批量折扣。

**预期节省**：通常 **50%**（具体折扣因厂商而异）。

**适用**：离线分析、数据标注、夜间批量推理。

---

## 5. Token 效率优化

**原理**：要求模型输出更简洁，减少冗余 tokens。

**技巧**：
| 技巧 | 说明 |
|------|------|
| 压缩 System Prompt | 去除不必要的上下文和示例 |
| 设置 `max_tokens` | 限制输出长度，避免冗长回复 |
| 使用 YAML/Markdown 而非 JSON | 结构化输出用 Markdown 表格省 token |
| 中文用表格而非 JSON | 每字段省 1-2 token |
| 利用 Opus 4.8 更高信息密度 | Anthropic 报告 Genie 基准上比 4.7 便宜 61% |

**预期节省**：**15-50%**。

---

## 6. DeepSeek V4 专属节省技巧

**Thinking Mode 不占上下文**：DeepSeek V4 在 Thinking Mode 中，不含 tool call 的回合的 `reasoning_content` 不参与后续上下文拼接（自动忽略）。多轮推理中可节省 **15-40%** 输入 tokens。

**缓存命中极低价**：$0.0028/M tokens，System Prompt 基本等同于免费。

---

## 对我们项目的影响
- **最容易实现的降本**：Prompt Caching（技巧1），只需将 System Prompt 静态部分前置即可，无需改代码
- **最大降本空间**：模型路由（技巧3），简单任务切到 DeepSeek V4 Flash，成本降 35x+
- **最被低估的降本**：Token 效率（技巧5），中文场景用 Markdown 表格而非 JSON，零成本改进
- **DeepSeek V4 用户专属**：Thinking Mode 自动忽略 reasoning_content（技巧6），多轮 Agent 场景受益最大

## 行动项

- [ ] 评估当前项目是否启用了 Prompt Caching（这是最容易实现的降本手段）
- [ ] 对非推理场景，评估切换到 DeepSeek V4 Flash 的成本节省
- [ ] 实现简易模型路由：简单任务 → Flash/小模型，复杂任务 → Opus/GPT-5.5
- [ ] 检查现有 System Prompt 是否可以精简 + 缓存优化

---

## 7. Tokenomics Foundation / AI Value 标准化开始成形

**日期**：2026-06-03
**来源**：[Linux Foundation press release](https://www.linuxfoundation.org/press/linux-foundation-announces-the-intent-to-launch-the-tokenomics-foundation-to-establish-open-standards-for-ai-cost-management)；[FinOps X 2026 Day 1 keynote](https://www.finops.org/insights/finops-x-2026-day-1-keynote/)；[Token Economics: The Atomic Unit of AI Value](https://www.finops.org/insights/token-economics-the-atomic-unit-of-ai-value/)
**可信度**：🟢 官方

### 背景：AI 成本管理开始标准化

Linux Foundation 与 FinOps Foundation 已经把 AI token 成本管理推到公开议程：

| 事件 | 事实 |
|------|------|
| Tokenomics Foundation | Linux Foundation 在 2026-06-03 宣布启动意向，目标是为 AI 成本管理建立开放标准 |
| FinOps X 2026 | 6/8-11 的大会把 AI Value / Token Economics 作为核心议题，FinOps Foundation 公开讨论 token economics 的定义与度量 |
| 研究材料 | FinOps Foundation 已发布 AI Value、token pricing 与 AI/ML on Kubernetes 相关工作材料 |

### Tokenomics Foundation 是什么

Linux Foundation 旗下的 Tokenomics Foundation 旨在统一 AI token 的计费语言和成本管理框架，帮助业界定义：
- cost-per-intelligence（单位智能成本）
- tokens-per-watt（单位能效）
- 更一致的 token 计价与指标口径

### 对我们项目的影响

- 需要尽早建立按模型、按场景、按开发者的 token 用量仪表盘。
- 只看 API 账单不足以定位成本黑洞，必须结合任务场景和路由策略。
- 低成本模型路由、Batch API、缓存命中率和输出上限，都会成为主要降本杠杆。

### 行动项

- [ ] 建立按模型 / 按场景 / 按开发者的 token 用量仪表盘
- [ ] 对每个使用者/团队设置 token 用量预警和硬性上限
- [ ] 评估商用模型路由方案（Factory）vs 自建路由
- [ ] 订阅 FinOps Foundation 的 AI Value / Tokenomics 工作组进展

---

## 8. Claude Agent SDK / `claude -p` 订阅额度拆分

**日期**：2026-06-09 公告，2026-06-15 生效
**来源**：[Claude Agent SDK overview](https://docs.anthropic.com/en/docs/claude-code/sdk)；[Claude Code legal and compliance](https://docs.anthropic.com/en/docs/claude-code/legal-and-compliance)
**可信度**：🟢 官方

### 变动内容
- 之前：Agent SDK 和 `claude -p` 订阅计划用量与交互式使用额度共用。
- 现在：从 2026-06-15 起，订阅计划上的 Agent SDK 和 `claude -p` 用量会改走新的月度 Agent SDK credit，与交互式使用额度分开。
- 变动幅度：额度被拆分，agent 任务的预算、监控和告警要单独做。

### 对我们项目的影响
- 如果团队在 Claude Code / Agent SDK 上跑批量 agent，不能再把它当成“交互式额度的附属消耗”。
- 预算面板需要把交互式聊天、`claude -p` 和 Agent SDK 分开统计。

### 行动项
- [ ] 给 Agent SDK 单独建预算和告警
- [ ] 检查 `claude -p` 和自动化任务是否需要迁移到独立额度
