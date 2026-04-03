# fast

## 功能
切换快速模式。

## 命令类型
`local-jsx`

## 使用方式
```
/fast [on|off]
```

## 可用性
- `claude-ai`
- `console`

## 说明
启用后，Claude Code 将仅使用快速模型（如 Haiku）以减少延迟和成本。

## 启用条件
需要 `isFastModeEnabled()` 返回 true。
