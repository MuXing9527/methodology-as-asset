---
name: stress-test
description: 压力测试——6 个预定义情景线性估算 P&L，scenarios_library.yaml 版本管理
inputs:
  - portfolio_id: 组合 ID
  - scenarios: 情景列表（默认全部，可指定）
outputs:
  - stress_test_<portfolio_id>_<date>.md
---

# 情景库（scenarios_library.yaml 管理，年度审查）

| 情景 ID | 名称 | 核心冲击 |
|---|---|---|
| A | A 股系统性下跌 | 沪深300 -20%，成交量萎缩 50% |
| B | 利率急升 | 10年国债收益率 +100bp |
| C | 人民币急贬 | USD/CNY +5% |
| D | 信用收缩 | AA 级信用利差 +150bp |
| E | 地缘冲突升级 | 大宗商品 +30%，避险资产需求上升 |
| F | 流动性危机 | 银行间利率飙升，股债双杀 |

# 步骤 1：读取持仓

mcp.portfolio.query_holdings_with_market_value()

# 步骤 2：线性估算每个情景下的 P&L

P&L_i = Σ (持仓市值_j × β_j × 情景冲击幅度)
β_j 从 Wind 获取（股票对情景因子的历史敏感性）

注意：线性估算在极端情景下会低估实际损失（不含非线性效应），这是模型局限，报告中须注明。

# 步骤 3：输出压力测试报告

| 情景 | 估算P&L（万元）| 占NAV% | 是否超阈值 |
|---|---|---|---|
| A | -XXXX | -X.X% | 是 / 否 |

**最大单一情景损失**：情景A，-X.X%（超过阈值 Y.Y%）

# 重要约束

压力测试结果仅供参考，不自动触发任何仓位变化。
所有操作决策由人做。
情景参数（β值和冲击幅度）不得由 LLM 自行设定，从 scenarios_library.yaml 读取。
