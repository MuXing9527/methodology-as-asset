# /portfolio

**用法**：`/portfolio`

触发 `portfolio-monitoring` Skill，扫描所有持仓的 thesis 状态，输出 FLAG 颜色预警。

**FLAG 说明**：
- `FLAG-RED`：thesis 失效，优先处理
- `FLAG-YELLOW`：逻辑减弱，需复核
- `FLAG-BLUE`：价格较成本 +30%+，考虑减仓
- `FLAG-GREY`：无 thesis 文件，需补写

**输出**：`portfolio_monitor_<date>.md`（仅内部路径，不对外发送）
