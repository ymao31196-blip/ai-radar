# 社区精选 Skill & MCP Server

> 从 [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers)（88.6k stars）中精选的高质量社区 MCP Server 和 Skill，按开发者日常高频场景分类。

**日期**：2026-05-22 ~ 06-11
**来源**：GitHub modelcontextprotocol 组织 + 各 SDK 仓库 + 社区项目
**可信度**：🟡 混合来源（官方 + 社区）

---

## 🤖 编码智能体 & 开发工具

## [MCP Server] Puppeteer

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
浏览器自动化——让 AI 控制 Chrome 浏览器进行网页操作、截图、表单填写和 E2E 测试。

#### 安装方式
```bash
npx -y @modelcontextprotocol/server-puppeteer

# Claude Desktop 配置
{
  "mcpServers": {
    "puppeteer": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
    }
  }
}
```

#### 核心能力
- 浏览器导航和页面交互
- 页面截图和 PDF 导出
- 表单自动填写
- 控制台日志捕获
- 网络请求监控

#### 有什么用
> Web 开发调试时让 AI 帮你打开页面检查渲染效果、抓取控制台错误、自动填写表单测试流程。

#### 使用示例
```markdown
「打开 localhost:3000，截图首页，检查控制台有没有报错」
```

#### 限制 & 注意
- 需要 Chrome/Chromium 浏览器
- 执行速度较慢
- 不适合高频调用

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Puppeteer MCP | 完整浏览器控制、截图 | 重量级、需浏览器 |
| Playwright MCP | 跨浏览器、更现代 | 类似重量 |
| Fetch MCP | 轻量 | 无 JS 渲染 |

---

## [MCP Server] Playwright

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/microsoft/playwright-mcp)
**可信度**：🟢 官方（Microsoft）
**平台**：Claude / 通用

#### 一句话描述
Microsoft 官方的 Playwright MCP Server——跨浏览器自动化，支持 Chromium / Firefox / WebKit。

#### 安装方式
```bash
npx -y @playwright/mcp

# Claude Desktop 配置
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp"]
    }
  }
}
```

#### 核心能力
- 跨浏览器测试（Chromium / Firefox / WebKit）
- 页面截图和视频录制
- 元素定位和交互
- 网络拦截和 Mock
- Trace 查看器

#### 有什么用
> E2E 测试的首选——比 Puppeteer 更现代、浏览器覆盖面更广，且由 Microsoft 官方维护。

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Playwright MCP | 官方、跨浏览器 | 安装较大 |
| Puppeteer MCP | 社区成熟 | 仅 Chromium |

---

## [MCP Server] Brave Search

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
Brave Search API 集成——让 AI 进行网页搜索和本地搜索。

#### 安装方式
```bash
npx -y @modelcontextprotocol/server-brave-search

# Claude Desktop 配置
{
  "mcpServers": {
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": {
        "BRAVE_API_KEY": "<YOUR_KEY>"
      }
    }
  }
}
```

#### 核心能力
- 网页搜索（10 条/次）
- 本地商户搜索
- 免费额度（2000 次/月）

#### 有什么用
> 让 Claude 获得实时互联网搜索能力——查最新文档、验证事实、获取当前事件信息。补足 AI 知识截止日期后的空白。

#### 使用示例
```markdown
「搜索 Go 1.23 的新特性并和我们的代码库对比兼容性」
```

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Brave Search | 免费额度、隐私友好 | 需 API Key |
| Google Search MCP | 结果更全 | 付费、隐私问题 |
| Perplexity MCP | AI 搜索 | 付费 |

---

## 🗄️ 数据库

## [MCP Server] PostgreSQL

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
PostgreSQL 数据库直连——让 AI 读取 Schema、执行查询、分析数据。

#### 安装方式
```bash
npx -y @modelcontextprotocol/server-postgres

# Claude Desktop 配置
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://user:pass@localhost/mydb"]
    }
  }
}
```

#### 核心能力
- 读取表结构和 Schema
- 执行只读查询
- 查询计划分析
- 多 Schema 支持

#### 有什么用
> 开发时直接在对话中查数据库——"这个表有哪些索引？"、"找出最近 7 天没有订单的用户"，不用切到数据库客户端。

#### 使用示例
```markdown
「分析 users 表的索引使用情况，找出缺失的索引」
```

#### 限制 & 注意
- 默认只读（安全考虑）
- 需要数据库网络可达
- 建议使用只读副本账号

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| PostgreSQL MCP | 官方社区维护 | 仅 PostgreSQL |
| SQLite MCP | 零配置 | 单机 |
| MySQL MCP | MySQL 支持 | 社区较小 |

---

## [MCP Server] SQLite

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
SQLite 数据库直连——零配置、单文件，快速数据分析。

#### 安装方式
```bash
uvx mcp-server-sqlite --db-path /path/to/database.db
```

#### 核心能力
- SQLite 文件读取
- 表和索引查询
- 数据分析
- 完全本地、零配置

#### 有什么用
> 分析本地 SQLite 数据库文件——调试应用本地存储、分析日志数据库、快速数据探索。

#### 使用示例
```markdown
「分析这个 SQLite 数据库的 users 表结构，找出缺少索引的查询」
```

#### 限制 & 注意
- 仅本地访问（无网络能力）
- 默认只读（安全考虑）
- 大数据库查询可能超时

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| SQLite MCP | 零配置、完全本地 | 仅 SQLite |
| PostgreSQL MCP | 生产级数据库 | 需配置连接 |

---

## 📂 知识管理 & 笔记

## [MCP Server] Obsidian

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/smithery-ai/mcp-obsidian)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
Obsidian 笔记库集成——让 AI 读取、搜索、编辑你的 Obsidian Vault。

#### 安装方式
```bash
npx -y @smithery/cli install @smithery-ai/obsidian --client claude
```

#### 核心能力
- 读取和搜索笔记
- 创建/编辑 Markdown 文件
- 标签和双向链接分析
- 知识图谱浏览

#### 有什么用
> 把 Obsidian 作为 AI 的知识库——让 Claude 理解你的笔记结构、补充内容、发现知识关联。个人知识管理的强大组合。

#### 使用示例
```markdown
「在我的 Vault 中找到所有关于『分布式系统』的笔记，总结核心观点并建议需要补充的部分」
```

#### 限制 & 注意
- 需要 Obsidian 本地 Vault
- 大 Vault 可能超 token
- 写入操作需确认

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Obsidian MCP | 双向链接、知识图谱 | 仅 Obsidian |
| Notion MCP | 协作、云端 | 需 API Key |

---

## [MCP Server] Notion

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/suekou/mcp-notion-server)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
Notion API 集成——让 AI 读写 Notion 页面、数据库和内容块。

#### 安装方式
```bash
npx -y @suekou/mcp-notion-server

# 环境变量
NOTION_API_KEY=secret_xxx
```

#### 核心能力
- 读取/创建/更新页面
- 数据库操作
- 搜索内容
- 块级编辑

#### 有什么用
> 团队知识库在 Notion 时，让 AI 自动整理、补全、检索文档——自动生成周报摘要、更新项目进度。

#### 使用示例
```markdown
「在我的 Notion 项目数据库中，列出所有 overdue 的任务并更新状态到本周 Sprint」
```

#### 限制 & 注意
- 需要 Notion API Key 和 Integration 授权
- 只能访问 Integration 有权限的页面
- 写入操作需谨慎

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Notion MCP | 云端协作、数据库 | 需 API Key |
| Obsidian MCP | 本地、隐私 | 单机 |

---

## 🔎 网页抓取 & 搜索

## [MCP Server] webclaw

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/0xMassi/webclaw)
**可信度**：🟡 社区热门
**平台**：Claude / Cursor / Windsurf / Codex

#### 一句话描述
新一代 Web 内容提取——TLS 指纹绕过反爬，比 raw HTML 减少 67% token 消耗。

#### 安装方式
```bash
npx create-webclaw  # 自动配置 Claude / Cursor / Windsurf / Codex
```

#### 核心能力
- 网页抓取、爬取、网站地图
- 批量提取和摘要
- 差异对比
- 品牌检测
- 反爬绕过

#### 有什么用
> 批量研究场景的最佳抓取工具——竞争对手分析、文档站点批量提取、SEO 研究。比 Fetch MCP 更适合生产级抓取。

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| webclaw | 反爬、降噪、token 省 | 较新、社区小 |
| Fetch MCP | 官方稳定 | 无反爬 |
| Firecrawl MCP | 更全功能 | 付费 |

---

## 🛠️ 项目管理 & 协作

## [MCP Server] Linear

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/tacticlaunch/mcp-linear)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
Linear 项目管理集成——创建/查看 Issue、管理 Sprint、搜索团队任务。

#### 安装方式
```bash
npx -y @tacticlaunch/mcp-linear
# 需要 LINEAR_API_KEY
```

#### 核心能力
- Issue CRUD
- Sprint 和周期管理
- 项目/团队搜索
- 评论和附件

#### 有什么用
> 开发者最爱的项目管理工具 + AI —— "把我这周的 Linear tasks 整理成汇报"、"根据最近的 Issue 创建 Sprint 计划"。

#### 使用示例
```markdown
「查看我当前 Sprint 的进度，找出 blocked 的任务并建议解决方案」
```

#### 限制 & 注意
- 需要 Linear API Key
- 写入操作需确认
- 仅 Linear 平台

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Linear MCP | 开发者体验最佳 | 仅 Linear |
| Jira MCP | 企业广泛使用 | 体验不如 Linear |

---

## 🐳 容器 & 基础设施

## [MCP Server] Docker

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/QuantGeekDev/docker-mcp)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
Docker 容器管理——让 AI 管理镜像、容器、卷和 Compose。

#### 安装方式
```bash
npx -y @quantgeekdev/docker-mcp
```

#### 核心能力
- 容器列表/启动/停止
- 镜像管理
- Docker Compose 操作
- 日志查看
- 资源监控

#### 有什么用
> DevOps 场景中让 AI 帮忙排查容器问题——"为什么这个容器一直重启？看看日志"、"清理所有 dangling images"。

#### 使用示例
```markdown
「查看所有运行中的容器状态，找出内存超过 1GB 的并查看日志」
```

#### 限制 & 注意
- 需要 Docker daemon 运行
- 操作权限等同于当前用户
- 生产环境需额外注意安全

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Docker MCP | 容器全生命周期管理 | 仅 Docker |
| K8s MCP | 编排级别 | 更复杂 |

---

## 🧠 AI & LLM 集成

## [MCP Server] Ollama Bridge

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/jaspertvdm/mcp-server-ollama-bridge)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
让 Claude 通过 MCP 调用本地 Ollama 模型——运行 Llama / Mistral / Qwen 等开源模型。

#### 安装方式
```bash
pip install mcp-server-ollama-bridge
```

#### 核心能力
- 调用本地 LLM（Ollama）
- 多模型切换
- 本地推理、隐私保护
- 免费、无速率限制

#### 有什么用
> 敏感数据处理场景——用本地模型处理隐私数据，用 Claude 负责最终整合。或者让 Claude 对比不同模型对同一问题的回答。

#### 使用示例
```markdown
「用 Ollama 的 Llama 3 模型先预处理这批用户反馈，然后我用 Claude 做最终分析」
```

#### 限制 & 注意
- 需要本地 Ollama 服务运行
- 模型性能取决于硬件
- 仅桥接，不替代 Claude

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Ollama Bridge | 本地、免费、隐私 | 自备硬件 |
| OpenAI Bridge | 云端强大模型 | 付费 |

---

## [MCP Server] Perplexity

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/tanigami/mcp-server-perplexity)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
Perplexity AI 搜索集成——带引用来源的深度搜索。

#### 安装方式
```bash
pip install mcp-server-perplexity
# 需要 PERPLEXITY_API_KEY
```

#### 核心能力
- 深度搜索带引用
- 实时信息获取
- 学术搜索
- 多源验证

#### 有什么用
> 需要准确、可引用来源的搜索场景——技术调研、竞品分析、论文查找。比普通搜索更适合严肃研究。

#### 使用示例
```markdown
「调研 Rust 在嵌入式领域的采用情况，找到最近半年的案例并附引用来源」
```

#### 限制 & 注意
- 需要 Perplexity API Key（付费）
- API 速率限制
- 仅搜索，不能操作

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Perplexity MCP | 深度、带引用 | 付费 |
| Brave Search MCP | 免费额度 | 引用不如 Perplexity |

---

## 🔧 实用工具

## [MCP Server] mcp-time

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/TheoBrigitte/mcp-time)
**可信度**：🟠 个人作品
**平台**：Claude / 通用

#### 一句话描述
增强版时间工具——自然语言解析、多格式输出、时区转换。

#### 安装方式
```bash
go install github.com/TheoBrigitte/mcp-time@latest
```

#### 核心能力
- 自然语言时间解析（"next Friday 3pm"）
- 多种格式化输出
- 跨时区转换
- 纯 Go 实现、单二进制

#### 有什么用
> 比官方 Time MCP 更灵活——自然语言输入"下周三下午三点东京时间是几点"直接得到答案。

#### 使用示例
```markdown
「下周五下午 2 点（太平洋时间）对应北京时间几点？用 RFC 3339 格式返回」
```

#### 限制 & 注意
- 非官方维护
- 仅时间功能（无日历）
- Go 单二进制，需编译或下载

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| mcp-time | 自然语言、Go 原生 | 个人作品 |
| Time MCP (官方) | 官方稳定 | 功能基础 |

---

## [MCP Server] DeepSeek Bridge

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[GitHub](https://github.com/arikusi/deepseek-mcp-server)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
DeepSeek AI 集成——让 Claude 调用 DeepSeek 的 Chat/Reasoning/Function Calling 能力。

#### 安装方式
```bash
npx -y deepseek-mcp-server
# 需要 DEEPSEEK_API_KEY
```

#### 核心能力
- DeepSeek Chat 和 Reasoning 模型
- 多轮对话
- Function Calling
- Thinking 模式
- 成本追踪

#### 有什么用
> 组合两个顶尖模型——Claude 做代码生成和复杂推理，DeepSeek 做高性价比的批量任务，成本大幅降低。

#### 使用示例
```markdown
「用 DeepSeek 批量翻译这些 100 条用户评论，然后我用 Claude 做情感分析总结」
```

#### 限制 & 注意
- 需要 DeepSeek API Key
- 不同模型有各自限制
- 桥接调用会增加延迟

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| DeepSeek Bridge | 高性价比、中文友好 | 需 API Key |
| OpenAI Bridge | GPT 生态最强 | 更贵 |

---

## 📦 Skill 市场 & 发现平台

> 以下条目使用简化的模板字段，因为这些是平台/框架而非单个 MCP Server。

---

### [平台] APIFold

**日期**：2025-07-01
**类型**：MCP 聚合平台（在线服务）
**来源**：[GitHub](https://github.com/Work90210/APIFold)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
将任何 REST API 变成 MCP Server。已有 18 个免费公共服务（GitHub、Stripe、Slack、OpenAI、Notion 等），无需部署、用自己的 API Key 即可使用。

#### 安装方式
在线服务，直接配置 URL 到 Claude Desktop：
```json
{
  "mcpServers": {
    "apifold-github": {
      "command": "npx",
      "args": ["-y", "@apifold/mcp-github"]
    }
  }
}
```

#### 核心能力
- 18+ 预建 MCP Server（GitHub/Stripe/Slack/OpenAI/Notion/Airtable...）
- 用自己的 API Key，数据不经过第三方
- 零部署，即配即用

#### 有什么用
> 不想自己搭建 MCP Server 时的快捷方式——一个配置就能让 Claude 接入 GitHub/Stripe 等服务。

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| APIFold | 零部署、即配即用 | 依赖第三方服务 |
| 自建 MCP Server | 完全控制 | 需开发/维护 |
| Smithery | 托管分发 | 更商业化 |

---

### [平台] MCPJungle

**日期**：2025-07-01
**类型**：私有 MCP 注册中心
**来源**：[GitHub](https://github.com/duaraghav8/MCPJungle)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
企业自托管的 MCP Server 注册中心——适合公司内部统一管理和分发 AI 工具。

#### 安装方式
```bash
# 自托管部署
git clone https://github.com/duaraghav8/MCPJungle
# 参考项目 README 完成部署
```

#### 核心能力
- 企业内部 MCP Server 注册和发现
- 访问控制和权限管理
- 版本管理

#### 有什么用
> 公司有 10+ 个内部 MCP Server 时，需要一个统一入口来管理分发和权限。

---

### [框架] FastMCP

**日期**：2025-07-01
**类型**：MCP 开发框架
**来源**：[GitHub (Python)](https://github.com/jlowin/fastmcp) · [GitHub (TypeScript)](https://github.com/punkpeye/fastmcp)
**可信度**：🟡 社区热门
**平台**：Claude / 通用

#### 一句话描述
构建 MCP Server 的高层框架——装饰器定义工具，零样板代码。Python 和 TypeScript 双版本。

#### 安装方式
```bash
# Python 版
pip install fastmcp

# TypeScript 版
npm install fastmcp
```

#### 核心能力
- 装饰器/注解式工具定义
- 自动资源管理
- 多传输协议支持
- 内置测试工具

#### 有什么用
> 想快速搭建一个 MCP Server 时，FastMCP 比直接使用 SDK 少写 80% 样板代码。5 分钟可以从零到一个可用的 Server。

#### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| FastMCP | 开发快、样板少 | 高层抽象可能受限 |
| MCP SDK 直接使用 | 完全控制 | 样板多 |
| Gomcp (Go) | Go 生态 | 语言限制 |

---

## 社区评价（综合）

- **MCP 生态 2025 年爆发增长**：awesome-mcp-servers 从 0 到 88.6k stars，收录 800+ 服务器
- **质量分化明显**：官方维护的 MCP Server 质量稳定，社区作品良莠不齐——认准 🎖️ 官方标记和活跃维护的仓库
- **最大痛点**：MCP Server 的发现和安装仍显碎片化——每个都需要单独配置 JSON，期待统一管理工具
- **趋势**：MCP 聚合器（APIFold、MCPJungle）和 Skill 市场（AISkillStore）正在兴起，类似 npm/PyPI 的 MCP 注册中心会成为基础设施
- **安全提醒**：社区 MCP Server 拥有文件、数据库、浏览器权限——只安装可信来源，审查代码后再用

### 行动项
- [ ] 是否安装 Brave Search MCP 获得实时搜索能力？
- [ ] 是否试用 Playwright MCP 做 E2E 测试？
- [ ] 评估是否需要 PostgreSQL/SQLite MCP 连接数据库
- [ ] 试用 Obsidian/Notion MCP 连接知识库
- [ ] 试用 FastMCP 快速搭建内部工具 MCP Server

---

## [MCP Server] Lovie — Company Formation MCP

**日期**：2026-06-10
**类型**：MCP Server
**来源**：[GitHub issue #4296](https://github.com/modelcontextprotocol/servers/issues/4296) ｜ [仓库](https://github.com/lovieco/lovie-company-formation-mcp-npx)
**可信度**：🟡 社区项目 / 官方仓库 issue
**平台**：Claude / 通用

### 一句话描述
把公司设立、银行开户、卡、发票和支付这类流程封装成一个可通过 MCP 调用的商业操作服务。

### 安装方式
```bash
npx -y lovie

{"mcpServers":{"lovie":{"command":"npx","args":["-y","lovie"]}}}
```

### 核心能力
- 公司设立（entity type、state、name availability、shareholders、certificate、filing fee）
- 银行账户开户
- 虚拟/实体卡发行
- 发票和支付
- 交易分类

### 有什么用
> 适合把重复的公司注册 / 基础财务运营流程交给 agent 做编排，再由人类在关键步骤做最终确认。

### 限制 & 注意
- 依赖 hosted HTTPS endpoint + OAuth，首次使用会要求认证
- 涉及公司注册和金融操作，必须按 jurisdiction / compliance 做人工审核
- npx 代理只是桥接层，不等于可以绕开合规流程

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Lovie MCP | 端到端公司设立/财务操作 | 高合规敏感度，依赖 OAuth |
| 手工表单流程 | 可控 | 低自动化、耗时高 |
| 通用 Agent + 网页操作 | 灵活 | 流程稳定性和审计性较弱 |
