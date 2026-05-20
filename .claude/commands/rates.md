---
name: rates
description: 中国利率债曲线晨报/周报入口 —— 调 rates-curve-brief Skill
---

# /rates <date> <daily|weekly>

Command 层只做 3 件事：

1. 参数解析：`date` + `mode`
2. 调用 Skill：`rates-curve-brief`
3. 输出整理：返回 MD + HTML

## 用法

```bash
/rates 2026-05-20 daily
/rates 2026-05-22 weekly
```

## 反模式

- Command 里直接判断利率方向
- Command 里拼五碗面正文
