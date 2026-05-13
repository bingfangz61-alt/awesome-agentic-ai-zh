> **繁體中文** | [简体中文](./README.zh-Hans.md) | [English](./README.en.md)

# 練習 6：Function schema 設計

這個練習用 `starter_bad.py` 與 `starter_good.py` 對照同一個問題：「把攝氏 32 度換成華氏」。壞 schema 的 description 太模糊，參數都用 string，沒有 required，也沒有 enum；模型很容易把溫度轉換丟給 `process_data`。好 schema 則把工具用途、參數型別、必填欄位與 enum 都寫清楚，讓模型能穩定選到 `convert_temperature`。

## 執行方式

```bash
pip install -r requirements.txt
export ANTHROPIC_API_KEY=sk-ant-...
python starter_bad.py
python starter_good.py
python test.py
```

`starter_bad.py` 故意保留 anti-pattern：`description` 只有「Process data」和「Convert a value」，LLM 無法判斷邊界。`starter_good.py` 則明確寫出 `process_data` 只適合 JSON 表格摘要，不適合溫度轉換；`convert_temperature` 使用 `value: number` 與 `unit: "celsius" | "fahrenheit"`。

## 測試重點

`test.py` 用 mock 示範兩種結果：bad schema 會選到錯的 `process_data`，good schema 會選到 `convert_temperature` 並得到 `89.6 fahrenheit`。測試也直接檢查 good schema 有 `required` 與 `enum`，而 bad schema 缺少這些限制。

## 延伸閱讀

schema 是 prompt 的一部分，而且是模型做工具選擇時最依賴的 prompt。寫 schema 時不要只想「人看得懂」，要想「模型能不能用它排除錯誤工具」。更多規則可以對照 [`resources/schema-design-cheatsheet.md`](../../../resources/schema-design-cheatsheet.md)：清楚用途、正確型別、必填欄位、enum 收斂，以及結構化錯誤回傳。

## 🦙 Path B — 本機 Ollama（qwen2.5:3b）

兩個 starter（`starter_bad.py` + `starter_good.py`）的對照邏輯**完全跨 backend**——bad schema 一樣會讓 qwen2.5:3b 挑錯 tool。Ollama 轉換照 [`../03-react-from-scratch/starter.py`](../03-react-from-scratch/starter.py) pattern：

- TOOLS_SPEC 包一層 `{"type": "function", "function": {name, description, parameters}}`
- response 從 `r.choices[0].message.tool_calls[0].function.name` 抓 tool 選擇
- `function.arguments` 是 JSON string、`json.loads(...)` 才拿 dict

**反而更有教學意義**：小 model（qwen2.5:3b）對 schema 質量比大 model **更敏感**——壞 schema 在 Claude haiku 上可能還能猜對，在 qwen2.5:3b 上幾乎必錯。**拿這題對照 Anthropic vs Ollama**、最能體會 schema 設計為什麼是 prompt engineering 的核心子題。
