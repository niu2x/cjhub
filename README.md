# Agent Skill Repository

这个仓库用于集中管理可安装的 Agent Skills。

## 目录约定

- `skills/<skill-name>/SKILL.md`：每个技能的入口说明文件。
- `skills/<skill-name>/`：技能相关的脚本、模板、资源文件。

## 快速开始

1. 创建技能目录与入口文件：

   ```bash
   mkdir -p skills/my-skill
   touch skills/my-skill/SKILL.md
   ```

2. 编辑 `skills/my-skill/SKILL.md`，写清楚：
   - 适用场景（何时触发）
   - 执行步骤（如何做）
   - 输入/输出约定（返回什么）

3. 根据需要新增脚本或资源文件。

## 技能列表

| 技能名称 | 简介 |
|---------|------|
| tuiqiao | 结构化需求管理技能，通过快捷指令实现需求澄清、计划起草、评审、执行、验收的完整闭环，支持跨会话继续。 |

## 提交建议

- 一个技能一个目录，目录名使用短横线风格（例如：`db-migration-helper`）。
- 保持 `SKILL.md` 结构清晰、可执行、可复用。
