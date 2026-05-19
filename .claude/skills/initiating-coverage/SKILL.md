---
name: initiating-coverage
description: 首次覆盖报告骨架生成——6节结构 + 2个人工检查点，判断由研究员完成
inputs:
  - ticker: 股票代码
  - company_name: 公司名称
outputs:
  - ic_draft_<ticker>.md
  - ic_skeleton_<ticker>.json
---

# 首次覆盖固定结构（6节）

| 节次 | 标题 | AI 负责 | 研究员负责 |
|---|---|---|---|
| 1 | 公司概览与业务描述 | 公开资料整理 | 核实准确性 |
| 2 | 行业与竞争格局 | 行业深度数据汇总 | 判断竞争护城河 |
| 3 | 财务分析 | 历史三表整理 + 比率分析 | 验证异常项 |
| 4 | 投资逻辑（核心）| 列出候选逻辑点 | **手写核心逻辑** |
| 5 | 估值 | 可比公司 PE/PB 区间 | **填入估值倍数和目标价** |
| 6 | 风险提示 | 列出通用风险清单 | 补充公司特有风险 |

# === HUMAN CHECKPOINT A（第4节前）===

AI 停止输出，等待研究员完成：
1. 手写 analyst_thesis（核心投资逻辑，不少于3条显式假设）
2. 确认竞争格局判断

研究员在 ic_skeleton_<ticker>.json 的 analyst_thesis 字段填写完毕后，继续运行。

# === HUMAN CHECKPOINT B（第5节估值）===

估值倍数和目标价留白，研究员必须手动填写：
- target_pe / target_pb
- target_price
- rating（研究员确认后才能生成结论段）

# 步骤 1：公司概览

调 cn-company-snapshot Subagent，获取公司基本信息、业务结构。

# 步骤 2：行业与竞争格局

调 industry-aggregator Subagent，获取行业数据。

# 步骤 3：财务分析

调 financial-reader Subagent，获取近5年三表数据和比率分析。

# 步骤 4：等待 HUMAN CHECKPOINT A

# 步骤 5：估值框架搭建

可比公司区间由 AI 提供（不含判断），目标价由研究员填写。

# 步骤 6：输出完整草稿

ic_draft_<ticker>.md + ic_skeleton_<ticker>.json
