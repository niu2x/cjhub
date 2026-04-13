# 输出格式：tuiqiao-new

## 输出到

| 文件 | 写入方式 |
|------|----------|
| requirement.md | 覆盖 |
| meta.json | 覆盖 |
| index.json | 追加 |

---

## 需求简报（终端输出）

```markdown
# 需求简报

## 目标
<一句话描述目标>

## 范围
- 包含：<列出包含内容>
- 不包含：<列出不含内容>

## 约束
<技术/时间/资源约束>

## 验收标准
<可客观判断的标准，每条一行>

## 未决事项
<若无写"无">
```

---

## requirement.md 格式

```markdown
# 需求定义

## 基本信息
- ID：RQ-YYYYMMDD-HHMMSS
- 名称：<8-20字需求名称>
- 创建时间：YYYY-MM-DD HH:mm

## 目标
<需求目标>

## 范围
- 包含：<...>
- 不包含：<...>

## 约束
<...>

## 验收标准
1. <标准1>
2. <标准2>

## 未决事项
<无 或 列出>
```

---

## meta.json 格式

```json
{
  "id": "RQ-YYYYMMDD-HHMMSS",
  "name": "<需求名称>",
  "status": "需求澄清中",
  "created_at": "YYYY-MM-DD HH:mm",
  "updated_at": "YYYY-MM-DD HH:mm"
}
```

---

## index.json 追加格式

```json
{
  "id": "RQ-YYYYMMDD-HHMMSS",
  "name": "<需求名称>",
  "status": "需求澄清中",
  "path": ".tuiqiao/requirements/RQ-YYYYMMDD-HHMMSS/",
  "created_at": "YYYY-MM-DD HH:mm"
}
```
