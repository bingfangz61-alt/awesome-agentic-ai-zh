> **繁體中文** | [简体中文](./README.zh-Hans.md) | [English](./README.en.md)

# `examples/` — 動手練習可跑範例

> [← 回主路線 README](../README.md)

學習地圖每個 stage 都有「動手練習」section、講「該做什麼」。這個資料夾補上**真的可以跑的範例 code**——複製 → 裝依賴 → `python starter.py` 看到預期輸出。

## 目錄結構

```
examples/
├── stage-3/                     # Tool Use & Agent 入門
│   ├── 03-react-from-scratch/   # 練習 3：從零實作 ReAct
│   │   ├── starter.py           # 主程式（~70 行可跑）
│   │   ├── test.py              # 自我驗證（pure assert、無 pytest）
│   │   ├── README.md            # 200-400 字走查（+.zh-Hans.md +.en.md）
│   │   └── requirements.txt     # 依賴釘版本
│   └── ...
├── stage-1/
└── ...
```

短的練習（≤30 LOC）直接以 `<details>` 收摺塞在 stage 檔內、不開資料夾。長的（>30 LOC）才開資料夾——避免 stage 檔被 code block 撐爆。

## 怎麼跑任一個範例

```bash
cd examples/stage-3/03-react-from-scratch
pip install -r requirements.txt
export ANTHROPIC_API_KEY=sk-ant-...   # 各範例頂端會說它要哪個 key
python starter.py                     # 跑真的 API 看輸出（會花一點點錢、約 $0.001）
python test.py                        # 跑驗證（用 mock、不花錢）
```

## 設計原則

| 維度 | 規則 |
|---|---|
| 程式長度 | starter ≤80 LOC、超過拆檔 |
| 依賴 | stdlib + 最多 2 個 pip 套件、釘版本 |
| 測試 | 純 `assert`、不用 pytest、reader 跑 `python test.py` 看 ✅ |
| 註解 | 中文（zh-TW 為主）、變數 / 函式名英文 |
| 自我驗證 | 每個 starter.py 結尾必有 `# === 自我驗證 ===` 區塊 |
| 環境變數 | 頂端註解寫清楚需要哪些 key |
| Free-tier 友善 | 用最便宜 model（claude-haiku / Ollama）、註解寫怎麼換 Sonnet |
| **Windows 編碼** | **每個 .py 頂端必須有 UTF-8 reconfigure**（見下） |

### Windows cp950 編碼 fix（每個 starter.py / test.py 必加）

Windows 預設 console 是 cp950（Big5）、印不出 emoji 跟非 Big5 中文。每個 `.py` 檔頂端 import 區後立刻加：

```python
import sys
if hasattr(sys.stdout, "reconfigure"):
    sys.stdout.reconfigure(encoding="utf-8", errors="replace")
```

否則 Windows reader 在 PowerShell / cmd 跑會炸 `UnicodeEncodeError: 'cp950' codec can't encode character '✅'`。

## 沒 API key 也能練習嗎？

可以的兩條路：
1. **Ollama 本機跑**：每個有 Ollama 替代版本的 starter 會有 `starter_ollama.py` 對照
2. **Mock 模式**：所有 `test.py` 都用 `unittest.mock` 不打 API、reader 可以先看程式邏輯通過再決定要不要花錢跑真實 API

## 對應 stage 索引

| Stage | 練習 | 範例位置 |
|---|---|---|
| 1 LLM 基礎 | 6 個 | inline 4 + folder 2（`examples/stage-1/`） |
| 2 Prompt eng | 4 個 | 全 inline |
| **3 Tool use** | **6 個** | inline 1 + folder 5（`examples/stage-3/`） |
| 4 Frameworks | 5 個 | 全 folder（`examples/stage-4/`） |
| 5 Claude Code 生態 | 11 個 | inline 6 + folder 5（`examples/stage-5/`） |
| 6 Memory/RAG | 5 個 | 全 folder（`examples/stage-6/`） |
| 7 Multi-agent | 5 個 | inline 1 + folder 4（`examples/stage-7/`） |
| Track A1-A3 | 12 個 | 全 inline、外加 2 個小 folder（CLI-9 / CLI-10） |

→ T1 完成範圍：**只有 Stage 3 全部 6 個**（剩餘 stage 按 plan 分批推進）。

## 貢獻 / 報錯

跑不過、結果跟預期輸出對不上、或想補一個新練習：
- 開 issue 標 `examples` label
- 或直接 PR、follow 本資料夾「設計原則」表格的規則

## 為什麼這樣分（不直接全塞 stage 檔）

1. **Stage 檔保持 readable**：學習地圖讀者不一定要看 code、只想理解 concept；長 code block 干擾閱讀流
2. **範例可獨立演進**：API SDK 升版、model name 改、範例需要單獨 commit、不污染學習地圖 git log
3. **Reader 可以 clone 單一 example**：`svn export` 或 `git clone --filter=tree:0` 只抓一個資料夾
4. **未來 CI**：example 失敗不應 block mdbook deploy；分開可讓 CI 有條件性檢查
