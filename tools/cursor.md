# Cursor

**类型**：AI 编码 IDE / Agent 平台
**官网**：https://cursor.com
**GitHub**：不开源（SDK 部分开源）

---

## 更新记录

### v3.6 — 2026-05-29

**来源**：https://cursor.com/changelog
**可信度**：🟢 官方

#### 变化了什么
- 新功能：**Auto-review Run Mode** — Shell/MCP/Fetch 调用的智能审批分类器
  - 通过 `permissions.json` 配置白名单/黑名单规则
  - 自动判断操作是否需要人工审批
- Breaking Change：无

#### 有什么用
- **安全自动化**：Shell/Fetch 操作不再每次弹窗审批，白名单命令自动放行
- **MCP 工具管控**：对 MCP Server 的工具调用可以分级管理

#### 迁移成本
- 渐进式功能，无需迁移。如需启用 Auto-review，配置 `permissions.json` 即可

#### 行动项
- [ ] 配置 Auto-review 白名单：将常用安全命令加入白名单
- [ ] 评估 MCP 工具的分级管理策略

---

### v3.7 — 2026-06-04/05

**来源**：https://cursor.com/changelog
**可信度**：🟢 官方

#### 变化了什么
- 新功能：
  - **Design Mode 改进**：多选元素、语音输入
  - **Cursor SDK 大更新**：
    - `local.customTools`：自定义工具函数注册（无需手动搭建 MCP server）
    - JSONL 存储后端
    - **嵌套子 Agent**：Agent 可 spawn 子 Agent
    - auto-review SDK 支持
- 修复：HTTP/1.1 cloud streaming

#### 有什么用
- **自定义工具零门槛**：`local.customTools` 让开发者直接在 Cursor 中注册 Python 函数为 Agent 工具，比搭建 MCP Server 简单很多
- **嵌套 Agent**：复杂任务可自动分解为子 Agent 并行执行（类似 Claude Code Dynamic Workflows）
- **Design Mode + 语音**：非开发者也能用自然语言+语音设计 UI

#### 迁移成本
- 现有用户无迁移成本，功能渐进式上线

---

### 企业版 (Enterprise Organizations) — 2026-06-03

**来源**：https://cursor.com/changelog
**可信度**：🟢 官方

#### 变化了什么
- 新功能：Enterprise Organizations — 多团队管理、组织级 IDP（身份提供商）、用量分析
- Breaking Change：无

#### 有什么用
- 大团队采购时可以统一管理多个 Team、查看跨团队用量

#### 迁移成本
- 现有 Team 用户可升级至 Organization，无强制迁移

#### 行动项
- [ ] 试用 `local.customTools`：将内部脚本注册为 Cursor Agent 工具
- [ ] 评估 Auto-review 白名单是否能替代现有审批流程
- [ ] 关注嵌套子 Agent 在生产环境的表现
- [ ] 如果团队规模大，评估 Enterprise Organizations 的统一管理能力
