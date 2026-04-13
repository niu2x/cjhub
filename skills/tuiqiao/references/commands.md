# 指令与路由

## 指令总览

| 指令 | 作用 |
|------|------|
| `tuiqiao-new <需求简述>` | 新建需求 |
| `tuiqiao-plan <需求ID> [补充约束]` | 起草/修订方案 |
| `tuiqiao-review <需求ID> [评审重点]` | 评审方案 |
| `tuiqiao-auto-plan <需求ID>` | 自动迭代规划评审直到通过 |
| `tuiqiao-apply-task <需求ID> <TaskID>` | 执行单Task |
| `tuiqiao-apply <需求ID>` | 执行所有未完成Task |
| `tuiqiao-accept <需求ID>` | 最终验收 |

---

## 用法示例

```
tuiqiao-new 做一个会员积分到期提醒系统
tuiqiao-plan RQ-20260412-101500 增加灰度发布约束
tuiqiao-review RQ-20260412-101500 重点看回滚与监控
tuiqiao-auto-plan RQ-20260412-101500
tuiqiao-apply-task RQ-20260412-101500 Task-03
tuiqiao-apply RQ-20260412-101500
tuiqiao-accept RQ-20260412-101500
```

---

## 路由规则

1. 仅按快捷指令路由，不按自然语言猜测模式。
2. 参数缺失时停止执行，并返回用法示例。
3. 若用户只说"用 tuiqiao"但未给指令，返回指令清单并要求重试。

---

## 非法输入响应

当输入不合法时，返回：

1. 错误原因（缺哪个参数/格式不对）。
2. 可用指令列表。
3. 1-2 条正确示例。
