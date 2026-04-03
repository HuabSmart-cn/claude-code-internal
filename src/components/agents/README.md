# agents/

## 功能
Agent 管理系统，负责 Agent 的创建、编辑、选择和列表展示。

## 组件列表

### 核心组件
- `AgentsMenu.tsx` - Agent 菜单（70KB）
- `AgentsList.tsx` - Agent 列表（52KB）
- `AgentDetail.tsx` - Agent 详情
- `AgentEditor.tsx` - Agent 编辑器
- `ToolSelector.tsx` - 工具选择器（64KB）
- `ModelSelector.tsx` - 模型选择器
- `ColorPicker.tsx` - 颜色选择器
- `AgentNavigationFooter.tsx` - 导航页脚
- `Byline.tsx` - Agent 描述组件

### Agent 创建向导
- `new-agent-creation/`
  - `CreateAgentWizard.tsx` - 创建向导主组件
  - `wizard-steps/` - 向导步骤
    - `TypeStep.tsx` - 类型步骤
    - `DescriptionStep.tsx` - 描述步骤
    - `PromptStep.tsx` - 提示词步骤
    - `ToolsStep.tsx` - 工具步骤
    - `ModelStep.tsx` - 模型步骤
    - `MemoryStep.tsx` - 记忆步骤
    - `ColorStep.tsx` - 颜色步骤
    - `LocationStep.tsx` - 位置步骤
    - `MethodStep.tsx` - 方法步骤
    - `GenerateStep.tsx` - 生成步骤
    - `ConfirmStep.tsx` - 确认步骤
    - `ConfirmStepWrapper.tsx` - 确认步骤包装

### 工具函数
- `agentFileUtils.ts` - Agent 文件工具
- `generateAgent.ts` - Agent 生成
- `validateAgent.ts` - Agent 验证
- `utils.ts` - 通用工具
- `color.ts` - 颜色工具

### 类型定义
- `types.ts` - 类型定义（ModeState, AgentValidationResult）

## 重要组件

### AgentsMenu
主 Agent 菜单组件，提供：
- Agent 列表展示
- 创建新 Agent
- 编辑现有 Agent
- 删除 Agent

### CreateAgentWizard
完整的 Agent 创建向导，采用步骤式流程：
1. 选择 Agent 类型
2. 填写描述
3. 配置提示词
4. 选择工具
5. 选择模型
6. 配置记忆
7. 选择颜色
8. 选择位置
9. 确认创建

### ToolSelector
工具选择界面，允许用户为 Agent 选择可用的工具集合。
