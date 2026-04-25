# Hermes Skill Graph Architecture

Agent-native skill system architecture — the routing layer, context layer, and manifest pattern.

Based on [Agent-Native Systems and Skill Graphs](https://baselinestudio.design/blog/agent-native-systems-and-skill-graphs) by Trent Mitchell.

## Three Layers

| Layer | Purpose | Location |
|-------|---------|----------|
| **Skills** | Domain methodologies | Per-skill repos |
| **Context** | Business knowledge (identity, voice, preferences) | `context/` |
| **Frameworks** | Cross-cutting reusable patterns | Per-skill repos |

## Files

- `CANONICAL.md` — The routing layer. Read first, every time. Maps tasks to skills, defines workflow orchestration.
- `context/identity.md` — Agent voice, values, boundaries. Loaded by every skill.
- `context/EXAMPLE-user.md` — Example user preferences file. Copy and customize.
- `context/manifest.yaml` — Declares what context exists and what loads where.

## Manifest Pattern

Every skill declares what it needs in YAML frontmatter:

```yaml
manifest:
  always_load:    # Loaded every time
    - CANONICAL.md
    - context/identity.md
  context:        # Business-specific, loaded per domain
    - context/user.md
  references:     # Depth when needed
    - templates/
```

## Five-Step Workflow

1. **Plan** → State understanding, outline approach, wait for approval
2. **Clarify** → Gather information, ask if ambiguous
3. **Load context** → Read manifest, load relevant files
4. **Execute** → Domain-specific work
5. **Verify** → Quality checks, binary pass/fail

## Portability

Works with Claude Code, Cursor, Windsurf, Codex, GitHub Copilot, JetBrains AI. Agent reads CANONICAL.md and knows what to do.

## License

MIT
