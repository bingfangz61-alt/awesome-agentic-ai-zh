# Project Memory — awesome-agentic-ai-zh

> Standing instructions for any AI agent (Claude, Codex, Gemini) working on this repo. Read this **first** before touching exercises or model recommendations.

## Canonical Ollama models (verified against user's `ollama list`)

| Model tag | When to use | Notes |
|---|---|---|
| **`gemma4:e4b`** | Stage 1 + 2 (plain chat, prompt engineering) | Effective 4B params, ~7.5 GB download, CPU-friendly. **The `:e4b` tag matters** — NOT `gemma3n:e4b`, NOT `gemma3:4b`, NOT `gemma4:latest`. |
| **`gemma4:e2b`** | Low-RAM-machine alternative for Stage 1+2 | ~4 GB, runs on 4 GB RAM machines |
| **`qwen2.5:3b`** | Stage 3+ (tool use / agent / ReAct) | 1.9 GB, **reliable tool-use support** (OpenAI function-calling format), default for any agent / function-calling exercise |
| **`llama3.2:3b`** | `qwen2.5:3b` alternative for tool use | 2.0 GB, similar capability |
| **`mistral-nemo:12b`** | Higher-quality local fallback | 7.1 GB, closer-to-cloud quality |

**Wrong tags I've used in error before** (now fixed across 13 files via `.ai/.../rename_gemma.py`):
- ❌ `gemma3:4b` — older naming, replaced 2026-05-12
- ❌ `gemma3n:e4b` — wrong family, replaced 2026-05-12
- ✅ `gemma4:e4b` — correct (per user's Ollama installation screenshot)

If unsure, ask the user to run `ollama list` and verify.

## Canonical Anthropic models

| Model | Use case | Pricing (per 1M tokens) |
|---|---|---|
| **`claude-haiku-4-5`** | Cheapest cloud option, OK for all exercises | $1 input / $5 output |
| **`claude-sonnet-4-5`** | Production default, agent development | $3 input / $15 output |
| **`claude-opus-4-5`** | Highest quality, complex reasoning | $15 input / $75 output |

## Framing rules (do not violate)

1. **Claude is the canonical / production reference** in documentation positioning.
2. **Ollama is the practice default** because of cost — students should not be blocked by API fees during learning.
3. **Every exercise must ship BOTH paths**:
   - Path A (Ollama, `<details open>`, primary practice runnable)
   - Path B (Anthropic, `<details>`, optional cloud-quality comparison)
4. **Every exercise must mention budget explicitly** — single-run cost + total stage cost.
5. **Local LLMs must appear in any model recommendation list** — never list cloud-only options.

## Exercise file conventions

- `starter.py` = Ollama / OpenAI-compatible default (Path A)
- `starter_anthropic.py` = Anthropic SDK version (Path B)
- `test.py` = mock-based tests for the Ollama starter (OpenAI-compat response shape)
- `test_anthropic.py` = mock-based tests for the Anthropic starter (content-block shape)
- `requirements.txt` = both `openai` and `anthropic` pinned
- `README.md` = trilingual switcher + 怎麼跑（兩條 path）+ budget per path + walkthrough + common pitfalls
- Each starter ends with `# === 自我驗證 ===` block containing 2+ `assert` statements
- Each Python file headers Windows-cp950 UTF-8 reconfigure:
  ```python
  import sys
  if hasattr(sys.stdout, "reconfigure"):
      sys.stdout.reconfigure(encoding="utf-8", errors="replace")
  ```

## Translation rules

- **zh-TW canonical** (`.md` without language suffix). zh-Hans + en mirror.
- **Claude does translations** — do NOT delegate to Codex/Gemini.
- For zh-Hans bulk char conversion, use a per-char map (script in `.ai/2026/05/12/t2-trad-to-simp/`) then manual fix-up for remaining stragglers.

## Codex delegation rules

- Codex executes bulk batches (multiple exercises following an established pattern).
- Claude writes the pilot template + reviews codex output.
- Codex briefs must include the file structure (starter.py + starter_anthropic.py + test.py + test_anthropic.py + README.md + requirements.txt) and the framing rules above.
- Codex cannot commit (sandbox `.git` permission); Claude commits on its behalf per CLAUDE.md `~/.claude/CLAUDE.md` "agent boundary = commit boundary" rule.

## Existing curriculum state (as of 2026-05-12)

| Component | Status |
|---|---|
| Stage 0-3 inline exercises (3 langs) | ✅ Done — Path A Ollama / Path B Anthropic + budget callouts |
| Stage 3 folder `03-react-from-scratch` | ✅ Pilot rename done — `starter.py` (Ollama) + `starter_anthropic.py` (Anthropic) + dual test files |
| Stage 3 folders `02/04/05/06` | ⚪ Pending — need Ollama `starter.py` + rename existing → `starter_anthropic.py` |
| Stage 1 folder `04-cross-provider` | ✅ Multi-provider (already includes Ollama via `call_ollama` in README) |
| Stage 1 folder `05-error-handling` | ⚪ Pending — needs Ollama version with openai SDK exceptions |
| Stage 4/5/6/7 + Track A (38 exercises) | ⚪ Pending T3+ — full new write, Ollama-default by design |
| `examples/README` LLM list + budget table | ✅ Done (3 langs) |
| Per-stage budget callouts | ✅ Done for Stage 1+2+3 (3 langs each) |

## Reference scripts (in `.ai/2026/05/12/`)

- `t2-trad-to-simp/convert.py` — zh-TW → zh-Hans bulk char map (Stage 2)
- `t2-trad-to-simp/stage3_convert.py` — Stage 3 練習 1 inline section conversion
- `t2-trad-to-simp/en_swap.py` — Anthropic SDK → OpenAI SDK bulk substitution
- `t2-trad-to-simp/en_pathb_expand.py` — Compact 🦙 hint → full Path B `<details>` block
- `t2-trad-to-simp/rename_gemma.py` — `gemma3n:e4b` → `gemma4:e4b` (this commit's fix)

Keep these scripts — they're reusable for T3+ work.
