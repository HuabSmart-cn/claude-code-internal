# screens

## 功能
屏幕管理模块，包含主要界面的屏幕组件。

## 文件说明

- `Doctor.tsx` - Doctor 诊断界面 (73KB)
- `REPL.tsx` - REPL 主界面 (895KB) - 最大文件
- `ResumeConversation.tsx` - 恢复对话界面 (59KB)

## 核心概念

### REPL 界面
主要的交互界面，包含：
- 命令输入
- 输出显示
- 交互式辅助

### Doctor 界面
诊断工具界面，用于：
- 环境检测
- 配置检查
- 问题排查

### ResumeConversation 界面
恢复对话界面，处理：
- 历史会话加载
- 对话续接
- 上下文恢复

## 屏幕层级
REPL 是主屏幕，Doctor 和 ResumeConversation 是模态或子屏幕。
