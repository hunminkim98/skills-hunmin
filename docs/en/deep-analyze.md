# deep-analyze

[한국어](../ko/deep-analyze.md) · [Docs home](README.md) · [SKILL.md](../../cursor/deep-analyze/SKILL.md)

Investigate exactly the question you asked. Do not change the project. Do not widen the hunt to look helpful.

## Why it exists

Public "research this repo" skills often write a `research/` folder, an HTML briefing, or a SaaS pitch. Public "deep research" skills often fan out until they have answered a broader question than you asked, or they require a paid API.

This one is **strict, read-only, and scoped**. A confident wrong answer is worse than a slow right one. The job is to find what would break the answer, not to confirm a hunch.

Use it for audits and "is this actually true?" questions. Do not use it to implement the fix.

## How it works

Hard rules, in order:

1. **Read-only.** No create, edit, delete, move, commit, install, push, deploy, or wiki notes. Read, search, and fetch are allowed. A command that only prints (`git log`, `git show`, existing tests that do not mutate the tree) is allowed when the question needs that evidence.
2. **Stay in scope.** If the target is missing, ask **one** clarifying question and stop. Do not invent a wider investigation.
3. **Evidence before claims.** Load-bearing facts need a path and line range, a URL, or a command plus its result. Training memory is not evidence. If the source cannot be shown, write `unverified` or `insufficient evidence` and drop the precise number, quote, or date.
4. **Attack the answer.** Before finishing, test at least one hypothesis that would make the main answer wrong. Report what was checked.
5. **No improvement pitch.** Describe what is true now. No refactors or "next you should…" unless you asked in the same request.
6. **Same language as the question.**

Phases stay separate: **scope → gather → verify → synthesize**. The report is not drafted while gathering is still open.

Gathering uses your words and their synonyms. Code questions read the implementation, not only the docs. Web questions prefer official docs, source, and standards. Unread titles are not citations. Outside-world claims need two independent sources or a `[single-source]` mark. A code fact may rest on one canonical implementation if it was read.

The chat report follows [`references/report-shape.md`](../../cursor/deep-analyze/references/report-shape.md): answer first, then evidence, what would make it wrong, gaps, and sources actually opened.

Stop when more search would not change the answer, or when the remaining gaps are explicit. Volume is not rigor. No paid research API is required. Sub-agents are optional and only for two independent angles still inside scope.

Harmful dual-use requests (weapons, CSAM, malware, doxxing) get one short refusal. No steps.

## When to use it

Use `/deep-analyze` when you want the truth about a claim, a path, a contract, or a page, and you do not want files touched.

Skip it for "please implement," for prompt rewriting, for wiki closeout, and for multi-stakeholder trade-offs ([discussion](discussion.md)).

This skill is **slash only**.

## Install

```bash
npx skills add hunminkim98/skills-hunmin --skill deep-analyze --agent cursor
```

See the [docs home](README.md) for project vs global.

## How to use it

1. New Agent chat.
2. `/deep-analyze` plus a specific question ("Does finalize lock on the batch row or on the object key?").
3. If the target is unclear, answer the one clarifying question.
4. Read Answer → Evidence → What would make this wrong → Gaps.

You should not see new files in `git status` after a clean run.

## With other skills

- Facts first, then [discussion](discussion.md) if you still have a value trade-off.
- Do not expect [wiki-for-llm](wiki-for-llm.md) notes from this skill.
- Do not run this instead of [meta-prompting](meta-prompting.md) when you wanted a prompt.

## Limits

Read-only means the agent will not apply the fix it discovered. Single-source web claims stay marked. If a source cannot be opened, the claim is downgraded, not guessed.
