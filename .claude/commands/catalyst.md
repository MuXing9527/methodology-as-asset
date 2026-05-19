# /catalyst

**用法**：`/catalyst [--days 90]`

触发 `catalyst-calendar` Skill，汇总持仓未来 N 天的关键事件（默认 90 天）。

**输出**：`catalyst_calendar_<date>.md`

事件按 thesis 相关性分级（high / medium / low / none）。
近 30 天内的高相关性事件单独置顶。
