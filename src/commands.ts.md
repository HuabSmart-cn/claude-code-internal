# commands.ts

## 文件概述
**路径**: `src/commands.ts`
**功能**: 管理所有斜杠命令(slash commands)的注册、过滤和查找
**重要程度**: ★★★★★

---

## 核心概念
### Command (命令)
斜杠命令是用户输入的特殊指令，格式为 `/command-name`。

### 命令类型
- `prompt`: 提示型命令（展开为文本发送给模型）
- `local`: 本地命令（直接执行，返回文本）
- `local-jsx`: 本地 JSX 命令（渲染 Ink UI）

### 命令来源
- `builtin`: 内置命令
- `bundled`: 打包技能
- `skills`: 技能目录
- `plugin`: 插件命令
- `mcp`: MCP 服务器提供

---

## 主要类型/接口
```typescript
type Command = {
  type: 'prompt' | 'local' | 'local-jsx'
  name: string
  aliases?: string[]
  description: string
  source: string
  availability?: ('claude-ai' | 'console')[]
  // ...
}

type CommandBase = Command

type LocalCommandResult = {
  // ...
}
```

---

## 关键函数
```typescript
/**
 * 获取所有可用命令（包含技能、插件、工作流）
 * 重要：这是一个昂贵的加载操作，被 memoize 缓存
 */
async function getCommands(cwd: string): Promise<Command[]>

/**
 * 获取技能工具命令（模型可调用的技能）
 */
const getSkillToolCommands = memoize(async (cwd: string): Promise<Command[]> => ...)

/**
 * 获取斜杠命令技能
 */
const getSlashCommandToolSkills = memoize(async (cwd: string): Promise<Command[]> => ...)

/**
 * 过滤远程模式安全命令
 */
function filterCommandsForRemoteMode(commands: Command[]): Command[]

/**
 * 检查命令是否可远程安全执行
 */
function isBridgeSafeCommand(cmd: Command): boolean

/**
 * 查找命令
 */
function findCommand(commandName: string, commands: Command[]): Command | undefined

/**
 * 获取命令（带报错）
 */
function getCommand(commandName: string, commands: Command[]): Command
```

---

## 重要常量
```typescript
// 远程安全命令
const REMOTE_SAFE_COMMANDS: Set<Command> = [
  session, exit, clear, help, theme, color, vim, cost, usage, copy, btw,
  feedback, plan, keybindings, statusline, stickers, mobile
]

// 桥接安全命令（移动端可执行）
const BRIDGE_SAFE_COMMANDS: Set<Command> = [
  compact, clear, cost, summary, releaseNotes, files
]
```

---

## 与其他模块的关系
- 调用：
  - `skills/loadSkillsDir.ts` - 加载技能目录
  - `plugins/loadPluginCommands.ts` - 加载插件命令
  - `bundledSkills.ts` - 打包技能
- 被调用：
  - `main.tsx` - 获取命令列表
  - `REPL.tsx` - 命令处理
  - `interactiveHelpers.tsx` - 帮助系统

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Command | 命令 |
| Slash command | 斜杠命令 |
| Prompt command | 提示命令 |
| Local command | 本地命令 |
| availability | 可用性 |
| bundled | 打包的 |
| plugin | 插件 |
| skill | 技能 |
| memoize | 记忆化 |
