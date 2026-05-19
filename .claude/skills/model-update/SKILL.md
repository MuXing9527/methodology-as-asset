---
name: model-update
description: 财报模型更新 Skill——读取季报实际值，更新三表模型，xlsx-author 生成文件，audit-xls 验结构
inputs:
  - ticker: 股票代码
  - period: 报告期
  - earnings_json: 财报实际数据 JSON（来自 earnings-note-cn 输出）
outputs:
  - <ticker>_model_<period>.xlsx
  - model_update_audit_<period>.md
---

# 步骤 1：读取财报实际值

从 earnings_json 提取关键财务指标：
- 营业收入 / 净利润 / 毛利率 / 期间费用率
- 资产负债表关键项目（应收账款 / 存货 / 有息负债）
- 现金流量：经营活动现金流 / 资本支出

# 步骤 2：xlsx-author 生成更新后模型

调用 xlsx-author Skill，按三色约定写入 xlsx：
- 蓝色（hardcoded）：新录入的实际财务数据
- 黑色（formula）：比率计算、预测期外推
- 绿色（cross-link）：跨表引用（IS→BS→CF）

# 步骤 3：audit-xls 验结构

必须通过以下验证才能生成最终 xlsx：
- [ ] BS 平衡：资产 = 负债 + 所有者权益（误差 ≤ 1元）
- [ ] CF 勾稽：经营+投资+筹资现金流 = 现金净变化
- [ ] 历史期实际数据与公告一致（不得手工覆盖）

# 步骤 4：输出审计报告

model_update_audit_<period>.md 记录：
- 更新了哪些单元格
- audit-xls 验证结果
- 与预览预期（earnings-preview JSON）的差异

# 重要约束

目标价和估值倍数由研究员手动填写，LLM 不自动更新估值假设。
