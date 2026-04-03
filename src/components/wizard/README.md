# wizard/

## 功能
向导系统组件，提供步骤式对话框框架。

## 组件列表

- `WizardProvider.tsx` - 向导 Provider（18KB）
- `WizardDialogLayout.tsx` - 向导对话框布局
- `WizardNavigationFooter.tsx` - 向导导航页脚
- `useWizard.ts` - 向导 Hook
- `index.ts` - 导出

## 重要组件

### WizardProvider
向导上下文 Provider，管理向导的状态和导航。

### WizardDialogLayout
统一的向导对话框布局，包含：
- 标题区域
- 内容区域
- 导航按钮（上一步/下一步/完成）

## 使用方式
Wizard 系统被 `agents/new-agent-creation/` 中的创建向导使用。
