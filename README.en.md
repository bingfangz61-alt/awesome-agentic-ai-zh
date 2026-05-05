# awesome-agentic-ai-zh

[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Status](https://img.shields.io/badge/status-Phase%204%20complete%20%C2%B7%20134%20projects-success)](#phase-1-current-state)
[![Lang](https://img.shields.io/badge/lang-English-blue)](README.en.md) [![繁中](https://img.shields.io/badge/語言-繁體中文-red)](README.md)

> **English companion to the [繁體中文 canonical README](README.md).**

A learning roadmap for agentic AI — from your first LLM API call to shipping multi-agent production systems. **Structured as a 7-stage path, not a flat list**, with curated projects, hello-world demos, and required reading at every stage.

> Stage detail pages (00-07) and branch files are currently in English; full zh-TW translation is Phase 2 work.

---

## Why this exists

Most "awesome" lists for AI agents are flat catalogs — useful when you already know what you're looking for, useless when you're trying to figure out **what to learn next**.

This repo is a **structured learning roadmap**:

- 7 stages from prerequisites to production
- Hello-X projects you must run (not just read)
- Curated projects categorized by stage and audience
- English canonical with curated Chinese-language entry points where they exist
- Honest time estimates (14-19 weeks minimum, 5-6 months realistic)

If you're a learner trying to break into agentic AI without getting lost in the noise — this is for you.

---

## The 7-Stage Learning Map

```mermaid
flowchart LR
    S0["Stage 0<br/>Foundations"] --> S1["Stage 1<br/>LLM Basics"]
    S1 --> S2["Stage 2<br/>Prompt"]
    S2 --> S3["Stage 3 ⭐<br/>Tool Use<br/>Hello Agent"]
    S3 --> S4["Stage 4<br/>Frameworks"]
    S4 --> S5["Stage 5 ⭐⭐<br/>Claude Code"]
    S5 --> S6["Stage 6<br/>Memory · RAG"]
    S6 --> S7["Stage 7<br/>Multi-Agent · Advanced"]
    S7 --> R["🔬 Researcher"]
    S7 --> D["💻 Developer"]
    S7 --> T["🎓 Teacher"]
    S7 --> K["📊 Knowledge Worker"]

    style S0 fill:#f3f4f6,stroke:#6b7280
    style S3 fill:#fef3c7,stroke:#b45309
    style S5 fill:#fde68a,stroke:#92400e
    style R fill:#dbeafe,stroke:#1e40af
    style D fill:#dcfce7,stroke:#166534
    style T fill:#fce7f3,stroke:#9d174d
    style K fill:#f3e8ff,stroke:#6b21a8
```

```
Stage 0  Foundations           (Python · CLI · git · API · JSON)         1-2 wks
Stage 1  LLM Fundamentals      (tokens · API · model comparison)         1 wk
Stage 2  Prompt Engineering    (system prompts · few-shot · CoT)         1-2 wks
Stage 3  Tool Use & Hello Agent ⭐ (function calling · ReAct · 5 hello-X) 2-3 wks
Stage 4  Agent Frameworks      (LangGraph · AutoGen · CrewAI · ...)      2-3 wks
Stage 5  Claude Code Ecosystem ⭐⭐ (MCP · Skills · Plugins)              3-4 wks
Stage 6  Memory · RAG · Advanced (vector DBs · long-term memory)         2 wks
Stage 7  Multi-Agent · Advanced (orchestration · eval · SDK)             2-4 wks
```

**Total main path: 14-19 weeks minimum, ~5-6 months realistic** at 5-8 hr/week part-time. The lower bound assumes you skip Stage 0 and don't get stuck on framework installs.

After main path, choose a specialized branch (**not sure which?**):

```mermaid
flowchart TD
    Q1{What's your main work?}
    Q1 -->|Papers / lit / experiments| R["🔬 Researcher<br/>for-researcher"]
    Q1 -->|Code / system maintenance| D["💻 Developer<br/>for-developer"]
    Q1 -->|Teaching / curriculum| T["🎓 Teacher<br/>for-teacher"]
    Q1 -->|Reports / meetings / analysis| K["📊 Knowledge Worker<br/>for-knowledge-worker"]

    style R fill:#dbeafe,stroke:#1e40af
    style D fill:#dcfce7,stroke:#166534
    style T fill:#fce7f3,stroke:#9d174d
    style K fill:#f3e8ff,stroke:#6b21a8
```

- 🔬 [For Researchers](branches/for-researcher.md)
- 💻 [For Developers](branches/for-developer.md)
- 🎓 [For Teachers](branches/for-teacher.md) — *currently the smallest section; community contributions especially welcome*
- 📊 [For Knowledge Workers](branches/for-knowledge-worker.md)

---

## Note on self-citation

About a sixth of the curated projects (~12 entries) are repos maintained by this catalog's author (`WenyuChiou/...`). They're included as concrete pattern examples (multi-plugin marketplace, single-plugin bundle, single-skill plugin, sub-CLI delegation, governance layer). Each entry's notes section explains the *pattern* it teaches. If a non-self repo teaches the same pattern more cleanly, please open a PR — see CONTRIBUTING.md.

---

## Quick Reference: Stages At A Glance

| Stage | Title | Key Question | Detailed page |
|---|---|---|---|
| 0 | Foundations | Do I have the basics? | [stages/00-foundations.md](stages/00-foundations.md) |
| 1 | LLM Fundamentals | What is an LLM, really? | [stages/01-llm-basics.md](stages/01-llm-basics.md) |
| 2 | Prompt Engineering | How do I make LLMs behave? | [stages/02-prompt-engineering.md](stages/02-prompt-engineering.md) |
| 3 | Tool Use & Hello Agent ⭐ | How do I build my first agent? | [stages/03-tool-use-and-hello-agent.md](stages/03-tool-use-and-hello-agent.md) |
| 4 | Agent Frameworks | Which framework should I learn? | [stages/04-agent-frameworks.md](stages/04-agent-frameworks.md) |
| 5 | Claude Code Ecosystem ⭐⭐ | How do I extend Claude Code? | [stages/05-claude-code-ecosystem.md](stages/05-claude-code-ecosystem.md) |
| 6 | Memory · RAG · Advanced | How do agents remember? | [stages/06-memory-rag.md](stages/06-memory-rag.md) |
| 7 | Multi-Agent · Advanced | How do I run multi-agent systems with eval + observability? | [stages/07-multi-agent-production.en.md](stages/07-multi-agent-production.en.md) |

---

## How to Use This Repo

1. **Skim the 7 stages above** to find where you are.
2. **Click into the matching stage page** (links above). Each page has:
   - Learning goals (what you'll be able to do after)
   - Entry conditions (prerequisites)
   - Required reading (3-5 links)
   - Hello-X projects you must run
   - Curated case-study projects (with my notes on each)
   - Self-check questions before moving on
3. **Don't skip Stage 3 Hello Agent.** Reading without doing the 5 hello-X projects = wasted time.
4. **Stage 5 is where most readers spend the most time.** That's expected.

---

## Curation Criteria

Every project listed has been evaluated on:

- **Active maintenance** (commits within last 6 months)
- **Quality of documentation** (README clarity, hello-world reproducibility)
- **Educational value** (does it teach a generalizable lesson?)
- **License clarity** (avoid no-license repos)
- **Trustworthiness** (well-known maintainer or org)

Recommendation stars (⭐ to ⭐⭐⭐⭐⭐):
- ⭐⭐⭐⭐⭐ — Must-read for the stage
- ⭐⭐⭐⭐ — Highly recommended, study this
- ⭐⭐⭐ — Solid example, worth running
- ⭐⭐ — Useful reference, browse if interested
- ⭐ — Niche / advanced / for completeness

---

## Related Awesome Lists

This repo doesn't try to replace flat awesome lists. Use them when you already know what to look for:

- [**hesreallyhim/awesome-claude-code**](https://github.com/hesreallyhim/awesome-claude-code) — broad Claude Code resources catalog (currently restructuring)
- [**wong2/awesome-mcp-servers**](https://github.com/wong2/awesome-mcp-servers) — flat MCP server catalog
- [**punkpeye/awesome-mcp-servers**](https://github.com/punkpeye/awesome-mcp-servers) — alternative MCP list
- [**travisvn/awesome-claude-skills**](https://github.com/travisvn/awesome-claude-skills) — Claude Skills catalog
- [**modelcontextprotocol/servers**](https://github.com/modelcontextprotocol/servers) — official MCP reference servers
- [**datawhalechina/hello-agents**](https://github.com/datawhalechina/hello-agents) — Datawhale Chinese tutorial (zh-CN)
- [**WangRongsheng/awesome-LLM-resources**](https://github.com/WangRongsheng/awesome-LLM-resources) — comprehensive zh-CN LLM resources catalog (8k+ stars)
- [**HqWu-HITCS/Awesome-Chinese-LLM**](https://github.com/HqWu-HITCS/Awesome-Chinese-LLM) — open-source Chinese LLM catalog (22k+ stars)

---

## Phase 1: Current State

This is Phase 1 — the 7-stage spine with anchor curation (~80 projects). Phase 2 work:
- Native zh-TW companion translation
- 100+ additional curated projects
- Self-citation reduction as community contributes alternatives
- Stack-at-a-glance diagram in Stage 5
- `resources/style-guide.md` for terminology consistency

## Contributing

PRs welcome. See [CONTRIBUTING.md](CONTRIBUTING.md). Highest-value contributions:

- Add a project to a stage with explanation of why it teaches that stage
- Translate a stage page to 繁中
- Flag a project that's gone stale or unmaintained

---

## License

MIT. Maintained by [@WenyuChiou](https://github.com/WenyuChiou).
