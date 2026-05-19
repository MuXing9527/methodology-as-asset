# /report

**用法**：`/report <source_md> --client <retail|institutional|qualified_investor|offshore>`

**示例**：`/report ./research/600519_IC_draft.md --client institutional`

触发 `client-report` Skill，按客户类型适当性过滤，合规黑名单扫描，双格式输出。

**输出**：
- `client_report_<date>.md`（内部存档）
- `client_report_<date>.html`（客户发送版，经合规审核后发送）

**注意**：html 版本须经合规人员审核后方可发送。
