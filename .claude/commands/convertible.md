---
name: convertible
description: 中国可转债个券/池子分析入口 —— 调 convertible-bond-analyzer Skill
---

# /convertible <bond_code> [mode]

Command 层只做 3 件事：

1. 参数解析：转债代码、模式
2. 调用 Skill：`convertible-bond-analyzer`
3. 输出整理：返回 MD + HTML

## 用法

```bash
/convertible 123456.SH single_bond
/convertible all weekly_pool
/convertible all clause_watch
```

## 反模式

- Command 里直接套双低筛选结论
- Command 里把正股上涨逻辑直接当转债结论
