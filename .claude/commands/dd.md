# /dd

**用法**：`/dd <ticker> [--type full|targeted] [--meeting management|channel_check]`

**示例**：
- `/dd 600519.SH` — 生成完整尽调清单
- `/dd 600519.SH --meeting management` — 生成管理层调研问题

触发 `dd-checklist` Skill（生成三层清单）或 `dd-meeting-prep` Skill（会议问题准备）。

**⚠ 合规提醒**：
- MNPI 标记项目（⚠）中提及的未公开信息，绝对不得输入任何 LLM
- 会议纪要须经合规审核后方可共享
