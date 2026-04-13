# 模式 C/D：执行步骤与最终验收

## C. alexis-apply-step

触发：`alexis-apply-step <需求ID> <TaskID>`

只执行一个 Task，不做整包推进。

---

### 前序校验（强制）

1. 读取 `design.md`，确认 Task 存在且定义完整。
2. 读取 `execution.md`，确认前序 Task 全为 `done`。
3. 若有未完成前序，拒绝执行并给出阻塞清单。
4. 若目标 Task 已完成，不重复执行，返回已有产物信息。

---

### 执行与记录

执行时使用 `template-apply.md` 格式输出，写入 `execution.md`：

| 字段 | 内容 |
|------|------|
| TaskID | 执行的Task编号 |
| 前序校验 | 通过/不通过 + 说明 |
| 执行动作 | 具体操作 |
| 产出 | 产物路径和描述 |
| 验收 | 通过/不通过 + 依据 |
| 下一步 | 建议执行的Task |

同时更新 `meta.json` 的 `updated_at` 和状态。

---

## D. alexis-accept

触发：`alexis-accept <需求ID>`

---

### 验收前检查（强制）

1. 读取 `requirement.md`（原始目标 + 验收标准）。
2. 读取 `design.md`（完整 Task List）。
3. 读取 `execution.md`（Task 状态）。

---

### 双条件判定

验收通过必须同时满足：

| 条件 | 说明 |
|------|------|
| A | 所有 Task 均为 `done` |
| B | 整体达成原始需求目标 |

任一不满足 → 总体不通过。

---

### 落库规则

1. 使用 `template-accept.md` 格式输出验收报告。
2. 验收过程写入 `acceptance.md`。
3. 更新 `meta.json` 状态。
4. 若不通过，额外写 `acceptance_feedback.md`（整改意见）。
5. 若通过，更新 `index.json` 的 `archived_at` 和 `final_status`。
