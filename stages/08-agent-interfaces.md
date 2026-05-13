# Stage 8 — Agent Interfaces · Computer Use · Browser Use · Code Sandbox

> **繁體中文** | (zh-Hans / en mirror defer 中)

⏱ **時間估算**：2-3 週（約 12-20 小時）

> 💡 用語密度高（Computer Use / DOM / microVM / Firecracker / Sandbox / Cold start⋯）→ **本章內部就地解釋**，不熟先讀過 §1 跟 §7 術語小辭典。

> 📋 **本章組成**：〔Agent Interfaces 是什麼（先定位）+ 三層 interface〕→ 學習目標 → 進入條件 → 必修閱讀 → 🖱 Computer Use（螢幕級）→ 🌐 Browser Use（web 級）→ 📦 Code Sandbox（隔離環境含**術語小辭典**）→ Track A 怎麼用 → Track B 怎麼 build → ⚠ 2026 Safety / Security → 動手練習 → 常用工具推薦 → 精選 Projects → 自我檢查 → 下一個 frontier（Voice / VLA forward note）

> 🔑 **關鍵名詞**：見本章內部解釋 + [`resources/glossary.md`](../resources/glossary.md)

**兩 track 共用 hub**——跟 Stage 5（Claude Code 生態）一樣、Track A（CLI Power User）+ Track B（Agent Builder）兩條路徑都會用到。Stage 5 + Stage 8 是 curriculum 兩個 hub。

## 🎯 Agent Interfaces 是什麼（先定位）

**Agent Interfaces = agent 跟「非 API 世界」互動的 IO 邊界層**。Stage 0-7 教你「**怎麼建 agent 本身**」（LLM → prompt → tool → context → memory → multi-agent → harness）；本 stage 教「**agent 蓋好後、怎麼操作真實環境**」。

**3 層 interface**：

| Interface | 操作對象 | 工作原理 | 代表工具 |
|---|---|---|---|
| **🖱 Computer Use**（screen-level）| 任何桌面 app（Excel / SAP / Photoshop / 沒 API 的軟體）| screenshot → vision → 算座標 → 模擬鍵鼠 | Anthropic Claude Computer Use / OpenAI Codex desktop / Gemini in Chrome |
| **🌐 Browser Use**（web-level）| 任何網頁 | DOM-aware navigation + 必要時 vision fallback | Atlas / Comet / browser-use（OSS 86k stars）|
| **📦 Code Sandbox**（isolated exec）| agent 生成的 code 在隔離環境跑 | microVM / Container / 用戶空間 kernel | E2B / Daytona / Modal / Vercel Sandbox / OpenAI Agents SDK（April 2026 內建）|

### 跟前面 stage 的差別（避免概念混淆）

**Reader 第一個直覺問題**：這跟 Stage 3 Tool Use / Stage 5 MCP / Stage 7 Harness 有何不同？

| 比較對象 | 那邊管什麼 | 本 stage 管什麼 |
|---|---|---|
| **Stage 3 Tool Use** | agent **呼 API**（function calling、JSON schema）| agent **操作環境**（沒 API 的軟體 / 真實網頁 / 跑 code）|
| **Stage 5 MCP** | tool / data source 怎麼**標準化暴露**給 agent | agent 怎麼**實際 interact** 環境（MCP 是協定、Interface 是行為）|
| **Stage 7 Harness** | agent **runtime 控制流**（loop / retry / safety）| agent **IO 邊界**（runtime 內看不到的外界互動）|

→ **核心區分**：Tool 是 **API 呼叫**、Interface 是 **操作環境**——前者抽象 API、後者直接面對真實 GUI / web / OS。

### 為什麼 2024-2026 是 Agent Interface 的 breakthrough 年

**Why 現在才補這課**：

- **2024-10 之前**：agent 只能跟有 API 的世界互動（呼叫 OpenAI / GitHub / Slack API、回文字）
- **2024-10**：Anthropic Computer Use beta → **agent 第一次能操作真實螢幕**
- **2025-2026**：OpenAI（Atlas + Codex desktop）/ Google（Gemini in Chrome）全進場 → 主流化
- **2026-05**：OSWorld benchmark 達 **76.26%**（superhuman vs 72% human baseline）→ 從研究 curiosity 變 production reality

**沒這個 stage 的 curriculum gap**：學完 Stage 7 你以為 done、實際上 agent 只能跟 API 對話、**不能操作沒 API 的軟體 / 真實網頁 / 跑 code**——遇 safety issue（Comet 注入 / Amazon injunction、見 §10）也沒警告過。

### 為什麼兩 track 共用

跟 Stage 5（Claude Code 生態）一樣、本 stage 是 **hub** 而非 track-specific：

- **Track A（CLI Power User）**：用 Claude Computer Use 委派桌面任務、用 Codex background mode、在 Claude Code 接 browser MCP
- **Track B（Agent Builder）**：embed browser-use 進自己 agent、用 E2B / Daytona 跑 agent-generated code、用 OpenAI Agents SDK 內建 sandbox

**兩個 track 都繞不開這 3 層 interface**——所以放 hub 位置。

## 📌 學習目標

學完本 stage 你能：

- 區分 3 層 agent interface（Computer Use / Browser Use / Sandbox）+ 跟 Tool / MCP / Harness 的關係
- 講出 Computer Use / Browser Use **mental model**（screenshot → vision → coords vs DOM-aware）
- 講出 microVM / Container / Firecracker / gVisor / Cold start 等隔離技術術語
- 知道 2026-05 OSWorld / WebArena SOTA 數字 + 解讀 reward-hacking 警告
- **Track A**：在 daily CLI 工作流接 Computer Use + browser MCP + Codex background mode
- **Track B**：用 browser-use / E2B 在自己 agent 內 embed 環境互動 + sandbox 隔離
- 設計 4 個 safety pattern（approval gate / sandbox / human-in-loop / output filter）防注入攻擊

## 🚪 進入條件

你應該已經：

- 完成 [Stage 5](05-claude-code-ecosystem.md)（懂 MCP / Skills / Plugins、Claude Code 用過 daily）
- 完成 [Stage 7](07-multi-agent-production.md)（懂 harness engineering、knows what reward-hacking warning is about）
- 對 Docker / VM 概念基礎熟悉（本章會解釋 microVM / Container 差異、但完全沒接觸過 Docker 會卡）
- **若只 Track A**：Stage 5 完成就夠，Stage 7 可選；本章 Track A 部分不依賴 build 經驗
- **若 Track B**：Stage 7 必修，否則 §9 build 範例會卡

沒到 → 回前面補。

## 📚 必修閱讀

1. [**Anthropic — Introducing Computer Use**](https://www.anthropic.com/news/3-5-models-and-computer-use) — Computer Use 原始 launch、reading 工作原理必看
2. [**Anthropic — Claude Opus 4.7 Release Notes**](https://docs.anthropic.com/en/release-notes/overview) — 2026-04 最新 Opus 4.7 含 Computer Use 改進
3. [**OpenAI — The next evolution of the Agents SDK**](https://openai.com/index/the-next-evolution-of-the-agents-sdk/) ⭐ **2026-04** — 內建 sandbox + harness 抽象、production coding agent architecturally sound milestone
4. [**OpenAI — Computer-Using Agent (CUA)**](https://openai.com/index/computer-using-agent/) — OpenAI 版 Computer Use + WebArena / OSWorld 數字
5. [**browser-use docs**](https://docs.browser-use.com/) — OSS web agent 第一名（86k+ stars）、5 行 Python 起步
6. [**Microsoft OmniParser**](https://microsoft.github.io/OmniParser/) — 開源 GUI parsing、Computer Use 重要 building block

> 💡 **挑著讀**：純 Track A 讀 1 + 2、純 Track B 必讀 3 + 5 + 6、想理解全局都讀。

## 🖱 Computer Use — 螢幕級 agent

### Mental model — 工作流跟 Why

**工作流**：
```
agent 收到任務
    ↓
1. 截圖（screenshot）→ 看到當前螢幕
    ↓
2. vision model 解析 → 識別按鈕 / 文字框 / icon
    ↓
3. 算出座標 → 「按鈕在 (453, 218)」
    ↓
4. 模擬鍵鼠 → click(453, 218) / type("hello")
    ↓
5. 再截圖 → 看結果、決定下一步
```

**Why 這個 paradigm（vs Tool Use）**：
- 大多軟體**沒 API、只有 GUI**——SAP / Excel / Photoshop / 任何傳統桌面 app、你要 agent 用就只能 screen-level
- API integration（Stage 3 Tool Use）要等廠商開介面、有時等不到
- Screen-level 是**最後一哩**——「agent 能做 human 在電腦上做的任何事」

**Why 2026 才行得通**：
- **Vision model 進步**：Claude 4.x / GPT-5.x 全 multimodal、看螢幕識別 element 準度大幅升
- **OS-level 訓練資料**：[OSWorld dataset (NeurIPS 2024)](https://github.com/xlang-ai/OSWorld) 釋出 369 個跨 OS 真實任務、讓 frontier lab 有資料訓
- **Anthropic Computer Use beta（2024-10）開啟商業競賽**——OpenAI / Google 跟上、benchmark 一路飆

### 2026 frontier 4 強對比

| Vendor | 產品 | 2026 狀態 | OSWorld | 強項 |
|---|---|---|---|---|
| **Anthropic** | [Claude Opus 4.7 / Sonnet 4.6 Computer Use](https://www.anthropic.com/news/3-5-models-and-computer-use) | GA、跨 macOS / Linux / Windows（Docker）| **Opus 4.6 達 72.7%**（近 human baseline 72%）| reasoning + code agent、Stage 5/7 主場 |
| **OpenAI** | [Codex desktop](https://openai.com/index/codex-for-almost-everything/)（April 2026）| GA、**background mode** 不搶 cursor、in-app browser、90+ plugins | CUA 38.1% | 跟 ChatGPT + Atlas 合併成 **Desktop Superapp** |
| **OpenAI** | [Computer-Using Agent (CUA)](https://openai.com/index/computer-using-agent/) | API | 38.1% / WebArena 58.1% | API-first、可整合自己 stack |
| **Google** | [Gemini in Chrome](https://gemini.google/overview/gemini-in-chrome/)（Gemini 3）| GA + Android | — | **Auto Browse** + **Chrome Skills**、Chrome Enterprise Premium $6/user/月 |
| **OpenAI Operator** | （**停運 2025-08**）| ❌ 不可用 | — | CAPTCHA / JS / session 處理不穩、被 Atlas 取代 |

→ 詳細現況見 [Agentic Browser Landscape 2026](https://nohacks.co/blog/agentic-browser-landscape-2026)、[OSWorld leaderboard](https://os-world.github.io/)

### 為什麼 OSWorld 數字差這麼大（理解 benchmark 紀律）

**現況**：

| Model | OSWorld | 跟 human baseline 距離 |
|---|---|---|
| Human baseline | **72%** | — |
| Claude Opus 4.6（Anthropic）| **72.7%** | 持平 |
| 2026-05 SOTA（最強模型）| **76.26%** | **superhuman** |
| OpenAI CUA | 38.1% | -34% |
| 多數一般 model | 30-50% | -22% ~ -42% |

**Why 比 SWE-bench 難**：
- **更開放任務**：SWE-bench 有清楚 test 判 pass / fail；OSWorld 任務 spec 模糊（"幫我把 csv 變成圖"）
- **跨多個 OS**：Ubuntu / Windows / macOS 都有
- **跨應用 chain**：常要打開 3-4 個 app（Excel → Chrome → Slack）

**Why 真實能力 ≠ 數字**（呼應 [Stage 7 §reward-hacking 警告](07-multi-agent-production.md#-agent-benchmark-landscape2026-05-最新--reward-hacking-警告)）：
- OSWorld 也在 [UC Berkeley 2026-04 reward-hacking 報告](https://rdi.berkeley.edu/blog/trustworthy-benchmarks-cont/) 名單上、被證可 hack 到 100%
- **看數字紀律**：別只看 leaderboard top、看你自己 use case 的 hold-out test 才是 ground truth

### 平台支援現況（2026-05）

| OS | Anthropic | OpenAI | Google |
|---|---|---|---|
| **macOS** | ✅ GA | ✅ Atlas + Codex desktop GA | Chrome 內 |
| **Linux** | ✅ Docker | ⚠ 較緊 | Chrome 內 |
| **Windows** | ✅ Docker | 🔜 native preview / Atlas Win coming | Chrome 內 |
| **Mobile** | — | — | ✅ Gemini in Chrome on Android |

## 🌐 Browser Use — web 級 agent

### Mental model — DOM-aware vs screen-pixel + Why

**核心區分**：

| 路線 | 怎麼工作 | 何時用 |
|---|---|---|
| **DOM-aware**（瀏覽器內、有 DOM）| 直接 query `<button id="submit">`、`document.querySelector('.cart-item')` | 一般 web app、structured page |
| **Screen-pixel + vision**（沒 DOM、看截圖）| 跟 Computer Use 一樣、screenshot → vision → coords | iframe / Canvas / Shadow DOM / 防自動化 |

**Why DOM-aware 比 screenshot 精準**：
- 直接抓 `<input name="username">` element、**不用 vision 解析像素**
- 速度快 10-100×（不跑 vision model）
- 不會 misclick（element 有確切 bounding box）
- **缺點**：JS 動態渲染 / Shadow DOM / Canvas / iframe 之內 DOM 不暴露時失效

**結論 — production browser agent pattern**：**DOM-first + screenshot fallback**——先嘗試 DOM、抓不到再用 vision。browser-use / Atlas / Comet 都用這 pattern。

### Mini-glossary（就地解釋）

| 術語 | 解釋 |
|---|---|
| **DOM**（Document Object Model）| 瀏覽器內部把 HTML 解析成的樹狀結構、可程式化 query |
| **CSS selector** | 選 element 的語法（`#submit-btn`、`.cart > li:nth-child(2)`）|
| **Shadow DOM** | Web Component 的內部 DOM、外部 DOM query 不到（如 Salesforce / Reddit 新版）|
| **iframe** | 嵌入另一個網頁、跨 origin 的 DOM 通常隔離 |
| **Canvas** | `<canvas>` 元素內的圖形、純像素、DOM 看不到內容（如 Figma / Google Sheets）|

### 閉源 AI Browser 5 強對比（2026-05）

| Browser | 來源 | 平台 | Agent Mode | 風險 / 注意 |
|---|---|---|---|---|
| **Atlas** | OpenAI（2025-10）| macOS GA、Win 🔜 | ✅（Plus / Pro / Business）| — |
| **Comet** | Perplexity | iOS / Android / Win / Mac | ✅ research 最強 | ⚠ 2026 Brave 發現可被惡意網頁注入；2026-03 federal injunction 禁存取 Amazon |
| **Dia** | [Browser Company（被 Atlassian $610M 收購）](https://efficient.app/compare/dia-vs-comet) | macOS | ❌（**不走 agent mode**、聚焦效能）| — |
| **Gemini in Chrome** | Google（Gemini 3）| Chrome 全平台 + Android | ✅ **Auto Browse** + **Chrome Skills** | Enterprise Premium $6/user/月 |
| **Operator** | OpenAI | — | ❌ **停運 2025-08** | CAPTCHA / JS / session 處理不穩 |

→ 完整比較：[Best AI Browsers 2026 Tested](https://kahana.co/blog/best-ai-browsers-2026-tested-real-workflows)、[AI Browser Comparison 2026](https://www.webfx.com/blog/ai/best-ai-browsers/)

### 開源 Browser Use 框架

| 框架 | 狀態 | 強項 |
|---|---|---|
| [**browser-use**](https://github.com/browser-use/browser-use) ⭐ | **86k+ stars、MIT** | 2026 最火 OSS、Python、5 行起步、支援 OpenAI / Claude / Gemini / Ollama |
| [**Microsoft OmniParser v2**](https://github.com/microsoft/OmniParser) | 2026 更新、Apache 2.0 | vision-based GUI parsing、60% latency 改善、ScreenSpot Pro 39.6% accuracy |
| [**OmniTool**](https://github.com/microsoft/OmniParser) | 2025-02 | Windows 11 VM 控制、可搭配 GPT-4o / o1 / DeepSeek-R1 / Qwen 2.5VL / Claude Computer Use |
| **Playwright + LLM**（DIY）| — | 不是專門 framework、但 Playwright 是 web automation 標準、加 LLM wrapper 就能用 |

**Why browser-use 86k stars 這麼火**：
- DOM-first paradigm **比 screenshot+vision 對 web 精準** + 速度快
- LLM-vendor agnostic（不綁 Claude / GPT）
- 5 行 Python 起步、entry barrier 低

### 跟 web scraping / RPA 的差別

| 工具類 | 怎麼工作 | 適合 |
|---|---|---|
| **Web scraping**（BeautifulSoup / Scrapy）| 固定 selector、純 pull data | 結構穩定的網站、只要資料 |
| **RPA**（UiPath / Power Automate）| 固定 click / type script、不 reasoning | 流程已知 + 不變的企業內部任務 |
| **Browser Agent**（本 stage）| **可 reason + 動態決定怎麼操作** | 任務描述模糊、流程可能變、需要 agent 自己探索 |

## 📦 Code Execution Sandbox — 隔離環境（含術語小辭典）

### 為什麼 agent 一定要 sandbox

**Threat model**：agent 寫 code → 在哪跑？
- ❌ **Host 機器（最壞）**：agent 可能 `rm -rf /` / 連 internet 泄資料 / 讀 `.ssh/id_rsa` / 安裝 malware
- ⚠ **同 user 隔離 process（中等）**：能擋部分但 file system / network 仍開
- ✅ **隔離 sandbox（必要）**：獨立 filesystem / process / network、出事可丟掉

**為什麼 2026 才正式變 production 要求**：
- **2026-04 OpenAI Agents SDK 更新**：[內建支援 7 個 sandbox provider](https://openai.com/index/the-next-evolution-of-the-agents-sdk/)（Blaxel / Cloudflare / Daytona / E2B / Modal / Runloop / Vercel）
- 之前都靠 [Claude Code](05-claude-code-ecosystem.md) / [Cursor](https://www.cursor.com) 的 approval gate 擋——但 production agent **無人盯、必須 sandbox**

### 🔑 隔離技術術語小辭典

新 reader 卡關常見、就地解釋：

| 術語 | 一句解釋 | 隔離強度 | 啟動速度 | 典型用途 |
|---|---|---|---|---|
| **Container**（Docker / OCI）| Linux kernel namespace + cgroups、**多 container 共用 host kernel** | 弱（kernel exploit 跨界）| 快（< 1s）| 一般 web app、低風險 task |
| **VM**（Virtual Machine）| Hypervisor 配虛擬硬體、**獨立 kernel** | 最強 | 慢（秒級）| 高風險 / enterprise |
| **microVM** | VM 的精簡版、極小 footprint、仍獨立 kernel | **強** | **快（< 100ms）** | agent sandbox 甜蜜點 |
| **Firecracker** | AWS 開源 microVM、Rust 寫、**AWS Lambda 底層**、E2B 用它做 isolation | 強 | 快 | serverless / agent |
| **gVisor** | Google 寫的「用戶空間 kernel」、攔截 syscall 自己模擬、不用 hypervisor | 中強 | 中快 | 介於 container / VM |
| **Cold start** | sandbox 從零啟動到可用的時間（Daytona 最快 27ms、E2B microVM 較慢）| — | — | latency-critical 場景關鍵 |
| **Persistence** | state 跨呼叫保留嗎（檔案 / process / network） | — | — | long-running agent 必要 |
| **GPU passthrough** | VM / microVM 訪問 host GPU 的技術（**Modal 唯一支援**）| — | — | sandbox 內跑 inference / fine-tune |

**核心要記**：
- **Container** = 快 + 隔離弱（共用 kernel）
- **VM** = 慢 + 隔離強（獨立 kernel）
- **microVM** = 兼顧（快 < 100ms + 獨立 kernel）→ **agent sandbox 多半選 microVM**

### 7 個 sandbox 對比（2026-05）

| Sandbox | 隔離技術 | 冷啟 | 強項 | 何時用 |
|---|---|---|---|---|
| [**Daytona**](https://www.daytona.io/) | Container | **< 90ms（最快 27ms）** | 啟動快、Docker 生態整合 | latency-critical |
| [**E2B**](https://github.com/e2b-dev/E2B) | **Firecracker microVM** | ~ 200ms | Python REPL iterative、最多 community template | agent 跑 Python loop |
| [**Modal**](https://modal.com/) | microVM + GPU | ~ 1s | **唯一 GPU sandbox** | sandbox 內 inference / fine-tune |
| [**Vercel Sandbox**](https://vercel.com/docs/sandbox) | Container | < 500ms | Vercel ecosystem 整合 | web stack |
| [**Cloudflare**](https://developers.cloudflare.com/workers-ai/) | Workers / Containers | < 100ms | edge global 部署 | low-latency 全球 |
| **Runloop** | — | — | 2026 OpenAI SDK 新支援 | （新進場）|
| **Blaxel** | — | — | 同上 | （新進場）|

→ 詳細 benchmark：[AI Code Sandbox Benchmark 2026 — Modal vs E2B vs Daytona](https://www.superagent.sh/blog/ai-code-sandbox-benchmark-2026)

### OpenAI Agents SDK April 2026 更新 — Why 是 milestone

**這次更新為什麼重要**：

- **之前**：production coding agent 用 OpenAI SDK 是「**prototype**」——sandbox 要自己接、harness 要自己寫、auditability 不足
- **2026-04 之後**：**architecturally sound**——SDK 內建 harness 抽象層 + sandbox 抽象層 + Codex filesystem tools

**3 個關鍵新功能**：
1. **Native harness** — agent loop / model calls / tool routing / handoffs / approvals / tracing / recovery 全在 SDK 層
2. **Native sandbox execution** — bring your own sandbox 或用內建 7 個 provider（Blaxel / Cloudflare / Daytona / E2B / Modal / Runloop / Vercel）
3. **Codex filesystem tools** — agent 寫檔 / 讀檔 / 跑 command 都有 SDK-level API

→ Python first、TypeScript 之後。**Anthropic Claude Agent SDK 早就有類似抽象**——OpenAI 終於追上。

---

<!-- 以下 §8-15 將在 Commit C 加入 -->
