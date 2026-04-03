# services/lsp - 语言服务器协议

## 功能

LSP 服务集成语言服务器，提供代码诊断、补全、跳转到定义等功能。

## 文件列表

| 文件 | 功能 |
|------|------|
| `LSPClient.ts` | LSP 客户端封装 |
| `LSPServerInstance.ts` | LSP 服务器实例管理 |
| `LSPServerManager.ts` | 服务器生命周期管理 |
| `LSPDiagnosticRegistry.ts` | 诊断结果注册 |
| `manager.ts` | 总体管理器 |
| `passiveFeedback.ts` | 被动反馈收集 |
| `prompts.ts` | LSP 相关提示词 |

## 支持的语言

通过配置不同的 LSP 服务器实现:
- TypeScript/JavaScript → `typescript-language-server`
- Python → `pylsp`
- Rust → `rust-analyzer`
- Go → `gopls`
- 以及其他支持 LSP 的语言

## 功能列表

| 功能 | 说明 |
|------|------|
| 诊断 | 语法错误、类型错误、lint 问题 |
| 补全 | 代码自动补全 |
| 跳转到定义 | Go to Definition |
| 查找引用 | Find References |
| 重命名 | Rename Symbol |
| 悬停信息 | Hover Documentation |

## 配置

```json
{
  "lsp": {
    "servers": {
      "typescript": {
        "command": "typescript-language-server",
        "args": ["--stdio"],
        "rootIndicators": ["tsconfig.json", "package.json"]
      }
    }
  }
}
```

## 诊断流程

```
代码变更
    ↓
LSP Server 诊断
    ↓
LSPDiagnosticRegistry 收集
    ↓
UI 展示诊断标记
```
