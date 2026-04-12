# Agent Skill Repository

这个仓库用于集中管理可安装的 Agent Skills。

## 目录约定

- `skills/<skill-name>/SKILL.md`：每个技能的入口说明文件。
- `skills/<skill-name>/`：技能相关的脚本、模板、资源文件。

## 快速开始

1. 复制模板目录：

   ```bash
   cp -r skills/_template skills/my-skill
   ```

2. 编辑 `skills/my-skill/SKILL.md`，写清楚：
   - 适用场景（何时触发）
   - 执行步骤（如何做）
   - 输入/输出约定（返回什么）

3. 根据需要新增脚本或资源文件。

## 提交建议

- 一个技能一个目录，目录名使用短横线风格（例如：`db-migration-helper`）。
- 保持 `SKILL.md` 结构清晰、可执行、可复用。
