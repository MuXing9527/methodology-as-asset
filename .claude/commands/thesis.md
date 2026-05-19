# /thesis

**用法**：`/thesis <ticker>`

触发 `thesis-tracker` Skill，读取 `.claude/thesis/<ticker>.md`，逐条核对假设状态。

**输出**：
- `thesis_check_<ticker>_<date>.json`
- `thesis_check_<ticker>_<date>.md`

**Thesis 状态说明**：
- `HOLDING`：假设仍然成立
- `WEAKENING`：有减弱迹象，需关注
- `BROKEN`：假设已不成立，建议复核持仓
- `UNVERIFIABLE`：无法从公开数据核实

**注意**：`recommended_action` 是建议，最终由研究员决定。
