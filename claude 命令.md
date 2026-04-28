---
title: Claude CLI 命令参考
tags:
  - CLI
  - Claude
  - 工具
created: 2026-04-24
---

# Claude CLI 命令参考

> [!info] 简介
> Claude Code 是 Anthropic 官方提供的命令行工具，用于与 Claude 模型进行交互。默认启动交互式会话，使用 `-p/--print` 可进行非交互式输出。

## 基本用法

```bash
claude [options] [command] [prompt]
```

---

## 全局选项

### 会话管理

| 选项 | 说明 |
|------|------|
| `-c, --continue` | 继续当前目录中最近的对话 |
| `-r, --resume [value]` | 通过会话 ID 恢复对话，或打开交互式选择器 |
| `--session-id <uuid>` | 为对话指定特定的会话 ID |
| `--fork-session` | 恢复时创建新的会话 ID |
| `-n, --name <name>` | 设置会话显示名称 |
| `--from-pr [value]` | 通过 PR 编号/URL 恢复会话 |

### 模型与代理

| 选项 | 说明 |
|------|------|
| `--model <model>` | 指定模型（如 `sonnet`、`opus` 或完整模型名） |
| `--agent <agent>` | 指定当前会话的代理 |
| `--agents <json>` | JSON 对象定义自定义代理 |
| `--effort <level>` | 设置努力级别：`low`、`medium`、`high`、`max` |
| `--fallback-model <model>` | 默认模型过载时自动回退到指定模型 |

### 输出控制

| 选项 | 说明 |
|------|------|
| `-p, --print` | 打印响应并退出（非交互模式） |
| `--output-format <format>` | 输出格式：`text`、`json`、`stream-json`（仅 `-p` 模式） |
| `--input-format <format>` | 输入格式：`text`、`stream-json`（仅 `-p` 模式） |
| `--json-schema <schema>` | JSON Schema 结构化输出验证 |
| `--brief` | 启用代理到用户的通信工具 |
| `--verbose` | 启用详细模式 |
| `--replay-user-messages` | 在 stdout 回显 stdin 的用户消息（需 `--input-format=stream-json` 和 `--output-format=stream-json`） |

### 权限与安全

| 选项 | 说明 |
|------|------|
| `--permission-mode <mode>` | 权限模式：`default`、`acceptEdits`、`bypassPermissions`、`dontAsk`、`plan`、`auto` |
| `--allowedTools, --allowed-tools <tools...>` | 允许的工具列表，逗号或空格分隔（如 `"Bash(git:*) Edit"`） |
| `--disallowedTools, --disallowed-tools <tools...>` | 禁止的工具列表，逗号或空格分隔 |
| `--dangerously-skip-permissions` | 跳过所有权限检查（仅限无网络访问的沙盒环境） |
| `--allow-dangerously-skip-permissions` | 启用跳过权限检查选项（不默认启用） |

### 配置与设置

| 选项 | 说明 |
|------|------|
| `--settings <file-or-json>` | 加载设置文件或 JSON 字符串 |
| `--setting-sources <sources>` | 设置来源：`user`、`project`、`local` |
| `--mcp-config <configs...>` | 加载 MCP 服务器配置 |
| `--strict-mcp-config` | 仅使用 `--mcp-config` 中的 MCP 服务器 |
| `--add-dir <directories...>` | 添加允许工具访问的目录 |
| `--plugin-dir <path>` | 从指定目录加载插件 |

### 系统提示

| 选项 | 说明 |
|------|------|
| `--system-prompt <prompt>` | 设置系统提示 |
| `--append-system-prompt <prompt>` | 追加到默认系统提示 |

### 调试与诊断

| 选项 | 说明 |
|------|------|
| `-d, --debug [filter]` | 启用调试模式，可选类别过滤（如 `"api,hooks"` 或 `"!1p,!file"`） |
| `--debug-file <path>` | 将调试日志写入文件（隐式启用调试模式） |
| `--include-hook-events` | 在输出流中包含 hook 生命周期事件（需 `--output-format=stream-json`） |
| `--include-partial-messages` | 包含部分消息块（需 `-p` 和 `--output-format=stream-json`） |
| `--mcp-debug` | **已弃用**：启用 MCP 调试模式，请改用 `--debug` |

### 其他选项

| 选项 | 说明 |
|------|------|
| `--bare` | 最小模式：跳过 hooks、LSP、插件同步、归属、自动内存、后台预取、钥匙串读取和 CLAUDE.md 自动发现。设置 `CLAUDE_CODE_SIMPLE=1` |
| `--tools <tools...>` | 指定可用工具集，使用 `""` 禁用所有工具，`"default"` 使用所有工具 |
| `--chrome` | 启用 Chrome 集成 |
| `--no-chrome` | 禁用 Chrome 集成 |
| `--ide` | 自动连接到 IDE（仅当恰好有一个有效 IDE 可用时） |
| `--tmux` | 为 worktree 创建 tmux 会话（需 `--worktree`），可用 iTerm2 时使用原生面板；`--tmux=classic` 使用传统 tmux |
| `-w, --worktree [name]` | 为会话创建新的 git worktree（可选指定名称） |
| `--file <specs...>` | 启动时下载文件资源，格式：`file_id:relative_path`（如 `--file file_abc:doc.txt`） |
| `--betas <betas...>` | 包含 beta 请求头（仅 API 密钥用户） |
| `--max-budget-usd <amount>` | API 调用最大花费限制（仅 `-p` 模式） |
| `--no-session-persistence` | 禁用会话持久化（仅 `-p` 模式） |
| `--disable-slash-commands` | 禁用所有技能 |
| `-v, --version` | 输出版本号 |
| `-h, --help` | 显示帮助信息 |

---

## 子命令

### `claude agents`

列出已配置的代理。

```bash
claude agents [options]
```

### `claude auth`

管理身份验证。

```bash
claude auth
```

### `claude auto-mode`

检查自动模式分类器配置。

```bash
claude auto-mode
```

### `claude doctor`

检查 Claude Code 自动更新器的健康状态。

> [!warning] 注意
> 此命令会跳过工作区信任对话框并启动 stdio 服务器进行健康检查。仅在信任的目录中使用。

```bash
claude doctor
```

### `claude install`

安装 Claude Code 原生版本。

```bash
claude install [options] [target]
```

- `target` 可以是：`stable`、`latest` 或特定版本号

### `claude mcp`

配置和管理 MCP 服务器。

```bash
claude mcp
```

### `claude plugin` / `claude plugins`

管理 Claude Code 插件。

```bash
claude plugin
claude plugins
```

### `claude setup-token`

设置长期身份验证令牌（需要 Claude 订阅）。

```bash
claude setup-token
```

### `claude update` / `claude upgrade`

检查更新并安装。

```bash
claude update
claude upgrade
```

---

## 斜杠命令

在 Claude Code 会话中，输入 `/` 可查看所有可用命令，或输入 `/` 后跟字母进行筛选。

> [!info] 说明
> - 标记 **[Skill]** 的是捆绑技能，基于提示词驱动 Claude 执行任务
> - 其他为内置命令，行为直接编码在 CLI 中
> - 命令可用性取决于平台、计划和运行环境
> - `<arg>` 表示必需参数，`[arg]` 表示可选参数

### 会话管理

| 命令                        | 说明                                     | 备注             |
| ------------------------- | -------------------------------------- | -------------- |
| `/clear`                  | 开始新对话，清空上下文。别名：`/reset`、`/new`         | ⭐ 常用：对话跑偏时重新开始 |
| `/compact [instructions]` | 压缩对话以释放上下文，可选传入摘要焦点指令                  | ⭐ 常用：上下文过长时使用  |
| `/resume [session]`       | 恢复对话。别名：`/continue`                    | ⭐ 常用：恢复之前的工作   |
| `/branch [name]`          | 在当前点创建对话分支。别名：`/fork`                  | 探索不同方案时使用      |
| `/rewind`                 | 回退对话或代码到之前的状态。别名：`/checkpoint`、`/undo` | Claude 做错时回退   |
| `/rename [name]`          | 重命名当前会话，无参数时自动生成名称                     | 整理会话列表         |
| `/export [filename]`      | 导出对话为纯文本                               | 分享或存档对话        |
| `/recap`                  | 生成当前会话的一行摘要                            | 快速回顾会话内容       |

### 模型与配置

| 命令 | 说明 | 备注 |
|------|------|------|
| `/model [model]` | 选择或更改 AI 模型 | ⭐ 常用：切换 Sonnet/Opus |
| `/effort [level\|auto]` | 设置模型努力级别：`low`、`medium`、`high`、`xhigh`、`max` | 复杂任务用 high/max |
| `/fast [on\|off]` | 切换快速模式 | ⭐ 常用：加速简单任务 |
| `/config` | 打开设置界面。别名：`/settings` | ⭐ 常用：调整各项配置 |
| `/theme` | 更改颜色主题，支持自动检测终端明暗 | 个人偏好设置 |
| `/statusline` | 配置状态栏 | 自定义显示信息 |
| `/keybindings` | 打开或创建快捷键配置文件 | 自定义快捷键 |
| `/terminal-setup` | 配置终端快捷键（Shift+Enter 等） | VS Code 等终端需要 |
| `/tui [default\|fullscreen]` | 设置终端 UI 渲染器 | 全屏模式更流畅 |

### 权限与安全

| 命令 | 说明 | 备注 |
|------|------|------|
| `/permissions` | 管理工具权限规则。别名：`/allowed-tools` | ⭐ 常用：减少权限弹窗 |
| `/sandbox` | 切换沙盒模式（仅支持平台） | 隔离环境测试 |
| `/privacy-settings` | 查看和更新隐私设置（仅 Pro/Max 订阅） | 隐私控制 |

### 工具与集成

| 命令 | 说明 | 备注 |
|------|------|------|
| `/mcp` | 管理 MCP 服务器连接和 OAuth 认证 | ⭐ 常用：配置外部工具 |
| `/ide` | 管理 IDE 集成并显示状态 | ⭐ 常用：连接 VS Code 等 |
| `/chrome` | 配置 Claude in Chrome 设置 | 浏览器集成 |
| `/hooks` | 查看 hook 配置 | 自动化工作流 |
| `/plugin` | 管理 Claude Code 插件 | 扩展功能 |
| `/reload-plugins` | 重新加载所有活动插件 | 插件开发调试 |
| `/agents` | 管理代理配置 | 自定义子代理 |
| `/skills` | 列出可用技能，按 `t` 按令牌数排序 | ⭐ 常用：查看可用技能 |
| `/memory` | 编辑 CLAUDE.md 内存文件，管理自动内存 | ⭐ 常用：项目上下文配置 |

### Git 与 PR

| 命令 | 说明 | 备注 |
|------|------|------|
| `/autofix-pr [prompt]` | 启动 Web 会话监控 PR 并自动修复 CI 失败和评审意见 | CI 自动修复 |
| `/install-github-app` | 为仓库设置 Claude GitHub Actions 应用 | GitHub 集成 |

### 任务与调度

| 命令 | 说明 | 备注 |
|------|------|------|
| `/tasks` | 列出和管理后台任务。别名：`/bashes` | ⭐ 常用：查看后台任务 |
| `/schedule [description]` | 创建、更新、列出或运行例程。别名：`/routines` | 定期执行的工作流 |

### 诊断与调试

| 命令                     | 说明                                     | 备注           |
| ---------------------- | -------------------------------------- | ------------ |
| `/doctor`              | 诊断 Claude Code 安装和设置                   | ⭐ 常用：排查环境问题  |
| `/debug [description]` | **[Skill]** 启用调试日志并排查问题                | 调试会话问题       |
| `/context`             | 可视化当前上下文使用情况                           | ⭐ 常用：查看上下文占用 |
| `/usage`               | 显示会话成本、计划使用限制和活动统计。别名：`/cost`、`/stats` | ⭐ 常用：查看用量和费用 |
| `/heapdump`            | 写入 JavaScript 堆快照用于诊断高内存使用             | 内存问题诊断       |

### 代码质量

| 命令                    | 说明                               | 备注          |
| --------------------- | -------------------------------- | ----------- |
| `/simplify [focus]`   | **[Skill]** 审查最近更改的代码并修复问题       | ⭐ 常用：代码优化   |
| `/init`               | **[Skill]** 使用 CLAUDE.md 指南初始化项目 | ⭐ 常用：新项目配置  |
| `/plan [description]` | 直接进入计划模式                         | ⭐ 常用：规划实现方案 |
| `/review [PR]`        | **[Skill]** 在本地会话中审查 PR          | ⭐ 常用：代码审查   |
| `/security-review`    | **[Skill]** 分析当前分支待更改的安全漏洞       | 提交前安全检查     |
| `/frontend-design`    | **[Skill]** 创建高质量前端界面            | Web 组件开发    |

### 云端与远程

| 命令 | 说明 | 备注 |
|------|------|------|
| `/desktop` | 在 Claude Code 桌面应用中继续当前会话。别名：`/app` | 切换到桌面应用 |
| `/remote-control` | 使会话可从 claude.ai 远程控制。别名：`/rc` | 远程协作 |
| `/teleport` | 将 Web 会话拉取到终端。别名：`/tp` | Web → 终端 |
| `/remote-env` | 配置远程环境默认设置 | 远程环境配置 |
| `/web-setup` | 使用本地 gh CLI 凭据连接 GitHub 账户 | GitHub 连接 |
| `/ultraplan <prompt>` | 在 ultraplan 会话中起草计划 | 云端深度规划 |
| `/ultrareview [PR]` | 在云沙盒中运行深度多代理代码审查 | 云端深度审查 |

### 其他命令

| 命令 | 说明 | 备注 |
|------|------|------|
| `/help` | 显示帮助和可用命令 | ⭐ 常用：查看帮助 |
| `/exit` | 退出 CLI。别名：`/quit` | ⭐ 常用：退出会话 |
| `/login` | 登录 Anthropic 账户 | 首次使用 |
| `/logout` | 登出 Anthropic 账户 | 切换账户 |
| `/diff` | 打开交互式 diff 查看器 | ⭐ 常用：查看更改 |
| `/copy [N]` | 复制最近的助手响应到剪贴板 | 复制输出内容 |
| `/color [color\|default]` | 设置提示栏颜色 | 个性化设置 |
| `/focus` | 切换焦点视图 | 简洁输出模式 |
| `/btw <question>` | 提问临时问题而不添加到对话 | 快速提问 |
| `/add-dir <path>` | 添加工作目录 | 多目录工作 |
| `/feedback [report]` | 提交反馈。别名：`/bug` | 反馈问题 |
| `/insights` | 生成 Claude Code 使用分析报告 | 使用统计 |
| `/team-onboarding` | 从使用历史生成团队入门指南 | 团队协作 |
| `/powerup` | 通过交互式课程发现 Claude Code 功能 | 学习新功能 |
| `/release-notes` | 查看更新日志 | 查看新版本 |
| `/mobile` | 显示下载 Claude 移动应用的二维码。别名：`/ios`、`/android` | 移动端 |
| `/voice [hold\|tap\|off]` | 切换语音听写 | 语音输入 |
| `/extra-usage` | 配置额外使用量以在达到速率限制时继续工作 | 超额使用 |
| `/upgrade` | 打开升级页面 | 升级计划 |
| `/passes` | 与朋友分享免费的 Claude Code 周 | 邀请好友 |
| `/stickers` | 订购 Claude Code 贴纸 | 周边 |

### 批量操作技能

| 命令                                              | 说明                                              | 备注        |
| ----------------------------------------------- | ----------------------------------------------- | --------- |
| `/batch <instruction>`                          | **[Skill]** 在代码库中并行编排大规模更改                      | 大规模重构     |
| `/claude-api [migrate\|managed-agents-onboard]` | **[Skill]** 构建、调试 Claude API / Anthropic SDK 应用 | API 开发参考  |
| `/fewer-permission-prompts`                     | **[Skill]** 扫描脚本并添加权限白名单以减少提示                   | 减少弹窗干扰    |
| `/loop [interval] [prompt]`                     | **[Skill]** 循环运行提示或斜杠命令                         | 定时任务、轮询状态 |
| `/update-config`                                | **[Skill]** 配置 Claude Code 设置（权限、环境变量、hooks）    | 自动化配置     |
| `/keybindings-help`                             | **[Skill]** 自定义键盘快捷键                            | 快捷键配置     |

### Superpowers 工作流技能

> [!info] 说明
> Superpowers 是一套系统化的工作流技能，帮助 Claude 遵循最佳实践完成任务。

| 命令                                | 说明                             | 备注           |
| --------------------------------- | ------------------------------ | ------------ |
| `/brainstorming`                  | **[Skill]** 创意工作前的需求探索和设计      | ⭐ 创建功能前必用    |
| `/writing-plans`                  | **[Skill]** 编写多步骤任务的实现计划       | 规划实现方案       |
| `/executing-plans`                | **[Skill]** 在独立会话中执行实现计划       | 执行计划         |
| `/test-driven-development`        | **[Skill]** 测试驱动开发工作流          | ⭐ TDD 开发     |
| `/systematic-debugging`           | **[Skill]** 系统化调试工作流           | ⭐ 遇到 bug 时使用 |
| `/verification-before-completion` | **[Skill]** 完成前验证工作是否真正完成      | ⭐ 提交/PR 前验证  |
| `/requesting-code-review`         | **[Skill]** 请求代码审查             | 完成功能后审查      |
| `/receiving-code-review`          | **[Skill]** 处理代码审查反馈           | 收到审查意见时      |
| `/finishing-a-development-branch` | **[Skill]** 完成开发分支的合并/PR/清理    | 开发完成后        |
| `/using-git-worktrees`            | **[Skill]** 创建隔离的 git worktree | 功能隔离开发       |
| `/dispatching-parallel-agents`    | **[Skill]** 分派并行代理处理独立任务       | 并行处理多任务      |
| `/subagent-driven-development`    | **[Skill]** 子代理驱动开发            | 复杂任务分解       |
| `/writing-skills`                 | **[Skill]** 创建或编辑技能            | 编写新技能        |

### MCP 提示

MCP 服务器可以暴露作为命令出现的提示，格式为 `/mcp__<server>__<prompt>`，从连接的服务器动态发现。

---

## 常用示例

### 快速提问

```bash
claude -p "解释什么是 MCP"
```

### 使用特定模型

```bash
claude --model opus
claude --model claude-sonnet-4-6
```

### 继续上次对话

```bash
claude -c
```

### 恢复特定会话

```bash
claude -r <session-id>
```

### JSON 输出

```bash
claude -p --output-format json "列出当前目录的文件"
```

### 创建隔离工作环境

```bash
claude -w feature-branch
```

### 调试模式

```bash
claude --debug
claude --debug api,hooks
claude --debug-file ./claude-debug.log
```

---

## 相关链接

- [[Claude Code 官方文档]]
- [[MCP 服务器配置]]
- [[Claude API 使用指南]]

---

> [!tip] 提示
> 使用 `claude --help` 查看最新帮助信息，使用 `claude <command> --help` 查看子命令详情。
