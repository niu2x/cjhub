# 输出格式：tuiqiao-auto-plan

## 执行流程

1. 读取 `requirement.md` 确认需求已定义
2. 初始化迭代计数器 `iteration = 0`
3. 循环执行（最大 5 次）：
   - `iteration++`
   - 使用 Task 工具启动子 Agent 执行 `tuiqiao-plan <需求ID>`
   - 等待子 Agent 完成
   - 使用 Task 工具启动子 Agent 执行 `tuiqiao-review <需求ID>`
   - 等待子 Agent 完成
   - 读取 `plan_review.md` 获取评审结论
   - 若结论为"可执行"或"有条件可执行"，退出循环
   - 否则继续迭代（修订方案）
4. 输出迭代汇总

---

## 终端输出格式

### 成功收敛时

```markdown
## tuiqiao-auto-plan 完成 - YYYY-MM-DD HH:mm

### 需求ID
RQ-xxx

### 迭代过程
| 轮次 | Plan | Review | 结论 |
|------|------|--------|------|
| 1 | 完成 | 完成 | 需修订 |
| 2 | 完成 | 完成 | 可执行 |

### 最终状态
- 迭代次数：2
- 评审结论：可执行
- 方案文件：design.md

### 下一步
建议执行：tuiqiao-apply RQ-xxx
```

### 达到最大迭代时

```markdown
## tuiqiao-auto-plan 未收敛 - YYYY-MM-DD HH:mm

### 需求ID
RQ-xxx

### 迭代过程
| 轮次 | Plan | Review | 结论 |
|------|------|--------|------|
| 1 | 完成 | 完成 | 需修订 |
| 2 | 完成 | 完成 | 需修订 |
| 3 | 完成 | 完成 | 需修订 |
| 4 | 完成 | 完成 | 需修订 |
| 5 | 完成 | 完成 | 需修订 |

### 警告
达到最大迭代次数（5次）仍未收敛

### 建议
手动检查 plan_review.md，确认问题根源后重新执行
```

---

## 子 Agent 调用规范

**Plan 阶段**：
```
Task(
  description="执行 tuiqiao-plan",
  prompt="tuiqiao-plan <需求ID>",
  subagent_type="general"
)
```

**Review 阶段**：
```
Task(
  description="执行 tuiqiao-review",
  prompt="tuiqiao-review <需求ID>",
  subagent_type="general"
)
```

**关键约束**：
- 每次迭代使用新的子 Agent（不复用）
- 必须等待子 Agent 完成后再启动下一个
- 读取评审结论时，检查 `plan_review.md` 最新记录

---

## 评审结论判定

| 评审结论 | 处理 |
|----------|------|
| 可执行 | 退出循环，输出成功 |
| 有条件可执行 | 退出循环，输出成功 |
| 不可执行 | 继续迭代，修订方案 |

---

## 异常处理

| 情况 | 处理方式 |
|------|----------|
| 子 Agent 执行失败 | 停止流程，输出失败原因 |
| 需求未定义 | 停止并提示先执行 tuiqiao-new |
| 达到最大迭代次数 | 输出警告，保持当前状态（方案待修订），建议手动检查 |

---

## 输出到

| 文件 | 写入方式 |
|------|----------|
| design.md | 由子 Agent 覆盖 |
| plan_review.md | 由子 Agent 追加 |
| meta.json | 覆盖（更新状态） |
