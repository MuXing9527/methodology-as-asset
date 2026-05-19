---
name: dd-meeting-prep
description: 调研会议问题准备——从 dd-checklist 中提炼核心问题 + 合规提醒
inputs:
  - ticker: 股票代码
  - checklist_md: dd-checklist 输出文件路径
  - meeting_type: management | investor_day | channel_check
outputs:
  - dd_meeting_prep_<ticker>.md
---

# 步骤 1：读取 dd-checklist

从 checklist_md 提取未解答的关键问题（优先财务异常项 + 运营核心指标）。

# 步骤 2：生成会议问题（≤10题）

从清单中提炼：
- 直接问题（需要对方给具体数字）
- 验证性问题（核实已有信息）
- 前瞻性问题（判断管理层信心）

# 步骤 3：合规提醒（会议前必读）

⚠ 调研合规提醒：
1. 不主动索取未公开财务数据
2. 管理层提及的具体订单 / 合同信息，若尚未公告，记录后需向合规部门确认处理方式
3. 竞争对手信息只接受公开渠道信息
4. 会议纪要须经合规审核后方可在研究体系内共享

# 步骤 4：会后清单

- [ ] 纪要整理（meeting-minutes-analyzer Skill）
- [ ] 核实 MNPI 嫌疑信息
- [ ] 更新 thesis 文件
- [ ] 更新 dd-checklist（已解答项打钩）
