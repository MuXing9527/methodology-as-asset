# /diagnosis

**用法**：`/diagnosis <portfolio_id> <drawdown_start_date> [drawdown_end_date]`

**示例**：`/diagnosis FUND_A 2024-09-10 2024-10-15`

触发 `drawdown-diagnosis` Skill，Brinson 分解回撤期贡献，逐仓核查 thesis 状态。

**输出**：`drawdown_diagnosis_<portfolio_id>_<date>.md`

区分：thesis 失效导致的回撤 vs 市场系统性风险导致的回撤。
