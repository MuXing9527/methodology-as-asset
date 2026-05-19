---
name: earnings-preview
description: 财报预览 Skill——基于数据查询清单生成季报 / 年报预览报告
inputs:
  - ticker: 股票代码（如 600519.SH）
  - period: 报告期（如 2024Q4 / 2024FY）
outputs:
  - earnings_preview_<ticker>_<period>.md
  - earnings_preview_<ticker>_<period>.json
---

# 数据查询清单

在开始分析前，逐项确认以下数据已就绪：

| 项目 | 数据源 | 状态 |
|---|---|---|
| 历史季度营收（近8季） | Wind / 公司公告 | [ ] |
| 历史季度净利润（近8季） | Wind / 公司公告 | [ ] |
| 卖方一致预期（营收/净利润/EPS） | Wind WSEST | [ ] |
| 最近一次管理层指引 | 电话会纪要 | [ ] |
| 行业高频数据（本季相关月份） | 行业协会 / Wind | [ ] |

# 步骤 1：历史数据分析

调 financial-reader Subagent 读取近 8 季度财务数据。
计算：QoQ / YoY 增速、毛利率趋势、费用率趋势。

# 步骤 2：一致预期对比

读取卖方一致预期，与近期高频数据交叉验证。
识别：超预期概率（bullish case / base case / bearish case）。

# 步骤 3：输出预览报告

输出 markdown 格式（earnings_preview_<ticker>_<period>.md）
同步输出 JSON（earnings_preview_<ticker>_<period>.json），供 model-update Skill 消费。

## 输出结构

```json
{
  "ticker": "",
  "period": "",
  "base_case": {
    "revenue_cny_m": null,
    "net_profit_cny_m": null,
    "gross_margin_pct": null
  },
  "vs_consensus_pct": null,
  "key_assumptions": [],
  "risks": []
}
```

# [VERIFY] 标记

所有涉及一致预期数字必须标注来源（Wind WSEST + 日期），不得凭记忆填写。
