# interactiveHelpers.tsx

## 文件概述
**路径**: `src/interactiveHelpers.tsx`
**功能**: 交互式辅助函数集合，包括对话框渲染、错误处理和应用退出管理
**重要程度**: ★★★★★

---

## 核心概念
### showDialog
基础对话框渲染函数，返回 Promise。

### showSetupDialog
包装在 `AppStateProvider` 和 `KeybindingSetup` 中的对话框。

### renderAndRun
渲染主 UI 并等待退出。

### exitWithMessage / exitWithError
通过 Ink 渲染消息后退出进程。

---

## 主要函数
```typescript
/**
 * 显示对话框
 */
function showDialog<T>(
  root: Root,
  renderer: (done: (result: T) => void) => React.ReactNode
): Promise<T>

/**
 * 显示设置对话框（包含 AppStateProvider 和 KeybindingSetup）
 */
function showSetupDialog<T>(
  root: Root,
  renderer: (done: (result: T) => void) => React.ReactNode,
  options?: { onChangeAppState?: typeof onChangeAppState }
): Promise<T>

/**
 * 渲染主 UI 并运行直到退出
 */
async function renderAndRun(root: Root, element: React.ReactNode): Promise<void>

/**
 * 显示消息后退出
 */
async function exitWithMessage(
  root: Root,
  message: string,
  options?: { color?: TextProps['color']; exitCode?: number; beforeExit?: () => Promise<void> }
): Promise<never>

/**
 * 显示错误消息后退出
 */
async function exitWithError(
  root: Root,
  message: string,
  beforeExit?: () => Promise<void>
): Promise<never>

/**
 * 显示设置屏幕（onboarding、trust dialog 等）
 */
async function showSetupScreens(
  root: Root,
  permissionMode: PermissionMode,
  allowDangerouslySkipPermissions: boolean,
  commands?: Command[],
  claudeInChrome?: boolean,
  devChannels?: ChannelEntry[]
): Promise<boolean>
```

---

## 与其他模块的关系
- 调用：
  - `ink.ts` - 渲染
  - `state/AppState.js` - 状态管理
  - `keybindings/KeybindingProviderSetup.js` - 键绑定
  - `components/` - 各种对话框组件
- 被调用：
  - `main.tsx` - 主入口
  - `dialogLaunchers.tsx` - 对话启动器
  - `replLauncher.tsx` - REPL 启动

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Interactive helpers | 交互辅助函数 |
| Dialog | 对话框 |
| Setup | 设置 |
| Render | 渲染 |
| Exit | 退出 |
| Onboarding | 入门引导 |
| Trust dialog | 信任对话框 |
