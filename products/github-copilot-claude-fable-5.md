# GitHub Copilot — Claude Fable 5 上线后暂停访问

**日期**：2026-06-09（上线）/ 2026-06-12（暂停访问）
**官网**：https://github.com/features/copilot
**来源**：[GitHub Changelog](https://github.blog/changelog/2026-06-09-claude-fable-5-is-generally-available-for-github-copilot/)；[Anthropic 暂停访问声明](https://www.anthropic.com/news/fable-mythos-access)
**阶段**：🔴 暂停访问

### 一句话定位
GitHub 曾把 Anthropic 的 Claude Fable 5 纳入 Copilot 模型选择器，但已于 2026-06-12 在全部 Copilot 入口暂停访问；其他 Claude 模型不受影响。

### 核心功能
- 在 Copilot 的模型选择器中可选 Claude Fable 5，覆盖 VS Code、Visual Studio、Copilot CLI、云端 agent、Copilot app、github.com、GitHub Mobile、JetBrains、Xcode、Eclipse 等多个入口。
- 适用范围包括 Copilot Pro+、Max、Business、Enterprise。
- 企业和商业版管理员需要在 Copilot 设置里显式打开对应策略，默认是关闭的。
- 该模型要求开启数据保留，GitHub 明确提示它与其他 Claude 模型的 ZDR 路径不同。
- GitHub 在 6 月 12 日更新公告，确认 Fable 5 已从全部 Copilot 体验暂停。

### 技术栈（已知/推测）
- 模型：Anthropic Claude Fable 5
- 平台：GitHub Copilot 多端产品线
- 计费：Usage Based Billing 下按 provider list pricing 结算

### 商业模式
- 通过更强的模型菜单抬高 Copilot 高阶套餐的付费价值，重点服务 Pro+、Max、Business、Enterprise。
- 仍然走 usage-based 路径，但把模型选择和计费绑定到 GitHub 的产品体系里。
- 企业客户要先过管理员策略和数据保留约束，商业化和合规绑定得更紧。

### 增长策略
- 用多端覆盖放大模型上新的可见度，让用户在 IDE、CLI、Web、Mobile 里都能碰到同一能力。
- 用「更适合长任务和自治编码」的定位抢占高复杂度工作流。
- 通过企业管理员策略和明确的数据处理说明，降低大客户落地阻力。

### 可复用的点
- 新模型上线时，不能只说“能用”，还要一次讲清楚“谁能用、在哪能用、管理员怎么开、数据怎么处理”。
- 对企业产品来说，权限策略和数据保留规则本身就是产品的一部分，不是附录。

### 踩过的坑
- 当前无法在 GitHub Copilot 中使用 Claude Fable 5，恢复时间尚未公布。
- Claude Fable 5 不是默认对企业组织开放，管理员没开 policy 时用户看不到。
- 如果团队对数据驻留或合规要求很严，这个模型未必能直接落地。

### 行动项
- [ ] 跟踪 GitHub 与 Anthropic 的恢复公告，恢复前不要依赖该模型。
- [ ] 如果团队用 Copilot Business / Enterprise，先确认是否允许 30 天数据保留。
- [ ] 检查管理员侧是否已经启用 Claude Fable 5 policy。
- [ ] 评估是否要把“更多模型选择”作为高阶套餐的核心卖点。
