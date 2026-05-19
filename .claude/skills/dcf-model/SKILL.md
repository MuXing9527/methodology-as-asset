---
name: dcf-model
description: DCF 估值模型骨架——FCFF + 终值 + WACC + 敏感性矩阵，xlsx-author 生成
inputs:
  - ticker: 股票代码
  - model_json: 来自 3-statement-model 的自由现金流序列（可选）
outputs:
  - <ticker>_dcf.xlsx
---

# 重要约束

**LLM 提供骨架，研究员填假设**。以下蓝色单元格由研究员手动填写：
- WACC 各分项（Rf / β / ERP / Rd / 资本结构）
- 终值增速（g）
- 预测期 FCFF 的增速假设

# 步骤 1：FCFF 计算链（黑色公式）

FCFF = EBIT × (1 - 税率) + D&A - ΔWC - CapEx
（从 3-statement-model 输出读取，或手动输入历史 FCFF）

# 步骤 2：WACC 计算页（蓝色输入）

| 参数 | 单元格 | 来源 |
|---|---|---|
| 无风险利率 Rf | B3 | 研究员填（参考10年国债） |
| β系数 | B4 | 研究员填（Wind β或再杠杆β）|
| 市场风险溢价 ERP | B5 | 研究员填 |
| 债务成本 Rd | B6 | 研究员填 |
| 所得税率 | B7 | 历史有效税率（黑色） |

# 步骤 3：终值与现值计算（黑色）

终值 = FCFF_n × (1+g) / (WACC - g)
NPV = Σ FCFF_t/(1+WACC)^t + 终值/(1+WACC)^n
每股内在价值 = (Enterprise Value - 净债务) / 总股本

# 步骤 4：敏感性矩阵（3×3）

WACC（行）× 终值增速g（列）的每股价值矩阵
自动生成，输出为 xlsx Checks 页内的独立区域

# 步骤 5：audit-xls 验证

- 现值计算的折现因子是否单调递减
- 终值占企业价值比例 > 80% 时标黄（过度依赖终值）
