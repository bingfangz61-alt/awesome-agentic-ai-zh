# Testing Plan — T3+ Verification Roadmap

> Status as of 2026-05-12. Owns: `@WenyuChiou`. Tracks: what's verified, what's pending, how to verify.

This doc tracks **runtime verification** of the T3+ batch (Stage 4 / 6 / 7 — 15 Python exercises). The exercises are written and committed on branch `t3-stage-4-6-7-unverified`. **They are NOT yet on `main`** because the framework dependencies haven't been pip-installed and tested in a clean environment.

## ✅ Verified (on main)

| Batch | What | How verified |
|---|---|---|
| Phase 3 — Stage 1 + 3 folder renames (5 folders) | `starter.py` (Ollama) / `starter_anthropic.py` / both test suites | Both `python test.py` and `python test_anthropic.py` were run for each folder; all passed |
| Phase A — `stages/03-tool-use-and-hello-agent.md` inline `<details>` (練習 2-6) | 5 simplified inline blocks + zh-Hans Trad-char drift fix | `wc -l` confirms 3-lang parity; `grep` confirms no residual Trad chars |
| Phase B — `examples/stage-5/tool-calling-tutor/` skill | SKILL.md + 3 references + evals + trilingual READMEs | `yaml.safe_load` confirms frontmatter parses; `json.load` confirms evals.json valid. **NOT yet `cp`'d into `~/.claude/skills/` for live Claude Code load test** |
| Phase C — cross-references | stages/03 + stages/05 + CLAUDE.md links to tool-calling-tutor | `grep -c` confirms 10 references across 7 files |

**`main` after this push** = `ee5a1c9` (Phase C close) + this README update + this TESTING_PLAN.

## ⚠ Pending verification (on branch `t3-stage-4-6-7-unverified`)

| Batch | Folders | Files | Risk |
|---|---|---|---|
| Stage 4 — Agent frameworks | 5 (01-same-agent-two-frameworks, 02-multi-agent-roles, 03-graph-workflow, 04-codeact-vs-json-tool, 05-typed-agent) | 41 | **High** — 5 different frameworks (LangGraph / CrewAI / Smolagents / Pydantic AI), API drift between minor versions, deeply nested deps |
| Stage 6 — Memory & RAG | 5 (01-embeddings, 02-vector-db, 03-chunking-comparison, 04-full-rag-pipeline, 05-long-term-memory) | 40 | **Medium** — `chromadb` API stable since 0.4, `sentence-transformers` model download (~80MB), mostly Python-only |
| Stage 7 — Production | 5 (01-multi-agent-debate, 02-eval, 03-observability, 04-sdk-advanced, 05-deploy) | 41 (incl. Dockerfile) | **Low-Medium** — `fastapi.TestClient` is stable; only `04-sdk-advanced` has anthropic prompt-caching API which has evolved (cache_creation_input_tokens / cache_read_input_tokens) |

## Why these are quarantined

Each exercise's `test.py` was written but **not run** because:

1. **15 Python frameworks not in dev environment** — `langgraph`, `crewai`, `smolagents`, `pydantic-ai`, `chromadb`, `sentence-transformers`, `fastapi[uvicorn]`, plus deps. Estimated 30-60 min pip-install time (network + dep resolution).
2. **Sentence-transformer model download** — ~80MB first-run.
3. **API drift risk** — examples to watch:
   - **Pydantic AI** changed `result_type` → `output_type` between 0.0.x and 0.1+ (current code uses `output_type`)
   - **CrewAI** `@tool` decorator interface changed between 0.5 and 0.8 (tests have graceful fallback)
   - **Smolagents** model classes (`OpenAIServerModel` / `LiteLLMModel`) names varied across versions
   - **chromadb** `EphemeralClient` is 0.4+ only
   - **LangGraph** `InMemorySaver` vs `MemorySaver` rename
4. **Cost** — Path B (Anthropic) exercises would burn $0.05-0.10 to fully smoke-test live runs across 15 exercises.

## How to verify (next session)

Suggested execution order, sorted by risk:

### Pass 1: Static + import (~30 min, $0)

Spin up a clean venv, batch install, run only `python -c "import starter; import starter_anthropic; import test"` for each folder. Catches API drift early.

```bash
git checkout t3-stage-4-6-7-unverified
python -m venv .venv-t3 && source .venv-t3/Scripts/activate
for folder in examples/stage-4/0*/ examples/stage-6/0*/ examples/stage-7/0*/; do
  echo "--- $folder ---"
  cd $folder && pip install -q -r requirements.txt && python -c "import starter, starter_anthropic" && cd -
done
```

Fix any `ImportError` / `AttributeError` first.

### Pass 2: Mock-based test suites (~30 min, $0)

```bash
for folder in examples/stage-4/0*/ examples/stage-6/0*/ examples/stage-7/0*/; do
  echo "=== $folder ==="
  cd $folder
  python test.py && python test_anthropic.py
  cd -
done
```

Capture failures, fix, re-run. Most failures will be:
- Mock shape mismatching the actual framework response
- Missing or renamed framework class/function

### Pass 3: Live smoke tests (~1-2h, ~$0.05)

For each folder, run `python starter.py` (Ollama) and `python starter_anthropic.py` (Claude) once with real APIs. Confirms the dual-path framing actually executes end-to-end.

### Pass 4: Skill install test (~5 min, $0)

Verify the tool-calling-tutor skill loads in Claude Code:

```bash
cp -r examples/stage-5/tool-calling-tutor/SKILL.md \
      examples/stage-5/tool-calling-tutor/references \
      examples/stage-5/tool-calling-tutor/evals \
      ~/.claude/skills/tool-calling-tutor/
# Restart Claude Code
# Prompt: 「為什麼 LLM 不呼叫我的 tool」 → skill should auto-load
```

### Pass 5: Merge to main

After all passes are green, merge `t3-stage-4-6-7-unverified` to `main`:

```bash
git checkout main
git merge --ff-only t3-stage-4-6-7-unverified
git push origin main
git branch -d t3-stage-4-6-7-unverified
```

If the merge isn't fast-forward (because `main` advanced), rebase the branch first.

## Stage 5 + Track A status

23 exercises remaining (Stage 5 sub-§ 5.1-5.4 + Track A1-A3 CLI-1 through CLI-12). **Not started.** Different shape — they're mostly bash / MCP / markdown / SKILL.md authoring, not Python SDK code. The Ollama-vs-Anthropic dual-path framing doesn't apply directly.

Framing decisions needed before writing:

| Stage 5 sub-§ | Likely framing |
|---|---|
| 5.1 Claude Code 基礎 | CLI walkthrough only, no dual-path |
| 5.2 MCP | Python MCP SDK example (single path) |
| 5.3 Skills | SKILL.md authoring tutorial; the `tool-calling-tutor` we shipped is the canonical example |
| 5.4 Plugins | plugin.json + marketplace.json walkthrough |

| Track A | Likely framing |
|---|---|
| A1 CLI intro | Compare 7 CLIs (Claude Code / Codex / OpenCode / Gemini CLI / goose / Aider / Hermes) — already structured in the outline |
| A2 CLI workflow | `CLAUDE.md` authoring + slash command + portable prompt patterns |
| A3 CLI production | MCP + GitHub Actions + cost tracking + plugin sharing |

These should be scoped in a follow-up session.
