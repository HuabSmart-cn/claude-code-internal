# builtinPlugins.ts - 内置插件注册表

## 文件概述
**路径**: `src/plugins/builtinPlugins.ts`
**功能**: 管理随 CLI 一起发布的内置插件，支持通过 `/plugin` UI 启用/禁用

---

## 核心概念
- **内置插件（Built-in Plugin）**: 与打包技能（bundled skills）的区别在于有独立的 UI 和用户可控开关
- **插件 ID 格式**: `{name}@builtin` 用于区分内置插件和市场插件 `{name}@{marketplace}`
- **默认启用**: 插件默认启用，用户设置可覆盖
- **多组件提供**: 插件可提供技能（skills）、钩子（hooks）、MCP 服务器

## 关键类型/接口
```typescript
// 内置插件定义
type BuiltinPluginDefinition = {
  name: string
  description: string
  version: string
  isAvailable?: () => boolean
  defaultEnabled?: boolean
  skills?: BundledSkillDefinition[]
  hooks?: PluginHookMatcher[]
  mcpServers?: McpServerDefinition[]
}

// 加载的插件
type LoadedPlugin = {
  name: string
  manifest: { name, description, version }
  path: string
  source: string
  repository: string
  enabled: boolean
  isBuiltin: boolean
  hooksConfig?: PluginHookMatcher[]
  mcpServers?: McpServerDefinition[]
}
```

## 核心函数

```typescript
/**
 * 注册内置插件（在启动时通过 initBuiltinPlugins() 调用）
 */
export function registerBuiltinPlugin(definition: BuiltinPluginDefinition): void

/**
 * 检查插件 ID 是否为内置插件（以 @builtin 结尾）
 */
export function isBuiltinPluginId(pluginId: string): boolean

/**
 * 获取特定内置插件定义
 */
export function getBuiltinPluginDefinition(
  name: string,
): BuiltinPluginDefinition | undefined

/**
 * 获取所有已注册插件，分为启用/禁用两组
 */
export function getBuiltinPlugins(): {
  enabled: LoadedPlugin[]
  disabled: LoadedPlugin[]
}

/**
 * 从已启用的内置插件获取技能命令列表
 */
export function getBuiltinPluginSkillCommands(): Command[]

/**
 * 清除插件注册表（仅用于测试）
 */
export function clearBuiltinPlugins(): void
```

## 中英对照
| English | 中文 |
|---------|------|
| Built-in Plugin | 内置插件 |
| Plugin Registry | 插件注册表 |
| Plugin ID | 插件 ID |
| Marketplace | 市场 |
| Bundled Skill | 打包技能 |
| Enabled/Disabled | 启用/禁用 |
| Default Enabled | 默认启用 |
| Hooks | 钩子 |
| MCP Servers | MCP 服务器 |
| User Settings | 用户设置 |
| isAvailable | 可用性检查 |
| Skill Command | 技能命令 |
