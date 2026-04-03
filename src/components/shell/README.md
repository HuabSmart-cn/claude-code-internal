# shell/

## 功能
Shell 输出展示组件，负责渲染终端命令的输入输出。

## 组件列表

- `ShellProgressMessage.tsx` - Shell 进度消息
- `ShellDetailDialog.tsx` - Shell 详情对话框
- `OutputLine.tsx` - 输出行组件
- `ExpandShellOutputContext.tsx` - 展开上下文
- `ShellTimeDisplay.tsx` - 时间显示

## 重要组件

### OutputLine
单行输出渲染，支持：
- 标准输出/错误区分
- ANSI 颜色解析
- 超长输出截断

### ShellProgressMessage
Shell 执行的进度展示。
