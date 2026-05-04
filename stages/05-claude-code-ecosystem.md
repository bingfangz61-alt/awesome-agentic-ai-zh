# Stage 5 — Claude Code 生態系 ⭐⭐

> [English](./05-claude-code-ecosystem.en.md) | **繁體中文**

⏱ **時間估計**：3-4 週（約 15-25 小時）

## Stack 一覽

```
┌──────────────────────────────────────────────────┐
│  Plugins / Marketplaces  (5.4 — packaging)       │
├──────────────────────────────────────────────────┤
│  Skills                  (5.3 — behavior)        │
├──────────────────────────────────────────────────┤
│  MCP                     (5.2 — protocol)        │
├──────────────────────────────────────────────────┤
│  Tool Use / Function Calling (Stage 3)           │
├──────────────────────────────────────────────────┤
│  Anthropic API + SDK     (Stage 1, Stage 7)      │
├──────────────────────────────────────────────────┤
│  LLM (Claude)                                    │
└──────────────────────────────────────────────────┘
```

每一層各自加上一種能力：
- **API + SDK**：用程式存取 LLM
- **Tool Use**：讓 LLM 呼叫你定義的 function
- **MCP**：標準化協定，讓任何 LLM host 都能使用任何 tool server
- **Skills**：Claude Code 的行為包，可以包住 MCP tool
- **Plugins**：把 Skills、hooks、commands、MCP 設定打包成一個單位發佈

這個階段有 4 個子章節，**請按順序做**——每一節都建立在前一節之上。

```
5.1  Claude Code 基礎          3-5 天   （安裝、slash commands、CLAUDE.md）
5.2  MCP — 協定層              5-7 天   （寫你的第一個 MCP server）
5.3  Skills — 行為層            5-7 天   （寫你的第一個 SKILL.md）
5.4  Plugins 與 Marketplaces   5-7 天   （打包並發佈）
```

跑完這個階段，你會能擴充 Claude Code、寫自己的 MCP server、發佈一個 plugin marketplace。

---

## 5.1 — Claude Code 基礎

### 學習目標
- 在你的作業系統上安裝 Claude Code
- 使用 slash commands（`/help`、`/compact`、`/clear`、`/plan`）
- 了解 `~/.claude/` 目錄結構
- 寫一份 project 層級的 `CLAUDE.md` 來客製化行為

### 必修閱讀
1. [**Anthropic — Claude Code Quickstart**](https://docs.anthropic.com/en/docs/claude-code/quickstart) — 官方安裝指南
2. [**Anthropic — CLAUDE.md best practices**](https://docs.anthropic.com/en/docs/claude-code/memory) — 怎麼寫專案 memory
3. [**KimYx0207/Claude-Code-x-OpenClaw-Guide-Zh**](https://github.com/KimYx0207/Claude-Code-x-OpenClaw-Guide-Zh) — 簡中入門指南

### Hello-X
- **Hello Claude Code** — 安裝、跑第一個 session、請 Claude 讀檔案並摘要
- **Hello CLAUDE.md** — 寫一份專案 CLAUDE.md，觀察行為的差異

### 精選 Projects
- [**anthropics/claude-code**](https://github.com/anthropics/claude-code) — 官方 repo（issues、releases）
- [**KimYx0207/Claude-Code-x-OpenClaw-Guide-Zh**](https://github.com/KimYx0207/Claude-Code-x-OpenClaw-Guide-Zh) — 簡中走讀
- [**hesreallyhim/awesome-claude-code**](https://github.com/hesreallyhim/awesome-claude-code) — 較廣泛的資源清單（目前正在重整）

---

## 5.2 — MCP（Model Context Protocol）⭐ 基礎

### 學習目標
- 解釋 MCP 的三個抽象（Tools、Resources、Prompts）
- 把現成的 MCP server 接上 Claude Desktop 或 Claude Code
- 用 Python 寫一個最小的 MCP server，提供 1-2 個 tool
- 區分 MCP server vs Tool Use vs Skills vs Plugins

### 必修閱讀
1. [**Anthropic — Introducing MCP**](https://www.anthropic.com/news/model-context-protocol) — 最初發表，概念總覽
2. [**MCP Specification**](https://spec.modelcontextprotocol.io/) — 實際的協定規格
3. [**Complete Guide to MCP in 2026**](https://dev.to/x4nent/complete-guide-to-mcp-model-context-protocol-in-2026-architecture-implementation-and-4a11) — 實作走讀

### Hello-X
- **Hello MCP client** — 安裝 `modelcontextprotocol/servers/filesystem`，從 Claude Desktop 連上去。看著 Claude 讀你的檔案。
- **Hello MCP server** — 寫一個 Python MCP server，提供一個 tool（例如「換算溫度」）。從 Claude Code 連過去。
- **Hello MCP in production** — 在同一個 Claude session 裡同時連 2-3 個 MCP server，看它們互相搭配。

### 精選 Projects

#### [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) ⭐ 官方

| 欄位 | 內容 |
|---|---|
| Maintainer | Anthropic（官方） |
| 語言 | TypeScript / Python |
| Stars | ★ 85k+ |
| License | MIT |
| 推薦度 | ⭐⭐⭐⭐⭐ |

**教什麼**：20+ 個參考用 MCP server（filesystem、git、github、sqlite、time、fetch、memory、sequential thinking）。寫自己的 server 時最標準的範例。

**適合誰**：Hello-1 以及之後當參考用。讀 `everything` server 跟 `filesystem` server 的原始碼，理解協定怎麼運作。

**怎麼跑**：
```bash
npx -y @modelcontextprotocol/server-filesystem /path/to/dir
# 或用 Python servers：
pip install mcp-server-fetch
```

---

#### [modelcontextprotocol/python-sdk](https://github.com/modelcontextprotocol/python-sdk)

| 欄位 | 內容 |
|---|---|
| Maintainer | Anthropic（官方） |
| 語言 | Python |
| License | MIT |
| 推薦度 | ⭐⭐⭐⭐⭐ |

**教什麼**：寫 MCP server 的官方 Python SDK。Hello-2 用這個。

**怎麼跑**：
```bash
pip install mcp
# 然後跟著 https://github.com/modelcontextprotocol/python-sdk#quickstart 做
```

---

#### [modelcontextprotocol/typescript-sdk](https://github.com/modelcontextprotocol/typescript-sdk)

| 欄位 | 內容 |
|---|---|
| Maintainer | Anthropic（官方） |
| 語言 | TypeScript |
| License | MIT |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：Python SDK 的 TypeScript 版本。喜歡 TS 的人選這個。

---

#### [wong2/awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers) ⭐ 目錄

| 欄位 | 內容 |
|---|---|
| Maintainer | wong2 |
| 格式 | 精選清單 |
| 推薦度 | ⭐⭐⭐⭐⭐ |

**教什麼**：150+ 個社群 MCP server 的目錄，按類別分類——search、code、cloud、communication、finance。

**適合誰**：在自己寫之前，先看看是不是已經有現成的。有特定 tool 需求時來逛這個。

**備註**：投稿要走他們網站（mcpservers.org）。

---

#### [punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers)

| Maintainer | punkpeye |
|---|---|
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：另一份 MCP server 目錄，組織方式不同（通常更新比較即時）。

**適合誰**：跟 wong2 的清單交叉比對。不同策展人會挖出不同的 project。

---

#### [github/github-mcp-server](https://github.com/github/github-mcp-server)

| 欄位 | 內容 |
|---|---|
| Maintainer | GitHub |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：真正在 production 跑的 MCP server 長什麼樣子。GitHub 官方維護。

**適合誰**：把原始碼當作 production 等級 MCP server 的參考實作來讀。

---

#### [21st-dev/magic-mcp](https://github.com/21st-dev/magic-mcp)

| 推薦度 | ⭐⭐⭐ |
|---|---|

**教什麼**：一個非平凡的 MCP server，會生成 UI 元件。讓你看到 MCP 不只能做資料抓取。

**適合誰**：做完 Hello-2 之後找靈感——MCP server 還能做出什麼有創意的東西。

---

## 5.3 — Skills（Claude Code 的行為層）

### 學習目標
- `SKILL.md` 的結構（YAML frontmatter + 本文）
- skill 何時會自動載入（description 比對）
- 怎麼寫一份能解決你日常工作的 SKILL.md
- `references/`、`scripts/`、`evals/` 子目錄的用途

### 必修閱讀
1. [**Anthropic — Claude Skills 文件**](https://docs.anthropic.com/en/docs/claude-code/skills)
2. **幾份範例 SKILL.md**——從 `anthropics/claude-code` 或社群 marketplace 拿

### Hello-X
- **Hello SKILL.md** — 寫一份 200 字的 skill，解決你日常工作中的某一件事
- **Hello SKILL with references** — 加一份 `references/` markdown 讓 skill 可以引用
- **Hello SKILL eval** — 加 `evals/evals.json`，放 3-5 個自我測試

### 精選 Projects

#### [anthropics/claude-code（官方 skills 範例）](https://github.com/anthropics/claude-code)

| 推薦度 | ⭐⭐⭐⭐⭐ |
|---|---|

**教什麼**：Anthropic 維護的官方 skill 範例。SKILL.md 結構的參考。

---

#### [WenyuChiou/ai-research-skills](https://github.com/WenyuChiou/ai-research-skills)

| 欄位 | 內容 |
|---|---|
| Maintainer | Wenyu Chiou |
| Stars | ★ 41+ |
| License | MIT |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：5-plugin marketplace、14 個研究 skills，涵蓋文獻分流、論文 memory 建構、NotebookLM 驗證、Zotero 整理。**multi-plugin marketplace 的範例。**

**適合誰**：研究一個 marketplace 怎麼把多個來自不同來源 repo 的 plugin 編在一起。

**怎麼跑**：
```bash
claude plugin marketplace add WenyuChiou/ai-research-skills
claude plugin install research-workspace@ai-research-skills
```

---

#### [WenyuChiou/agent-collab-skills](https://github.com/WenyuChiou/agent-collab-skills)

| 欄位 | 內容 |
|---|---|
| Maintainer | Wenyu Chiou |
| License | MIT |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：5 個用來做 multi-agent orchestration 的 skill（task splitter、output reconciler、debate、shared memory、acceptance gate）。**single-plugin bundle 的範例。**

**適合誰**：研究 single-plugin marketplace 怎麼把相關的 skill 包在一起。

---

#### [WenyuChiou/codex-delegate](https://github.com/WenyuChiou/codex-delegate)

| 欄位 | 內容 |
|---|---|
| Stars | ★ 57+ |
| License | MIT |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：單一 skill 的 repo，從 Claude Code 委派工作給 Codex CLI。wrapper script + result.json contract 的範例。

**適合誰**：single-skill plugin 的範例 + 子 CLI 委派的範例。

---

#### [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)

| 推薦度 | ⭐⭐⭐⭐ |
|---|---|

**教什麼**：社群 Claude Skills 的精選目錄。

**適合誰**：自己寫之前先看看有沒有現成的。

---

#### [obra/superpowers](https://github.com/obra/superpowers)

| 推薦度 | ⭐⭐⭐⭐ |
|---|---|

**教什麼**：20+ 個經過實戰檢驗的 skill（TDD、debugging、合作模式），附 `/brainstorm`、`/write-plan`、`/execute-plan` 命令以及 skills-search tool。

**適合誰**：power user 的設定。讀 SKILL.md 原始碼學進階寫法。

---

#### [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)

| 推薦度 | ⭐⭐⭐ |
|---|---|

**教什麼**：1000+ 個 agent skill，相容於 Claude Code、Codex、Gemini CLI、Cursor。跨工具的視角。

**適合誰**：搞懂 SKILL.md 之後，逛逛找想法。

---

#### [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills)

| 推薦度 | ⭐⭐⭐ |
|---|---|

**教什麼**：232+ 個 Claude Code skill，跨 engineering、marketing、product、compliance。

**適合誰**：找特定領域的 skill 範例。

---

## 5.4 — Plugins 與 Marketplaces

### 學習目標
- `plugin.json` schema（name、version、skills array、configuration）
- `marketplace.json` schema（plugins array、source、metadata）
- `claude plugin marketplace add` 的流程
- 區分 single-plugin bundle vs multi-plugin marketplace
- 發佈自己的 marketplace

### 必修閱讀
1. [**Anthropic — Plugins 文件**](https://docs.anthropic.com/en/docs/claude-code/plugins)
2. **讀下面 2-3 個 marketplace 的 `plugin.json` 與 `marketplace.json`**

### Hello-X
- **Hello plugin install** — 安裝下面的某一個 marketplace，看它載入
- **Hello plugin.json** — 把 5.3 寫的 SKILL.md 打包成一個 plugin
- **Hello marketplace publish** — push 到 GitHub，用 `claude plugin marketplace add` 安裝

### 精選 Projects

#### [WenyuChiou/ai-research-skills](https://github.com/WenyuChiou/ai-research-skills)（multi-plugin marketplace 範例）

5.3 已經提過。讀它的 `.claude-plugin/marketplace.json` 來研究 multi-plugin 寫法（5 個 plugin、5 個來源 repo）。

---

#### [WenyuChiou/agent-collab-skills](https://github.com/WenyuChiou/agent-collab-skills)（single-plugin bundle 範例）

讀它的 `.claude-plugin/marketplace.json` 跟 `.claude-plugin/plugin.json` 研究 single-plugin bundle 的寫法。

---

#### [obra/superpowers](https://github.com/obra/superpowers)（production marketplace）

規模較大、實戰過的 marketplace。讀它的打包結構。

---

#### [rohitg00/awesome-claude-code-toolkit](https://github.com/rohitg00/awesome-claude-code-toolkit)

| 推薦度 | ⭐⭐⭐ |
|---|---|

**教什麼**：社群中規模最大的 Claude Code agents、skills、hooks、templates 目錄之一。涵蓋的 use case 很廣。

**適合誰**：跑完 Hello-3 之後逛逛看外面有什麼。

---

## ✅ 進入 Stage 6 前的自我檢查

你能不能：
- [ ] 安裝 Claude Code 並使用 5 個不同的 slash command
- [ ] 在同一個 Claude session 裡接 2 個 MCP server
- [ ] 用 Python 寫自己的 MCP server，提供 1 個能用的 tool
- [ ] 寫一份能在特定觸發詞自動載入的 `SKILL.md`
- [ ] 把 skill 打包成 plugin，再用 `marketplace.json` 發佈
- [ ] 從角色分工說出 MCP / Skills / Plugins / SDK 各自的位置

如果都可以 → 前往 [Stage 6 — Memory & RAG](06-memory-rag.md)。

## 💡 Bonus：完成這個階段之後

- 對 `anthropics/claude-code` cookbook 發一個 PR（小修正、文件更新）
- 把自己的 plugin 投稿到社群 marketplace
- 寫一篇文章，比較自己的 hello-MCP server 跟官方 `modelcontextprotocol/servers` 收的某一個
