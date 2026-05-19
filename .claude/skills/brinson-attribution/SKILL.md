---
name: brinson-attribution
description: Brinson 业绩归因报告——配置效应 + 选股效应 + 交叉效应，Independent Recompute 验证加总
inputs:
  - portfolio_id: 组合 ID
  - start_date: 归因起始日
  - end_date: 归因结束日
outputs:
  - attribution_<portfolio_id>_<period>.md
  - attribution_<portfolio_id>_<period>.json
---

# Brinson 公式

配置效应 = Σ (w_pi - w_bi) × R_bi
选股效应 = Σ w_bi × (R_pi - R_bi)
交叉效应 = Σ (w_pi - w_bi) × (R_pi - R_bi)
超额收益 = 配置效应 + 选股效应 + 交叉效应

（w_pi = 组合权重，w_bi = 基准权重，R_pi = 组合收益，R_bi = 基准收益）

# Trust Boundary

持仓数据和收益数据属于 Restricted Tier，通过 mcp.portfolio 读取。
不输出每只股票的绝对权重数字（只输出主动偏离和效应分解）。

# 步骤 1：数据查询

mcp.portfolio.query_holdings_and_returns(portfolio_id, start_date, end_date)
→ 返回逐日持仓权重和收益序列

mcp.wind.query_index_constituent_weights(benchmark, start_date, end_date)
→ 基准逐日成分权重和收益

# 步骤 2：调 brinson-recompute Subagent

Subagent 从底层数据独立重算三效应，不使用绩效系统汇总数字。
输出 recomputed_* 字段。

# 步骤 3：与绩效系统对比（Independent Recompute）

| 项目 | 系统数字 | 重算数字 | 差值 | 结论 |
|---|---|---|---|---|
| 配置效应 | X bp | X bp | ≤0.01bp | PASS |
| 选股效应 | X bp | X bp | ≤0.01bp | PASS |
| 交叉效应 | X bp | X bp | ≤0.01bp | PASS |
| 加总超额收益 | X bp | X bp | 差异 | PASS/FAIL |

差值 > 0.01bp = FAIL，需人工核查。

# 步骤 4：输出报告

行业层面的三效应分解，按贡献绝对值排序。
不含个股投资建议。
