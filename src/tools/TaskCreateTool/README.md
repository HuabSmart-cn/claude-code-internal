# TaskCreateTool

## 功能

创建新任务（TodoV2 模式）。

## 核心文件

- `TaskCreateTool.ts` - 主工具实现
- `constants.ts` - 常量定义
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface TaskCreateInput {
  subject: string            // 任务标题
  description: string        // 任务描述
  activeForm?: string        // 进行中的描述
  metadata?: Record<string, unknown>  // 附加元数据
}
```

## 特性

- **任务依赖** - 通过 TaskUpdate 设置 blockedBy
- **所有者分配** - 任务可分配给特定 agent
- **元数据** - 支持任意元数据

## 对应命令/用途

TaskCreate 用于在团队协作中创建结构化任务。

**条件**：仅在 `isTodoV2Enabled()` 时可用。
