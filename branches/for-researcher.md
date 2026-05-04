# 給研究者 — 專業分支

> [English](./for-researcher.en.md) | **繁體中文**

> 從 Stage 7 結尾分支出來。把 agentic AI 應用到研究流程上。

## 使用情境

- 文獻分流與比較矩陣建立
- 論文記憶提取（claim、figure、citation）
- Multi-agent 論文審查（peer review 模式）
- NotebookLM brief 驗證
- 文獻管理自動化

## 精選 Projects

### 研究流程 Marketplace

#### [WenyuChiou/ai-research-skills](https://github.com/WenyuChiou/ai-research-skills) ⭐⭐⭐⭐

5 個 plugin 的 Claude Code marketplace，14 個 skill 涵蓋文獻分流、論文記憶、NotebookLM brief 驗證、Zotero 整理、研究設計協助。安裝：`claude plugin marketplace add WenyuChiou/ai-research-skills`

#### [WenyuChiou/zotero-skills](https://github.com/WenyuChiou/zotero-skills) ⭐⭐⭐

透過 Claude Code 程式化操作 Zotero 的 CRUD。搜尋、新增、分類、註記、整理文獻。

#### [WenyuChiou/research-hub](https://github.com/WenyuChiou/research-hub) ⭐⭐⭐⭐

可由 AI 操作的研究工作環境，整合 Zotero、Obsidian、NotebookLM。可以透過 CLI、MCP、REST 使用任兩個或全部三個。

#### [WenyuChiou/academic-writing-skills](https://github.com/WenyuChiou/academic-writing-skills) ⭐⭐⭐

嚴謹學術論文寫作、修改、禁用詞稽核、期刊格式檢查的 Claude Code skill。

### 研究 Framework

#### [WenyuChiou/WAGF](https://github.com/WenyuChiou/WAGF) ⭐⭐⭐⭐

LLM 驅動 agent-based model 的治理層。6 階段驗證流程。3 個參考實作（洪災調適、multi-agent 洪災、Colorado 灌溉）。

#### [flonat/claude-research](https://github.com/flonat/claude-research) ⭐⭐⭐

給博士研究者的 Claude Code 基礎建設——學術流程用的 skill、agent、hook、規則。LaTeX / 文獻管理為主。

### Multi-Agent for Research

#### [WenyuChiou/agent-collab-skills](https://github.com/WenyuChiou/agent-collab-skills) ⭐⭐⭐⭐

5 個應用在研究流程的 multi-agent 協作 skill。Task splitter、output reconciler、debate、shared memory、acceptance gate。

## 必修閱讀

1. [The Effortless Academic — Claude Code beginner guides](https://effortlessacademic.com/claude-code-and-cowork-for-academics-beginner-guide-part-1/)
2. [Pedro Sant'Anna — Researcher setup guide](https://paulgp.substack.com/p/getting-started-with-claude-code)

## 必練流程

- **文獻分流**：research-hub `auto` → ai-research-skills `literature-triage-matrix` → 輸出到 Obsidian
- **論文 draft 循環**：paper-memory-builder → academic-writing-skills → multi-agent review（codex + gemini）
- **Multi-agent 研究跑一輪**：agent-task-splitter → 平行跑 codex/gemini task → output reconciler → acceptance gate
