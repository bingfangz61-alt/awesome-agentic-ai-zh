# 給開發者 — 專業分支

> [English](./for-developer.en.md) | **繁體中文**

> 從 Stage 7 結尾分支出來。把 agentic AI 應用到 coding 流程上。

## 使用情境

- AI 結對程式設計（Cursor、Aider、Claude Code）
- Code review 自動化
- 測試生成
- Multi-agent coding 任務（規劃 + 執行)
- CLI 委派（Codex、Gemini 處理重 token 的程式碼工作）

## 精選 Projects

### Coding Agents

#### [Cursor](https://www.cursor.com/) ⭐⭐⭐⭐⭐
編輯器整合的 AI 結對程式設計工具。AI 輔助 coding 的業界標準。

#### [Aider](https://github.com/Aider-AI/aider) ⭐⭐⭐⭐⭐
直接修改你 repo 中程式碼的 CLI 結對工具。Open source，模型不限。對終端機使用者很友善。

#### [anthropics/claude-code](https://github.com/anthropics/claude-code) ⭐⭐⭐⭐⭐
Anthropic 官方的 agentic coding 助理。有 Skills + plugin 生態系。

#### [OpenHands (前身為 OpenDevin)](https://github.com/All-Hands-AI/OpenHands) ⭐⭐⭐⭐
Open source 的自主軟體開發 agent。

### CLI 委派

#### [WenyuChiou/codex-delegate](https://github.com/WenyuChiou/codex-delegate) ⭐⭐⭐⭐
把重 token 的程式碼工作委派給 Codex CLI 的 Claude Code skill。Wrapper script + result.json 契約模式。

#### [WenyuChiou/gemini-delegate-skill](https://github.com/WenyuChiou/gemini-delegate-skill) ⭐⭐⭐⭐
同樣的模式但給 Gemini CLI——長 context 整合、雙語撰寫、第二意見審查。

### Code Review

#### [obra/superpowers](https://github.com/obra/superpowers) ⭐⭐⭐⭐
20+ 個經過實戰驗證的 skill，包括 TDD 模式、debug、協作模式。設計 code-review skill 時的好參考。

## 必練流程

- **AI 結對程式設計**：日常工作用 Claude Code 或 Cursor
- **Multi-agent coding**：agent-task-splitter → codex-delegate（實作）+ gemini-delegate（審查）→ reconciler
- **測試生成**：寫一個 skill，從 function signature 生出 pytest 測試
- **Code review 自動化**：在每一個 PR 上呼叫 Claude API 的 GitHub Action
