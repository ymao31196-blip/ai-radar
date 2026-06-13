# GitHub Copilot CLI — `/security-review` 公开预览

**日期**：2026-06-10
**官网**：https://github.com/features/copilot
**来源**：[GitHub Changelog](https://github.blog/changelog/2026-06-10-dedicated-security-review-command-now-available-in-copilot-cli/)
**阶段**：🟡 公开预览

### 一句话定位
GitHub Copilot CLI 新增 `/security-review` 命令，可以在终端直接对当前变更做安全审查。

### 核心功能
- 直接在 Copilot CLI 中运行安全审查，帮助在提交前发现漏洞。
- 这是一条 Copilot 驱动的扫描链路，不依赖 GitHub code scanning、Dependabot 或 secret scanning。
- 适合作为轻量、按需的补充审查，而不是替代完整的仓库安全流程。

### 归档边界
- 这里仅记录 Copilot CLI 侧的产品功能，不重复 `agents/mcp-ecosystem.md` 里的第三方 coding agents 安全验证机制。
- 如果要追踪机制层面的安全治理，请继续放在 `agents/` 目录。

### 可复用的点
- 为终端原生 agent 提供按需安全审查入口。
- 用产品入口承载安全审查，可以降低用户切换到浏览器或独立工具的摩擦。

### 踩过的坑
- 不要把它当成 GitHub code scanning 的替代品。
- 不要和仓库级安全验证机制混写到同一条资讯里。
