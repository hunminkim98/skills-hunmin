# output-debt

[한국어](../ko/output-debt.md) · [Docs home](README.md) · [SKILL.md](../../cursor/output-debt/SKILL.md)

Score leftover agent outputs from 5 to 1. Move anything below 3 into `garbage/` with a memo. Leave 3 and above where they are. Do not delete.

## Why it exists

Agent work is a lot of fast trials. Each trial writes a file. After a day you have `render.png`, `render2.png`, `render_final.png`, and nobody remembers which one the README means. That is cognitive debt: the human and the next agent both have to guess.

Public cleanup skills usually do one of two things. They delete tmp and screenshots, or they split KEEP vs ARCHIVE and ask you to confirm buckets. Deleting is too sharp. A binary keep/drop is too crude for files you might want next week.

This skill keeps a **scale**. 5 is the live artifact. 1 is a failed export. Only scores **below 3** leave the working tree, and they go to `garbage/`, not `/dev/null`. You empty that folder later, or you move a file back using the path in the memo.

It is not unused-code cleanup. It is not [wiki-for-llm](wiki-for-llm.md). Wiki notes stay in the wiki.

## How it works

Slash only. The agent does not start because `git status` is noisy.

1. Scope: a folder you named, or the project root minus never-move trees (`node_modules`, `.git`, source that is the product).
2. Nominate run outputs: untracked dumps, `tmp/`, duplicate `*_v2*` next to a newer copy, renders no README points at. An untracked `.ts` in `src/` is unfinished work, not a render.
3. Score 1–5 with one line of evidence. Rules live in [`references/scoring.md`](../../cursor/output-debt/references/scoring.md). If the agent cannot tell, it scores **3** and leaves the file.
4. Move 1 and 2 into `garbage/YYYY-MM-DD/`, keeping the original relative path. Write `MEMO.md`. Layout: [`references/garbage-layout.md`](../../cursor/output-debt/references/garbage-layout.md).
5. If the repo has a `.gitignore` and `garbage/` is not already tracked, add `garbage/` so git status stays about real work.
6. Chat report: counts, moves, memo path. [`references/report-shape.md`](../../cursor/output-debt/references/report-shape.md).

Never-move list: [`references/never-move.md`](../../cursor/output-debt/references/never-move.md). Secrets are not copied into `garbage/`. Source, `AGENTS.md`, and `llm-wiki/` are not nominated.

## When to use it

Use `/output-debt` after a stretch of experiments, before a commit, or when you and the agent are arguing about which CSV is current.

Skip it for "delete node_modules," for refactoring dead code, for writing the work log, and for rewriting a prompt.

This skill is **slash only**.

## Install

```bash
npx skills add hunminkim98/skills-hunmin --skill output-debt --agent cursor
```

Add `--global` if every Cursor project on the machine should see it. See the [docs home](README.md) for the picker.

## How to use it

1. New Agent chat.
2. `/output-debt`, optionally with a folder (`tmp/`, `demo/`).
3. Read Stayed vs Moved. Open `garbage/YYYY-MM-DD/MEMO.md` if anything moved.
4. Restore by moving a file back to the original path in the memo. Delete from `garbage/` only when you mean it.

You should not see product source relocated. If you do, the skill was ignored; move it back.

## With other skills

- [wiki-for-llm](wiki-for-llm.md) records decisions. This skill moves files. After a cleanup you can ask for a wiki note if the quarantine rule should stick.
- [deep-analyze](deep-analyze.md) if you only want to know what a folder is, with no moves.
- Do not run this instead of [discussion](discussion.md) when the fight is "which design do we ship."

## Limits

The agent will not empty `garbage/` for you. A bad score of 3 leaves clutter on purpose. GitHub will not see quarantined files if `garbage/` is gitignored. That is the point for local cognitive load. If you need the quarantine on a remote, stop gitignoring and commit it yourself.
