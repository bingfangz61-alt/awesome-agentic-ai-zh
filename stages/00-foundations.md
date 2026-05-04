# Stage 0 — 基礎建設

> [English](./00-foundations.en.md) | **繁體中文**

⏱ **時間估算**：1-2 週（約 5-15 小時，已具備可跳過）

## 何時可以跳過這個階段

如果你能：
- 寫一個會呼叫公開 API 並解析 JSON 回應的 Python 函式
- 用 git 做 clone、commit、push，並處理基本的 merge 衝突
- 在自己的作業系統上使用命令列（cd、ls、mkdir、執行 script）
- 看懂 YAML / JSON 檔案

→ **直接跳到 [Stage 1](01-llm-basics.md)**。

如果做不到，就把這個階段走完。不要跳——後面每個階段都會預設你已經會這些。

## 📌 學習目標

- 寫 Python：函式、類別、async/await 基本用法
- 用 git：clone、branch、commit、push、基本衝突處理
- 用 REST API：發 GET/POST、解析 JSON、處理 auth header
- 讀寫 YAML 跟 JSON

## 🛠 Hello-X

- **Hello Python** — 寫一個 Python script 呼叫 https://api.github.com/users/torvalds 並印出 follower 數量
- **Hello git** — clone 任何一個公開 repo，做一次 commit，push 到自己的 fork
- **Hello YAML** — 用 Python 讀一個 `.yaml` 設定檔，改一個值，再寫回去

## 🎯 精選資源（不是完整 Project，只是學習素材）

### Python
- [**Python Crash Course**](https://github.com/ehmatthes/pcc_3e) — 書 + 練習（書要付費，練習免費）
- [**Real Python tutorials**](https://realpython.com/) — 高品質免費文章
- **datawhalechina/learn-python (zh-CN)** — 中文 Python 入門

### Git
- [**Pro Git book**](https://git-scm.com/book/en/v2) — 免費完整參考書
- [**Atlassian Git Tutorials**](https://www.atlassian.com/git/tutorials) — 以 workflow 為主
- [**Oh Shit, Git!?!**](https://ohshitgit.com/) — 出包時的救命手冊

### REST API
- [**MDN — HTTP**](https://developer.mozilla.org/en-US/docs/Web/HTTP) — 協定基礎
- [**Postman Learning Center**](https://learning.postman.com/) — API 探索工具

### YAML / JSON
- [**YAML 官網**](https://yaml.org/) — 規格
- [**JSON crash course**](https://www.json.org/json-en.html) — 官方快速指南

## 為什麼有這個階段

大多數「AI agent」教學都預設你已經會這些。如果你還沒，就會在奇怪的地方卡關（tool 需要 async、設定檔是 YAML、SDK 安裝要用 git）。在這裡花一週的投資，可以省下後面 10 週以上的挫折。
