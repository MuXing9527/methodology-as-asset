---
name: thesis-tracker
description: 持仓逻辑追踪——逐条核对 thesis 假设与当前数据，输出 thesis_status / confidence
inputs:
  - ticker: 股票代码
  - thesis_file: thesis 文件路径（默认 .claude/thesis/<ticker>.md）
outputs:
  - thesis_check_<ticker>_<date>.json
  - thesis_check_<ticker>_<date>.md
---

# Thesis 文件格式（.claude/thesis/<ticker>.md）

```markdown
## 核心逻辑
<1-2句核心判断>

## 关键假设
- [ ] 假设1：<具体可核查的条件>（数据来源：<Wind/公司公告>）
- [ ] 假设2：...

## 核心驱动因素
- 催化剂1：<预期时间> — <触发条件>

## 失效条件（必填）
- 如果...，立即复核持仓

## 建仓日期
## 预计复核时间
```

# 步骤 1：读取 thesis 文件

解析 .claude/thesis/<ticker>.md，提取假设列表和失效条件。

# 步骤 2：数据查询

针对每条假设，查询对应的最新数据（Wind / 公司公告 / 行业数据）。
每条假设输出：HOLDING / WEAKENING / BROKEN / UNVERIFIABLE

# 步骤 3：输出 JSON

```json
{
  "ticker": "",
  "check_date": "",
  "thesis_status": "intact|degraded|broken",
  "confidence": 0.0,
  "assumptions": [
    {
      "assumption": "",
      "status": "HOLDING|WEAKENING|BROKEN|UNVERIFIABLE",
      "evidence": "",
      "source": ""
    }
  ],
  "invalidation_triggered": false,
  "recommended_action": "hold|review|exit"
}
```

# 重要约束

recommended_action 是建议，不是指令。研究员最终决定。
UNVERIFIABLE 假设必须在报告中明确标注，不得假设"未变"。
