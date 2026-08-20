# skills-hunmin docs

[한국어](../ko/README.md)

These pages explain the Cursor skills in this repository. They are written for a person who will install a skill and then use it in chat. The `SKILL.md` files remain the instructions the agent follows. If a page and a `SKILL.md` ever disagree, trust the skill file.

Cursor-specific skills live under [`cursor/`](../../cursor/). You pick the ones you want. Nothing here installs every skill by force.

## Which skill do I use?

| You want to… | Use |
|---|---|
| Turn a rough idea into a prompt you can paste into any chat | [prompt-optimizer](prompt-optimizer.md) |
| Improve a prompt, approve it with Y/N, then run or copy it | [meta-prompting](meta-prompting.md) |
| Keep work notes so the next agent does not ask you to recap | [wiki-for-llm](wiki-for-llm.md) |
| Investigate one question strictly, without changing files | [deep-analyze](deep-analyze.md) |
| Debate a hard trade-off with expert sub-agents, and stay in the loop | [discussion](discussion.md) |

These jobs do not replace each other. A fact hunt is not a debate. A debate is not a work log. A work log is not an article library (that would be a Karpathy-style `raw/` wiki, which this repo does not ship).

## How installation works

Run this in a **real terminal** (Cursor Terminal or iTerm). Agent chat skips the picker.

```bash
npx skills add hunminkim98/skills-hunmin
```

The CLI lists every skill it finds, including ones nested under `cursor/`. You search, toggle with space, and confirm with enter. Then you choose this project or every Cursor project on the machine, and which agents should receive the files.

Useful variants:

```bash
# One skill, this project, Cursor only
npx skills add hunminkim98/skills-hunmin --skill meta-prompting --agent cursor

# Every skill the picker would have shown, this project, Cursor only
npx skills add hunminkim98/skills-hunmin --agent cursor

# Same, but available in all Cursor projects
npx skills add hunminkim98/skills-hunmin --agent cursor --global
```

After install, open a **new** Agent chat and type `/` plus the skill name. Skills marked “slash only” in the pages below will not start themselves.

`npx skills add` copies skill folders. It does not edit `AGENTS.md` by itself. [wiki-for-llm](wiki-for-llm.md) may add a one-line pointer the first time it runs in a repo that has no richer closeout.

## How the collection is organized

```text
cursor/
  meta-prompting/     # needs prompt-optimizer next to it
  prompt-optimizer/
  wiki-for-llm/
  deep-analyze/
  discussion/
```

`meta-prompting` reads its sibling `prompt-optimizer`. Install both if you want the Y/N flow. The other three skills stand alone.

## Skill pages

- [meta-prompting](meta-prompting.md)
- [prompt-optimizer](prompt-optimizer.md)
- [wiki-for-llm](wiki-for-llm.md)
- [deep-analyze](deep-analyze.md)
- [discussion](discussion.md)
