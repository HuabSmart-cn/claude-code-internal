# review

## 功能
审查 Pull Request。

## 命令类型
`prompt`

## 使用方式
```
/review [PR number]
```

## 说明
使用 `gh` CLI 获取 PR 信息并对代码变更进行审查。

## ultrareview

深度代码审查功能，在 Claude Code Web 上运行，耗时约 10-20 分钟。

## 类型
`local-jsx` (用于渲染权限对话框)

## 启用条件
需要 `isUltrareviewEnabled()` 返回 true。
