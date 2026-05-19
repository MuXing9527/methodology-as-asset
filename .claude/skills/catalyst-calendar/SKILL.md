---
name: catalyst-calendar
description: 催化剂日历——汇总持仓未来 90 天的关键事件，标注 thesis 相关性
inputs:
  - days_forward: 前瞻天数（默认 90）
outputs:
  - catalyst_calendar_<date>.md
---

# 步骤 1：读取持仓和 thesis

从 portfolio-monitoring 输出读取持仓列表。
从 .claude/thesis/<ticker>.md 提取催化剂列表。

# 步骤 2：查询公开事件日历

mcp.wind.query_event_calendar(tickers, days=90) 获取：
- 财报披露日期（季报/年报）
- 分析师会议 / 行业会议
- 监管审批节点（如已公告）
- 指数调整窗口

# 步骤 3：打分 thesis 相关性

对每个事件：
- thesis_relevance: high / medium / low / none
- 依据：事件是否直接验证或证伪 thesis 假设

# 步骤 4：输出日历

按时间顺序排列，标注高相关性事件。
未来 30 天内的高相关性事件单独在顶部列出（"近期重点关注"）。
