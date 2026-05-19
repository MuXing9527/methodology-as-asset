# /excelmodel

**用法**：`/excelmodel <ticker> [--type 3statement|dcf|both]`

**示例**：`/excelmodel 600519.SH --type both`

触发三表模型（3-statement-model）或 DCF 模型（dcf-model）骨架生成。

**输出**：
- `<ticker>_3statement.xlsx`（三表模型）
- `<ticker>_dcf.xlsx`（DCF 估值，含 3×3 敏感性矩阵）

**三色约定**：蓝色=研究员手填假设，黑色=公式，绿色=跨表引用。
研究员负责填写蓝色单元格，AI 不覆盖假设输入。
