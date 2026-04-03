# services/tools - 工具执行服务

## 功能

工具执行服务负责调用和管理 Claude Code 中的各种工具，包括 Bash、文件操作、编辑等。

## 文件列表

| 文件 | 功能 | 大小 |
|------|------|------|
| `toolExecution.ts` | 工具执行核心 | 60KB |
| `StreamingToolExecutor.ts` | 流式工具执行器 | 17KB |
| `toolHooks.ts` | 工具钩子系统 | 22KB |
| `toolOrchestration.ts` | 工具编排 | 5KB |

## 核心组件

### toolExecution.ts
主要工具执行逻辑:
- 工具调用验证
- 参数处理
- 结果格式化
- 错误处理

### StreamingToolExecutor.ts
流式执行支持:
- 支持长时间运行的工具
- 进度报告
- 中断支持

### toolHooks.ts
工具生命周期钩子:
- `preToolExecution` - 执行前
- `postToolExecution` - 执行后
- 错误处理钩子

## 执行流程

```
1. useCanUseTool() 权限检查
       ↓
2. toolExecution.ts 参数验证
       ↓
3. 找到对应工具实现
       ↓
4. StreamingToolExecutor 流式执行
       ↓
5. toolHooks 后置处理
       ↓
6. 返回结果给 Claude
```

## 工具类型

| 类别 | 示例 |
|------|------|
| 文件操作 | Read, Write, Edit |
| Shell | Bash, PowerShell |
| 编辑器 | Diff, Search |
| MCP | 外部 MCP 服务器工具 |
| 搜索 | WebSearch, FileSearch |

## 工具结果处理

```typescript
interface ToolResult {
  tool_use_id: string
  content: ContentBlock[]
  is_error?: boolean
  // 流式支持
  stream?: AsyncIterable<ToolProgress>
}
```
