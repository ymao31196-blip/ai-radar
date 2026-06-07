# Claude 生态 MCP Server & Skill

> Anthropic 官方维护和推荐的 MCP Server 及 Claude 内置 Skill。涵盖参考实现、官方集成和 Claude Skill 体系。

---

## [MCP Server] Memory

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[官方](https://modelcontextprotocol.io/examples) · [GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟢 官方
**平台**：Claude / 通用

### 一句话描述
基于知识图谱的持久记忆系统，让 AI 跨会话记住用户偏好和关键信息。

### 安装方式
```bash
# TypeScript 版
npx -y @modelcontextprotocol/server-memory

# Claude Desktop 配置
{
  "mcpServers": {
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"]
    }
  }
}
```

### 核心能力
- 知识图谱存储（实体 + 关系）
- 跨会话持久记忆
- 自动识别和关联实体
- 支持自然语言查询记忆

### 有什么用
> 让 Claude 记住你的项目偏好、命名约定、个人习惯，不用每次对话都重复交代上下文。类似 Reasonix 的 `remember` 功能但更通用。

### 使用示例
```markdown
# 存入记忆
「记住：我偏好使用 Go 1.22 的 net/http 新路由语法」

# 查询记忆
「我们之前讨论过的认证方案是什么？」
```

### 限制 & 注意
- 数据存储在本地文件系统
- 不支持多用户隔离
- 知识图谱规模受限于本地存储

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Memory MCP | 知识图谱结构、跨会话 | 仅本地存储 |
| Reasonix remember | 项目级记忆、工具集成 | Reasonix 专属 |
| Mem0 | 云端、用户画像 | 需要 API、隐私顾虑 |

### 社区评价
- 官方推荐的基础 MCP Server 之一
- 适合个人使用，团队场景需额外方案

---

## [MCP Server] Filesystem

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[官方](https://modelcontextprotocol.io/examples) · [GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟢 官方
**平台**：Claude / 通用

### 一句话描述
安全文件操作，带可配置的目录访问控制——拒绝访问限定目录外的任何路径。

### 安装方式
```bash
npx -y @modelcontextprotocol/server-filesystem /path/to/allowed/files

# Claude Desktop 配置
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/me/projects"],
      "env": {
        "ALLOWED_DIRECTORIES": "/Users/me/projects,/Users/me/docs"
      }
    }
  }
}
```

### 核心能力
- 读取/写入/创建/删除文件
- 目录白名单访问控制
- 文件搜索（支持 glob）
- 文件元数据查询

### 有什么用
> 当 Claude Desktop 需要操作本地文件时使用——编辑器式文件操作，比内建的文件工具更系统化。

### 使用示例
```markdown
# 读取所有 Go 文件并检查编译错误
「读取 /project/internal/ 下所有 .go 文件，检查是否有未使用的 import」
```

### 限制 & 注意
- 必须显式配置允许的目录（安全第一）
- 不支持网络路径
- 大文件可能超出 token 限制

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Filesystem MCP | 安全白名单、跨平台 | 需配置、仅本地 |
| Reasonix read_file | 零配置、智能分页 | 受限工具集 |
| Claude Code | 深度集成 | Claude Code 专属 |

---

## [MCP Server] Git

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[官方](https://modelcontextprotocol.io/examples) · [GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟢 官方
**平台**：Claude / 通用

### 一句话描述
Git 仓库操作工具：读取、搜索和操作 Git 仓库，支持 log、diff、blame、branch 等。

### 安装方式
```bash
# Python 版（推荐 uvx）
uvx mcp-server-git

# 或 pip
pip install mcp-server-git
python -m mcp_server_git

# Claude Desktop 配置
{
  "mcpServers": {
    "git": {
      "command": "uvx",
      "args": ["mcp-server-git", "--repository", "/path/to/repo"]
    }
  }
}
```

### 核心能力
- git log / diff / show
- git blame 追溯
- git branch / tag 管理
- git status 检查
- 多仓库支持

### 有什么用
> 让 Claude 直接分析 Git 历史——理解代码演进的上下文、追溯谁在何时为什么改了某行、分析提交模式。

### 使用示例
```markdown
# 分析最近一周的变更模式
「查看最近一周的 git log，总结主要变更方向」
```

### 限制 & 注意
- 不支持 push / force push（安全限制）
- 需要本地仓库
- 大型仓库的 log 可能超 token

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Git MCP | 语义化 Git 操作 | 无 push/force push |
| GitHub MCP | 远程仓库、PR/Issue | 需要 Token |
| Reasonix (bash git) | 全功能 | 无结构化输出 |

---

## [MCP Server] Fetch

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[官方](https://modelcontextprotocol.io/examples) · [GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟢 官方
**平台**：Claude / 通用

### 一句话描述
Web 内容抓取并将 HTML 转为适合 LLM 消费的纯文本（Markdown）。

### 安装方式
```bash
uvx mcp-server-fetch

# Claude Desktop 配置
{
  "mcpServers": {
    "fetch": {
      "command": "uvx",
      "args": ["mcp-server-fetch"]
    }
  }
}
```

### 核心能力
- URL 内容抓取
- HTML → Markdown 智能转换
- 去除广告、脚本等噪音
- 支持递归抓取深度控制

### 有什么用
> 替代 web_fetch 工具用于 Claude Desktop——把任意网页变成 Claude 可理解的上下文，比原生 web_fetch 更擅长处理现代前端渲染的页面。

### 使用示例
```markdown
「抓取 https://go.dev/doc/effective_go 并总结并发模式部分」
```

### 限制 & 注意
- 不支持 JS 渲染后的 SPA 页面
- 大页面可能截断
- 需遵守 robots.txt 和网站 ToS

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Fetch MCP | HTML→MD 转换优秀 | 无 JS 渲染 |
| Reasonix web_fetch | 内置、即时 | 转换效果一般 |
| Puppeteer MCP | JS 渲染 | 更重、更慢 |

---

## [MCP Server] Sequential Thinking

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[官方](https://modelcontextprotocol.io/examples) · [GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟢 官方
**平台**：Claude / 通用

### 一句话描述
动态和反思式问题解决——通过思维序列实现逐步推理、修正和分支。

### 安装方式
```bash
npx -y @modelcontextprotocol/server-sequential-thinking

# Claude Desktop 配置
{
  "mcpServers": {
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"]
    }
  }
}
```

### 核心能力
- 逐步推理链
- 思维修正和回退
- 假设分支探索
- 推理过程可视化

### 有什么用
> 复杂问题的结构化推理引擎——数学证明、逻辑推理、系统设计权衡等需要严密思维的场景。

### 使用示例
```markdown
「分析这个分布式系统的一致性方案，用 Sequential Thinking 逐步推理」
```

### 限制 & 注意
- 推理步骤有上下文消耗
- 不适用于快速问答
- 需要 Claude 主动调用

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Sequential Thinking | 结构化、可修正 | 额外开销 |
| Claude Extended Thinking | 原生、透明 | 仅 Claude API |
| o1-style CoT | 隐式 | 不可控 |

---

## [MCP Server] Time

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[官方](https://modelcontextprotocol.io/examples) · [GitHub](https://github.com/modelcontextprotocol/servers)
**可信度**：🟢 官方
**平台**：Claude / 通用

### 一句话描述
时间和时区转换工具——获取当前时间、转换时区、格式化日期。

### 安装方式
```bash
uvx mcp-server-time

# Claude Desktop 配置
{
  "mcpServers": {
    "time": {
      "command": "uvx",
      "args": ["mcp-server-time", "--local-timezone=America/Chicago"]
    }
  }
}
```

### 核心能力
- 获取当前时间（指定时区）
- 时区转换
- 日期格式化
- 相对时间计算

### 有什么用
> Claude 本身不知道现在几点、用户在哪。Time MCP 让它能说"现在是北京时间下午3点"而非模糊的"根据我的知识截止日期..."。

### 使用示例
```markdown
「把下周三 UTC 14:00 转成北京时间，看是不是工作时间」
```

### 限制 & 注意
- 依赖系统时钟
- 不支持日历事件（需额外工具）

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| Time MCP | 官方、轻量 | 功能单一 |
| mcp-time (社区) | 自然语言、多格式 | 非官方 |

---

## [MCP Server] GitHub

**日期**：2025-07-01
**类型**：MCP Server
**来源**：[官方集成](https://github.com/modelcontextprotocol/servers)
**可信度**：🟢 官方
**平台**：Claude / 通用

### 一句话描述
GitHub API 官方集成——管理仓库、Issue、PR、Actions 等。

### 安装方式
```bash
npx -y @modelcontextprotocol/server-github

# Claude Desktop 配置
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

### 核心能力
- 创建/管理 Issue 和 PR
- 搜索仓库和代码
- 读取/写入文件
- Actions 工作流管理
- Code Review 操作

### 有什么用
> 在 Claude 对话中完成全套 GitHub 操作——从读 Issue 到提 PR，不用跳到浏览器。类似 Reasonix 的代码操作但针对 GitHub 远程仓库。

### 使用示例
```markdown
「找到标有 bug 的开放 issue，分析每个并创建修复 PR」
```

### 限制 & 注意
- 需要 GitHub Personal Access Token
- Token 权限范围决定可用操作
- 写入操作有速率限制

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| GitHub MCP | 官方、全功能 | 需 Token、仅 GitHub |
| Git MCP | 无需网络 | 仅本地操作 |
| GitLab MCP (社区) | GitLab 支持 | 非官方 |

---

## [Skill] xlsx — Excel 文档生成

**日期**：2025-07-01
**类型**：Skill（Claude 内置）
**来源**：[Anthropic 官方](https://www.anthropic.com/news/create-files)
**可信度**：🟢 官方
**平台**：Claude (API / Desktop / Web)

### 一句话描述
创建和操作 Excel 工作簿，支持公式、图表、格式化和数据透视表。

### 安装方式
Claude 内置，无需安装。通过 API 调用需启用 beta header：
```python
client = Anthropic(
    default_headers={
        "anthropic-beta": "skills-2025-10-02,code-execution-2025-08-25,files-api-2025-04-14"
    }
)
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    container={"skills": [{"type": "anthropic", "skill_id": "xlsx", "version": "latest"}]},
    tools=[{"type": "code_execution_20250825", "name": "code_execution"}],
    messages=[{"role": "user", "content": "创建一个带图表的预算报表"}]
)
```

### 核心能力
- 创建/编辑 Excel 工作簿
- 公式和函数计算
- 图表生成（柱状图、折线图、饼图等）
- 数据透视表
- 条件格式和样式

### 有什么用
> 一句话生成专业 Excel 报表——财务分析、数据汇总、预算跟踪。不再需要手动拖拽公式和调图表。

### 使用示例
```markdown
# Claude Web / Desktop 中直接对话
「把这个 CSV 数据导入 Excel，创建按地区的销售汇总表，用柱状图对比各季度业绩」
```

### 限制 & 注意
- 仅 Claude 平台可用
- 生成的文件通过 Files API 下载
- 复杂格式可能有偏差

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| xlsx Skill | 自然语言生成、图表内置 | 仅 Claude 平台 |
| Python openpyxl | 完全控制 | 需要编程 |
| Google Sheets MCP | 在线协作 | 需 Google 账号 |

---

## [Skill] pptx — PowerPoint 演示文稿生成

**日期**：2025-07-01
**类型**：Skill（Claude 内置）
**来源**：[Anthropic 官方](https://www.anthropic.com/news/create-files)
**可信度**：🟢 官方
**平台**：Claude (API / Desktop / Web)

### 一句话描述
生成专业演示文稿，支持幻灯片、图表、过渡动画和品牌模板。

### 安装方式
Claude 内置，使用方式同 xlsx Skill（skill_id: `pptx`）。

### 核心能力
- 自动排版多页幻灯片
- 图表和表格嵌入
- 主题和配色方案
- 演讲备注

### 有什么用
> 季度汇报、项目提案、技术分享——告诉 Claude 主题和要点，自动生成排版精美的 PPT。

### 使用示例
```markdown
「用我们上周的 Q3 销售数据做一个 10 页的季度汇报 PPT，包含趋势图和竞争对手分析」
```

### 限制 & 注意
- 仅 Claude 平台可用
- 复杂图表可能需手动微调
- 品牌模板需提前准备

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| pptx Skill | 自然语言生成、内置 Claude | 仅 Claude 平台 |
| Google Slides MCP | 在线协作 | 需 Google 账号 |
| Python pptx | 完全控制 | 需编程、门槛高 |

---

## [Skill] pdf — PDF 文档生成

**日期**：2025-07-01
**类型**：Skill（Claude 内置）
**来源**：[Anthropic 官方](https://www.anthropic.com/news/create-files)
**可信度**：🟢 官方
**平台**：Claude (API / Desktop / Web)

### 一句话描述
创建格式化 PDF 文档，支持文本、表格、图片和排版。

### 安装方式
Claude 内置，使用方式同上（skill_id: `pdf`）。

### 核心能力
- 多页 PDF 生成
- 文本格式化和排版
- 表格和图片嵌入
- 页眉页脚

### 使用示例
```markdown
「把这份 Markdown 文档转成格式精美的 PDF，加上页眉和页码」
```

### 限制 & 注意
- 仅 Claude 平台可用
- 不适用于编辑已有 PDF
- 复杂排版可能需多次迭代

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| pdf Skill | 自然语言生成、内置 Claude | 仅 Claude 平台 |
| LaTeX | 精确排版 | 学习曲线陡 |
| wkhtmltopdf | HTML 转 PDF | 需自行排版 |

---

## [Skill] docx — Word 文档生成

**日期**：2025-07-01
**类型**：Skill（Claude 内置）
**来源**：[Anthropic 官方](https://www.anthropic.com/news/create-files)
**可信度**：🟢 官方
**平台**：Claude (API / Desktop / Web)

### 一句话描述
生成 Word 文档，支持富文本格式、表格、样式和结构化排版。

### 安装方式
Claude 内置，使用方式同上（skill_id: `docx`）。

### 核心能力
- 富文本格式化
- 标题/段落/列表样式
- 表格和图表
- 模板支持

### 使用示例
```markdown
「整理这个项目的 API 文档，生成一份带目录和代码示例的 Word 文档」
```

### 限制 & 注意
- 仅 Claude 平台可用
- 不支持 .doc 旧格式
- 复杂表格可能需手动调整

### 同类对比
| 工具 | 优势 | 劣势 |
|------|------|------|
| docx Skill | 自然语言生成、内置 Claude | 仅 Claude 平台 |
| Google Docs MCP | 在线协作 | 需 Google 账号 |
| Pandoc | 多格式转换 | 无 AI 辅助 |

### 社区评价
- Claude Skills 是 Claude 独有的差异化能力（Reasonix 不支持文档生成）
- 搭配 Claude Desktop 的 File Creation 功能，形成"对话→文件"的无缝体验
- 社区期待更多 Skills（如 Google Slides、Figma 等）

### 行动项
- [ ] 评估是否需要 Memory MCP 来跨会话记忆偏好
- [ ] 试用 Fetch MCP 替代 web_fetch 抓取复杂网页
- [ ] 是否在 Claude Desktop 中配置 GitHub MCP
