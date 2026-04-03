# SendMessageTool

## 功能

向团队成员发送消息。

## 核心文件

- `SendMessageTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface SendMessageInput {
  teammate: string           // 收件人名称
  message: {
    type: 'message' | 'shutdown_request' | 'shutdown_response' |
          'plan_approval_response'
    content: string
    // ... 类型特定字段
  }
}
```

## 消息类型

- **message** - 普通消息
- **shutdown_request** - 关闭请求
- **shutdown_response** - 关闭响应
- **plan_approval_response** - 计划审批响应

## 对应命令/用途

SendMessageTool 用于团队成员之间的通信和协调。
