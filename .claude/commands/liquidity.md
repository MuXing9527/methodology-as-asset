# /liquidity

**用法**：`/liquidity [--rate 0.20]`

触发 `liquidity-risk-monitor` Skill，计算持仓流动性覆盖天数，输出三情景压力估算。

**三情景**：正常市场（成交量100% / 参与率20%）/ 轻度压力（×50% / 15%）/ 严重压力（×20% / 10%）

**阈值**：退出天数 >5天 = Yellow；>10天 = Red

**建议频率**：
- 正常市场：每周一次
- VaR/回撤触发 Yellow Alert：升频至每天
- 市场成交量连续3日萎缩 >30%：每天 + 盘中检查

**输出**：`liquidity_monitor_<date>.md`
