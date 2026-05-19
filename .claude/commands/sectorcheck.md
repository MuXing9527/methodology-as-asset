# /sectorcheck

**用法**：`/sectorcheck`

触发 `equity-sector-limit` Skill，按 WIND/CICS 一级行业分类，检查权益组合行业集中度主动偏离是否超限。

**关键指标**：主动偏离 = 组合权重 - 基准权重（不只看绝对权重）

**预警**：主动偏离超过限额（常见设定 +20%）即触发警告

**输出**：`sector_monitor_<date>.md`
