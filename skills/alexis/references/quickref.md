# 指令速查表

## 指令总览

| 指令 | 作用 | 读取文件 | 输出文件 | 模板 |
|------|------|----------|----------|------|
| alexis-new | 新建需求 | 无 | requirement.md, meta.json, index.json | template-new.md |
| alexis-plan | 起草/修订方案 | requirement.md, design.md, plan_review.md | design.md, plan_review.md, handoff.md, meta.json | template-plan.md |
| alexis-review | 评审方案 | requirement.md, design.md, plan_review.md | plan_review.md, meta.json | template-review.md |
| alexis-apply-step | 执行单Task | design.md, execution.md | execution.md, meta.json | template-apply.md |
| alexis-accept | 最终验收 | requirement.md, design.md, execution.md | acceptance.md, meta.json, acceptance_feedback.md | template-accept.md |

---

## 指令用法

```
alexis-new <需求简述>
alexis-plan <需求ID> [补充约束]
alexis-review <需求ID> [评审重点]
alexis-apply-step <需求ID> <TaskID>
alexis-accept <需求ID>
```

---

## 写入方式说明

| 方式 | 含义 |
|------|------|
| 覆盖 | 替换文件全部内容 |
| 追加 | 在文件末尾追加内容 |

---

## 文件用途

| 文件 | 用途 |
|------|------|
| requirement.md | 需求定义与验收标准 |
| design.md | 执行方案与Task List |
| plan_review.md | 评审记录（追加写入） |
| execution.md | 执行记录与Task状态 |
| acceptance.md | 验收过程与结论 |
| acceptance_feedback.md | 验收不通过意见 |
| handoff.md | 跨会话接手说明 |
| meta.json | 当前状态与元数据 |
| index.json | 需求索引 |

---

## 执行前检查

每个指令执行前必须：

1. 校验参数完整性
2. 读取所需文件
3. 检查文件存在性
4. 缺失时停止并提示
