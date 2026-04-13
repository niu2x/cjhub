# 输出格式：alexis-apply-step

## 输出到

| 文件 | 写入方式 |
|------|----------|
| execution.md | 追加 |
| meta.json | 覆盖 |

---

## 单步执行结果（终端输出 + execution.md）

```markdown
### Task-XX 执行记录 - YYYY-MM-DD HH:mm

## 前序校验
- 结论：<通过/不通过>
- 说明：<阻塞的Task或"无阻塞">

## 执行动作
<具体执行的操作>

## 产出
- 路径：<产物文件路径>
- 内容：<产物描述>

## 验收
- 结果：<通过/不通过>
- 依据：<验收条件核对结果>

## 下一步
建议执行：alexis-apply-step RQ-xxx Task-YY
```

---

## 前序阻塞时输出

```markdown
### Task-XX 执行失败 - YYYY-MM-DD HH:mm

## 前序校验
- 结论：不通过
- 阻塞清单：
  - Task-AA：未完成
  - Task-BB：未完成

## 建议
先完成前序Task后再执行本Task
```

---

## execution.md 初始格式

```markdown
# 执行记录

## 需求ID
RQ-xxx

## Task状态
| Task | 状态 | 完成时间 |
|------|------|----------|
| Task-01 | todo | - |
| Task-02 | todo | - |

---

## 执行日志
<追加区域>
```

---

## Task状态更新规则

执行成功后更新 Task状态表：
- 状态改为 `done`
- 完成时间填入当前时间
