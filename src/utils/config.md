# config.ts - 配置管理系统

## 功能概述

`config.ts` 是 Claude Code 的核心配置管理模块，负责：
- 全局配置（GlobalConfig）- 存储在 `~/.claude.json`
- 项目配置（ProjectConfig）- 按 git 仓库根目录组织
- 配置的持久化、读取、备份和迁移

## 核心类型

### GlobalConfig
全局配置对象，包含应用程序的各种设置：

**账户与认证：**
```typescript
oauthAccount?: AccountInfo      // OAuth 账户信息
apiKeyHelper?: string           // API Key 辅助（已废弃）
primaryApiKey?: string          // 主 API Key
```

**主题与界面：**
```typescript
theme: ThemeSetting             // 主题设置
editorMode?: EditorMode         // 编辑器模式
showTurnDuration: boolean      // 显示回合时长
terminalProgressBarEnabled: boolean  // 终端进度条
showStatusInTerminalTab?: boolean    // 标签状态显示
```

**功能开关：**
```typescript
autoCompactEnabled: boolean     // 自动压缩
todoFeatureEnabled: boolean    // Todo 功能
speculationEnabled?: boolean    // 推测执行
```

**跟踪与遥测：**
```typescript
cachedStatsigGates: Record<string, boolean>    // Statsig 门控
cachedDynamicConfigs?: Record<string, unknown> // 动态配置
cachedGrowthBookFeatures?: Record<string, unknown> // GrowthBook 特性
```

**Sonnet 1M 相关：**
```typescript
s1mAccessCache?: Record<string, { hasAccess: boolean; ... }>
s1mNonSubscriberAccessCache?: Record<string, { hasAccess: boolean; ... }>
```

### ProjectConfig
项目级配置：

```typescript
allowedTools: string[]          // 允许的工具
mcpServers?: Record<string, McpServerConfig>  // MCP 服务器
lastAPIDuration?: number        // 上次 API 耗时
lastCost?: number               // 上次成本
hasTrustDialogAccepted?: boolean // 信任对话框已接受
activeWorktreeSession?: { ... } // 工作树会话
```

## 核心函数

### getGlobalConfig(): GlobalConfig
获取全局配置。使用缓存机制，首次调用时从文件读取。

```typescript
export function getGlobalConfig(): GlobalConfig
```

**特性：**
- 缓存读取结果
- 监控文件变化（使用 `fs.watchFile`）
- 启动时同步读取（可接受，因为只执行一次）

### saveGlobalConfig(updater: (current: GlobalConfig) => GlobalConfig)
保存全局配置。

```typescript
export function saveGlobalConfig(
  updater: (currentConfig: GlobalConfig) => GlobalConfig,
): void
```

**特性：**
- 使用文件锁防止并发写入
- 自动备份（`~/.claude/backups/`）
- 保留最近 5 个备份
- 防止覆盖认证状态

### getCurrentProjectConfig(): ProjectConfig
获取当前项目的配置。

```typescript
export function getCurrentProjectConfig(): ProjectConfig
```

### saveCurrentProjectConfig(updater: (current: ProjectConfig) => ProjectConfig)
保存当前项目配置。

```typescript
export function saveCurrentProjectConfig(
  updater: (currentConfig: ProjectConfig) => ProjectConfig,
): void
```

### checkHasTrustDialogAccepted(): boolean
检查是否已接受信任对话框。

```typescript
export function checkHasTrustDialogAccepted(): boolean
```

**逻辑：**
- 检查会话级信任
- 检查项目配置
- 遍历父目录检查信任状态

### getProjectPathForConfig(): string
获取项目配置路径（memoized）。

```typescript
export const getProjectPathForConfig = memoize((): string => { ... })
```

**逻辑：**
- 返回 git 仓库根目录（如果存在）
- 否则返回原始工作目录

### isPathTrusted(dir: string): boolean
检查任意目录是否受信任。

```typescript
export function isPathTrusted(dir: string): boolean
```

### getOrCreateUserID(): string
获取或创建用户 ID。

```typescript
export function getOrCreateUserID(): string
```

### getMemoryPath(memoryType: MemoryType): string
获取记忆文件路径。

```typescript
export function getMemoryPath(memoryType: MemoryType): string
```

**内存类型：**
- `User` - `~/.claude/CLAUDE.md`
- `Local` - `./CLAUDE.local.md`
- `Project` - `./CLAUDE.md`
- `Managed` - 托管路径
- `AutoMem` - 自动记忆

## 安全机制

### 防止认证状态丢失
```typescript
function wouldLoseAuthState(fresh: GlobalConfig): boolean
```

如果写入会导致 OAuth 账户或 onboarding 状态丢失，拒绝写入。

### 配置损坏处理
- 检测配置解析错误
- 自动备份损坏的配置到 `~/.claude/backups/<file>.corrupted.<timestamp>`
- 尝试恢复最近的备份

### 文件锁
使用 `lockfile` 包防止多进程同时写入。

## 配置备份

备份目录：`~/.claude/backups/`

**策略：**
- 每 60 秒最多创建一个备份
- 保留最近 5 个备份
- 备份文件名格式：`<base>.backup.<timestamp>`

## 迁移机制

### migrateConfigFields()
迁移旧字段：
- `autoUpdaterStatus` -> `installMethod` + `autoUpdates`

### removeProjectHistory()
从项目配置中移除历史字段（已迁移到 `history.jsonl`）
