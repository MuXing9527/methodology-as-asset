# /earningspreview

**用法**：`/earningspreview <ticker> <period>`

**示例**：`/earningspreview 600519.SH 2024Q4`

触发 `earnings-preview` Skill，生成季报/年报预览报告。

**输出**：
- `earnings_preview_<ticker>_<period>.md`
- `earnings_preview_<ticker>_<period>.json`（供后续 model-update 消费）

**注意**：所有一致预期数字必须标注来源（Wind WSEST + 日期）。
