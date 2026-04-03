# compact

## 功能
清除对话历史但保留摘要。

## 命令类型
`local`

## 使用方式
```
/compact [instructions for summarization]
```

## 说明
压缩当前上下文，保留摘要信息以便继续对话。可选地提供自定义的摘要指令。

## 禁用条件
当 `DISABLE_COMPACT` 环境变量设置时禁用。
