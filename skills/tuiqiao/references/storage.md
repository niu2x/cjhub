# 外部文件与状态管理

## 工作区

| 路径 | 用途 |
|------|------|
| `./.tuiqiao/` | 根目录 |
| `./.tuiqiao/index.json` | 需求索引 |
| `./.tuiqiao/requirements/<requirement_id>/` | 单需求目录 |

## requirement_id 规范

格式：`RQ-YYYYMMDD-HHMMSS`

---

## 单需求文件清单

| 文件 | 用途 |
|------|------|
| requirement.md | 需求定义与验收标准 |
| design.md | 执行方案与Task List |
| plan_review.md | 评审记录（追加写入） |
| execution.md | 执行记录与Task状态 |
| acceptance.md | 验收过程与结论 |
| acceptance_feedback.md | 验收不通过意见 |
| handoff.md | 跨会话接手说明 |
| meta.json | 元数据与当前状态 |

**新建需求时必须创建以上 8 个文件**，避免后续流程缺档。

---

## index.json 规则

```json
{
  "id": "RQ-xxx",
  "name": "<需求名称>",
  "status": "<当前状态>",
  "path": ".tuiqiao/requirements/RQ-xxx/",
  "created_at": "YYYY-MM-DD HH:mm",
  "updated_at": "YYYY-MM-DD HH:mm",
  "archived_at": "YYYY-MM-DD HH:mm",  // 验收通过时写入
  "final_status": "验收通过"           // 验收通过时写入
}
```

- 必须保存全部历史需求，不仅是进行中需求。
- 需求结束时写入 `archived_at` + `final_status`。

---

## Task状态枚举（严格）

`execution.md` 中只允许：

| 状态 | 含义 |
|------|------|
| todo | 待执行 |
| in_progress | 执行中 |
| done | 已完成 |
| blocked | 被阻塞 |

**禁止 `skipped`**：若Task不执行，必须修订 `design.md`，并在 `plan_review.md` 记录原因。

---

## 会话独立检查

以下动作必须满足"新会话仅读文档即可执行"：

- `tuiqiao-plan`
- `tuiqiao-review`
- `tuiqiao-apply-task`
- `tuiqiao-accept`

若发现关键信息仅存在对话中，先补文档再继续。
