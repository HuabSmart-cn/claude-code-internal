# BriefTool

## 功能

向用户发送消息（主动通知）。

## 核心文件

- `BriefTool.ts` - 主工具实现
- `attachments.ts` - 附件处理
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface BriefInput {
  message: string            // 消息内容（支持 markdown）
  attachments?: string[]     // 附件路径
  status?: 'normal' | 'proactive'  // 状态
}
```

## 特性

- **Markdown 支持** - 消息支持格式化
- **附件支持** - 可附加文件
- **主动状态** - 用于用户未主动请求的通知

## 对应命令/用途

BriefTool 用于 AI 向用户发送消息或通知。
