# OpenAI Codex

**类型**：AI 编码 CLI / Agent 平台
**官网**：https://github.com/openai/codex
**GitHub**：https://github.com/openai/codex

---

## 更新记录

### 0.139.0 — 2026-06-09

**来源**：[OpenAI Codex changelog](https://developers.openai.com/codex/changelog)
**可信度**：🟢 官方

#### 变化了什么
- **代码模式增强**：Codex 的 code mode 可以直接发起独立网页搜索，并把结果以纯文本带回后续工具调用。
- **MCP / connector 兼容性更好**：工具与连接器输入 schema 在压缩时保留更多结构，对 `oneOf`、`allOf` 这类更复杂定义更友好。
- **诊断信息更完整**：`codex doctor` 会输出编辑器与 pager 环境信息，同时在 JSON 输出里继续做脱敏。
- **插件市场更顺滑**：插件列表会暴露来源，并优先用缓存目录再后台刷新。
- **稳定性修复**：`resume` / `fork` 的尾随参数解析、MCP 启动警告归属、图片编辑路径、代理网络约束等问题都得到修补。
- Breaking Change：无

#### 有什么用
- 适合把网页检索直接纳入 Codex 工作流，减少在浏览器和 CLI 之间来回切换。
- 复杂 MCP 工具链更容易接入，不必为了 schema 兼容性频繁降级定义。
- 排障时 `codex doctor` 给出的环境信息更完整，定位本地问题更快。

#### 迁移成本
- 稳定版 0.139.0 没有明显迁移门槛。
- 如果你依赖自定义 MCP / connector schema，建议先在非生产环境验证压缩后的行为。

#### 行动项
- [ ] 如果已经在用 Codex CLI，优先评估是否升级到 `0.139.0`。
- [ ] 检查内部 MCP 工具定义是否依赖 `oneOf` / `allOf` 的复杂结构。
- [ ] 复核本地 `codex doctor` 输出，确认排障信息能满足团队需要。

---

### 0.140.0-alpha.8 — 2026-06-11（预览）

**来源**：https://github.com/openai/codex/releases
**可信度**：🟡 官方预览

#### 变化了什么
- GitHub releases 在 6 月 11 日出现了新的 alpha.8 预览构建。
- 当前发布页没有给出独立的稳定版功能摘要，暂时只能把它当作继续演进的预览分支。

#### 有什么用
- 适合想提前验证下一轮 Codex 行为变化的团队做隔离测试。

#### 迁移成本
- 预览版行为可能继续变化，正式生产环境不建议直接跟随。

#### 行动项
- [ ] 如果要试 alpha，单独 pin 版本并准备回退方案。
- [ ] 不要把 pre-release 作为默认升级路径。
