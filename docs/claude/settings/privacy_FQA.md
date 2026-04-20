# 隱私權FQA

## 1. `permissions` 是否可以只設定 `allow`，不設定 `deny`？

- **可以只寫 `allow`，不寫 `deny`。**([Claude API Docs][2])

可以。Claude Code 文件明確提到可以在 `settings.json` 或 `settings.local.json` 加 `permissions.allow` 規則；也有說明 `permissions.deny` 是用來封鎖特定工具、命令或路徑。換句話說，`allow` 和 `deny` 都是合法配置，不是一定要同時存在。([Claude API Docs][1])

不過要注意一件事：

- `deny` 是「封鎖名單」思維：擋掉特定項目，其餘照常。
- `allow` 比較接近「允許名單」思維：只先核准你列出的規則，常用在預先允許某些工具或操作。這點從官方對 subagents 的說明也看得出來：`permissions.allow` 可以限制只允許某些 agent 類型，若要「只擋特定的、其他都放行」，就改用 `permissions.deny`。([Claude API Docs][2])

所以實務上：

- 你如果想做「隱私保護」，通常會更常用 `deny`
- 你如果想做「只允許少數安全操作」，才會偏向用 `allow` 或 allowlist 的思路。([Claude API Docs][2])

如果你的目標是「**不要讓 Claude Code 碰敏感檔案**」，建議優先這樣寫：

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)",
      "Read(./*.pem)",
      "Read(./*.key)"
    ]
  }
}
// 像 Read(./.env.*)，意思是指禁止讀取目前目錄下所有以 .env. 開頭的檔案
```

因為這種需求本質上是「封鎖少數高風險路徑」，用 `deny` 會比只寫 `allow` 更直觀，也比較不容易漏掉常用工具。這是依官方 `permissions.deny` 的用途延伸出的實務建議。([Claude API Docs][1])

---

## 2. `permissions` 不設定的話，代表都允許嗎？

- **不寫 `permissions`，不是代表全部都允許，而是代表沒有額外套用你的自訂規則；實際上仍可能走 Claude Code 本身的權限確認流程。**([Claude API Docs][3])

比較精準的理解是：

- 如果你**沒有設定 `permissions.allow` / `permissions.deny` 規則**，Claude Code 就**不會額外套用你自訂的允許或封鎖清單**。([Claude API Docs][1])
- 但這不表示它會「完全不問直接全部放行」，因為 Claude Code 還有自己的**權限提示 / approval 機制**。官方文件提到可以透過 `/permissions` 讓特定工具「永遠要求確認」，也有 hooks 機制可讓結果變成 `ask` 或 `deny`；這代表是否能執行，除了 `permissions` 外，還會受互動式權限流程影響。([Claude API Docs][3])

所以你可以把它理解成：

- **沒設定 `permissions`**
  = 沒有你自訂的白名單/黑名單規則
  ≠ 所有操作都無條件放行。([Claude API Docs][3])

[1]: https://docs.anthropic.com/en/docs/claude-code/settings?utm_source=chatgpt.com "Claude Code settings - Claude Code Docs"
[2]: https://docs.anthropic.com/en/docs/claude-code/sub-agents?utm_source=chatgpt.com "Create custom subagents - Claude Code Docs"
[3]: https://docs.anthropic.com/en/docs/claude-code/hooks-guide?utm_source=chatgpt.com "Automate workflows with hooks - Claude Code Docs"
