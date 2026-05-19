---
name: drawdown-diagnosis
description: 回撤诊断——Brinson 分解回撤期贡献，逐仓 thesis 状态检查
inputs:
  - portfolio_id: 组合 ID
  - drawdown_start: 回撤开始日期
  - drawdown_end: 回撤结束日期（默认今日）
outputs:
  - drawdown_diagnosis_<portfolio_id>_<date>.md
---

# 步骤 1：计算回撤来源

对回撤期间运行 Brinson 归因（调 brinson-attribution Skill）：
- 哪个行业的配置效应最大？
- 哪个行业的选股效应最大？
- 找出贡献最大的 3-5 只负向个股

# 步骤 2：逐仓 thesis 状态检查

对负贡献前 5 只股票，运行 thesis-tracker Skill。
判断：这些股票的跌幅是因为 thesis 失效，还是市场系统性风险？

# 步骤 3：回撤诊断报告

## 回撤诊断（{回撤期间}）

**回撤总量**：X.X%（组合）vs Y.Y%（基准），超额回撤 Z.Z%

**回撤来源分解**：
| 贡献来源 | 效应类型 | 贡献 bp |
|---|---|---|
| 行业A（超配）| 配置效应 | -XX bp |
| 股票B（选股）| 选股效应 | -XX bp |

**Thesis 检查**：
| 股票 | Thesis 状态 | 结论 |
|---|---|---|
| XXX | BROKEN | 建议复核持仓 |
| YYY | INTACT | 市场系统性回调，无需操作 |
