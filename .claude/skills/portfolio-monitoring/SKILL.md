---
name: portfolio-monitoring
description: 持仓组合监测——逐仓核对 thesis 状态，输出 FLAG 颜色预警
inputs: []
outputs:
  - portfolio_monitor_<date>.md
---

# Trust Boundary

持仓数据（Restricted Tier）通过 mcp.portfolio.query_holdings 读取。
输出报告只存内部路径，不走 Dual Output，不出 HTML。

# 步骤 1：读取当前持仓

mcp.portfolio.query_holdings() → 持仓列表（ticker / 权重 / 成本 / 市值）

# 步骤 2：逐仓运行 thesis-tracker

对每只持仓调用 thesis-tracker Skill（如 thesis 文件存在）。
汇总 thesis_status。

# 步骤 3：FLAG 分级

| FLAG | 条件 | 含义 |
|---|---|---|
| FLAG-RED | thesis_status = broken | 持仓逻辑失效，优先处理 |
| FLAG-YELLOW | thesis_status = degraded | 逻辑减弱，需要复核 |
| FLAG-BLUE | 价格较成本 +30% 以上 | 估值可能充分反映，考虑减仓 |
| FLAG-GREY | 无 thesis 文件 | 缺乏显式逻辑，需要补写 |

# 步骤 4：输出

按 FLAG 严重程度排序，输出每只持仓的状态和建议动作。
