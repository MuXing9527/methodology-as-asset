# /dv01check

**用法**：`/dv01check`

触发 `dv01-limit-monitor` Skill，读取债券/利率衍生品组合的 DV01，对照机构级审批限额逐维度检查。

**维度**：总 DV01 / 期限桶分配（1Y以下/1-5Y/5-10Y/10Y以上）/ 期货空头对冲 DV01

**预警**：使用率 ≥ 80% = Yellow；> 100% = Red（超限，触发人工审批流程）

**限额来源**：mcp.risk.query_limit_config（机构级风控系统，研究员不得自行修改）

**输出**：`dv01_monitor_<date>.md`
