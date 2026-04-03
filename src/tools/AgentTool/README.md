# AgentTool

## 功能

在 Claude Code 中启动和管理**子代理（Subagent）**的核心工具。允许主代理创建异步后台任务来处理复杂的多步骤工作。

## 核心文件

- `AgentTool.tsx` - 主工具实现，负责代理的启动、生命周期管理和结果收集
- `runAgent.ts` - 代理执行逻辑
- `forkSubagent.ts` - Fork 模式子代理
- `resumeAgent.ts` - 恢复已暂停的代理
- `prompt.ts` - 代理提示词
- `UI.tsx` - 渲染组件
- `constants.ts` - 常量定义
- `loadAgentsDir.ts` - 加载 agents 目录

## 内置子代理 (built-in/)

| 文件 | 功能 |
|------|------|
| `generalPurposeAgent.ts` | 通用目的代理 |
| `planAgent.ts` | 计划模式代理 |
| `exploreAgent.ts` | 探索代理 |
| `verificationAgent.ts` | 验证代理 |
| `claudeCodeGuideAgent.ts` | Claude Code 指南代理 |
| `statuslineSetup.ts` | 状态栏设置 |

## 关键类型/函数

```typescript
// 启动代理
const result = await AgentTool.call(args, context, canUseTool, parentMessage, onProgress)

// 关键参数
interface AgentToolInput {
  tool: string           // 代理名称
  agentType?: string     // 代理类型
  prompt: string         // 代理提示
  // ... 其他参数
}
```

## 对应命令/用途

AgentTool 是 Claude Code 多代理架构的核心，允许：
- 创建后台任务
- 并行执行多个代理
- 团队协作（TeamCreate/TeamDelete）

**重要工具**：AgentTool 是实现复杂工作流和并行处理的关键工具。
