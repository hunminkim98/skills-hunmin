---
name: output-debt
description: Scores existing agent outputs from 5 to 1 and moves scores below 3 into garbage/ with a memo. Use when the user invokes /output-debt, or asks to sort keep vs throwaway artifacts, quarantine old renders, or reduce clutter from repeated experiments. Do not use for code cleanup, wiki closeout, prompt rewriting, or deleting secrets.
disable-model-invocation: true
---

# Output debt

Repeated agent runs leave files. Humans and the next agent then cannot tell which file is the live one. This skill scores those outputs and quarantines the weak ones. It does not delete.

This is not unused-code cleanup. It is not [wiki-for-llm](../wiki-for-llm/SKILL.md) (that writes notes). It is not a trash-emptying script.

Slash only. Do not start because `git status` looks messy.

## Hard rules

1. **Score 1 through 5.** Do not use keep/delete as the first cut. Read `references/scoring.md`.
2. **Below 3 moves. 3 and up stay.** Scores 1 and 2 go to `garbage/`. Scores 3, 4, and 5 stay where they are.
3. **When unsure, score 3.** A wrong quarantine costs more than a leftover file. Bias toward leaving the file in place.
4. **Never delete.** Quarantine is a move plus a memo. Emptying `garbage/` is a later human decision.
5. **Never touch the never-move list.** Read `references/never-move.md` first. Source, secrets, git metadata, and live docs stay.
6. **One run, one dated folder.** Layout is in `references/garbage-layout.md`. Do not dump files onto the `garbage/` root.
7. **Match the user's language** in chat.

Refuse harmful dual-use requests in one short paragraph. No steps.

## Workflow

### 1. Scope

If the user named a folder, stay inside it. If they did not, use the project root, but skip `node_modules/`, virtualenvs, `.git/`, and other never-move trees.

If there is nothing that looks like an agent output, say so and stop. Do not invent clutter.

### 2. Nominate

Look for files and folders that are *outputs of a run*, not the product itself. Typical signals:

- Untracked generated files (`git status`)
- `tmp/`, `tmp`, `outputs/`, `results/`, screenshot dumps, Playwright artifacts
- Duplicate names (`*copy*`, `*_v2*`, `final_final*`) sitting next to a newer copy
- Renders, CSVs, notebooks, or drafts that no README, test, or import points at

Do not treat every untracked file as junk. An untracked source file under `src/` or `frontend/` is not an output.

### 3. Score

For each nominee, assign 1–5 with one sentence of evidence (path referenced from X, superseded by Y, untracked dump from a failed run). Read `references/scoring.md`. Write the score before you move anything.

### 4. Move scores below 3

Create `garbage/` only when at least one file will move. Follow `references/garbage-layout.md`.

- Tracked file: `git mv` into the dated folder, keeping the original relative path under it
- Untracked file: filesystem move, same layout
- Write `MEMO.md` in that dated folder: path, score, why, original location

If `.gitignore` exists and `garbage/` is not already tracked, add a `garbage/` line so the quarantine does not show up as new work in `git status`. Do not rewrite an existing gitignore beyond that one line.

### 5. Report

Follow `references/report-shape.md`. Chat gets the counts, the moves, and the memo path. Do not paste the memo body.

## Tools

Read, search, and move are allowed for nominated outputs. Do not commit unless the user asked. Do not push. Do not install packages. Do not edit product code to "make cleanup easier."
