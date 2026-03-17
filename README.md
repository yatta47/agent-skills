# agent-skills

Reusable agent skills for [Claude Code](https://claude.ai/claude-code) and [Codex CLI](https://github.com/openai/codex).

## Skills

| Skill | Description |
|-------|-------------|
| [til-extract](skills/til-extract/) | Extract TILs (Today I Learned) from conversations or files and save as Markdown notes |
| [session-feedback](skills/session-feedback/) | Review a session and propose improvements to project rules, skills, and workflows |
| [pretty-mermaid](skills/pretty-mermaid/) | Render beautiful Mermaid diagrams as SVG or ASCII art with 15+ themes |

## Installation

### Claude Code (Plugin)

```bash
/plugin install agent-skills@yatta47/agent-skills
```

Then use skills with the namespace prefix:

```
/agent-skills:til-extract
/agent-skills:session-feedback
/agent-skills:pretty-mermaid
```

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

### Manual (any agent)

Copy the skill folder into your project's skills directory:

```bash
cp -r agent-skills/skills/til-extract .claude/skills/
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
