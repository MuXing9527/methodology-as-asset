# /margincheck

**用法**：`/margincheck`

触发 `futures-margin-check` Skill，检查期货账户保证金使用率和各合约距强平距离。

**关键字段**：`margin_to_force_close`——距强平还差多少浮亏，每日必须知道。

**风险等级**：normal(<60%) / caution(60-75%) / warning(75-85%) / critical(>85%)

**警告**：使用率 > 80% 时，需要当天处理，不是第二天。
建议日内追加一次检查（尤其在高波动行情中）。

**输出**：`margin_check_<date>.md`
