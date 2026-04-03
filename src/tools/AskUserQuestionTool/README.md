# AskUserQuestionTool

## 功能

向用户提出多项选择问题。

## 核心文件

- `AskUserQuestionTool.tsx` - 主工具实现（React 组件）
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface AskUserQuestionInput {
  question: string           // 问题内容
  header: string             // 简短标签
  options: Array<{
    label: string            // 选项标签
    description: string      // 选项描述
    preview?: string         // 预览内容
  }>
  multiSelect?: boolean      // 是否多选
}
```

## 特性

- **选项限制** - 2-4 个选项
- **预览支持** - 选项可包含预览内容
- **多选支持** - 可选择多个选项
- **注释收集** - 收集用户备注

## 对应命令/用途

AskUserQuestionTool 用于需要用户做出选择的场景。
