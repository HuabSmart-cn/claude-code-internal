# hooks.ts - 钩子 Zod 模式定义

## 文件概述
**路径**: `src/schemas/hooks.ts`
**功能**: 定义钩子相关的 Zod 模式，用于验证钩子配置、打破循环依赖

---

## 核心概念
- **钩子（Hook）**: 在特定事件发生时执行的回调，支持命令、提示、HTTP、Agent 四种类型
- **权限规则语法**: `if` 条件字段使用权限规则语法（如 `"Bash(git *)"`）过滤钩子触发
- **惰性模式（Lazy Schema）**: 使用 `lazySchema()` 避免循环依赖
- **区分联合（Discriminated Union）**: 通过 `type` 字段区分不同钩子类型

## 关键类型/接口
```typescript
// 钩子命令类型
type HookCommand =
  | BashCommandHook
  | PromptHook
  | AgentHook
  | HttpHook

// Bash 命令钩子
type BashCommandHook = {
  type: 'command'
  command: string
  if?: string
  shell?: 'bash' | 'powershell'
  timeout?: number
  statusMessage?: string
  once?: boolean
  async?: boolean
  asyncRewake?: boolean
}

// 提示钩子
type PromptHook = {
  type: 'prompt'
  prompt: string
  if?: string
  timeout?: number
  model?: string
  statusMessage?: string
  once?: boolean
}

// HTTP 钩子
type HttpHook = {
  type: 'http'
  url: string
  if?: string
  timeout?: number
  headers?: Record<string, string>
  allowedEnvVars?: string[]
  statusMessage?: string
  once?: boolean
}

// Agent 验证钩子
type AgentHook = {
  type: 'agent'
  prompt: string
  if?: string
  timeout?: number
  model?: string
  statusMessage?: string
  once?: boolean
}

// 钩子匹配器
type HookMatcher = {
  matcher?: string
  hooks: HookCommand[]
}

// 钩子设置
type HooksSettings = Partial<Record<HookEvent, HookMatcher[]>>
```

## 核心模式

```typescript
export const HookCommandSchema = lazySchema(() =>
  z.discriminatedUnion('type', [
    BashCommandHookSchema,
    PromptHookSchema,
    AgentHookSchema,
    HttpHookSchema,
  ])
)

export const HookMatcherSchema = lazySchema(() =>
  z.object({
    matcher: z.string().optional(),
    hooks: z.array(HookCommandSchema()),
  })
)

export const HooksSchema = lazySchema(() =>
  z.partialRecord(z.enum(HOOK_EVENTS), z.array(HookMatcherSchema()))
)
```

## 中英对照
| English | 中文 |
|---------|------|
| Hook | 钩子 |
| Hook Schema | 钩子模式 |
| Hook Event | 钩子事件 |
| Hook Command | 钩子命令 |
| Bash Command Hook | Bash 命令钩子 |
| Prompt Hook | 提示钩子 |
| HTTP Hook | HTTP 钩子 |
| Agent Hook | Agent 钩子 |
| Hook Matcher | 钩子匹配器 |
| If Condition | 条件判断 |
| Permission Rule Syntax | 权限规则语法 |
| Discriminated Union | 区分联合 |
| Lazy Schema | 惰性模式 |
| Timeout | 超时 |
| Once | 单次执行 |
| Async | 异步 |
