# feedback

## 功能
提交关于 Claude Code 的反馈。

## 命令类型
`local-jsx`

## 使用方式
```
/feedback [report]
/bug [report]
```

## 别名
- `bug`

## 说明
向 Anthropic 提交关于 Claude Code 的反馈或问题报告。

## 禁用条件
在以下情况下禁用：
- 使用 Bedrock/Vertex/Foundry
- `DISABLE_FEEDBACK_COMMAND` 或 `DISABLE_BUG_COMMAND` 设置
- Essential Traffic Only 模式
- Ant 用户类型
- 策略不允许时
