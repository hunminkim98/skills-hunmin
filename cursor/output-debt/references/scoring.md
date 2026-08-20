# Scoring

Assign one integer. Do not use 2.5. The action falls out of the number.

| Score | Meaning | Action |
|---|---|---|
| 5 | Canonical live output. The product, test, or published doc depends on it. | Stay |
| 4 | In the current working set. Referenced this week, or the user named it as keep. | Stay |
| 3 | Still belongs here. Fixture, demo the README points at, or a useful original that is not canonical. This is the stay floor. | Stay |
| 2 | Superseded experiment. Duplicate, old render, "try 4 of 7." Might matter for a later compare. | Move to `garbage/` |
| 1 | Throwaway from a run. Log, stray screenshot, empty stub, failed export. | Move to `garbage/` |

Scores **below 3** (1 and 2) move. Scores **3 and above** stay.

## How to pick the number

Ask, in order:

1. Does source, a test, or a published doc import or link this path? If yes, it is 5 or 4. Never 2.
2. Is there a newer file that is clearly the same artifact? The old one is 2 unless the user is comparing them on purpose (then 3).
3. Is it untracked generated media at the repo root, or under `tmp/` / `outputs/` with no README mention? Start at 1 or 2.
4. Would a cold agent need this file to continue the *current* task? If yes, 4 or 5.
5. If you cannot tell, score **3** and leave it.

## What this scale is not

- Not "how much I like the file"
- Not git tracked vs untracked (tracked junk can still be 2; untracked source can be 5)
- Not "old means 1" (a year-old fixture the tests use is 5)
