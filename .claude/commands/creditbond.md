---
name: creditbond
description: 中国信用债主体/个券分析入口 —— 调 credit-bond-analyzer Skill
---

# /creditbond <issuer> [bond_code] [mode]

Command 层只做 3 件事：

1. 参数解析：主体、债券代码、模式
2. 调用 Skill：`credit-bond-analyzer`
3. 输出整理：返回 MD + HTML

## 用法

```bash
/creditbond 某城投 012345.IB issuer_review
/creditbond 某银行 123456.SH bond_admission
/creditbond 全市场 spread_weekly
```

## 反模式

- Command 里写主体信用结论
- Command 里把评级当最终判断
