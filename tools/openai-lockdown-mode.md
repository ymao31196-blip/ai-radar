# OpenAI Lockdown Mode

**类型**：LLM 安全工具 / Prompt Injection 防御
**官网**：https://chatgpt.com
**GitHub**：N/A（ChatGPT 内置功能）

---

## 更新记录

### v1.0 — 2026-06-06

**来源**：https://techcrunch.com/2026/06/06/openai-unveils-lockdown-mode-to-protect-sensitive-data-from-prompt-injection-attacks/
**可信度**：🟢 官方

#### 变化了什么
- 新功能：**Lockdown Mode** — 一键关闭 ChatGPT 的四个高风险能力以缩小 prompt injection 攻击面：
  - ❌ 实时网页浏览（仅保留缓存内容）
  - ❌ 网页图片检索/显示
  - ❌ Deep Research（深度研究）
  - ❌ Agent Mode（代理模式）
- 适用对象：处理敏感数据的组织和用户（ChatGPT Business + 符合条件的个人账户）
- 限制：**非银弹** — 缓存的网页内容和上传文件仍可能携带注入攻击

#### 有什么用
- **敏感数据处理场景**：金融、法律、医疗等需要严格控制数据泄露风险的场景，可以锁定 ChatGPT 的安全模式
- **架构设计参考**：如果你的产品也面临 prompt injection 风险，Lockdown Mode 的「四点切断」策略可复用：
  1. 切断实时外部内容获取
  2. 切断富媒体检索
  3. 切断自主研究能力
  4. 切断 Agent 自主行动
- **安全评估框架**：Lockdown Mode 的取舍（安全 vs 功能）提供了一个评估 AI 产品攻击面的框架

#### 迁移成本
- 无迁移成本；功能渐进式推出，用户自行决定是否开启

#### 行动项
- [ ] 在敏感数据处理场景中启用 Lockdown Mode
- [ ] 评估自有 AI 产品的 prompt injection 攻击面，参考 Lockdown Mode 的四点切断策略
- [ ] 注意：上传文件仍是注入向量，需额外防护
