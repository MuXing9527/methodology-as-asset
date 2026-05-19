---
name: 3-statement-model
description: 三表财务模型骨架生成——IS/BS/CF 公式链 + Checks 验证标签页
inputs:
  - ticker: 股票代码
  - years_history: 历史年度数 (默认 5)
  - years_forecast: 预测年度数 (默认 3)
outputs:
  - <ticker>_3statement.xlsx
---

# 三色约定（必须遵守）

| 颜色 | 含义 | 示例 |
|---|---|---|
| 蓝色 | Hardcoded 输入（人工填写的假设或实际数据）| 历史营收、毛利率假设 |
| 黑色 | 公式（由假设推算的结果）| 毛利润 = 营收 × 毛利率 |
| 绿色 | 跨表引用（从另一个 sheet 取值）| CF 表读 BS 变化量 |

蓝色单元格由研究员填写，LLM 不覆盖。

# 步骤 1：数据查询清单

| 项目 | 数据源 |
|---|---|
| 历史三表数据 | Wind / 公司公告 |
| 行业平均毛利率 | Wind 行业数据 |
| 折旧摊销历史 | 附注 |
| 资本支出历史 | CF 表 |
| 营运资金历史 | BS 表 |

# 步骤 2：xlsx-author 生成三表骨架

IS（利润表）：营收 → 毛利润 → EBIT → 净利润
BS（资产负债表）：流动资产 / 非流动资产 / 负债 / 权益
CF（现金流量表）：经营 / 投资 / 筹资

关键勾稽公式（黑色）：
- 净利润 → 留存收益（IS→BS）
- D&A + ΔWC → 经营现金流（IS+BS→CF）
- CapEx → PPE净值（CF→BS）

# 步骤 3：Checks 标签页

自动生成验证页，调 audit-xls：
- BS 平衡检查（误差 ≤ 1元 = PASS）
- CF 与 BS 现金勾稽
- 历史期公式锁定（不可手改）
