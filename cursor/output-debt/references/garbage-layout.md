# garbage/ layout

Create `garbage/` at the **project root** of the repo you are cleaning, not inside this skill folder.

Only create it when this run will move at least one path.

## Dated run

```text
garbage/
  README.md                 # what this folder is; write once
  2026-08-20/
    MEMO.md                 # this run
    tmp/old-render.png      # original relative path kept
    docs/draft-v2.md
```

Use today's date `YYYY-MM-DD`. If that folder already exists, use `YYYY-MM-DD-2` (then `-3`). Do not mix two runs in one folder.

Keep the original relative path under the dated folder so a restore is a reverse move.

## MEMO.md

For every moved path:

- Original path
- Score (1 or 2)
- One-sentence why
- Restore hint: move it back to the original path

Do not put secrets in the memo. Do not invent timestamps you did not see.

## README.md (once)

If `garbage/README.md` is missing, write a short note: this folder holds outputs scored below 3. Nothing here is deleted. Restore by moving back to the path in `MEMO.md`. Emptying the folder is a human decision.

## gitignore

If the project has a `.gitignore` and `garbage/` is not already tracked, append:

```
garbage/
```

So the quarantine stays on disk and out of `git status`. Do not add that line if `garbage/` is already committed on purpose.
