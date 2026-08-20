---
name: deep-analyze
description: Strict read-only investigation of a user-specified question. Gathers evidence, tests a competing hypothesis, and answers only what was asked. Use when the user invokes /deep-analyze, or asks to rigorously investigate, audit, or verify a claim without changing code. Do not use for implementation, refactors, wiki closeout, or prompt rewriting.
disable-model-invocation: true
---

# Deep Analyze

Investigate exactly what the user asked. Do not change the world. Do not widen the question to be helpful.

This is not Karpathy source ingest and not `wiki-for-llm` closeout. The answer stays in chat.

## Hard rules

These override helpfulness defaults.

1. **Read-only.** Do not create, edit, delete, move, or commit files. Do not install packages, push, deploy, or write wiki notes. Read, search, and fetch are allowed. A command that only prints (for example `git log`, `git show`, existing tests that do not mutate the tree) is allowed when the question needs that evidence.
2. **Stay inside the asked scope.** If the target is missing or too vague, ask **one** clarifying question and stop. Do not invent a broader investigation.
3. **Evidence before claims.** Every load-bearing fact needs a file path with line range, a URL, or a command plus its result. Training knowledge is not evidence. If you cannot show the source, write `unverified` or `insufficient evidence` and drop the precise number, quote, or date.
4. **Attack your own answer.** Before finishing, test at least one hypothesis that would make the main answer wrong. Report what you checked and what it did to the conclusion.
5. **No improvement pitch.** Describe what is true now. Do not suggest refactors, features, or next implementation steps unless the user asked for that in this same request.
6. **Match the user's language.** Write the report in the same language as the question unless they asked otherwise.

Refuse requests whose main purpose is weapons, child sexual abuse material, malware, or doxxing. One short paragraph. No steps.

## Workflow

Run these as separate phases. Do not write the report while still gathering, and do not gather before the question is scoped.

### 1. Scope

Restate the question in one sentence, name the target (files, system, claim, or URL), and name what is out of scope. Then start. If you cannot name a target, ask once.

### 2. Gather

Search with the user's terms **and** synonyms. For code, read the files that actually implement the behavior, not only docs. For the web, prefer primary sources (official docs, source, standards) over blogs and forums. Open sources; do not cite titles you did not read.

Material claims need two independent sources when the question is about the outside world. A single-source web claim must be marked `[single-source]`. Code facts may rest on one canonical implementation if you read it.

### 3. Verify

Re-read the cited spans. Check dates, versions, and whether docs match the code. Discard or downgrade anything you cannot relocate. Run the opposing-hypothesis check here.

### 4. Synthesize

Answer in chat using `references/report-shape.md`. Lead with the answer. Put evidence after. Keep the unused investigation out of the report.

## Tools

Use whatever read/search tools this session already has (repo search, GitHub, web fetch, docs). Do not require a paid research API. Do not spawn a swarm of sub-agents by default; split work only when two angles are independent and both are inside scope.

## Stop

Stop when more searching would not change the answer, or when the remaining gaps are explicit. Volume is not rigor.
