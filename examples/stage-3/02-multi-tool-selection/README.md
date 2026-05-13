> **繁體中文** | [简体中文](./README.zh-Hans.md) | [English](./README.en.md)

# 練習 2：多工具選擇

這個練習讓 Claude 在同一輪回應裡面面對三個工具：`web_search`、`calculator`、`calendar_lookup`。重點不是工具本身有多厲害，而是看見 schema 的 `name`、`description`、`input_schema` 如何影響模型判斷「這題該呼叫哪一個工具」。

## 執行方式

```bash
pip install -r requirements.txt
export ANTHROPIC_API_KEY=sk-ant-...
python starter.py
python test.py
```

`starter.py` 使用 Anthropic SDK 0.40+ 的 `client.messages.create(model=, tools=, messages=...)` 介面。問題送進 Claude 後，程式會讀取第一個 `tool_use` block，依照工具名稱查表執行本地函式，再印出工具名稱、輸入參數與 observation。

## 測試重點

`test.py` 不需要 API key。它用 `unittest.mock.MagicMock` 與 `types.SimpleNamespace` 模擬 Anthropic 回傳，固定讓模型分別選擇計算機、行事曆與搜尋工具。測試會檢查三件事：工具清單完整、Claude 選到的工具名稱正確、工具輸入能轉成對應 observation。

## 容易踩坑

多工具選擇最常見的錯誤是 description 寫得太像一般說明文件，而不是給模型做決策的判斷規則。`calendar_lookup` 應該明確描述日期與事件查詢；`web_search` 則適合外部或近期資訊；`calculator` 只處理算式。三者邊界越清楚，模型越少把「最新消息」誤丟給行事曆，或把「明天會議」誤丟給搜尋。

## 🦙 Path B — 本機 Ollama（qwen2.5:3b）

完整 pattern 看 [`../03-react-from-scratch/starter.py`](../03-react-from-scratch/starter.py)。三個 SDK 差異要點：

1. **Schema wrap**：Anthropic 直接 `tools=[{name, description, input_schema}, ...]`；OpenAI-compat（Ollama）要包一層 `tools=[{"type": "function", "function": {name, description, parameters}}, ...]`
2. **Response 抓 tool call**：Anthropic 從 `resp.content[i].type == "tool_use"`；OpenAI-compat 從 `resp.choices[0].message.tool_calls[i].function.name`
3. **input 格式**：Anthropic 是 dict（自動 parse）；OpenAI-compat 是 JSON string（自己 `json.loads(tc.function.arguments)`）

Tool selection 邏輯**完全跨 backend**——schema 寫好、qwen2.5:3b 一樣會挑對 tool。可以拿這題對照 Claude vs qwen2.5 「在哪幾題會挑錯」、是觀察小 model 邊界的好實驗。
