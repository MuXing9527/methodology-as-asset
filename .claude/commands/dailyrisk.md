# /dailyrisk

**用法**：`/dailyrisk`

触发 `daily-risk-pack` Skill，并行运行 VaR / 回撤 / 仓位限额三类监控，汇总每日风险报告。

**输出**：
- `daily_risk_<date>.md`
- `daily_risk_<date>.json`（含审计日志）

**整体状态**：GREEN / YELLOW / RED

**重要**：
- 所有数字 Independent Recompute，不直接消费风控系统汇总数字
- AI 只报告，操作决策由人做
- 审计日志保存 6 个月（监管合规要求）
