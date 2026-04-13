# 输出格式：tuiqiao-apply

## 执行流程

1. 读取 `design.md` 获取 Task List
2. 读取 `execution.md` 获取 Task 状态
3. 筛选状态为 `todo` 的 Task
4. 按顺序串行执行每个 Task：
   - 使用 Task 工具启动子 Agent
   - 子 Agent 执行 `tuiqiao-apply-task <需求ID> <TaskID>`
   - 若执行失败，停止流程，后续 Task 标记为 blocked
   - 若执行成功，继续下一个 Task
5. 全部完成后输出汇总

---

## 终端输出格式

```markdown
## tuiqiao-apply 执行汇总 - YYYY-MM-DD HH:mm

### 需求ID
RQ-xxx

### 执行顺序
| 序号 | Task | 状态 | 执行结果 |
|------|------|------|----------|
| 1 | Task-01 | done | 通过 |
| 2 | Task-02 | done | 通过 |
| ... | ... | ... | ... |

### 汇总
- 总Task数：N
- 成功：M
- 失败：K
- 跳过：L（blocked）

### 下一步
建议执行：tuiqiao-accept RQ-xxx
```

---

## 执行中断时输出

```markdown
## tuiqiao-apply 执行中断 - YYYY-MM-DD HH:mm

### 需求ID
RQ-xxx

### 执行顺序
| 序号 | Task | 状态 | 执行结果 |
|------|------|------|----------|
| 1 | Task-01 | done | 通过 |
| 2 | Task-02 | failed | 失败：xxx原因 |
| 3 | Task-03 | blocked | 前序Task失败 |

### 中断原因
Task-02 执行失败：xxx原因

### 下一步
修复问题后重新执行：tuiqiao-apply RQ-xxx
```

---

## 子 Agent 调用规范

每个 Task 使用 Task 工具启动子 Agent：

```
Task(
  description="执行 Task-XX",
  prompt="tuiqiao-apply-task <需求ID> Task-XX",
  subagent_type="general"
)
```

**关键约束**：
- 必须等待子 Agent 完成后再启动下一个
- 若子 Agent 返回失败，停止执行并输出失败汇总
- 后续 Task 因前序依赖未满足，不应继续执行

---

## 异常处理

| 情况 | 处理方式 |
|------|----------|
| 子 Agent 执行失败 | 停止流程，记录失败原因，后续 Task 标记为 blocked |
| Task 状态为 in_progress | 跳过该 Task，输出提示，继续下一个 |
| Task 被阻塞 | 停止流程，输出阻塞原因 |
| 无待执行 Task | 输出"无待执行Task"并退出 |

---

## 输出到

| 文件 | 写入方式 |
|------|----------|
| execution.md | 由子 Agent 追加 |
| meta.json | 覆盖（更新状态） |
