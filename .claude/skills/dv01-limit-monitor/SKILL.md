---
name: dv01-limit-monitor
description: 风控视角的 DV01 限额监控——机构级限额，超限触发人工审批流程
inputs: []
outputs:
  - dv01_monitor_<date>.md
---

# 和研究员 rates-portfolio-monitor 的区别

| 维度 | rates-portfolio-monitor (Ch23) | dv01-limit-monitor (本 Skill) |
|---|---|---|
| 视角 | 研究员工具 | 风控体系 |
| 限额来源 | CLAUDE.local.md（研究员自设）| mcp.risk.query_limit_config（机构级审批）|
| 超限响应 | 输出提醒 | 触发人工审批 + 审计日志 |

# 步骤 1：读取 DV01 快照

调 rates-derivatives-snapshot Subagent（Ch23 定义），返回组合 DV01 快照 JSON。

# 步骤 2：读取机构级限额配置

mcp.risk.query_limit_config(portfolio_id, limit_type="dv01")
→ 返回 total_dv01_limit / bucket_limits / approved_by / effective_date

限额不得由 LLM 自行设定，必须从风控系统读取。

# 步骤 3：逐维度对比

| 维度 | 当前值（万元/bp）| 限额 | 使用率 | 状态 |
|---|---|---|---|---|
| 总 DV01 | X | X | X% | 正常/接近/超限 |
| 1Y 以下桶 | X | X | X% | |
| 10Y 以上桶 | X | X | X% | |
| 期货 DV01（空头）| X | X | X% | |

使用率 ≥ 80% = Yellow；使用率 > 100% = Red（超限）

# 步骤 4：超限处理

超限时：输出具体超限金额 + 记录审计日志 + 触发通知 hook
"需要 [风控官员] 在开盘前确认"
