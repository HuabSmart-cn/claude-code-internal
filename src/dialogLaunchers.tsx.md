# dialogLaunchers.tsx

## 文件概述
**路径**: `src/dialogLaunchers.tsx`
**功能**: 提供各种设置对话框的动态导入和启动器
**重要程度**: ★★★★☆

---

## 核心概念
### 对话启动器模式
将大型 React 组件的动态导入延迟到实际需要时，减少初始加载时间。

每个启动器函数：
1. 动态导入组件
2. 使用 `showSetupDialog` 或 `renderAndRun` 渲染
3. 处理完成/取消回调

---

## 主要启动器函数
```typescript
/**
 * 快照更新对话框（Agent 内存快照更新提示）
 */
function launchSnapshotUpdateDialog(
  root: Root,
  props: { agentType: string; scope: AgentMemoryScope; snapshotTimestamp: string }
): Promise<'merge' | 'keep' | 'replace'>

/**
 * 无效设置对话框
 */
function launchInvalidSettingsDialog(
  root: Root,
  props: { settingsErrors: ValidationError[]; onExit: () => void }
): Promise<void>

/**
 * 助手会话选择器
 */
function launchAssistantSessionChooser(
  root: Root,
  props: { sessions: AssistantSession[] }
): Promise<string | null>

/**
 * 助手安装向导
 */
function launchAssistantInstallWizard(root: Root): Promise<string | null>

/**
 * 传送恢复包装器
 */
function launchTeleportResumeWrapper(root: Root): Promise<TeleportRemoteResponse | null>

/**
 * 传送仓库不匹配对话框
 */
function launchTeleportRepoMismatchDialog(
  root: Root,
  props: { targetRepo: string; initialPaths: string[] }
): Promise<string | null>

/**
 * 恢复对话选择器
 */
function launchResumeChooser(
  root: Root,
  appProps: AppWrapperProps,
  worktreePathsPromise: Promise<string[]>,
  resumeProps: Omit<ResumeConversationProps, 'worktreePaths'>
): Promise<void>
```

---

## 与其他模块的关系
- 调用：
  - `interactiveHelpers.tsx` - showSetupDialog, renderAndRun
  - `components/` - 各种对话框组件
- 被调用：`main.tsx` - 在需要时启动各种对话框

---

## 英文对照词汇表
| English | 中文 |
|---------|------|
| Dialog launcher | 对话启动器 |
| Dynamic import | 动态导入 |
| Setup dialog | 设置对话框 |
| Snapshot | 快照 |
| Resume | 恢复 |
| Teleport | 传送 |
| Wizard | 向导 |
