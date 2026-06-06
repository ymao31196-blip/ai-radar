# 降本技巧

> 更新日期：2026-06-05
> 来源：各厂商文档 + Anthropic Opus 4.8 发布公告 + DeepSeek API 文档
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
