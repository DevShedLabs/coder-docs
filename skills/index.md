# Skills

- **Progressive disclosure** every skill's name + one-line description sits in the system prompt at near-zero token cost; the full instructions body only loads when the model calls `use_skill`, keeping a large skill library cheap to carry
- **Shared by chat and Orchestrator** one skill library, `~/.coder/skills/<name>/SKILL.md`, available to the interactive chat agent and every Orchestrator stage (PM, builders, reviewer) alike
- **Managed in the Prompts panel** a "Skills" section lists every skill with its description, alongside a create (+) button and per-skill delete; clicking a skill opens its `SKILL.md` for editing like any other file
- **Just markdown** a skill is a folder with a `SKILL.md` (YAML frontmatter for `name`/`description`, then free-form instructions below); no code or registration required to add one

## Layout

```
~/.coder/skills/
  my-skill/
    SKILL.md        # frontmatter: name, description — then free-form instructions
    reference.md     # optional bundled reference file
    templates/
      foo.md          # bundled files can be nested in subfolders
```
