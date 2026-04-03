# SkillTool

## 功能

执行已安装的 skill（技能）。

## 核心文件

- `SkillTool.ts` - 主工具实现
- `prompt.ts` - 提示词

## 关键类型/函数

```typescript
interface SkillToolInput {
  name: string               // skill 名称
  input?: string             // skill 输入
}
```

## 特性

- **Skill 目录发现** - 扫描 ~/.claude/skills 等目录
- **条件激活** - 支持基于路径的条件激活
- **插件支持** - 支持插件提供的 skill

## 对应命令/用途

SkillTool 用于执行用户安装的扩展技能。
