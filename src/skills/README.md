# skills

## 功能
技能系统模块，提供可扩展的 slash commands 和自动化能力。

## 文件/子目录

### 核心文件
- `bundledSkills.ts` - 内置技能
- `loadSkillsDir.ts` - 技能目录加载 (34KB)
- `mcpSkillBuilders.ts` - MCP 技能构建器
- `bundled/` - 内置技能实现

### bundled/ - 内置技能
- `batch.ts` - 批量处理
- `claudeApi.ts` - Claude API 调用
- `claudeApiContent.ts` - API 内容处理
- `claudeInChrome.ts` - Chrome 集成
- `debug.ts` - 调试技能
- `index.ts` - 技能索引
- `keybindings.ts` - 快捷键技能
- `loop.ts` - 循环执行
- `loremIpsum.ts` - 占位文本生成
- `remember.ts` - 记忆技能
- `scheduleRemoteAgents.ts` - 远程 Agent 调度
- `simplify.ts` - 简化技能
- `skillify.ts` - 技能化工具
- `stuck.ts` - 卡住检测
- `updateConfig.ts` - 配置更新
- `verify.ts` - 验证技能
- `verifyContent.ts` - 内容验证

## 核心概念

### Slash Commands
以 `/` 开头的命令，扩展 Claude Code 的能力。

### 内置技能
开箱即用的技能，包括：
- **自动化**: loop, scheduleRemoteAgents
- **开发辅助**: simplify, verify, debug
- **内容处理**: batch, loremIpsum
- **集成**: claudeInChrome, updateConfig

### 技能加载
- 从指定目录加载自定义技能
- MCP 技能构建器支持
- 动态注册和卸载

### 技能类型
- **Command Skills**: 执行特定命令
- **Agent Skills**: 启动专用 Agent
- **Integration Skills**: 外部服务集成
