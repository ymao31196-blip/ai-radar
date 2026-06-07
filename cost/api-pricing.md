# API 定价速查表

> 更新日期：2026-06-05
> 来源：各厂商官方定价页 + Simon Willison 博客 (simonwillison.net)
> 可信度：🟢 官方（定价页）/ 🟡 第三方汇总（Simon Willison）

---

## 当前各模型价格速查

| 模型 | Input ($/1M) | Output ($/1M) | 缓存命中 Input | 备注 |
|------|-------------|---------------|---------------|------|
| **OpenAI GPT-5.5** | $5.00 | $30.00 | $0.50 | 前沿推理 |
| OpenAI GPT-5.4 | $2.50 | $15.00 | $0.25 | 性价比专业 |
| OpenAI GPT-5.4 mini | $0.75 | $4.50 | $0.075 | 支持 coding/agent |
| OpenAI GPT-5.4 nano | $0.20 | $1.25 | — | 入门级 |
| **Claude Opus 4.8** | $5.00 | $25.00 | Prompt Caching 支持 | 常规模式 |
| Claude Opus 4.8 Fast | $10.00 | $50.00 | — | 2.5x 速度 |
| Claude Sonnet 4.6 | $3.00 | $15.00 | Prompt Caching 支持 | |
| Claude Haiku 4.5 | $1.00 | $5.00 | Prompt Caching 支持 | |
| **DeepSeek V4 Flash** | $0.14 | $0.28 | $0.0028 | ⭐ 性价比之王 |
| DeepSeek V4 Pro | $0.435 | $0.87 | $0.0036 | MoE 大模型 |
| **Gemini 3.5 Flash** | $1.50 | $9.00 | — | 5月19日发布，涨3x |
| Gemini 3.1 Pro | $2.00 | $12.00 | — | |
| Gemini 3.1 Flash-Lite | $0.25 | $1.50 | — | |

---

## 近期价格变动汇总

### 涨价
| 模型 | 变动 | 幅度 |
|------|------|------|
| Gemini 3.5 Flash | 较 3 Flash Preview | **涨 3x** |
| Gemini 3.5 Flash | 较 3.1 Flash-Lite | **涨 6x** |
| GPT-5.5 | 较 GPT-5.4 | **涨 2x** |

### 不变
| 模型 | 说明 |
|------|------|
| Claude Opus 4.8 | 价格与 Opus 4.7 相同（$5/$25），但 token 效率提升，实际更便宜 |

### 降价
| 模型 | 说明 |
|------|------|
| Claude Opus 4.8 Fast Mode | 比 Opus 4.7 同等速度模式便宜 **3x**（$10/$50 vs $30/$150） |
| DeepSeek V4 Flash | 缓存命中仅 $0.0028，比 OpenAI 缓存价（$0.50）便宜 **99.4%** |

---

## 当前最优策略

> 成本按公式 `(1M × input价) + (0.5M × output价)` 计算，假设 30 天/月

| 场景 | 推荐模型 | 日成本 | 月成本 (~30天) |
|------|----------|--------|---------------|
| 复杂推理 | Claude Opus 4.8 / GPT-5.5 | ~$20/天 | ~$600/月 |
| 通用任务 | GPT-5.4 / Claude Sonnet 4.6 | ~$10/天 | ~$300/月 |
| Agent 原型 | DeepSeek V4 Pro | ~$0.87/天 | ~$26/月 |
| 大批量批处理 | DeepSeek V4 Flash | ~$0.28/天 | ~$8.40/月 |
| 缓存重度场景 | DeepSeek V4 Flash（缓存命中） | ~$0.14/天 | ~$4.28/月 |

**价格跨度**：最便宜的缓存场景（$0.14/天）与最贵的复杂推理（$20/天）相差 **140x**。合理选型的降本空间巨大。

---

## 对我们项目的影响
- **Agent 开发场景**：优先用 DeepSeek V4 Pro 做原型和测试，成本仅为 Claude Opus 的 1/20
- **生产推理**：复杂任务保留 Claude Opus 4.8 / GPT-5.5；其余任务路由到 DeepSeek V4 Flash
- **缓存优化**：System Prompt 静态部分利用 DeepSeek 缓存（$0.0028/M），几乎零成本
- **Gemini 涨价关注**：如果当前在用 Gemini 系列，3.5 Flash 涨 3-6x 后性价比大幅下降，建议评估切换

## 行动项
- [ ] 建立项目级模型选型表：标注每个场景的推荐模型和成本上限
- [ ] 统计当前 API 调用中各模型的 token 消耗占比，识别降本空间
- [ ] 评估是否因 Gemini 3.5 Flash 涨价而迁移现有调用

---

## 行业成本趋势：AI 支出失控与 SpaceX 成为最大算力提供商

**日期**：2026-06-05
**来源**：https://techcrunch.com/2026/06/05/google-will-pay-spacex-920m-per-month-for-compute/
**可信度**：🟢 官方（监管文件确认）

### 变动内容
- Google 签署协议，2026年10月至2029年6月向 SpaceX 支付 **$920M/月** 租用约 11 万张 Nvidia GPU
- Anthropic 此前已签约支付 **$1.25B/月** 租用 SpaceX Colossus 1 算力
- 两家合计：$2.17B/月 流向 SpaceX
- Google 称为「桥接容量」以满足 Gemini Enterprise Agent 平台的激增需求

### 对我们项目的影响
- **即使 Google（全球最大 AI 算力拥有者）也无法自给自足**——算力瓶颈是行业级约束
- **SpaceX 意外成为最大 AI 基础设施赢家**——AI 算力租赁市场规模远超预期
- **GPU 供应紧张将持续**→ API 价格短期内不会大幅下降，选型降本更加重要
