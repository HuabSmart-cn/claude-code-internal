# Commands 目录架构

## 概述

`commands/` 目录是 Claude Code 的核心命令实现目录，包含 100+ 个子目录，每个子目录代表一个独立的命令实现。

## 命令架构

### 命令类型 (Command Types)

| 类型 | 说明 | 渲染方式 |
|------|------|----------|
| `local-jsx` | Ink React 组件 | 渲染交互式 UI |
| `local` | 本地命令 | 输出文本结果 |
| `prompt` | AI 提示命令 | 展开为提示词发送给模型 |

### 命令结构

每个命令目录包含：
- `index.ts` - 命令元数据定义（名称、描述、类型等）
- `*.ts/js` - 实际实现代码

### 命令元数据

```typescript
{
  type: 'local-jsx' | 'local' | 'prompt',
  name: string,              // 命令名称
  aliases?: string[],        // 别名
  description: string,       // 命令描述
  argumentHint?: string,     // 参数提示
  isEnabled?: () => boolean, // 是否启用
  isHidden?: boolean,       // 是否隐藏
  supportsNonInteractive?: boolean,  // 支持非交互模式
  availability?: ('claude-ai' | 'console')[],  // 可用性要求
  load: () => import('...') // 懒加载实现
}
```

## 命令分类

### Git 操作

| 命令 | 类型 | 说明 |
|------|------|------|
| `branch` | local-jsx | 创建分支 |
| `commit` | prompt | 创建 git 提交 |
| `commit-push-pr` | prompt | 提交、推送并创建 PR |
| `diff` | local-jsx | 查看未提交变更 |
| `review` | prompt | 审查 PR |
| `ultrareview` | local-jsx | 深度代码审查 |

### 会话管理

| 命令 | 类型 | 说明 |
|------|------|------|
| `clear` | local | 清除会话历史 |
| `compact` | local | 压缩上下文保留摘要 |
| `session` | local-jsx | 远程会话管理 |
| `resume` | local-jsx | 恢复会话 |
| `rewind` | local | 回溯到之前状态 |
| `teleport` | - | 远程环境切换 |
| `tag` | local-jsx | 给会话打标签 |

### 配置管理

| 命令 | 类型 | 说明 |
|------|------|------|
| `config` | local-jsx | 打开配置面板 |
| `model` | local-jsx | 设置 AI 模型 |
| `theme` | local-jsx | 更改主题 |
| `color` | local-jsx | 设置提示栏颜色 |
| `keybindings` | local | 键盘绑定配置 |
| `output-style` | local-jsx | 输出样式设置（已废弃） |
| `privacy-settings` | local-jsx | 隐私设置 |

### 用户账户

| 命令 | 类型 | 说明 |
|------|------|------|
| `login` | local-jsx | 登录 Anthropic 账户 |
| `logout` | local-jsx | 登出账户 |
| `upgrade` | local-jsx | 升级到 Max |
| `usage` | local-jsx | 显示用量限制 |
| `extra-usage` | local-jsx | 配置额外用量 |

### 调试工具

| 命令 | 类型 | 说明 |
|------|------|------|
| `doctor` | local-jsx | 诊断安装状态 |
| `debug-tool-call` | - | 调试工具调用 |
| `heapdump` | local | 导出堆内存快照 |
| `perf-issue` | - | 性能问题追踪 |
| `bughunter` | - | Bug 猎人模式 |
| `ctx_viz` | - | 上下文可视化 |

### 扩展集成

| 命令 | 类型 | 说明 |
|------|------|------|
| `mcp` | local-jsx | 管理 MCP 服务器 |
| `plugin` | local-jsx | 插件管理 |
| `reload-plugins` | local | 重载插件 |
| `install-github-app` | local-jsx | 安装 GitHub App |
| `install-slack-app` | local | 安装 Slack 应用 |

### 信息查看

| 命令 | 类型 | 说明 |
|------|------|------|
| `help` | local-jsx | 显示帮助 |
| `stats` | local-jsx | 使用统计 |
| `cost` | local | 显示会话成本 |
| `status` | local-jsx | 显示状态信息 |
| `release-notes` | local | 发布说明 |
| `files` | local | 列出上下文中的文件 |
| `tasks` | local-jsx | 后台任务列表 |
| `skills` | local-jsx | 技能列表 |
| `hooks` | local-jsx | Hook 配置查看 |

### 工具命令

| 命令 | 类型 | 说明 |
|------|------|------|
| `permissions` | local-jsx | 工具权限管理 |
| `plan` | local-jsx | 计划模式 |
| `btw` | local-jsx | 快速提问 |
| `copy` | local-jsx | 复制上条回复 |
| `export` | local-jsx | 导出对话 |
| `rename` | local-jsx | 重命名会话 |
| `memory` | local-jsx | 编辑记忆文件 |

### 特殊功能

| 命令 | 类型 | 说明 |
|------|------|------|
| `thinkback` | local-jsx | 年度回顾 |
| `thinkback-play` | local | 播放回顾动画 |
| `desktop` | local-jsx | Claude Desktop 集成 |
| `mobile` | local-jsx | 移动端二维码 |
| `chrome` | local-jsx | Chrome 扩展设置 |
| `voice` | local | 语音模式切换 |
| `fast` | local-jsx | 快速模式切换 |
| `effort` | local-jsx | 努力级别设置 |
| `sandbox-toggle` | local-jsx | 沙箱模式切换 |

### 内部命令 (ANT ONLY)

以下命令仅在 `USER_TYPE=ant` 时可用：

- `backfill-sessions`
- `break-cache`
- `env`
- `files`
- `oauth-refresh`
- `tag`

### 已禁用的命令

这些命令返回 stub（始终禁用）：

- `ant-trace`
- `autofix-pr`
- `ctx_viz`
- `debug-tool-call`
- `good-claude`
- `issue`
- `mock-limits`
- `oauth-refresh`
- `onboarding`
- `perf-issue`
- `reset-limits`
- `share`
- `teleport`

## 根目录文件

| 文件 | 类型 | 说明 |
|------|------|------|
| `commit.ts` | prompt | 创建提交 |
| `commit-push-pr.ts` | prompt | 提交并创建 PR |
| `init.ts` | prompt | 初始化项目 |
| `init-verifiers.ts` | - | 初始化验证器 |
| `review.ts` | prompt | PR 审查 |
| `security-review.ts` | prompt | 安全审查 |
| `subscribe-pr.ts` | - | 订阅 PR |
| `torch.ts` | - | Torch 命令 |
| `ultraplan.tsx` | - | 超级计划 |
| `force-snip.js` | - | 历史裁剪 |
| `insights.ts` | prompt | 使用洞察报告 |
| `advisor.ts` | local | 顾问模型设置 |
| `brief.ts` | local-jsx | 简洁模式 |
| `statusline.tsx` | prompt | 状态行设置 |
| `bridge-kick.ts` | - | 桥接模式踢出 |

## 特性开关

很多命令由特性开关控制：

```typescript
const command = feature('FEATURE_NAME') ? require('./...').default : null

// 例如
const voiceCommand = feature('VOICE_MODE')
  ? require('./commands/voice/index.js').default
  : null
```

## 远程安全命令

`REMOTE_SAFE_COMMANDS` - 在远程模式下可用的命令：

- `session`, `exit`, `clear`, `help`, `theme`, `color`, `vim`, `cost`, `usage`, `copy`, `btw`, `feedback`, `plan`, `keybindings`, `statusline`, `stickers`, `mobile`

## 桥接安全命令

`BRIDGE_SAFE_COMMANDS` - 可通过桥接远程执行的命令：

- `compact`, `clear`, `cost`, `summary`, `releaseNotes`, `files`
