# hooks/ - 钩子系统

## 功能概述

`hooks/` 目录实现 Claude Code 的钩子系统，允许在各种事件发生时执行自定义逻辑。

## 文件列表

```
hooks/
├── AsyncHookRegistry.ts       # 异步钩子注册表
├── execAgentHook.ts          # 执行 Agent 钩子
├── execHttpHook.ts           # 执行 HTTP 钩子
├── execPromptHook.ts         # 执行提示钩子
├── fileChangedWatcher.ts     # 文件变化监视
├── hookEvents.ts            # 钩子事件定义
├── hookHelpers.ts           # 钩子辅助函数
├── hooksConfigManager.ts    # 钩子配置管理
├── hooksConfigSnapshot.ts    # 配置快照
├── hooksSettings.ts         # 钩子设置
├── postSamplingHooks.ts     # 采样后钩子
├── registerFrontmatterHooks.ts  # 前置matter钩子
├── registerSkillHooks.ts    # 技能钩子注册
├── sessionHooks.ts          # 会话钩子
├── skillImprovement.ts      # 技能改进
├── ssrfGuard.ts             # SSRF 防护
└── apiQueryHookHelper.ts    # API 查询辅助
```

## 钩子类型

### Pre-Task Hooks
- `preTask` - 任务执行前

### Post-Task Hooks
- `postTask` - 任务执行后

### Prompt Hooks
- `prePrompt` - 提示生成前
- `postPrompt` - 提示生成后

### Sampling Hooks
- `postSampling` - 采样后

### HTTP Hooks
- `http` - HTTP 请求钩子

### Agent Hooks
- `agent` - Agent 执行钩子

## 配置格式

钩子通过 `~/.claude/settings.json` 配置：

```json
{
  "hooks": {
    "preTask": [
      {
        "provider": "shell",
        "command": "echo 'Task starting'"
      }
    ]
  }
}
```

## 安全机制

### SSRF Guard
`ssrfGuard.ts` - 防止服务器端请求伪造攻击。

## 异步钩子

`AsyncHookRegistry.ts` 管理异步钩子的注册和执行。
