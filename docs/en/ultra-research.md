# ultra-research

[한국어](../ko/ultra-research.md) · [Docs home](README.md) · [SKILL.md](../../cursor/ultra-research/SKILL.md)

One slash. The chair decides whether you need the web, this repo, a decision — and in what order. Then it runs the sibling skills as themselves. It does not glue their manuals into one prompt.

## Why it exists

`deep-research`, `deep-analyze`, and `discussion` were written so they would not steal each other's job. That is still right. A lot of real asks sit on more than one job: "Should we put hybrid search into our batch pipeline?" needs the outside world, this tree, and a call.

Public orchestrators usually freeze the order (methods pipelines), write `plan.json` / debate folders (Cursor cloud orchestrate, dialectic kits), or make you pick the pipeline. A fixed web → code → debate run wastes the two skills that exist to stay narrow or to refuse a panel.

This skill keeps a **chair**. The chair classifies, skips, and sometimes reverses the order. Child rules stay in force.

## How it works

Slash only. Needs the three siblings **next to it** (`deep-research`, `deep-analyze`, `discussion`). Install those too, or pick them in the same CLI run.

1. Bind the question. Mark **web / repo / decision**. Rules: [`references/classify.md`](../../cursor/ultra-research/references/classify.md).
2. Show one path line. Do not wait for approval. Ask only if the sentence names two unrelated targets.
3. Run each chosen stage by reading that sibling `SKILL.md` first. Handoff packet: [`references/handoff.md`](../../cursor/ultra-research/references/handoff.md).
4. Web and repo may run in parallel when the file or symbol is already in the question. Decision is last, and only if a trade-off remains. Discussion's `AskQuestion` gates stay.
5. Chat report: [`references/report-shape.md`](../../cursor/ultra-research/references/report-shape.md). Path, answer, per-stage evidence.

No `research/` folder. No playbook. No wiki. Missing sibling: print the install command and skip that stage. Do not invent a cheap copy.

## When to use it

Use `/ultra-research` when you do not want to pick the pipeline, and the ask might need more than one of: wide web, this repo, a decision.

Skip it when you already know the stage. Then call that skill. Skip it for prompt work, wiki closeout, and leftover files.

This skill is **slash only**.

## Install

```bash
npx skills add hunminkim98/skills-hunmin --skill ultra-research --agent cursor
npx skills add hunminkim98/skills-hunmin --skill deep-research --agent cursor
npx skills add hunminkim98/skills-hunmin --skill deep-analyze --agent cursor
npx skills add hunminkim98/skills-hunmin --skill discussion --agent cursor
```

Or pick all four in the interactive installer. See the [docs home](README.md).

## How to use it

1. New Agent chat.
2. `/ultra-research` plus the ask ("Should we put hybrid search into our batch pipeline?").
3. Read the path line. You do not approve it unless two targets were confused.
4. If a discussion stage starts, answer the mid-debate question. That is the child skill, not extra ceremony.
5. Read Path → Answer → the stage blocks.

You should not get all three stages every time. If you do, the chair ignored the marks.

## With other skills

- A single known job is still [deep-research](deep-research.md), [deep-analyze](deep-analyze.md), or [discussion](discussion.md).
- Keep a decision with [wiki-for-llm](wiki-for-llm.md) after, if the next agent needs it.
- Approve the *question* first with [meta-prompting](meta-prompting.md) if the brief is still mush.
- Not a substitute for [output-debt](output-debt.md).

## Limits

Three parallel swarms in one sitting is expensive. The chair should have skipped a stage rather than max out. A missing sibling is a skip, not a rewrite of that skill. Implementation does not start unless you ask. Harmful dual-use topics are refused in one paragraph.
