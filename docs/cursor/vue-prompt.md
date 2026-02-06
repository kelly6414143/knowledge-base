# Cursor Vue Prompt 模板（前端工程師版）

## 1. 增加AI查閱專案的markdown【Ctrl + L】

```
你是一位資深前端工程師，請根據目前已開啟的檔案，
為此 Vue3 + Vite + Pinia 專案產出一份 README_AI.md 初版。

需求：
- 這是給 AI 使用的專案說明文件，不是對人文件
- 內容請務實、偏工程規範
- 不確定的地方請標註「需要確認」
- 不要捏造不存在的架構或規則

README_AI.md 請包含：
1. 專案基本資訊與技術棧
2. 專案結構說明（依實際資料夾）
3. Pinia 狀態管理使用方式
4. API / Service 層設計
5. 重構原則與禁止事項
6. AI 協作建議

請直接輸出完整 Markdown 內容。
```

## 2. i18n整合與移除 【Ctrl + L】

### step1: 找出 allKeysByFile、allKeysGlobal、usedKeys、dynamicSuspects、unusedCandidates

```
你是一位資深前端工程師，請協助我為此 Vue3 專案建立「i18n 未使用 key 掃描工具」。

【專案背景】
- i18n 檔案位置：i18n/lang/**/**/*.ts（包含多層資料夾）
- 每個 i18n 檔案格式為：
  export default { ...nested object... }
- i18n key 為 dot path，例如：a.b.123
- 專案為舊專案，i18n 使用方式很多元，請務必避免誤刪

【i18n 使用情境（請全部支援）】

1. Template 用法
- {{ $t('a.b.123') }}
- $t('a.b.123')
- v-t="'a.b.123'"

2. Script 用法（key 吃變數）
- t('a.b.123')
- t('a.b.123', ['xxx'])
- t('a.b.123', { name: 'xxx' })
- i18n.global.t('a.b.123', ...)

3. Key 寫成常數再使用
- const MAP = { x: 'a.b.123', y: 'c.d.456' }
- t(MAP[status])

4. <i18n-t> 元件
- <i18n-t keypath="a.b.123" />
- <i18n-t :keypath="'a.b.123'" />
- <i18n-t :keypath="cond ? 'a.b.123' : 'c.d.456'" />
- 支援 v-bind:keypath
- 若為 template literal 且包含 ${}，請視為動態 key

【掃描規則（非常重要）】

1. 先從 i18n/lang 底下所有 .ts 檔 flatten 出 allKeysGlobal（Set）
2. 掃描 src/**/*.{vue,ts,tsx,js,jsx}：
   - 抓 $t / t / i18n.global.t 第一個參數是「純字串」的 key
   - 同時掃描所有字串 literal（' " `），只要字串值存在於 allKeysGlobal，即視為 used key
   - 這是為了涵蓋「key 寫成常數再傳入 t()」的情境
3. 動態 key 規則：
   - template literal 含 ${}
   - 字串拼接（+）
   - 以上請記錄到 dynamicSuspects，不要列入 usedKeys，也不要判定 unused
4. <i18n-t :keypath>：
   - 從 expression 內抽取所有字串 literal
   - 命中 allKeysGlobal 即視為 used
   - 含 ${} 的 template literal 視為 dynamicSuspects

【輸出需求】

請新增腳本：
- scripts/i18n-audit.mjs

執行後輸出：
- reports/i18n-audit.json，包含：
  - allKeysByFile: { [filePath]: string[] }
  - allKeysGlobal: string[]
  - usedKeys: string[]
  - dynamicSuspects: string[]
  - unusedCandidates: string[]   // allKeysGlobal - usedKeys（排除 dynamicSuspects 影響範圍）

【限制】
- 腳本只做分析與輸出報告
- 不可修改任何翻譯檔或 src 程式碼
- 不可捏造不存在的 key 或結構
- 請以「避免誤刪」為最高優先

請提供完整可執行的 scripts/i18n-audit.mjs 原始碼，並簡要說明使用方式。

```

### step2: 移除 unusedCandidates，可以針對每個資料夾去做移除

```
請根據 reports/i18n-audit.json 的 unusedCandidates，
同步清理 {i18n/lang} 底下所有語系檔的未使用 key。

規則：
- 只刪除 unusedCandidates 內的 key
- 若某 key 在某語系檔不存在，略過
- 刪除後若產生空物件，請連同父層空物件一併移除（直到遇到非空或根）
- 不改變其他 key 的值與格式（縮排一致）
- 每個檔案的修改請列出摘要：刪除 key 數量 / 清掉哪些空物件層級
- 一次只處理 i18n/lang 下的檔案，不要動 src
```
