---
title: "Web 前端錯誤排查 SOP"
tags: ["frontend", "debug", "sop"]
owner: "web-team"
reviewer: ["sre-team"]
last_review: "2025-10-19"
status: "stable"
---

## 適用範圍
- 客戶端報錯、白屏、資源載入失敗

## 步驟
1. 開啟 DevTools，記錄 Console 與 Network（失敗請求/狀態碼）
2. 以關鍵字搜尋已知問題：本庫 `playbooks/`、`incidents/`
3. 發 Issue（使用 `doc_request` 模板）補齊缺漏
4. 如屬已知問題，回覆對應 FAQ 連結並標記案例

## 驗收
- 可重現/不可重現說明、相關截圖與日誌

## 回滾
- 切回前一版靜態資源或關閉新開關旗標（feature flag）
