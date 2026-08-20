# Round protocol

## Expert prompt (every launch)

Give the sub-agent a self-contained brief. It cannot see this chat.

Must include:

1. Bound problem, one sentence
2. Out of scope
3. This role's name, what it optimizes, what it must attack
4. The other roles' names, so it does not copy them
5. User answers so far (empty in round 1)
6. Headlines from other experts (round 2 only): their path + one-line objection
7. Output contract:

```text
Path: ...
Why: ...
Evidence: files, URLs, or explicit unverified
Against my path: ...
Needs from user: at most two questions
Falsifier: what would make me drop this path
```

8. Hard limits: no file edits, no implementation, no talking as other roles

## Chair after each round

- Collapse near-duplicates into one tension
- Keep at most three conflicts visible to the user
- Promote a conflict to `AskQuestion` only if the answer would reorder the paths
- If experts disagree about a fact, send that fact to `deep-analyze` only when the user asked for an audit, or note it as `unverified` and move on
