# /creditcheck

**用法**：`/creditcheck`

触发 `credit-risk-monitor` Skill，检查信用债组合的发行人/行业集中度，扫描近 30 天评级变化。

**输出**：`credit_monitor_<date>.md`

**评级变化预警**：任何持仓债券发行人被下调评级，报告中单独标出（⚠）。

**注意**：持仓数据属于 Restricted Tier，报告只存内部路径，不对外发送。
