# Skills 是什麼？

Skills 是自訂的 slash command（`/skill-name`），讓你可以把「怎麼做某件事」封裝成一個可重複呼叫的指令。它遵循 [agentskills.io 開放標準](https://agentskills.io)。

---

## 位置與名稱的規則

### 資料夾位置：固定的，只有兩個合法位置

| 位置 | 說明 |
| --- | --- |
| `~/.claude/skills/<skill-name>/` | 使用者全域，適用所有專案 |
| `.claude/skills/<skill-name>/` | 專案層級，放在專案根目錄下 |

Claude Code 只會從這兩個路徑去掃描 skills，不能放在其他任意位置。

---

### 資料夾名稱：決定 slash command 的名稱

```text
.claude/skills/deploy/SKILL.md    →  /deploy
.claude/skills/my-review/SKILL.md →  /my-review
```

資料夾名稱就是你呼叫時用的指令名稱，可以自訂，但要符合命名規則（小寫、可用連字號）。

---

### `SKILL.md` 檔名：固定的

主要定義檔一定要叫 `SKILL.md`，這是 Claude 掃描時的識別依據。  
其他輔助檔案（templates、scripts 等）可以自由命名放在同一資料夾下。

---

## Skill 的結構

```text
~/.claude/skills/my-skill/
├── SKILL.md          # 必要：指令定義
├── template.md       # 選用：模板
└── scripts/
    └── helper.sh     # 選用：輔助腳本
```
---

### 完整結構範例

```text
your-project/
├── .claude/
│   └── skills/
│       ├── deploy/          ← 資料夾名 = /deploy 指令
│       │   ├── SKILL.md     ← 固定檔名（必要）
│       │   └── helper.sh    ← 自由命名（選用）
│       └── code-review/     ← 資料夾名 = /code-review 指令
│           └── SKILL.md
```

---


`SKILL.md` 基本格式：

```yaml
---
name: my-skill
description: 描述這個 skill 的用途（Claude 靠這個決定何時自動使用）
---
```

```text
步驟 1：...
步驟 2：...
```

---

## 重要 Frontmatter 欄位

| 欄位 | 用途 |
| --- | --- |
| `description` | Claude 決定是否自動呼叫的依據 |
| `allowed-tools` | 預先核准的工具（避免每次確認） |
| `context: fork` | 在獨立 subagent 中執行 |
| `agent: Explore` | 指定 subagent 類型 |
| `disable-model-invocation: true` | 只有使用者能呼叫，Claude 不能自動使用 |
| `hooks` | 只在此 skill 執行期間生效的 hooks |

---

## Skills vs Hooks 的差別

|  | Skills | Hooks |
| --- | --- | --- |
| 本質 | 教 Claude「怎麼做某事」的劇本 | 在特定時機強制執行的 shell 命令 |
| 觸發方式 | 使用者呼叫 `/skill-name` 或 Claude 自動決定 | 自動觸發（事件驅動） |
| 控制權 | Claude 決策 | 系統強制，不經 Claude |
| 典型用途 | 封裝流程、部署步驟、程式碼審查 | 自動格式化、封鎖危險指令、記錄 log |

Hook 觸發時機點：`SessionStart`、`PreToolUse`、`PostToolUse`、`Stop`

---

## 串接自動化（Skills + Hooks）

這是最強大的組合。

典型流程範例：自動化部署

```text
用戶呼叫 /deploy
    ↓
PreToolUse Hook：驗證測試是否通過（失敗則阻擋）
    ↓
Skill 執行部署步驟
    ↓
Skill 內的 PostToolUse Hook：記錄每個步驟
    ↓
全域 PostToolUse Hook：自動格式化修改的檔案
    ↓
Stop Hook：確認部署成功
```

Skill 內嵌 Hook（Scoped Hooks）

```yaml
---
name: deploy
hooks:
  PostToolUse:
    - matcher: "Bash"
      hooks:
        - type: "command"
          command: "echo 'step done' >> /tmp/deploy.log"
---
```

這個 hook 只在 skill 執行期間生效，不影響其他場景。

---

## 檔案位置

| 位置 | 範圍 |
| --- | --- |
| `~/.claude/skills/` | 個人全域（所有專案） |
| `.claude/skills/` | 專案層級（可提交到 git） |
| `~/.claude/settings.json` | 個人全域 hooks 設定 |
| `.claude/settings.json` | 專案 hooks 設定（可分享） |

---

## 總結

- Skills = 封裝「流程知識」，告訴 Claude 怎麼做
- Hooks = 強制在特定時機執行某些動作，不經 Claude 決策
- 兩者可以串接：Hooks 負責驗證/攔截，Skills 負責執行邏輯
- Skills 本身不是自動化，但搭配 `context: fork` 或 Hooks 可以達成強大的自動化流水線
