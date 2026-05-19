---
name: equity-sector-limit
description: 权益组合行业集中度日监控——主动偏离 vs 基准，超限预警
inputs: []
outputs:
  - sector_monitor_<date>.md
---

# 步骤 1：调 equity-sector-monitor Subagent

返回各行业的组合权重 / 基准权重 / 主动偏离 / breach flag。

# 步骤 2：读取行业集中度限额

mcp.risk.query_limit_config(limit_type="sector_concentration")
常见限额：单一一级行业主动偏离 ≤ +20%，或绝对权重 ≤ 35%

# 步骤 3：输出行业敞口日报

## 行业敞口日报（{日期}）

**基准**：沪深300（或 CLAUDE.local.md 中配置的基准）

| 行业 | 组合权重 | 基准权重 | 主动偏离 | 限额 | 状态 |
|---|---|---|---|---|---|
| 消费 | X% | X% | X% | +20% | 正常 |

**主动敞口汇总**：
  超配行业总和：X%
  低配行业总和：X%

**超限预警**（如有）：
⚠ [行业名] 主动偏离 +X%，超过限额 +20%

# 注意

行业集中度分析要看主动偏离，不只看绝对权重。
组合重仓金融 25%，基准 30% → 实际是低配，不是集中度风险。
