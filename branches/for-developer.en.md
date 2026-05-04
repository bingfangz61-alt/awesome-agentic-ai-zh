# For Developers — Specialized Branch

> Branching from end of Stage 7. Apply agentic AI to coding workflows.

## Use Cases

- AI pair programming (Cursor, Aider, Claude Code)
- Code review automation
- Test generation
- Multi-agent coding tasks (planning + execution)
- CLI delegation (Codex, Gemini for token-heavy code)

## Curated Projects

### Coding Agents

#### [Cursor](https://www.cursor.com/) ⭐⭐⭐⭐⭐
Editor-integrated AI pair programmer. Industry standard for AI-assisted coding.

#### [Aider](https://github.com/Aider-AI/aider) ⭐⭐⭐⭐⭐
CLI pair programmer that edits code in your repo. Open source, model-agnostic. Strong for terminal users.

#### [anthropics/claude-code](https://github.com/anthropics/claude-code) ⭐⭐⭐⭐⭐
Anthropic's official agentic coding assistant. Skills + plugins ecosystem.

#### [OpenHands (formerly OpenDevin)](https://github.com/All-Hands-AI/OpenHands) ⭐⭐⭐⭐
Open-source autonomous software development agent.

### CLI Delegation

#### [WenyuChiou/codex-delegate](https://github.com/WenyuChiou/codex-delegate) ⭐⭐⭐⭐
Claude Code skill for delegating token-heavy code work to Codex CLI. Wrapper script + result.json contract pattern.

#### [WenyuChiou/gemini-delegate-skill](https://github.com/WenyuChiou/gemini-delegate-skill) ⭐⭐⭐⭐
Same pattern but for Gemini CLI — long-context synthesis, bilingual drafting, second-opinion review.

### Code Review

#### [obra/superpowers](https://github.com/obra/superpowers) ⭐⭐⭐⭐
20+ battle-tested skills including TDD patterns, debugging, collaboration patterns. Good source for code-review skill design.

## Workflows To Master

- **AI pair programming**: Claude Code or Cursor for daily work
- **Multi-agent coding**: agent-task-splitter → codex-delegate (impl) + gemini-delegate (review) → reconciler
- **Test generation**: write skill that generates pytest tests from a function signature
- **Code review automation**: GitHub Action calling Claude API on every PR
