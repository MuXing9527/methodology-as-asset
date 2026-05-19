# /stress

**用法**：`/stress <portfolio_id> [--scenarios A,B,C]`

**示例**：
- `/stress FUND_A` — 运行全部 6 个预定义情景
- `/stress FUND_A --scenarios A,E` — 只运行 A 股下跌 + 地缘冲突情景

触发 `stress-test` Skill，线性估算各情景下的 P&L。

**预定义情景**：A（A股-20%）/ B（利率+100bp）/ C（人民币贬值5%）/ D（信用收缩）/ E（地缘冲突）/ F（流动性危机）

**注意**：线性估算在极端情景下会低估实际损失，不含非线性效应。AI 只报告，不触发任何仓位变化。
