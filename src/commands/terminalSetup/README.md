# terminal-setup

## 功能
终端设置和键盘配置。

## 命令类型
`local-jsx`

## 使用方式
```
/terminal-setup
```

## 说明
根据终端类型提供特定的键盘快捷键设置：
- Apple Terminal: 启用 Option+Enter 换行和可视化铃声
- 其他终端: 安装 Shift+Enter 换行绑定

## 隐藏条件
对于原生支持 CSI u / Kitty 键盘协议的终端（Ghostty、Kitty、iTerm2、WezTerm）隐藏。
