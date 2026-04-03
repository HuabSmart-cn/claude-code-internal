# permissions/

## 功能
权限请求系统，负责在执行危险操作前向用户请求授权。这是 Claude Code 安全模型的核心 UI 层。

支持多种权限类型：
- Bash 命令执行
- 文件读写
- 网络请求
- 计划模式操作
- MCP 服务器操作
- Sandbox 操作

## 组件列表

### 核心权限组件
- `PermissionPrompt.tsx` - 权限提示对话框（主组件）
- `PermissionRequest.tsx` - 权限请求组件
- `PermissionDialog.tsx` - 权限对话框容器
- `PermissionExplanation.tsx` - 权限说明
- `PermissionRuleExplanation.tsx` - 权限规则说明
- `PermissionDecisionDebugInfo.tsx` - 决策调试信息
- `FallbackPermissionRequest.tsx` - 回退权限请求

### 权限类型特定组件
- `BashPermissionRequest/` - Bash 权限请求
- `FileEditPermissionRequest/` - 文件编辑权限
- `FileWritePermissionRequest/` - 文件写入权限
- `FilesystemPermissionRequest/` - 文件系统权限
- `AskUserQuestionPermissionRequest/` - 提问权限
- `EnterPlanModePermissionRequest/` - 进入计划模式权限
- `ExitPlanModePermissionRequest/` - 退出计划模式权限
- `NotebookEditPermissionRequest/` - Notebook 编辑权限
- `SedEditPermissionRequest/` - Sed 编辑权限
- `SkillPermissionRequest/` - Skill 权限
- `WebFetchPermissionRequest/` - Web 请求权限
- `ComputerUseApproval/` - 计算机使用批准
- `PowerShellPermissionRequest/` - PowerShell 权限
- `SandboxPermissionRequest.tsx` - Sandbox 权限

### 文件权限对话框
- `FilePermissionDialog/` - 文件权限对话框
  - `FilePermissionDialog.tsx` - 文件权限对话框主组件
  - `permissionOptions.tsx` - 权限选项
  - `useFilePermissionDialog.ts` - 对话框 Hook
  - `usePermissionHandler.ts` - 权限处理器 Hook
  - `ideDiffConfig.ts` - IDE 差异配置

### 权限规则管理 (rules/)
- `PermissionRuleList.tsx` - 权限规则列表（超大组件 118KB）
- `PermissionRuleInput.tsx` - 权限规则输入
- `AddPermissionRules.tsx` - 添加权限规则
- `AddWorkspaceDirectory.tsx` - 添加工作目录
- `RemoveWorkspaceDirectory.tsx` - 移除工作目录
- `PermissionRuleDescription.tsx` - 规则描述
- `RecentDenialsTab.tsx` - 最近拒绝记录
- `WorkspaceTab.tsx` - 工作区标签

### 辅助组件
- `PermissionRequestTitle.tsx` - 权限请求标题
- `WorkerBadge.tsx` - Worker 徽章
- `WorkerPendingPermission.tsx` - 待处理权限
- `hooks.ts` - 权限相关 Hooks
- `shellPermissionHelpers.tsx` - Shell 权限辅助函数
- `useShellPermissionFeedback.ts` - Shell 权限反馈 Hook
- `utils.ts` - 工具函数

## 重要组件

### PermissionPrompt
权限请求的核心对话框组件，展示：
- 请求的权限类型和详细信息
- 风险说明
- 允许/拒绝选项
- 记住决定选项

### PermissionRuleList
权限规则管理界面，允许用户：
- 查看已配置的权限规则
- 添加新的权限规则
- 为特定路径或操作设置默认行为

### ElicitationDialog
权限获取对话框（179KB），是最大的权限相关组件，处理复杂的权限请求流程。
