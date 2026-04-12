# 指令与路由

## 指令总览

1. `alexis-new <需求简述>`
2. `alexis-plan <需求ID> [补充约束]`
3. `alexis-review <需求ID> [评审重点]`
4. `alexis-apply-step <需求ID> <TaskID>`
5. `alexis-accept <需求ID>`

## 路由规则

- 仅按快捷指令路由，不按自然语言猜测模式。
- 参数缺失时停止执行，并返回用法示例。
- 若用户只说“用 alexis”但未给指令，返回指令清单并要求重试。

## 用法示例

- `alexis-new 做一个会员积分到期提醒系统`
- `alexis-plan RQ-20260412-101500 增加灰度发布约束`
- `alexis-review RQ-20260412-101500 重点看回滚与监控`
- `alexis-apply-step RQ-20260412-101500 Task-03`
- `alexis-accept RQ-20260412-101500`

## 非法输入响应模板

当输入不合法时，返回：

1. 错误原因（缺哪个参数/格式不对）。
2. 可用指令列表。
3. 1-2 条正确示例。
