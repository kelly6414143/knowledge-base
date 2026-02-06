# Cursor React Prompt 模板（前端工程師版）

## 1. 優化可讀性與可測試性【Ctrl + K】

> 格式: 目標 + 限制 + 驗收標準 + 專案規範

```
目標：優化這個 component 的可讀性與可測試性
限制：
1) 不新增第三方套件
2) 不改 UI 行為（loading、搜尋、列表結果需一致）
3) 維持現有 API 呼叫方式（fetchAuditList 仍在此檔或原 service）
驗收：
- 請列出你改了哪些點（條列）
- 提供重構後完整 code
- 若有抽 hook，檔名與 export 命名要符合本專案慣例（請先推測/遵循現有命名）

```

## 2. 調整內容【Ctrl + K】

```
把這段 data fetch 改成：
- 一律用 try/finally 確保 loading 正確關閉
- 加上取消請求/忽略過期回應，避免 unmount 後 setState
- 不改外部行為
```

## 3. Debug【Ctrl + L】

```
請先不要改 code。
1) 先推導有哪些情境會造成 loading 無法關閉（列出 3~5 種）
2) 指出最可能的 1~2 個原因，並對應到具體哪幾行
3) 最後再給出最小修正（minimal patch）
```

## 4. 重構拆 Hook【Ctrl + K】

```
請把「搜尋與過濾」抽成一個 hook：
- hook 名稱：useAuditFilter
- input：data, keyword
- output：filtered
- 不要把 UI 元件拆檔
- 保留 AuditItem 型別

```

## 5. 專案慣例(對照檔)【Ctrl + K】

```
請先讀取並記住本專案的 coding style：
- 參考 src/pages/User/index.tsx
- 參考 src/hooks/useSomething.ts
接下來我的重構都要符合這些檔案的風格
```
