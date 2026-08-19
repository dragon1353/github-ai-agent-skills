# GitHub AI Agent Skills

一套可直接放進 GitHub 專案的 AI Agent 規則與 Agent Skills 範本。它把「整個專案都要遵守的規則」、「GitHub Copilot 專用指令」、「需要時才載入的任務技能」與「自動驗證」分開管理，方便個人與團隊重用。

> Repository: `dragon1353/github-ai-agent-skills`

## 這個倉庫解決什麼問題？

AI coding agent 很會寫程式，但它不會自然知道你的專案規範、測試指令、審查標準或發佈流程。這個範本提供一個清楚的起點：

- 用 `AGENTS.md` 說明跨工具都能理解的專案規則。
- 用 `.github/copilot-instructions.md` 補充 GitHub Copilot 的 repository-wide instructions。
- 用 `.github/skills/<skill-name>/SKILL.md` 封裝可重複的任務工作流程。
- 用 GitHub Actions 自動檢查必要檔案、Skill frontmatter 與未完成的範本標記。

## 內建功能

| Skill | 用途 | 常見情境 |
| --- | --- | --- |
| `fix-ci` | 找出 CI 失敗原因、做最小修正並驗證 | GitHub Actions 紅燈、測試失敗、lint 或 build 錯誤 |
| `pr-review` | 以可行動、可重現的方式審查變更 | PR review、風險評估、測試缺口 |
| `documentation` | 讓文件與實際程式、指令保持一致 | README、API 文件、操作手冊、變更說明 |
| `release` | 準備版本、變更摘要與發佈前檢查 | tag、release notes、版本號、相容性檢查 |
| `security-audit` | 在授權範圍內找出並排序安全風險 | 依賴漏洞、輸入驗證、權限、secret exposure |
| `toeic-agent` | 分析 TOEIC 結果並建立讀書計畫 | 分數診斷、錯題分類、單字與能力缺口 |
| `folder-monitor-agent` | 設計安全、可恢復的資料夾監控流程 | 檔案到達後處理、去重、重試與隔離失敗檔案 |

前三個是通用核心 Skills；後四個示範如何擴充發佈、安全、學習分析與檔案自動化。

## 目錄結構

```text
.
├── AGENTS.md
├── LICENSE
├── README.md
└── .github/
    ├── copilot-instructions.md
    ├── skills/
    │   ├── fix-ci/
    │   │   ├── SKILL.md
    │   │   └── agents/openai.yaml
    │   ├── pr-review/
    │   ├── documentation/
    │   ├── release/
    │   ├── security-audit/
    │   ├── toeic-agent/
    │   └── folder-monitor-agent/
    └── workflows/
        └── test.yml
```

每個 Skill 的必要入口都是 `SKILL.md`。`agents/openai.yaml` 提供支援該中繼資料的工具更友善的顯示名稱與預設提示，不影響只讀取 `SKILL.md` 的 agent。

## 安裝方式

### 方法一：整套套用到新專案

1. Fork 或下載這個倉庫。
2. 把 `AGENTS.md`、`.github/copilot-instructions.md` 與需要的 `.github/skills` 複製到你的專案。
3. 依專案實際情況修改建置、測試、格式化及安全規則。
4. 提交到預設分支，讓團隊和 AI agent 使用同一份規範。

### 方法二：只安裝特定 Skill

手動複製所需資料夾，例如 `.github/skills/fix-ci/`，放入目標 repository 的 `.github/skills/` 下即可。Skill 資料夾名稱應使用小寫英文字母、數字與連字號。

### 方法三：使用 GitHub CLI 的 `gh skill`

GitHub CLI 2.90.0 以上提供公開預覽中的 `gh skill`。安裝前先預覽內容：

```bash
gh skill preview dragon1353/github-ai-agent-skills fix-ci
gh skill install dragon1353/github-ai-agent-skills fix-ci
```

第三方 Skill 可能含有不安全的指令或腳本；請先預覽並確認來源。這個倉庫刻意不在 frontmatter 預先允許 `shell`，讓執行指令前仍保留權限確認。

## 使用方式

把檔案提交到 repository 後，直接描述任務即可。支援 Agent Skills 的 GitHub Copilot 介面會依 Skill 的 `description` 判斷是否載入；也可在提示中明確說出 Skill 名稱。

```text
請用 fix-ci 分析這個 PR 的失敗檢查，找出根因並做最小修正。
請用 pr-review 審查目前的 diff，只回報可重現且值得修正的問題。
請用 documentation 依目前程式行為更新 README 和使用範例。
```

對 Codex、Claude Code 或其他 agent，保留 `AGENTS.md`，並依該工具支援的個人或專案 Skill 目錄安裝相同 Skill。不同產品與版本支援的位置可能不同，請以各工具官方文件為準。

## 四種設定各自負責什麼？

| 元件 | 載入時機 | 放什麼內容 |
| --- | --- | --- |
| `AGENTS.md` | agent 在其目錄範圍工作時 | 專案結構、驗證方式、修改邊界、安全規則 |
| `.github/copilot-instructions.md` | Copilot 在 repository 中工作時 | 幾乎每個任務都適用的精簡規則 |
| `SKILL.md` | 任務與 Skill 描述相關時 | 特定任務的步驟、判斷標準與輸出格式 |
| `.github/workflows/test.yml` | push / pull request | 自動檢查範本完整性 |

原則是：共通且短的規則放 custom instructions；較長、只在特定任務需要的流程放 Skills。

## 客製化建議

- 把實際的測試、lint、build 指令寫進 `AGENTS.md`，不要留下猜測。
- 調整 Skill 的 `description`，加入團隊真的會使用的觸發語境。
- 若流程反覆需要同一段可靠程式，再在 Skill 下新增 `scripts/`；先不要為了完整感建立空資料夾。
- 敏感操作、部署、發佈、刪除與權限變更，永遠保留人工確認。
- 對新增或下載的 Skill 先做內容審查，尤其注意腳本、外部連結與預先允許的工具。

## 自動驗證

`.github/workflows/test.yml` 會檢查必要檔案、`SKILL.md` frontmatter、Skill 資料夾與名稱一致性，以及是否殘留未完成的初始化範本標記。

## 適用情境

- 第一次導入 GitHub Copilot agent mode 或 cloud agent 的專案。
- 想讓不同 AI coding agents 共用基本工程規則的團隊。
- 想把 CI 修復、PR 審查、文件與 release SOP 變成可版本控制資產的人。
- 想公開分享可重用 Agent Skills，並讓社群 fork 後自行調整的人。

## 官方參考

- [GitHub Docs: About agent skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)
- [GitHub Docs: Adding agent skills for GitHub Copilot](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills)
- [GitHub Docs: Custom instructions support](https://docs.github.com/en/copilot/reference/custom-instructions-support)
- [OpenAI Developers: Codex use cases](https://developers.openai.com/codex/use-cases)

## License

MIT。你可以自由使用、修改與分享；請保留授權聲明。
