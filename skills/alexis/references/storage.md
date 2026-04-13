# 外部文件与状态管理

## 目标

确保所有必要信息文档化，支持跨会话继续执行。

## 工作区

- 根目录：`./.alexis/`
- 索引：`./.alexis/index.json`
- 需求目录：`./.alexis/requirements/<requirement_id>/`

## requirement_id 规范

- 格式：`RQ-YYYYMMDD-HHMMSS`

## index.json 规则

- 必须保存全部历史需求，不仅是进行中需求。
- 建议字段：`id` `name` `status` `path` `created_at` `updated_at` `archived_at` `final_status`
- 需求结束时写入：`archived_at` + `final_status`

## 单需求文件清单

1. `requirement.md`：需求定义与验收标准
2. `design.md`：执行方案与 Task List
3. `plan_review.md`：计划评审文档（结构见下方说明）
4. `execution.md`：执行记录与 Task 状态
5. `acceptance.md`：验收过程与结论
6. `acceptance_feedback.md`：验收不通过意见
7. `handoff.md`：跨会话接手说明
8. `meta.json`：元数据与当前状态

## plan_review.md 结构说明

该文档采用追加写入模式，包含以下区域：

1. **文档头部**：基本信息、版本历史、当前状态
2. **评审记录区**：存储所有评审记录（初次评审、复评）
3. **修订回应区**：存储对评审意见的回应
4. **验收失败改进区**：存储验收失败后的改进映射

详细结构参考 `templates.md` 中的"plan_review.md 文档结构"模板。

## 新建需求时必须创建

创建以上 8 个文件，避免后续流程缺档。

## Task 状态枚举（严格）

`execution.md` 中只允许：

- `todo`
- `in_progress`
- `done`
- `blocked`

不允许 `skipped`。若任务不执行，必须修订 `design.md`，并在 `plan_review.md` 记录原因。

## 会话独立检查

以下动作必须满足“新会话仅读文档即可执行”：

- `alexis-plan`
- `alexis-review`
- `alexis-apply-step`
- `alexis-accept`

若发现关键信息仅存在对话中，先补文档再继续。
