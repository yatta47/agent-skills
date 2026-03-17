# agent-skills

Reusable agent skills and sub-agents for [Claude Code](https://claude.ai/claude-code) and [Codex CLI](https://github.com/openai/codex).

## Skills

| Skill | Description |
|-------|-------------|
| [til-extract](skills/til-extract/) | Extract TILs (Today I Learned) from conversations or files and save as Markdown notes |
| [session-feedback](skills/session-feedback/) | Review a session and propose improvements to project rules, skills, and workflows |
| [pretty-mermaid](skills/pretty-mermaid/) | Render beautiful Mermaid diagrams as SVG or ASCII art with 15+ themes |

## Agents (Sub-agents)

| Agent | Description |
|-------|-------------|
| [codex-agent](agents/codex-agent.md) | Use Codex CLI as a second-opinion sub-agent for code review, design consultation, research, and more |

## Installation

### Claude Code (Plugin)

```bash
# Step 1: Add this repository as a marketplace
/plugin marketplace add yatta47/agent-skills

# Step 2: Install the plugin
/plugin install agent-skills@yatta47-agent-skills
```

Skills are available with the namespace prefix:

```
/agent-skills:til-extract
/agent-skills:session-feedback
/agent-skills:pretty-mermaid
```

The `codex-agent` sub-agent is automatically available via the Agent tool after installation.

### Codex CLI

Clone and symlink:

```bash
git clone https://github.com/yatta47/agent-skills.git
cd your-project
ln -s /path/to/agent-skills/skills .agents/skills
```

Then use skills directly:

```
/til-extract
/session-feedback
/pretty-mermaid
```

### Claude Code (Manual)

Copy skills and agents into your project:

```bash
# Skills
cp -r agent-skills/skills/til-extract .claude/skills/
cp -r agent-skills/skills/session-feedback .claude/skills/
cp -r agent-skills/skills/pretty-mermaid .claude/skills/

# Agents
mkdir -p .claude/agents
cp agent-skills/agents/codex-agent.md .claude/agents/
```

## Configuration

### til-extract

By default, TIL files are saved to `til/` in your project root. To customize, add to your `CLAUDE.md`:

```
TIL output directory: knowledge/til/
```

## Credits

- `pretty-mermaid` is based on [intellectronica/agent-skills](https://github.com/intellectronica/agent-skills) (CC0-1.0)

## License

MIT
