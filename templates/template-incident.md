---
title: "Incident YYYY-MM-DD"
tags: ["incident", "postmortem"]
owner: "oncall-team"
reviewer: ["sre-lead", "product-lead"]
last_review: "2025-10-19"
status: "draft"
---

## 摘要
- 影響範圍 / 指標 / 影響時段

## 時間線
- 00:00 發現…
- 00:05 緩解…

## 根因分析
- 技術 / 流程 / 人員

## 行動項目（需指派責任人與截止日）
- [ ] 修正項 A（owner: @alice，due: 2025-10-31）

## 相關連結
- 工單、PR、Dashboards、Log Query


```mermaid
flowchart TD
A[提案/問題] --> B{文檔類型?}
B -->|SOP| C[templates/template-sop.md]
B -->|FAQ| D[templates/template-faq.md]
B -->|Incident| E[templates/template-incident.md]
C --> F[PR + Lint + Link Check]
D --> F
E --> F
F --> G{CODEOWNERS 審核}
G -->|通過| H[合併發佈]
G -->|退回| I[修正再送]
markdown
複製程式碼
```

>備註：VS Code 內可用擴充套件預覽；GitHub 也原生支援 Mermaid。