# Microsoft ASSERT

**类型**：AI 行为测试框架 / Prompt 回归测试
**官网**：https://github.com/microsoft/assert（推测）
**GitHub**：开源（Microsoft Responsible AI 团队）

---

## 更新记录

### v1.0 — 2026-06-02

**来源**：https://techcrunch.com/2026/06/02/new-microsoft-tool-lets-devs-spin-up-ai-behavior-tests-using-text-descriptions/
**可信度**：🟢 官方

#### 变化了什么
- 新功能：**ASSERT**（Adaptive Spec-driven Scoring for Evaluation and Regression Testing）— 将自然语言描述的 AI 行为规范自动转化为结构化测试套件
  - 输入：自然语言行为描述（如「不要向公司外部发送邮件」）
  - 自动生成：可接受/不可接受的行为定义 + 对抗性测试场景
  - 执行测试 → 评分 → 记录中间步骤和工具调用
  - 支持持续部署后的行为监控
- Breaking Change：无（新工具）

#### 有什么用
- **System Prompt 迭代的回归测试**：每次修改 system prompt 后，运行 ASSERT 检查是否有行为退化
- **Agent 安全性验证**：用自然语言定义安全边界，自动生成攻击性测试用例
- **填补了通用 benchmark 和业务场景之间的空白**：HELM/METR 测的是通用能力，ASSERT 测的是你的具体业务行为规范
- **开源可自建**：不需要 SaaS 订阅

#### 迁移成本
- 新工具，零迁移成本。只需编写自然语言行为规范即可开始

#### 行动项
- [ ] 试用 ASSERT：为核心 Agent 场景编写行为规范并运行回归测试
- [ ] 将 ASSERT 集成到 CI/CD 流程中：每次 system prompt 变更自动触发行为测试
- [ ] 参考 ASSERT 的行为规范编写模式，为现有 Agent 建立行为边界文档
