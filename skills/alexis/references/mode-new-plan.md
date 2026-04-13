# 模式 A/B：新建需求与起草方案

## A. alexis-new

触发：`alexis-new <需求简述>`

### 执行步骤

1. 提炼需求名称（8-20 个中文字符，避免空泛词）。
2. 生成 `requirement_id`（格式：RQ-YYYYMMDD-HHMMSS）。
3. 创建需求目录 `./.alexis/requirements/<requirement_id>/`。
4. 创建 8 个文件（见 `storage.md`）。
5. 在 `index.json` 注册需求。
6. 回显建档结果（ID、名称、路径）。
7. 进入需求澄清（苏格拉底提问，每轮最多 3 问）。

### 需求澄清停止条件

以下 6 项全部明确才停止提问：

1. 目标
2. 范围（包含/不包含）
3. 约束
4. 优先级
5. 交付物
6. 验收标准

满足后：

1. 输出需求简报供用户确认（使用 `template-new.md` 格式）。
2. 用户确认后，更新 `requirement.md`。
3. 更新 `meta.json` 状态为 `需求已确认`。

---

## B. alexis-plan

触发：`alexis-plan <需求ID> [补充约束]`

### 基础输入

- `requirement.md`
- `design.md`（若存在）

### B1. 评审后修订分支

若已有 `plan_review.md` 且最近有评审记录：

1. 必读 `requirement.md` `design.md` `plan_review.md`。
2. 对评审意见逐条回应（采纳/不采纳 + 理由）。
3. 使用 `template-plan.md` 中的"修订回应"格式输出。
4. 回应结果追加写入 `plan_review.md`。
5. 更新 `meta.json` 状态。

### B2. 验收失败重规划分支

若最近验收为不通过：

1. 必读 `requirement.md` `design.md` `acceptance_feedback.md`。
2. 将每条验收不通过意见映射到计划改进项。
3. 使用 `template-plan.md` 中的"验收失败重规划"格式输出。
4. 映射结果追加写入 `plan_review.md`。
5. 更新 `meta.json` 状态。

### B3. 方案落库规则

1. 先输出草案，不立即写 `design.md`。
2. 用户确认后落库（覆盖 `design.md`）。
3. 更新 `meta.json` 状态为 `方案已确认`。
4. 更新 `handoff.md`，保证新会话可直接接手。

---

## Task List 质量要求

每个 Task 必须包含：

| 字段 | 含义 |
|------|------|
| 输入 | 前置完成后的当前状态 |
| 输出 | 可见产物 |
| 验收 | 客观可判断的条件 |
| 执行 | 最小上下文：文件/命令/依赖 |

附加约束：

- 默认 8-15 个 Task；小需求可少于 8。
- Task 必须局部化、可独立委派。
- 禁止"参考上文/刚才讨论"这类隐式上下文表达。
