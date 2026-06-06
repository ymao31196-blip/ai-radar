# Cursor — AI 编码平台的三级跳

**日期**：2026-06-05
**官网**：https://cursor.com
**来源**：cursor.com/blog（近两周 12 篇官方博客）+ Bloomberg + TechCrunch
**阶段**：🟢 已盈利 / 快速爆发

### 一句话定位
从 AI 编码 IDE 进化为「自我驱动代码库」平台——能独立管理 PR、rollout、生产监控的 AI Agent 平台。

### 核心功能
- **Composer 2.5**：长周期 Agent 任务，自动跨文件编辑、测试、提交
- **Cloud Agents**（新）：代码修改在云端沙箱运行，不占用本地资源
- **Design Mode**（新）：视觉提示 + 语音输入驱动 UI 生成
- **Bugbot**：自动发现和修复 Bug
- **Cursor SDK**（新）：编程式控制 Agent，支持自定义工具和嵌套子 Agent
- **Auto-review**（新）：Shell/MCP/Fetch 调用智能审批，白名单自动放行

### 技术栈（已知/推测）
- 模型：自研模型 + 多模型接入（Claude Opus 4.8 在 CursorBench 上表现最佳）
- 框架：Composer Agent 框架 + 云端沙箱
- 基础设施：Cloud Agents 运行时

### 商业模式
- 定价：个人免费 + Pro ($20/月) + Teams（2026-06-01 调整定价）
- 客户群：从个人开发者扩展到企业（PayPal、Faire、NAB、Amplitude）
- ARR：**$20 亿**（Bloomberg 报道，三个月内翻倍）

### 增长策略
- **客户案例驱动**：官网 4 个客户故事均有量化数据——
  - Faire：Cloud Agents 使 PR 交付量翻倍
  - PayPal：扩展了「什么是可能构建的」边界
  - NAB（澳洲国民银行）：遗留系统迁移加速
  - Amplitude：生产代码交付提升 3x
- **三级跳产品策略**：补全 → Composer（Agent）→ Cloud Agent（自动化工作流），每级扩展可解决任务范围 + 提升客单价
- **从工具到平台**：SDK + Organizations 将 Cursor 从个人工具变为团队基础设施

### 可复用的点
- **三级跳模式**：AI 产品从「辅助」→「协作」→「自主」的演进路径，每个阶段对应不同的功能边界和定价策略
- **客户案例 = 信任引擎**：量化数据（3x、翻倍）比功能列表有说服力得多
- **SDK 生态**：通过 SDK 让第三方自定义工具和扩展，建立平台粘性

### 踩过的坑
- 暂无公开的严重踩坑记录。需要注意：ARR $20 亿的快速增长可能面临企业合规和安全的压力测试

### 行动项
- [ ] 借鉴「三级跳」产品策略：我们的 AI 产品是否可以从辅助→协作→自主分阶段规划？
- [ ] 研究 Cursor SDK 的 nested sub-agent 实现方式
