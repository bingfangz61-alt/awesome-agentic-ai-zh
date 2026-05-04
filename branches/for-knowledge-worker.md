# 給知識工作者 — 專業分支

> [English](./for-knowledge-worker.en.md) | **繁體中文**

> 從 Stage 7 結尾分支出來。把 agentic AI 應用到辦公室 / 知識工作上。

## 使用情境

- Email 分流與草擬回信
- 會議筆記 → 行動項目
- 多來源報告整合
- 研究 / 市場情報蒐集
- 決策輔助流程

## 精選 Projects

### 工作流工具

#### [n8n](https://github.com/n8n-io/n8n) ⭐⭐⭐⭐
可自架的工作流自動化，內建 AI 整合。視覺化 node-based。

**適合誰**：要把多個 SaaS 工具串起來時（Slack + Gmail + Notion + AI）。

---

#### [Make.com](https://www.make.com/)（前身為 Integromat）
雲端代管的工作流自動化。AI 整合 node 很強。

---

### 知識工作者 Skills

#### [WenyuChiou/ai-research-skills](https://github.com/WenyuChiou/ai-research-skills) ⭐⭐⭐⭐

雖然定位給研究者，但有幾個 skill 對知識工作者也適用：
- `literature-triage-matrix` — 任何文件集合都能用，不只論文
- `paper-memory-builder` — 從任何文件擷取結構化資料
- `notebooklm-brief-verifier` — 驗證任何 AI 產生的 brief 是否符合來源

#### [obra/superpowers](https://github.com/obra/superpowers) ⭐⭐⭐⭐

腦力激盪、規劃、決策類的 skill。

---

### 對知識工作者有用的 MCP Server

#### 通訊類 MCP server ⭐⭐⭐⭐
Slack / Gmail / Discord 等。原本由 Anthropic host 的 reference server 在 2025 年重整過；社群維護的 server 現在放在 [**punkpeye/awesome-mcp-servers**](https://github.com/punkpeye/awesome-mcp-servers#communication) 跟 [**wong2/awesome-mcp-servers**](https://github.com/wong2/awesome-mcp-servers)。要找最新的 Slack / Gmail / Drive / Calendar MCP server 可以從這兩個清單去翻。

---

## 可以建的流程

- **每日 email 分流**：掃 inbox → 分類 → 草擬回信讓你 review → 標已讀
- **會議 → 行動項目**：逐字稿 → 主要決策 + 行動項目 → 指派 + 公告
- **每週報告整合**：從 N 個工具拉指標 → 整理 → email summary
- **研究 / 市場情報**：問題 → 多來源搜尋 → 交叉驗證 → 備忘錄

## 層級建議

大多數知識工作者應該從 **Tier 0**（Claude.ai 網頁版）開始，當你有需要對本機 / 雲端檔案重複跑的流程時，再升級到 **Tier 1**（Claude Desktop 加 MCP）。

**Tier 3+（CLI / SDK）對大多數知識工作者任務來說太重。** 不要被別人慫恿過去。

## 閱讀

- [How I Turned Claude Code Into My Personal AI Agent OS](https://aimaker.substack.com/p/how-i-turned-claude-code-into-personal-ai-agent-operating-system-for-writing-research-complete-guide) — 知識工作者個案研究
