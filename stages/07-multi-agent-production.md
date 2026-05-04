# Stage 7 — Multi-Agent · Production

> [English](./07-multi-agent-production.en.md) | **繁體中文**

⏱ **時間估計**：2-4 週（約 15-30 小時）

最後一個階段。你正從「我會做 agent」走向「我能在 production 跑起來，多個 agent 協作、有 eval、有 observability、會 deploy」。

## 📌 學習目標

- 設計 multi-agent orchestration 模式（debate、planner-executor、peer review）
- 為 agent 架一套 evaluation harness
- 加上 observability（tracing、logging、cost tracking）
- 用 Anthropic SDK / OpenAI SDK 做 production deploy（進階功能：streaming、prompt caching、batching）
- 把 agent deploy 到 production（Docker、serverless、monitoring）

## 📚 必修閱讀

1. [**Anthropic — Building Effective Agents**](https://www.anthropic.com/engineering/building-effective-agents) — 用 production 的角度再讀一次
2. [**Anthropic — Prompt Caching**](https://www.anthropic.com/news/prompt-caching) — 90% 成本下降的技巧
3. [**Anthropic — Message Batches API**](https://docs.anthropic.com/en/docs/build-with-claude/batch-processing) — 非同步 batch job
4. **任一 eval framework 的文件** — promptfoo 或 LangSmith 或 weave

## 🛠 Hello-X

- **Hello Multi-Agent** — 兩個 agent 辯論一個題目，第三個 agent 當裁判
- **Hello Eval** — 替 agent 寫 eval，跑 N 次量成功率
- **Hello Observability** — 把 LangSmith / Helicone / weave 接上 agent，看 trace
- **Hello SDK Advanced** — 在同一次呼叫裡用 streaming + prompt caching + tool use
- **Hello Deploy** — 把 agent 包進 Docker，deploy 到雲（任何平台都行）

## 🎯 精選 Projects

### Multi-Agent Orchestration

#### [WenyuChiou/agent-collab-skills](https://github.com/WenyuChiou/agent-collab-skills)

| 推薦度 | ⭐⭐⭐⭐ |
|---|---|

**教什麼**：5 個用在 multi-agent run 的 skill（task splitter、output reconciler、debate、shared memory、acceptance gate）。Claude Code multi-agent workflow 的範例。

**適合誰**：在 Claude Code 環境裡做 multi-agent。

---

#### [microsoft/autogen](https://github.com/microsoft/autogen)

Stage 4 已提過。在 production 場景下，AutoGen 的 GroupChat 協作模式是 multi-agent 辯論 / brainstorming 的好參考。

---

#### [crewAIInc/crewAI](https://github.com/crewAIInc/crewAI)

Stage 4 已提過。要做角色式的 multi-agent（例如 research → writer → reviewer 流水線），CrewAI 是最簡單的 production pattern。

---

#### [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph)

Stage 4 已提過。要 production 加上 audit trail、checkpoint、human-in-the-loop，LangGraph 領先。

---

### Evaluation Frameworks

#### [promptfoo/promptfoo](https://github.com/promptfoo/promptfoo)

| Stars | ★ 20k+ |
|---|---|
| License | MIT |
| 推薦度 | ⭐⭐⭐⭐⭐ |

**教什麼**：以 YAML 為基礎的 prompt 跟 agent eval harness。可以跨模型比較、在 CI 跑回歸測試。

**適合誰**：把 eval 流程標準化。取代「我用眼睛看一下就好」。

**怎麼跑**：
```bash
npx promptfoo init
# 編輯 promptfooconfig.yaml
npx promptfoo eval
```

---

#### [EleutherAI/lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness)

| Stars | ★ 12k+ |
|---|---|
| License | MIT |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：學術等級的 eval framework，內建幾百個標準 benchmark（MMLU、HellaSwag、GSM8K）。

**適合誰**：你需要主張「我們在 benchmark Y 上拿到 X%」的時候。比較研究風格。

---

#### [openai/evals](https://github.com/openai/evals)

| Stars | ★ 18k+ |
|---|---|
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：OpenAI 的 eval framework。可以針對特定 use case 寫客製 eval。

**適合誰**：你需要 OpenAI 專屬 eval、或想回饋上游時。

---

### Observability

#### [langfuse/langfuse](https://github.com/langfuse/langfuse)

| Stars | ★ 26k+ |
|---|---|
| License | MIT（開源）+ 付費雲端 |
| 推薦度 | ⭐⭐⭐⭐⭐ |

**教什麼**：開源的 LLM observability——traces、sessions、evals、prompt management。

**適合誰**：自架的 production observability。LangSmith 的開源替代方案，實力很強。

---

#### [LangSmith](https://www.langchain.com/langsmith)（商業）

**教什麼**：LangChain 的 observability 平台。Trace、eval、prompt 迭代。

**適合誰**：整套 stack 都在 LangChain / LangGraph 上面。只有 hosted 版。

---

#### [Helicone](https://github.com/Helicone/helicone)

| Stars | ★ 5k+ |
|---|---|
| License | Apache 2.0（開源）+ 付費雲端 |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：用 proxy 做 LLM observability——當作 OpenAI/Anthropic client 的替身，順便拿到 logging + caching。

**適合誰**：不想改程式、想快速上 instrumentation 時。

---

#### [weave（Weights & Biases 出品）](https://github.com/wandb/weave)

| 推薦度 | ⭐⭐⭐⭐ |
|---|---|

**教什麼**：W&B 出的 tracing + eval framework。跟他們的 ML 平台整合。

**適合誰**：團隊已經在用 W&B 做 ML 實驗追蹤。

---

### Anthropic SDK 進階

#### [anthropics/anthropic-sdk-python](https://github.com/anthropics/anthropic-sdk-python)

| 推薦度 | ⭐⭐⭐⭐⭐ |
|---|---|

**教什麼**：官方 Python SDK。streaming、async、tool use、prompt caching、batches、files API。

**適合誰**：直接基於 Claude API 做 production 應用。

---

#### [anthropics/anthropic-sdk-typescript](https://github.com/anthropics/anthropic-sdk-typescript)

**教什麼**：Python SDK 的 TS 版本。

**適合誰**：TypeScript / Node / web app。

---

#### [Anthropic Cookbook — Advanced patterns](https://github.com/anthropics/anthropic-cookbook)

之前已提過。特別是 `prompt_caching.ipynb`、`tool_use/`、`multimodal/` 三個 notebook,教 production 等級的 SDK 用法。

---

### Deployment

#### [BentoML/BentoML](https://github.com/bentoml/BentoML)

| Stars | ★ 8k+ |
|---|---|
| License | Apache 2.0 |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：把任何 ML/LLM model 包成 production API。Docker + serving framework。

**適合誰**：把 agent 包成可 deploy 的 service。

---

#### [LangServe](https://github.com/langchain-ai/langserve)

**教什麼**：把 LangChain app deploy 成 REST API。底層用 FastAPI。

**適合誰**：以 LangChain 為基礎的 agent 想快速 deploy。

---

#### [datawhalechina/self-llm](https://github.com/datawhalechina/self-llm)

| 欄位 | 內容 |
|---|---|
| Maintainer | datawhalechina |
| 語言 | 中文（zh-CN） |
| Stars | ★ 30k+ |
| License | Apache-2.0 |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：開源大模型食用指南——一份完整的中文指南，講怎麼在 Linux 上 fine-tune 跟 deploy 開源 LLM。涵蓋 Qwen / Llama / GLM / 多模態模型，全參數 + LoRA + deployment 都有。

**適合誰**：要自架開源 LLM 的中文團隊。training-to-deployment 整個流程的 production 等級中文教學。

---

### [vLLM](https://github.com/vllm-project/vllm)

| Stars | ★ 79k+ |
|---|---|
| License | Apache 2.0 |
| 推薦度 | ⭐⭐⭐⭐ |

**教什麼**：高吞吐量的 LLM serving。可以在 production 跑開源模型。

**適合誰**：自架開源 LLM（Llama、Qwen 等等）取代付費 API 的場景。

---

### Production 案例研究

#### [WenyuChiou/WAGF](https://github.com/WenyuChiou/WAGF)

| 推薦度 | ⭐⭐⭐⭐ |
|---|---|

**教什麼**：給 LLM 驅動的 agent-based model 用的 production 等級 governance 層。6 階段驗證流水線抓 hallucination、邏輯漂移、不安全的狀態變更。跨模型 ablation。3 個參考實作。

**適合誰**：研究 production LLM-agent 系統怎麼處理可靠度問題。

---

## ✅ Stage 7 之後的自我檢查

你能不能：
- [ ] 設計一個 multi-agent 系統，協作協定講得清楚
- [ ] 在 CI 跑自動 eval pipeline
- [ ] 把 observability（tracing）接到 production agent
- [ ] 用 prompt caching 在實際工作量上把成本降 50% 以上
- [ ] 把 agent deploy 到雲端（任何 provider）

如果都可以 → 你已經跑完主路線。挑一個[特化分支](../README.md#the-7-stage-learning-map)，或回過頭來貢獻這份 repo。

## 💡 接下來

你已經有基礎能力了。接下來 6-12 個月應該專注在：
1. **挑一個 production 系統** 從 prototype 推到 production
2. **回饋上游**（LangGraph、AutoGen、MCP servers、Anthropic cookbook）
3. **讀論文**——agent 研究進展很快
4. **做出看得到的東西**——開源一個真的工具，不要再寫教學了
