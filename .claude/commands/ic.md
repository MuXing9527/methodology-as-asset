# /ic

**用法**：`/ic <ticker> <company_name>`

**示例**：`/ic 600519.SH 贵州茅台`

触发 `initiating-coverage` Skill，生成首次覆盖报告骨架（6节结构）。

**流程**：
1. AI 完成公司概览 / 行业 / 财务分析
2. **HUMAN CHECKPOINT A**：研究员手写核心逻辑（analyst_thesis）
3. AI 完成估值框架（可比区间），目标价留白
4. **HUMAN CHECKPOINT B**：研究员填估值倍数和目标价

**输出**：`ic_draft_<ticker>.md` + `ic_skeleton_<ticker>.json`
