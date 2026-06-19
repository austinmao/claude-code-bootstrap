# Claude Code Bootstrap

> **For the AI agent:** Read this file top to bottom and execute each step. Do not ask the user to run commands — run them yourself using Bash. After each step, confirm success before continuing. If a step fails, diagnose and fix before moving on.

---

## What this installs

| Component | What it does |
|-----------|-------------|
| **superpowers** | Workflow meta-skills: brainstorming, debugging, TDD, git worktrees |
| **caveman** | Terse response mode — saves tokens on long sessions |
| **context-mode** | Context window management tools |
| **ecc** | Everything Claude Code: 100+ agents, skills, and coding rules |
| **canary** | Browser QA automation |
| **codex** | OpenAI Codex integration |
| **ruflo** | Multi-agent swarm orchestration |
| **feature-fix-swarm** | Feature/fix lifecycle with Stop hooks and run-state tracking |
| **MCPs** | Context7 (live docs), Playwright, Sequential Thinking + optional GitHub/Exa |

---

## Step 1 — Verify prerequisites

```bash
claude --version
node --version
brew --version
```

If `claude` is missing: stop and tell the user to install Claude Code from https://claude.ai/code.  
If `brew` is missing on macOS: install Homebrew first (`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`).

---

## Step 2 — Add plugin marketplaces

Run each of these:

```bash
claude plugin marketplace add https://github.com/obra/superpowers-marketplace
claude plugin marketplace add https://github.com/JuliusBrussee/caveman
claude plugin marketplace add https://github.com/mksglu/context-mode
claude plugin marketplace add https://github.com/affaan-m/everything-claude-code
claude plugin marketplace add https://github.com/wizenheimer/canary
claude plugin marketplace add https://github.com/openai/codex-plugin-cc
```

Verify: `claude plugin marketplace list`

---

## Step 3 — Install plugins

```bash
claude plugin install superpowers
claude plugin install caveman
claude plugin install context-mode
claude plugin install ecc
claude plugin install canary
claude plugin install codex
```

Verify: `claude plugin list`

---

## Step 4 — Install ruflo (swarm orchestration)

```bash
brew install ruflo
```

Then register as MCP:

```bash
claude mcp add ruflo -- /opt/homebrew/bin/ruflo mcp start
```

Verify: `ruflo --version`

---

## Step 5 — Install MCP servers (no key required)

```bash
claude mcp add context7 -- npx -y @upstash/context7-mcp
claude mcp add sequential-thinking -- npx -y @modelcontextprotocol/server-sequential-thinking
claude mcp add playwright -- npx -y @executeautomation/playwright-mcp-server
```

---

## Step 6 — Install MCP servers (keys required)

Ask the user:

> "Do you have a GitHub Personal Access Token? (github.com → Settings → Developer settings → Personal access tokens → Generate new token, scopes: repo + read:org)"

If yes, ask them to paste their token, store it in a variable, validate it is non-empty and at least 20 characters, then run:
```bash
# Replace ACTUAL_TOKEN_HERE with the value the user provided
claude mcp add github -e GITHUB_PERSONAL_ACCESS_TOKEN=ACTUAL_TOKEN_HERE -- npx -y @modelcontextprotocol/server-github
```

> "Do you have an Exa API key? (exa.ai → Dashboard → API Keys)"

If yes, ask them to paste their key, validate it is non-empty, then run:
```bash
# Replace ACTUAL_KEY_HERE with the value the user provided
claude mcp add exa -e EXA_API_KEY=ACTUAL_KEY_HERE -- npx -y exa-mcp-server
```

**Important:** Never run these commands with placeholder text. If the user skips, skip the step — they can add keys later with `claude mcp add`.

---

## Step 7 — Install feature-fix-swarm

```bash
git clone https://github.com/austinmao/feature-fix-swarm ~/feature-fix-swarm
cd ~/feature-fix-swarm && bash setup.sh
```

This installs Stop and SessionStart hooks for feature/fix lifecycle tracking.

---

## Step 8 — Copy coding rules

```bash
mkdir -p ~/.claude/rules/common
```

Write each file below verbatim to `~/.claude/rules/common/<filename>`:

**coding-style.md**
```markdown
# Coding Style

## Immutability (CRITICAL)
ALWAYS create new objects, NEVER mutate existing ones.

## File Organization
- 200–400 lines typical, 800 max
- High cohesion, low coupling
- Organize by feature/domain, not by type

## Functions
- <50 lines
- Max 4 levels of nesting — use early returns

## Error Handling
- Explicit at every level
- Never silently swallow errors
- User-friendly messages in UI; detailed context in server logs

## Input Validation
- Validate at system boundaries only (user input, external APIs)
- Schema-based validation where available
- Fail fast with clear error messages
```

**git-workflow.md**
```markdown
# Git Workflow

## Commit Format
<type>: <description>

Types: feat, fix, refactor, docs, test, chore, perf, ci

## PRs
1. Analyze full commit history (git diff [base]...HEAD)
2. Comprehensive summary
3. Include test plan

## Worktrees
Parallel specs MUST use separate git worktrees.
Never switch branches in the main worktree.
```

**testing.md**
```markdown
# Testing

## Minimum 80% coverage

## TDD (mandatory)
1. Write test first (RED)
2. Run — must FAIL
3. Implement (GREEN)
4. Run — must PASS
5. Refactor (IMPROVE)
```

**security.md**
```markdown
# Security

## Before every commit
- No hardcoded secrets (API keys, passwords, tokens)
- All user inputs validated
- Parameterized queries only (no SQL string concatenation)
- CSRF protection enabled
- Rate limiting on all endpoints
- Error messages don't leak sensitive data

## Secret management
NEVER hardcode secrets. ALWAYS use environment variables.
```

**performance.md**
```markdown
# Performance

## Model delegation
- Haiku: workers, searches, mechanical edits, formatting
- Sonnet: main development, orchestration (default)
- Opus: architecture decisions, security audits, adversarial verification

## Context window
Avoid large refactors in the last 20% of context window.
```

---

## Step 9 — Global CLAUDE.md (optional)

Ask the user:

> "Set up a global CLAUDE.md at ~/.claude/CLAUDE.md with starter coding rules? This applies to all Claude Code sessions. (yes/no)"

If yes, write to `~/.claude/CLAUDE.md`:

```markdown
# Global Claude Code Rules

## Code Style
- Immutable patterns — return new objects, never mutate
- Functions <50 lines, files <800 lines, nesting max 4 levels
- Explicit error handling — never swallow errors
- Validate inputs at system boundaries only

## Git
- Commit: `<type>: <description>` (feat/fix/refactor/docs/test/chore/perf/ci)
- Parallel work → separate git worktrees, never switch branches in main

## Testing
- TDD: write test first, then implement
- Minimum 80% coverage

## Security
- Zero hardcoded secrets — env vars always
- Parameterized queries only
- Rate limit all endpoints

## Model Selection
- Haiku: workers, searches, mechanical edits
- Sonnet: development, orchestration (default)
- Opus: architecture, security review, adversarial verification
```

---

## Step 10 — Verify

```bash
claude plugin list
claude mcp list
ruflo --version
ls ~/feature-fix-swarm/
ls ~/.claude/rules/common/
```

Report results to the user. Call out anything missing or failed.

---

## Done

Tell the user:

> Bootstrap complete. Restart Claude Code for all plugins to activate.
>
> **Quick reference:**
> - `/ecc-guide` — discover all ECC skills and agents
> - `/feature` — start a tracked feature run (feature-fix-swarm)
> - Ruflo swarms: `mcp__ruflo__swarm_init` for 3+ parallel agents
> - Caveman mode: type `/caveman` for terse responses
