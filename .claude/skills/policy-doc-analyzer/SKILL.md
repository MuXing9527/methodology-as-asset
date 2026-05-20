---
name: policy-doc-analyzer
version: 0.1.1
last_updated: 2026-05-20
maintainer: <团队>
description: 央行 / 财政 / 监管政策文件解读 —— 重点是措辞变化、隐含信号和固收资产传导
changelog:
  - 0.1.1: 补充利率债、信用债、可转债三类传导检查
  - 0.1.0: 初始骨架（教程 Ch23 对应）
---

# Skill: policy-doc-analyzer

> 这是 demo 结构骨架。实际落地要：(1) 维护历史政策文件库（pboc / csrc / mof）；(2) 措辞 diff 的规则按机构经验调整；(3) "隐含信号"部分慎写绝对结论。

## 输入

- `doc_path`: 政策文件 PDF / TXT 路径（必填）

## 输出

- `output/policy/{issuer}_{date}.md`
- `output/policy/{issuer}_{date}.html`

## 步骤

### 步骤 1：调 Subagent 读文件

`cn-policy-document-reader` —— UNTRUSTED 文档，返回措辞 diff（vs 历史 3-6 份同类文件）：

- `newly_added`: 新出现的关键措辞
- `removed`: 删除的措辞
- `replaced`: 替换的措辞对
- `intensified`: 强化的措辞
- `softened`: 弱化的措辞

### 步骤 2：补充历史对比数据

拉历史 3-6 份同类文件（同一发布主体），让 Subagent 做对比基线。

### 步骤 3：起草解读

1. 一句话定调
2. 关键措施清单
3. 措辞变化 diff 表
4. 隐含信号（用"倾向于" / "可能"等措辞）
5. 固收资产传导：
   - 利率债：政策利率路径、DR007 锚、财政供给、期限溢价
   - 信用债：再融资窗口、城投/地产/金融债分化、利差补偿
   - 可转债：正股风险偏好、转债估值、条款博弈

### 步骤 4：双输出 + 检查

- MD + HTML
- 黑名单 grep（推荐 / 必然 / 一定）

## 检查清单

- [ ] 措辞 diff 至少 3 条
- [ ] 隐含信号用条件性措辞
- [ ] 不出现"必然 / 一定"
- [ ] 没有把政策支持自动等同为信用下沉或转债估值扩张
