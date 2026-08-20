# humanizer

[한국어](../ko/humanizer.md) · [Docs home](README.md) · [SKILL.md](../../cursor/humanizer/SKILL.md)

Rewrite prose that reads like a chatbot. English blocks and Korean blocks get different rules. One slash command.

## Why it exists

The usual "humanizer" skills are monolingual. [blader/humanizer](https://github.com/blader/humanizer) hunts English tells (`delve`, em dashes, "Great question!"). [DaleSeo/korean-skills](https://github.com/DaleSeo/korean-skills) hunts Korean ones (`에 대해`, `~것입니다`, `되어진다`). Paste those two `SKILL.md` files together and they fight: English dash rules land on Korean sentences, Korean comma rules land on English ones, and the model loads seventy-plus patterns for a three-line edit.

This repo needed one installable skill because the README itself is bilingual. You should not have to remember which humanizer owns which heading.

It is also not "always on." An always-on unslop pass turns install docs into essays. You run `/humanizer` when you want a pass.

## How it works

The agent is a **router**, not a blender.

1. It takes pasted text or a file path. No input, it asks once and stops.
2. It masks protected spans first: code, commands, frontmatter, numbers, URLs, skill names. See [`references/leave-alone.md`](../../cursor/humanizer/references/leave-alone.md).
3. It splits the rest into **language blocks** (a heading plus the prose under it, or a run of paragraphs with the same majority script). Not sentence-by-sentence.
4. Latin-majority blocks load [`references/en-patterns.md`](../../cursor/humanizer/references/en-patterns.md) only. Hangul-majority blocks load [`references/ko-patterns.md`](../../cursor/humanizer/references/ko-patterns.md) only. The unused catalog stays closed.
5. It rewrites stock phrasing and keeps every claim. Technical docs stay neutral. No invented jokes, no invented facts.
6. It checks negation, names, and numbers, then estimates how much of the wording moved. Over about half, it stops and asks instead of replacing your draft.

A writing sample you paste wins on voice (rhythm, dashes, contractions). It does not win on facts.

Detect-only is available: "don't rewrite, just show the tells."

The catalogs are short working lists with attribution in [`references/sources.md`](../../cursor/humanizer/references/sources.md). They are not a vendored copy of the upstream skills, so this repo does not try to track every upstream version.

## When to use it

Use `/humanizer` on a draft that already says the right thing and sounds machine-made: a README, a changelog, a blog paragraph, a Korean announcement that reads like translated English.

Skip it when you want a prompt ([prompt-optimizer](prompt-optimizer.md) / [meta-prompting](meta-prompting.md)), a fact audit ([deep-analyze](deep-analyze.md)), a trade-off ([discussion](discussion.md)), or a work log ([wiki-for-llm](wiki-for-llm.md)). Skip code. Skip "make this undetectable."

This skill is **slash only**.

## Install

```bash
npx skills add hunminkim98/skills-hunmin --skill humanizer --agent cursor
```

Add `--global` if every Cursor project on the machine should see it. See the [docs home](README.md) for the picker.

If you already installed `blader/humanizer` under the same agent, both may register as `/humanizer`. Uninstall one of them if the slash menu is ambiguous.

## How to use it

1. New Agent chat.
2. `/humanizer` and the draft, or a path (`docs/en/README.md`).
3. Optional: paste two or three paragraphs of your own writing and say to match that voice.
4. Read the rewrite (or the path). The "what changed" list should be a handful of lines, not a paper.

For a bilingual file, expect one pass that treats the English section and the Korean section as separate blocks.

User-facing chatter follows the language you used in the request. The draft stays in its own language.

## With other skills

- Write the prompt first ([prompt-optimizer](prompt-optimizer.md)), then humanize the prompt only if the prompt itself sounds like slop. Do not humanize, then execute, unless you asked for that.
- After [discussion](discussion.md), humanize the recommendation if you want to publish it. Discussion itself writes no files.
- Do not run this instead of [deep-analyze](deep-analyze.md). Cleaner sentences are not a substitute for evidence.

## Limits

The agent will not add a personality the source never had. Korean technical 합니다-체 stays 합니다-체. Protected spans can make a page still look a bit stiff; that is preferred to a broken install command. Upstream skills keep evolving; this catalog is ours and will drift on purpose.
