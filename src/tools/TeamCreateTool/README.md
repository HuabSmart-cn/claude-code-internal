# TeamCreateTool

## 功能

创建 agent 团队（Swarm 模式）。

## 核心文件

- `TeamCreateTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词
- `UI.tsx` - 渲染组件

## 关键类型/函数

```typescript
interface TeamCreateInput {
  team_name: string          // 团队名称
  description?: string       // 团队描述
  agent_type?: string        // 团队领导类型
}
```

## 对应命令/用途

TeamCreateTool 用于创建多代理协作团队。

**条件**：仅在 `isAgentSwarmsEnabled()` 时可用。

**相关工具**：TeamDeleteTool, SendMessageTool
