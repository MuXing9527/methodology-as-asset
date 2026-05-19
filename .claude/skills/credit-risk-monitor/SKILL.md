---
name: credit-risk-monitor
description: 信用集中度日监控——单一发行人/行业超限检查 + 近30天评级变化预警
inputs: []
outputs:
  - credit_monitor_<date>.md
---

# 步骤 1：调 credit-concentration-monitor Subagent

返回发行人集中度 / 行业集中度 / 评级分布 JSON。

# 步骤 2：评级变化预警

mcp.wind.query_rating_actions(issuers=portfolio_issuers, days=30)
任何"评级下调"事件，在报告里单独标出（⚠）。

# 步骤 3：输出信用风险日报

## 信用风险日报（{日期}）

### 单一发行人集中度
| 发行人 | 持仓（万元）| 占NAV | 评级 | 状态 |
|---|---|---|---|---|
| 示例A | 5,000 | 8.5% | AAA | 正常 |

（超限条目用 ⚠ 标注）

### 行业集中度
| 行业 | 占NAV | 限额 | 状态 |
|---|---|---|---|
| 城投 | X% | 35% | |

### 评级分布
AAA: X% | AA+: X% | AA: X% | AA以下: X%
加权平均评级：

### 近 30 天评级变化
（如有下调事件单独列出）

# Trust Boundary

持仓和发行人名称属于 Restricted Tier，报告只存内部路径，不出 HTML。
