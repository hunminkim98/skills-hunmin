# skills-hunmin

Personal Cursor agent skills. Add more skill folders over time; installers pick only the ones they want.

`meta-prompting` uses sibling `prompt-optimizer` to rewrite a draft, then asks Y or N before using it. If you want that flow, select both.

## Install

Use the [skills](https://github.com/vercel-labs/skills) CLI. Run this in a real terminal (Cursor Terminal or iTerm), not inside an Agent chat. Agent shells skip the picker.

```bash
npx skills add hunminkim98/skills-hunmin
```

That opens a terminal UI:

1. Search and checkbox-select skills (type to filter, space to toggle, enter to confirm)
2. Choose this project or global
3. Choose Cursor (and any other agents)

**One skill, no UI**

```bash
npx skills add hunminkim98/skills-hunmin --skill meta-prompting --agent cursor
```

**This project only, skip the scope prompt**

```bash
npx skills add hunminkim98/skills-hunmin --agent cursor
```

**All Cursor projects**

```bash
npx skills add hunminkim98/skills-hunmin --agent cursor --global
```

Start a new Agent chat afterwards and type `/` plus the skill name.

## Skills

- [meta-prompting](meta-prompting/SKILL.md)
- [prompt-optimizer](prompt-optimizer/SKILL.md)
