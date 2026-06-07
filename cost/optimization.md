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

---

## 7. Tokenomics Foundation — AI 支出的行业标准即将到来

**日期**：2026-06-05
**来源**：https://techcrunch.com/2026/06/05/the-token-bill-comes-due-inside-the-industry-scramble-to-manage-ais-runaway-costs/
**可信度**：🟢 官方（Linux Foundation 旗下 FinOps Foundation 主导）

### 背景：AI 支出正在失控

2026 年上半年的 AI 支出数据堪称触目惊心：

| 事件 | 详情 |
|------|------|
| Uber | 2026 全年 AI 预算在 **4 月已耗尽** |
| Microsoft | 收回开发者的 Claude Code 许可证 |
| Priceline | Cursor 续费报价涨 **4-5x** |
| 某公司 | 忘记设用量限制，收到 **$5 亿 Claude 账单** |
| 总体 | 开发者人均 token 消耗 9 个月涨 **18.6x** |

### Tokenomics Foundation 是什么

Linux Foundation 旗下 FinOps Foundation 推动的新标准组织，目标是：
- 定义「tokenomics」的权威定义和框架
- 建立 AI token 用量和计费的开放标准/指标
- 提出新指标：**cost-per-intelligence**（单位智能成本）、**tokens-per-watt**（每瓦特 token 数）
- 统一跨厂商的 token 计价语言（目前每家对「token」的计量不同）
- 正式发布 **2026 年 7 月**

### 市场响应

多个赛道已在形成：
- **纯成本追踪**：Pay-i（AI 投入的追踪/测算/优化）、Paid（按实际价值 token 计费）
- **工程效能**：Jellyfish、Waydev、Faros AI（Agent 监控 + ROI 证明）
- **现有平台的扩展**：Ramp（AI 支出管理）、Datadog/New Relic（token 级可观测性）、AWS（预计下周推出 AI 财务管理功能）
- **模型路由**：Factory 推出自动选择最便宜模型的 router；Anthropic 企业版已将 Opus 调用自动路由到 Sonnet/Haiku

### 最佳 ROI 策略

Jellyfish 研究：
- Token 消耗最多的工程师生产力约为普通工程师的 **2x**，但 token 消耗是 **10x**
- 「最佳 ROI 来自将中间层从低→中等使用率提升，而非推动重度用户更高」

### 对我们项目的影响
- **立即建立 token 用量监控**：在 Tokenomics Foundation 标准发布前，至少要有按模型/按场景的用量面板
- **设置硬性上限**：参考 Uber 的教训——没有用量限制 = 预算黑洞
- **评估模型路由**：如果尚未实现模型路由（简单→Flash，复杂→Opus），这是最立竿见影的降本手段（35x+ 价差）
- **关注 Tokenomics Foundation 7 月发布**：标准确定后，各厂商将开始兼容，提前准备可抢占先机

### 行动项
- [ ] 建立按模型/按场景/按开发者的 token 用量仪表盘（最晚 7 月底前完成）
- [ ] 对每个使用者/团队设置 token 用量预警和硬性上限
- [ ] 评估商用模型路由方案（Factory）vs 自建路由
- [ ] 订阅 FinOps Foundation 的 Tokenomics 工作组进展
