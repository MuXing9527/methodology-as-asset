# /attribution

**用法**：`/attribution <portfolio_id> <start_date> <end_date>`

**示例**：`/attribution FUND_A 2024-01-01 2024-03-31`

触发 `brinson-attribution` Skill，生成 Brinson 业绩归因报告（配置效应 + 选股效应 + 交叉效应）。

**Independent Recompute**：调 brinson-recompute Subagent 从底层数据独立重算，与绩效系统对比验证（差值 ≤ 0.01bp = PASS）。

**输出**：
- `attribution_<portfolio_id>_<period>.md`
- `attribution_<portfolio_id>_<period>.json`
