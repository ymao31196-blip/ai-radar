# CodeWhale 命令与快捷键汇总

适用版本：CodeWhale 0.8.53 / codewhale-tui 0.8.53

说明：以下内容根据本机当前安装版本的 `codewhale --help`、`codewhale-tui --help`、`features list` 和 TUI 内置帮助文本整理。TUI 内也可以直接输入 `/help` 或按 `Ctrl+K` 查看命令面板。

## 多智能体powershell指令

### code

```powershell
powershell -ExecutionPolicy Bypass -File "C:\Users\86183\.codewhale\orchestrators\Invoke-CodeWhaleCodeWorkflow.ps1" `
  -ProjectDir "你的项目目录" `
  -Task "检查整个项目，制定计划，完成修改，运行测试，并调用 review 子智能体审查。" `
  -RunId "code-task-001"
```
### 论文

```powershell
powershell -ExecutionPolicy Bypass -File "C:\Users\86183\.codewhale\orchestrators\Invoke-CodeWhaleCodeWorkflow.ps1" `
  -ProjectDir "你的项目目录" `
  -Task "检查整个项目，制定计划，完成修改，运行测试，并调用 review 子智能体审查。" `
  -RunId "code-task-001"
```

## 常用启动方式

外层入口 `codewhale.exe` 使用 `-C` 指定工作区：

```powershell
codewhale --yolo -C "C:\Users\86183\Desktop\AI"
```

TUI 本体使用 `-w` 指定工作区：

```powershell
& "C:\Users\86183\AppData\Local\Programs\CodeWhale\bin\codewhale-tui.exe" --yolo -w "C:\Users\86183\Desktop\AI"
```

带初始任务：

```powershell
codewhale --yolo -C "C:\Users\86183\Desktop\AI" -p "先检查项目结构，不要修改文件。"
```

## 外部 CLI 命令

这些是在 PowerShell 里执行的命令，不是 TUI 里的 `/命令`。

```text
codewhale run          运行交互/非交互流程
codewhale doctor       诊断配置、API、工具依赖
codewhale models       列出 provider 可用模型
codewhale speech       小米 MiMo TTS 语音生成，别名 tts
codewhale sessions     列出保存的 TUI 会话
codewhale resume       恢复保存的会话
codewhale fork         分叉会话
codewhale init         在当前目录创建 AGENTS.md
codewhale setup        初始化 MCP / skills / tools / plugins
codewhale exec         非交互执行 prompt
codewhale review       基于 git diff 做代码审查
codewhale apply        应用 patch
codewhale eval         离线评测
codewhale mcp          管理 MCP 服务
codewhale features     查看功能开关
codewhale serve        启动本地服务
codewhale completions  生成 shell completion
codewhale login        配置 provider credentials
codewhale logout       删除登录状态
codewhale auth         管理认证
codewhale config       读写配置
codewhale model        解析或列出模型
codewhale thread       管理 thread / session 元数据
codewhale sandbox      评估 sandbox/审批策略
codewhale metrics      使用量统计
codewhale update       检查或更新 CodeWhale
```

常用外部参数：

```text
-C, --workspace <DIR>       指定工作区，外层 codewhale.exe 用这个
--provider <PROVIDER>       指定 provider，例如 deepseek
--model <MODEL>             指定模型
--api-key <API_KEY>         临时传 API key
--base-url <BASE_URL>       临时传 base URL
--yolo                      自动批准工具
-c, --continue              继续最近会话
-p, --prompt <PROMPT>       初始 prompt
--skip-onboarding           跳过 onboarding
--mouse-capture             开启鼠标捕获
--no-mouse-capture          关闭鼠标捕获
```

TUI 本体常用参数：

```text
-w, --workspace <DIR>       指定工作区，codewhale-tui.exe 用这个
-p, --prompt <PROMPT>       初始 prompt
--yolo                      自动批准工具和 shell 执行
--max-subagents <1-20>      最大并发子智能体数量
-r, --resume <ID>           恢复指定会话
-c, --continue              继续最近会话
--fresh                     忽略崩溃恢复，开新会话
--no-project-config         跳过项目级 .codewhale/config.toml
```

## TUI 内部 / 命令

### 会话与基础操作

```text
/help [command]              查看帮助
/home                        首页面板
/clear                       清空对话
/exit                        退出，别名 quit / q
/new [--force]               开新会话
/sessions [show|prune N]     会话列表/清理
/load [path]                 载入会话
/save [path]                 保存会话
/fork                        分叉当前会话
/rename <title>              重命名会话
/retry                       重试上一轮
/undo                        移除最后一组消息
/restore [N]                 回滚到快照
/export [path]               导出 Markdown
/share                       生成分享链接
```

### 模型、模式、配置

```text
/mode [agent|plan|yolo|1|2|3]       切换模式
/model [name]                       查看/切换模型
/models                             列出 API 可用模型
/provider [name] [model]            切换 provider/model
/profile <name>                     切换配置 profile
/config                             打开交互配置
/settings                           查看持久配置
/theme [name]                       切换主题
/verbose [on|off]                   详细输出开关
/status                             运行状态
/statusline                         配置底部状态栏
/cost                               会话成本
/balance                            provider 余额
/cache [count|inspect|stats|zones|warmup]  DeepSeek 缓存统计
/links                              DeepSeek/API 链接
/logout                             清除 API key
/translate                          输出翻译开关
/workspace [path]                   查看/切换 workspace
/trust [on|off|add|remove|list]     工作区信任
/lsp [on|off|status]                LSP 诊断开关
```

### 上下文、记忆、附件

```text
/anchor <text>                      固定长期事实
/anchor list                        查看固定事实
/anchor remove <n>                  删除固定事实
/attach <path>                      添加图片/视频/文件
/context                            上下文检查器
/compact                            压缩上下文
/purge                              让 agent 裁剪历史
/note add <text>                    添加工作区笔记
/note list                          查看笔记
/note show <n>                      查看某条笔记
/note edit <n> <text>               编辑笔记
/note remove <n>                    删除笔记
/note clear                         清空笔记
/note path                          查看笔记路径
/memory show                        查看用户记忆
/memory path                        查看记忆路径
/memory clear                       清空记忆
/memory edit                        输出编辑命令
/memory help                        查看 memory 帮助
/stash list                         查看暂存草稿
/stash pop                          恢复暂存草稿
/stash clear                        清空暂存草稿
/queue list                         查看队列消息
/queue edit <n>                     编辑队列消息
/queue drop <n>                     删除队列消息
/queue clear                        清空队列
```

### 智能体、任务、工具

```text
/agent [N] <task>                   开持久子智能体
/subagents                          查看子智能体状态
/task add <prompt>                  添加后台任务
/task list                          查看后台任务
/task show <id>                     查看任务详情
/task cancel <id>                   取消任务
/jobs list                          查看后台命令
/jobs show <id>                     查看命令详情
/jobs poll <id>                     查询命令状态
/jobs wait <id>                     等待命令完成
/jobs stdin <id> <input>            给命令输入 stdin
/jobs close-stdin <id>              关闭 stdin
/jobs cancel <id>                   取消某个命令
/jobs cancel-all                    取消所有后台命令
/hunt <quarry> [budget: N]          多智能体 fanout 任务
/rlm [N] <file_or_text>             持久 RLM 上下文
/review <target>                    结构化代码审查
/mcp init                           初始化 MCP 配置
/mcp add stdio <name> <command>     添加 stdio MCP
/mcp add http <name> <url>          添加 HTTP MCP
/mcp enable <name>                  启用 MCP
/mcp disable <name>                 禁用 MCP
/mcp remove <name>                  删除 MCP
/mcp validate                       校验 MCP
/mcp reload                         重新加载 MCP
/network list                       查看网络策略
/network allow <host>               允许 host
/network deny <host>                拒绝 host
/network remove <host>              删除 host 规则
/network default <allow|deny|prompt> 设置默认网络策略
/hooks list                         查看 hooks
/hooks events                       查看 hooks 事件
/init                               生成 AGENTS.md
```

### 技能与扩展

```text
/skills                             列出本地 skills
/skills <prefix>                    按前缀筛选 skills
/skills --remote                    浏览远程 curated registry
/skills sync                        同步 registry
/skill <name>                       启用 skill
/skill install <spec>               安装 skill
/skill update <name>                更新 skill
/skill uninstall <name>             卸载 skill
/skill trust <name>                 信任 skill
/slop [query|export]                SlopLedger 查询/导出
/feedback [bug|feature|security]    反馈
```

### 其他命令

```text
/system                             查看当前 system prompt
/edit                               编辑/修改相关入口
/diff                               查看改动
/change [version]                   查看 changelog
```

## 快捷键

### 输入与编辑

```text
Enter                               发送
Alt+Enter / Ctrl+J / Shift+Enter    换行
Esc                                 关闭菜单/取消请求/清空当前输入
Ctrl+C                              取消请求；空闲时再按一次退出
Ctrl+D                              输入为空时退出
Backspace / Delete                  删除字符，或移除选中附件
Ctrl+U                              清空当前草稿
Ctrl+S                              暂存草稿，配合 /stash pop 恢复
Alt+R                               搜索历史 prompt / 恢复本地草稿
Tab / Shift+Tab                     补全 /command；切换模式/推理强度
```

### 导航与查看

```text
Up / Down                           历史输入、滚动 transcript、选择附件
PgUp / PgDn                         按页滚动 transcript
Ctrl+Home / Ctrl+End                跳到顶部/底部
g / G                               输入为空时跳到顶部/底部
[ / ]                               在工具输出块之间跳转
Home / End                          光标到行首/行尾
Ctrl+A / Ctrl+E                     光标到行首/行尾
Alt+V                               查看选中工具/消息的详细信息
Ctrl+O                              打开工具详情/完整 reasoning pager
Ctrl+T                              打开实时 transcript/活动详情
Esc Esc                             进入回退上一条用户消息流程
```

### 模式、面板、命令

```text
Ctrl+K                              打开命令面板
Ctrl+P                              文件选择器，插入 @path
Ctrl+B                              打开前台 shell 控制
Ctrl+X                              Plan / Agent 模式切换
Alt+1 / Alt+2 / Alt+3               跳到 Plan / Agent / YOLO
Alt+P / Alt+A / Alt+Y               另一组 Plan / Agent / YOLO 快捷键
Alt+! / Alt+@ / Alt+# / Alt+$ / Alt+0 聚焦侧栏 Work / Tasks / Agents / Context / Auto
Ctrl+Alt+0                          隐藏侧栏
Ctrl+R                              打开/恢复会话
F1                                  输入为空时打开帮助
Ctrl+/                              切换帮助 overlay
```

### 剪贴板与附件

```text
Ctrl+V                              粘贴文本或附加剪贴板图片
Ctrl+Shift+C                        复制当前选择
右键                                上下文菜单/复制选择
@path                               添加本地文本文件或目录到上下文
```

## 最常用速记

```text
/help                               帮助
Ctrl+K                              命令面板
/model                              切模型
/mode yolo                          开自动工具模式
/skills                             看技能
/skill <name>                       启用技能
/agent [N] <task>                   开子智能体
/subagents                          看子智能体状态
/jobs                               看后台命令
Ctrl+R                              恢复会话
Ctrl+S                              暂存草稿
Alt+V                               查看详情
```

## 当前功能开关

本机当前 `codewhale features list`：

```text
shell_tool      stable        true
subagents       experimental  true
web_search      experimental  true
apply_patch     experimental  true
mcp             experimental  true
exec_policy     experimental  true
vision_model    experimental  false
```
