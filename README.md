# claude-code-bootstrap

One-file bootstrap for a complete Claude Code setup — plugins, MCPs, agents, swarm orchestration, and coding rules.

## Usage

1. Clone this repo: `git clone https://github.com/austinmao/claude-code-bootstrap`
2. Open Claude Code inside the cloned directory
3. Say: **"Read BOOTSTRAP.md and execute it"**

That's it. The agent handles everything.

## What gets installed

### Plugins
| | Plugin / Tool | Source |
|--|--------------|--------|
| 🧠 | superpowers | [obra/superpowers-marketplace](https://github.com/obra/superpowers-marketplace) |
| 🪨 | caveman | [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) |
| 📦 | context-mode | [mksglu/context-mode](https://github.com/mksglu/context-mode) |
| ⚡ | ecc (Everything Claude Code) | [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) |
| 🐦 | canary | [wizenheimer/canary](https://github.com/wizenheimer/canary) |
| 🤖 | codex | [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) |

### Tools & MCPs
| | Tool | Notes |
|--|------|-------|
| 🐝 | ruflo (swarm orchestration) | brew install ruflo |
| 🔁 | feature-fix-swarm | [austinmao/feature-fix-swarm](https://github.com/austinmao/feature-fix-swarm) |
| 🔌 | context7 | Live docs for any library |
| 🎭 | playwright | Browser automation |
| 🔗 | sequential-thinking | Structured reasoning chains |
| 🧠 | memory | Persistent knowledge graph across sessions |
| 🌐 | fetch | Web fetching |
| 🐙 | github | (optional — needs token) |
| 🔍 | exa | (optional — needs API key) |

### Agents (12 specialists)
Copied to `~/.claude/agents/` — available in every project:

| Agent | Specialization |
|-------|----------------|
| nextjs-frontend-engineer | Next.js 15, React 19, TailwindCSS, shadcn/ui |
| nextjs-backend-engineer | Next.js API routes, tRPC, server patterns |
| python-engineer | async SQLAlchemy, Pydantic v2, uv, Ruff |
| python-backend-infrastructure-engineer | FastAPI, PostgreSQL, Docker |
| api-integration-engineer | REST APIs, Prisma ORM, multi-tenant |
| ai-agent-workflow-engineer | LangGraph, RAG, multi-agent orchestration |
| mcp-server-engineer | MCP server dev (TypeScript + Python) |
| n8n-engineer | n8n workflow automation, custom nodes |
| trpc-api-engineer | tRPC v11, Zod, Drizzle ORM |
| code-auditor | Multi-language code quality audit |
| testing-quality-assurance-engineer | pytest, Vitest, Playwright, coverage |
| ui-designer | Visual design, design systems, accessibility |

### Coding Rules (9 files → `~/.claude/rules/common/`)
`coding-style` · `git-workflow` · `testing` · `security` · `performance` · `agents` · `code-review` · `development-workflow` · `patterns`

## What does NOT get installed

- Your API keys — you provide those when prompted
- Tenant-specific skills or agents — generic only
- Any personal config

## License

MIT
