# /modelupdate

**用法**：`/modelupdate <ticker> <period> <earnings_json_path>`

**示例**：`/modelupdate 600519.SH 2024Q4 ./earnings_note_600519_2024Q4.json`

触发 `model-update` Skill，读取财报实际值，更新三表模型骨架，audit-xls 验证结构完整性。

**输出**：
- `<ticker>_model_<period>.xlsx`
- `model_update_audit_<period>.md`

**注意**：目标价和估值倍数留白，由研究员手动填写。
