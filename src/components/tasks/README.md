# tasks/

## 功能
任务和后台进程管理 UI，负责展示长时间运行的任务、远程会话和 Shell 进度。

## 组件列表

### 任务对话框
- `BackgroundTasksDialog.tsx` - 后台任务对话框（116KB）
- `RemoteSessionDetailDialog.tsx` - 远程会话详情（96KB）
- `ShellDetailDialog.tsx` - Shell 详情（39KB）
- `DreamDetailDialog.tsx` - Dream 详情
- `AsyncAgentDetailDialog.tsx` - 异步 Agent 详情

### 任务组件
- `BackgroundTask.tsx` - 后台任务组件（31KB）
- `BackgroundTaskStatus.tsx` - 后台任务状态（43KB）
- `ShellProgress.tsx` - Shell 进度
- `RemoteSessionProgress.tsx` - 远程会话进度

### 辅助组件
- `InProcessTeammateDetailDialog.tsx` - 队友详情对话框
- `renderToolActivity.tsx` - 工具活动渲染
- `taskStatusUtils.tsx` - 任务状态工具

## 重要组件

### BackgroundTasksDialog
后台任务管理界面：
- 列出所有进行中的后台任务
- 显示任务进度
- 允许取消或查看详情

### RemoteSessionDetailDialog
远程会话详情展示，包括：
- 会话状态
- 执行的活动
- 输出日志

### ShellProgress
Shell 命令执行进度展示，用于长时间运行的命令。
