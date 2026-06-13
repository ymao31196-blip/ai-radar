# OpenAI Lockdown Mode

**类型**：LLM 安全工具 / Prompt Injection 防御
**官网**：https://chatgpt.com
**GitHub**：N/A（ChatGPT 内置功能）

---

## 更新记录

### v1.0 — 2026-06-04

**来源**：[OpenAI Blog](https://openai.com/index/introducing-lockdown-mode-and-elevated-risk-labels-in-chatgpt/)；[OpenAI Help Center](https://help.openai.com/articles/20001061)
**可信度**：🟢 官方

#### 变化了什么
- 新功能：**Lockdown Mode** — 面向高安全需求用户的可选安全设置，可显著收紧 ChatGPT 对外部系统的连接面。
- 受影响能力：实时网页访问、网页图片支持、Deep Research（含购物研究）、Agent Mode、Canvas 网络访问、实时连接器和文件下载都会被限制或关闭。
- 适用对象：ChatGPT Enterprise，后续扩展到个人 ChatGPT 账户以及 self-serve ChatGPT Business 账户。
- 限制：**非银弹** — 它能减少 prompt injection 风险，但不能保证彻底杜绝数据外泄。

#### 有什么用
- **敏感数据处理场景**：金融、法律、医疗等需要严格控制数据泄露风险的场景，可以使用更保守的 ChatGPT 安全模式。
- **架构设计参考**：如果你的产品也面临 prompt injection 风险，Lockdown Mode 的思路可以复用为“限制联网面 + 限制文件/富媒体输入 + 限制自动代理动作”。
- **安全评估框架**：Lockdown Mode 的取舍（安全 vs 功能）提供了一个评估 AI 产品攻击面的框架

#### 迁移成本
- 无迁移成本；功能渐进式推出，用户自行决定是否开启

#### 行动项
- [ ] 在敏感数据处理场景中启用 Lockdown Mode
- [ ] 评估自有 AI 产品的 prompt injection 攻击面，参考 Lockdown Mode 的四点切断策略
- [ ] 注意：上传文件仍是注入向量，需额外防护
