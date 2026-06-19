# claude-code-bootstrap

One-file bootstrap for a complete Claude Code setup — plugins, MCPs, swarm orchestration, coding rules.

## Usage

1. Open Claude Code in any directory
2. Say: **"Read BOOTSTRAP.md and execute it"**

That's it. The agent handles everything.

## What gets installed

| | Plugin / Tool | Source |
|--|--------------|--------|
| 🧠 | superpowers | [obra/superpowers-marketplace](https://github.com/obra/superpowers-marketplace) |
| 🪨 | caveman | [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) |
| 📦 | context-mode | [mksglu/context-mode](https://github.com/mksglu/context-mode) |
| ⚡ | ecc (Everything Claude Code) | [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) |
| 🐦 | canary | [wizenheimer/canary](https://github.com/wizenheimer/canary) |
| 🤖 | codex | [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc) |
| 🐝 | ruflo (swarm orchestration) | brew install ruflo |
| 🔁 | feature-fix-swarm | [austinmao/feature-fix-swarm](https://github.com/austinmao/feature-fix-swarm) |
| 🔌 | MCPs | Context7, Playwright, Sequential Thinking (+ optional GitHub, Exa) |

## What does NOT get installed

- Your API keys — you provide those when prompted
- Tenant-specific skills or agents — generic only
- Any personal config

## License

MIT
