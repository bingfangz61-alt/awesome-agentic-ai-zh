# For Researchers — Specialized Branch

> Branching from end of Stage 7. Apply agentic AI to research workflows.

## Use Cases

- Literature triage and matrix building
- Paper memory extraction (claims, figures, citations)
- Multi-agent paper review (peer review patterns)
- NotebookLM brief verification
- Reference management automation

## Curated Projects

### Research Workflow Marketplaces

#### [WenyuChiou/ai-research-skills](https://github.com/WenyuChiou/ai-research-skills) ⭐⭐⭐⭐

5-plugin Claude Code marketplace, 14 skills covering literature triage, paper memory, NotebookLM brief verification, Zotero curation, research design helper. Install: `claude plugin marketplace add WenyuChiou/ai-research-skills`

#### [WenyuChiou/zotero-skills](https://github.com/WenyuChiou/zotero-skills) ⭐⭐⭐

Programmatic Zotero CRUD via Claude Code. Search, add, classify, annotate, organize literature.

#### [WenyuChiou/research-hub](https://github.com/WenyuChiou/research-hub) ⭐⭐⭐⭐

AI-operable research workspace integrating Zotero, Obsidian, NotebookLM. Use any two or all three through CLI, MCP, REST.

#### [WenyuChiou/academic-writing-skills](https://github.com/WenyuChiou/academic-writing-skills) ⭐⭐⭐

Claude Code skill for rigorous academic paper writing, revision, banned-word audit, journal format checks.

### Research Frameworks

#### [WenyuChiou/WAGF](https://github.com/WenyuChiou/WAGF) ⭐⭐⭐⭐

Governance layer for LLM-driven agent-based models. 6-stage validation pipeline. 3 reference implementations (flood adaptation, multi-agent flood, Colorado irrigation).

#### [flonat/claude-research](https://github.com/flonat/claude-research) ⭐⭐⭐

Claude Code infrastructure for PhD researchers — skills, agents, hooks, rules for academic workflows. Strong LaTeX/bibliography focus.

### Multi-Agent for Research

#### [WenyuChiou/agent-collab-skills](https://github.com/WenyuChiou/agent-collab-skills) ⭐⭐⭐⭐

5 skills for multi-agent orchestration applied to research workflows. Task splitter, output reconciler, debate, shared memory, acceptance gate.

## Required Reading

1. [The Effortless Academic — Claude Code beginner guides](https://effortlessacademic.com/claude-code-and-cowork-for-academics-beginner-guide-part-1/)
2. [Pedro Sant'Anna — Researcher setup guide](https://paulgp.substack.com/p/getting-started-with-claude-code)

## Workflows To Master

- **Literature triage**: research-hub `auto` → ai-research-skills `literature-triage-matrix` → output to Obsidian
- **Paper draft cycle**: paper-memory-builder → academic-writing-skills → multi-agent review (codex + gemini)
- **Multi-agent research run**: agent-task-splitter → parallel codex/gemini tasks → output reconciler → acceptance gate
