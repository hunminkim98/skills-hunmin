# skills-hunmin

Personal Cursor agent skills.

`meta-prompting` uses sibling `prompt-optimizer` to rewrite a draft, then asks Y or N before using it. Install both skills together.

## Install

Use the [skills](https://github.com/vercel-labs/skills) CLI. It is the `pip install` equivalent for agent skills.

If you omit the flags, the CLI asks whether to install into the current project or globally, and which skills to take.

**This project only** (default). Cursor reads them from `.agents/skills/`.

```bash
npx skills add hunminkim98/skills-hunmin --agent cursor --skill '*'
```

**All Cursor projects** on this machine.

```bash
npx skills add hunminkim98/skills-hunmin --agent cursor --skill '*' --global
```

**Ask each time**

```bash
npx skills add hunminkim98/skills-hunmin
```

Start a new Agent chat afterwards and type `/meta-prompting` or `/prompt-optimizer`.

## Skills

- [meta-prompting](meta-prompting/SKILL.md)
- [prompt-optimizer](prompt-optimizer/SKILL.md)
