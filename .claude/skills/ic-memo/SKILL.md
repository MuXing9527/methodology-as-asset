---
name: ic-memo
description: 投委会 Memo 生成——目标价和仓位留白，analyst_thesis 强制手填
inputs:
  - ticker: 股票代码
  - company_name: 公司名称
outputs:
  - ic_memo_<ticker>_v1.md
  - ic_memo_<ticker>_v1.json
---

# LLM 不做终审原则

本 Skill 生成 Memo 骨架，以下字段 **永远留白**，由研究员手动填写：
- TARGET_PRICE（目标价）
- POSITION_SIZE（建议仓位 %）
- analyst_thesis（核心投资逻辑，不少于 3 条）

不接受 LLM 生成上述字段。Memo 提交前须人工确认。

# 步骤 1：数据汇总

整合已有材料：
- ic_skeleton_<ticker>.json（如已完成首次覆盖）
- thesis 文件
- 财务模型摘要
- dd-checklist 状态

# 步骤 2：生成 Memo 骨架（7节）

1. 公司概况（一页摘要）
2. 核心投资逻辑（analyst_thesis 字段——**留白，研究员手填**）
3. 财务摘要（历史3年 + 预测2年关键指标）
4. 估值分析（可比公司区间，目标价字段留空）
5. 催化剂时间表
6. 主要风险（必须包含 "失效条件"）
7. 建议仓位（**留白，投委会讨论后填写**）

# === HUMAN CHECKPOINT ===

第2节 analyst_thesis 和第7节仓位建议必须由研究员手写。
AI 在这两个字段只填占位符：`[研究员填写]`

# 步骤 3：版本管理

v1 = 初稿（AI 生成骨架，等待研究员填写关键字段）
v2 = 研究员填完后的版本
SUBMITTED = 提交投委会版本（不再修改）
