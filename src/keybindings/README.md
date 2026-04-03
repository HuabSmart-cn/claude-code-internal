# keybindings

## 功能
快捷键绑定系统，负责解析、匹配和管理用户自定义快捷键。

## 文件说明

- `defaultBindings.ts` - 默认快捷键绑定
- `KeybindingContext.tsx` - 快捷键上下文
- `KeybindingProviderSetup.tsx` - 快捷键提供者设置
- `loadUserBindings.ts` - 加载用户快捷键
- `match.ts` - 快捷键匹配
- `parser.ts` - 快捷键解析器
- `reservedShortcuts.ts` - 保留快捷键
- `resolver.ts` - 快捷键解析
- `schema.ts` - 快捷键 schema
- `shortcutFormat.ts` - 快捷键格式
- `template.ts` - 快捷键模板
- `useKeybinding.ts` - 快捷键 hook
- `useShortcutDisplay.ts` - 快捷键显示 hook
- `validate.ts` - 快捷键验证

## 核心概念

### 快捷键解析
将用户输入的快捷键表示（如 `Ctrl+C`, `Cmd+Shift+P`）解析为内部结构。

### 快捷键匹配
- 支持单键快捷键
- 支持组合键（多修饰符）
- 支持键序列

### 保留快捷键
系统保留的快捷键不可被用户覆盖，如：
- 退出程序
- 中断当前操作

### 快捷键上下文
通过 React Context 提供快捷键状态和管理能力。

### 用户配置
支持用户自定义快捷键配置，从配置文件加载。
