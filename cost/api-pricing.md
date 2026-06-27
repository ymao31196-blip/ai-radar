# API 定价速查表

> 更新日期：2026-06-12
> 来源：各厂商官方定价页（OpenAI / Anthropic / DeepSeek / Google）
> 可信度：🟢 官方

---

## Anthropic Claude Fable 5 / Claude Mythos 5 定价更新

**日期**：2026-06-09
**来源**：[Anthropic 发布公告](https://www.anthropic.com/news/claude-fable-5-mythos-5)；[Anthropic Pricing](https://platform.claude.com/docs/en/about-claude/pricing)；[暂停访问声明](https://www.anthropic.com/news/fable-mythos-access)
**可信度**：🟢 官方

### 变动内容
- 之前：Claude Opus 4.8 仍是 Anthropic 最强广泛发布模型，标准价为 $5 / $25 per MTok。
- 现在：Claude Fable 5 GA，Claude Mythos 5 限量开放；标准 API 价为 $10 / $50 per MTok，Batch 价为 $5 / $25 per MTok。
- 变动幅度：标准输入/输出翻倍；Batch 保持 50% 折扣。
- 可用性：Anthropic 于 2026-06-12 暂停两款模型的全部访问，价格保留作恢复后的预算参考。

### 通俗解释
Fable 5 / Mythos 5 的价格可以理解成 Anthropic 新旗舰的“豪华档”：标准实时调用比 Opus 4.8 贵一倍，只有能排队异步处理的 Batch 才能回到 Opus 4.8 的价格水平。因为两款模型当前暂停访问，这里更像是提前记账：恢复后也不能默认全量使用，只适合最值钱的任务。

### 对我们项目的影响
- 最难的知识工作、长上下文 agent 任务要单独预算，默认不要路由到 Fable 5。
- 能异步的任务优先 Batch，能直接把标准价减半。

### 行动项
- [ ] 将 Fable 5 只路由给最高价值任务，并给其设置独立预算上限
- [ ] 评估哪些长任务可以迁移到 Batch

---

## 当前各模型价格速查

| 模型 | Input ($/1M) | Output ($/1M) | 缓存命中 Input | 备注 |
|------|-------------|---------------|---------------|------|
| Claude Fable 5 | $10.00 | $50.00 | $1.00 | 当前暂停访问；Batch $5/$25 |
| Claude Mythos 5 | $10.00 | $50.00 | $1.00 | 当前暂停访问；Batch $5/$25 |
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

### 新增
| 模型 | 变动 | 幅度 |
|------|------|------|
| Claude Fable 5 / Claude Mythos 5 | 新旗舰发布 | 标准价 $10/$50；Batch $5/$25 |

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
| 极致旗舰 / 最难知识工作 | Claude Fable 5（恢复后） | ~$35/天 | ~$1,050/月 |
| 复杂推理 | Claude Opus 4.8 / GPT-5.5 | ~$20/天 | ~$600/月 |
| 通用任务 | GPT-5.4 / Claude Sonnet 4.6 | ~$10/天 | ~$300/月 |
| Agent 原型 | DeepSeek V4 Pro | ~$0.87/天 | ~$26/月 |
| 大批量批处理 | DeepSeek V4 Flash | ~$0.28/天 | ~$8.40/月 |
| 缓存重度场景 | DeepSeek V4 Flash（缓存命中） | ~$0.14/天 | ~$4.28/月 |

**价格跨度**：最便宜的缓存场景（$0.14/天）与最贵的极致旗舰（$35/天）相差 **250x**。合理选型的降本空间巨大。

---

## 对我们项目的影响
- **Agent 开发场景**：优先用 DeepSeek V4 Pro 做原型和测试，成本仅为 Claude Opus 的 1/20
- **生产推理**：当前复杂任务保留 Claude Opus 4.8 / GPT-5.5；Fable 5 恢复后再评估最高难度任务；其余任务路由到 DeepSeek V4 Flash
- **缓存优化**：System Prompt 静态部分利用 DeepSeek 缓存（$0.0028/M），几乎零成本
- **Gemini 涨价关注**：如果当前在用 Gemini 系列，3.5 Flash 涨 3-6x 后性价比大幅下降，建议评估切换

## 行动项
- [ ] 建立项目级模型选型表：标注每个场景的推荐模型和成本上限
- [ ] 统计当前 API 调用中各模型的 token 消耗占比，识别降本空间
- [ ] 评估是否因 Gemini 3.5 Flash 涨价而迁移现有调用

---

## 行业成本趋势：AI 支出失控与 SpaceX 成为最大算力提供商

**日期**：2026-06-05
**来源**：[SpaceX SEC filing](https://www.sec.gov/Archives/edgar/data/1181412/000162828026041150/spacexagreementfwp.htm)
**可信度**：🟢 官方（监管文件确认）

### 变动内容
- Google 与 SpaceX 在 2026-06-05 签署 Cloud Service Agreement，SpaceX 向 SEC 披露该客户将从 2026-10 到 2029-06 支付 **$920M/月**，租用约 11 万张 Nvidia GPU 和相关资源
- Anthropic 此前已签约支付 **$1.25B/月** 租用 SpaceX Colossus 1 算力
- 两家合计：$2.17B/月 流向 SpaceX
- Google 称为「桥接容量」以满足 Gemini Enterprise Agent 平台的激增需求

### 通俗解释
这条说明 AI 公司缺的不是想法，而是算力。连 Google 这种有大量数据中心的公司，也要向 SpaceX 租 GPU 来补容量；这意味着未来一段时间 API 价格很难快速下降，开发者更需要做模型路由、缓存和批处理，不然账单会被大模型吞掉。

### 对我们项目的影响
- **即使 Google（全球最大 AI 算力拥有者）也无法自给自足**——算力瓶颈是行业级约束
- **SpaceX 意外成为最大 AI 基础设施赢家**——AI 算力租赁市场规模远超预期
- **GPU 供应紧张将持续**→ API 价格短期内不会大幅下降，选型降本更加重要

---

## Anthropic 6/15 订阅计费拆分 — Agent SDK 独立信用池

**日期**：2026-06-15（生效）
**来源**：[Anthropic Support — Agent SDK 信用额](https://support.claude.com/en/articles/15036540-use-the-claude-agent-sdk-with-your-claude-plan) ｜ [Codersera 解读](https://codersera.com/blog/anthropic-june-2026-billing-change-claude-code/)
**可信度**：🟢 官方

### 变动内容
- Claude Agent SDK、`claude -p` 命令、Claude Code GitHub Actions 及所有第三方 Agent 应用（OpenClaw、Conductor、Zed、Jean 等）**移出**订阅使用池
- 改为**独立月度信用额**，按完整 API 费率计费，**不滚动**（月底清零）

### 通俗解释
以前很多人会把 Claude 订阅理解成“我已经付了月费，Agent 自动化也差不多包含在里面”。这次拆分后，交互聊天和自动化 Agent 变成两个钱袋子：你在终端、GitHub Actions 或第三方 Agent 里跑任务，会消耗独立信用池，用完就需要额外付费或升级。

| 订阅计划 | 月度 Agent 信用额 | 备注 |
|---------|-------------------|------|
| Pro | $20 | 约等于 2M Fable 5 输入 token（$10/1M input 计） |
| Max (5x) | $100 | |
| Max (20x) | $200 | |
| Team / Enterprise | 按席位 | |
| API Key 用户 | 不适用 | 直接走 API 账单 |

### 对我们项目的影响
- **成本拆分清晰化**：交互式 Claude Code 终端使用仍走订阅；自动化 Agent 走信用池 — 两个池子分别管控
- **Agent 用量可视化**：信用池按 API 费率计量，消耗更透明，也更容易用完
- **第三方 Agent 影响**：所有依赖 Agent SDK 的第三方工具（如 OpenClaw、Conductor）不再享受订阅无限量

### 行动项
- [ ] 检查是否已通过 Anthropic 邮件 Claim 信用额（需在 6/15 前领取）
- [ ] 审计现有 Claude Agent 用量的计费归属（订阅 vs Agent SDK）
- [ ] 评估 $20/$100/$200 信用池是否够用，如果不够需升级订阅或切到 API Key 模式
