# skills-hunmin docs

[한국어](../ko/README.md)

These pages are for someone who will install a skill and then use it in chat. The agent still follows each `SKILL.md`. If a page and a skill file disagree, trust the skill file.

Cursor skills live under [`cursor/`](../../cursor/). Pick the ones you want. Nothing here force-installs the whole set.

## Which skill do I use?

| You want to… | Use |
|---|---|
| Turn a rough idea into a prompt you can paste into any chat | [prompt-optimizer](prompt-optimizer.md) |
| Improve a prompt, approve it with Y/N, then run or copy it | [meta-prompting](meta-prompting.md) |
| Keep work notes so the next agent does not ask you to recap | [wiki-for-llm](wiki-for-llm.md) |
| Investigate one question strictly, without changing files | [deep-analyze](deep-analyze.md) |
| Debate a hard trade-off with expert sub-agents, and stay in the loop | [discussion](discussion.md) |
| Make English or Korean prose sound less like a chatbot | [humanizer](humanizer.md) |
| Sort leftover agent outputs: keep in place or quarantine | [output-debt](output-debt.md) |

Do not swap these jobs. A fact hunt is not a design choice. A debate is not a work log. This repo does not ship a Karpathy-style `raw/` wiki. Cleaning chatbot phrasing is a separate pass. Quarantining old renders is not deleting dead code.

## How installation works

Run this in a **real terminal** (Cursor Terminal or iTerm). Agent chat skips the picker.

```bash
npx skills add hunminkim98/skills-hunmin
```

The CLI lists every skill it finds, including ones nested under `cursor/`. Search, toggle with space, confirm with enter. Then choose this project or every Cursor project on the machine, and which agents should receive the files.

Useful variants:

```bash
# One skill, this project, Cursor only
npx skills add hunminkim98/skills-hunmin --skill meta-prompting --agent cursor

# Every skill the picker would have shown, this project, Cursor only
npx skills add hunminkim98/skills-hunmin --agent cursor

# Same, but available in all Cursor projects
npx skills add hunminkim98/skills-hunmin --agent cursor --global
```

After install, open a **new** Agent chat and type `/` plus the skill name. Skills marked "slash only" in the pages below will not start themselves.

`npx skills add` copies skill folders. It does not edit `AGENTS.md` by itself. [wiki-for-llm](wiki-for-llm.md) may add a one-line pointer the first time it runs in a repo that has no richer closeout.

## How the collection is organized

```text
cursor/
  meta-prompting/     # needs prompt-optimizer next to it
  prompt-optimizer/
  wiki-for-llm/
  deep-analyze/
  discussion/
  humanizer/
  output-debt/
```

`meta-prompting` reads its sibling `prompt-optimizer`. Install both if you want the Y/N flow. The other skills stand alone.

## Skill pages

- [meta-prompting](meta-prompting.md)
- [prompt-optimizer](prompt-optimizer.md)
- [wiki-for-llm](wiki-for-llm.md)
- [deep-analyze](deep-analyze.md)
- [discussion](discussion.md)
- [humanizer](humanizer.md)
- [output-debt](output-debt.md)
