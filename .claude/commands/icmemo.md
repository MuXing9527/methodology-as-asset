# /icmemo

**用法**：`/icmemo <ticker> <company_name>`

触发 `ic-memo` Skill，生成投委会 Memo 骨架。

**LLM 不做终审**：以下字段永远留白，由研究员手填：
- `TARGET_PRICE`（目标价）
- `POSITION_SIZE`（建议仓位 %）
- `analyst_thesis`（核心投资逻辑，≥3条假设）

**版本管理**：v1（骨架）→ v2（研究员填完）→ SUBMITTED（提交投委会）

**输出**：`ic_memo_<ticker>_v1.md` + `ic_memo_<ticker>_v1.json`
