---
name: ultra-research
description: Orchestrates deep-research, deep-analyze, and discussion. The chair picks which stages to run and in what order, then follows each sibling skill as-is. Use when the user invokes /ultra-research, or wants web, repo, and a decision handled in one run without picking the pipeline. Do not use for a single known stage, prompt rewriting, wiki closeout, or output cleanup.
disable-model-invocation: true
---

# Ultra research

The chair (this agent) is an orchestrator. It classifies the question, picks a path through the sibling skills, and keeps their rules intact. It does not paste the three `SKILL.md` files into one prompt. It does not always run web → repo → debate.

Siblings, when present:

- [`../deep-research/SKILL.md`](../deep-research/SKILL.md) — wide web
- [`../deep-analyze/SKILL.md`](../deep-analyze/SKILL.md) — scoped repo (or one tight claim)
- [`../discussion/SKILL.md`](../discussion/SKILL.md) — decision with user gates

Slash only. Need all three siblings installed beside this folder. If a chosen stage's skill is missing, name the install command and skip that stage.

## Hard rules

1. **Need a question.** If `/ultra-research` has none, ask once and stop.
2. **Chair picks the path.** Read `references/classify.md`. Mark web / repo / decision. Choose stages and order from those marks. Do not ask the user to approve the path. Show the path in one line and start. Ask only when the question names two unrelated targets.
3. **Skip unused stages.** A repo lock question is `deep-analyze` only. A market brief is `deep-research` only. A values fight with facts already in the thread is `discussion` only. Running all three as ceremony is a failed run.
4. **Follow the child skill.** Before a stage, read that sibling's `SKILL.md` and the references it names. The chair does not override "stay narrow," "fan out," "complex problems only," or discussion's `AskQuestion` gates.
5. **Handoff, do not restart.** Each finished brief is input to the next stage. Read `references/handoff.md`.
6. **Chat only.** No `research/`, `debate/`, playbook, wiki, or commit. Implementation starts only if the user asks in this same request.
7. **Match the user's language.**

Refuse weapons, CSAM, malware, and doxxing in one short paragraph. No steps.

## Workflow

### 1. Bind and classify

Restate the question in one sentence. Fill the three marks. Name the path (stages in order, or one stage). If every mark is no, answer directly and stop.

### 2. Run the path

For each chosen stage, in the chosen order:

1. Read that sibling skill.
2. Bind that stage's question using the original ask plus prior briefs.
3. Execute that skill to its own stop condition.
4. Keep the stage report. Do not rewrite it into a different genre.

If web and repo are both needed and the repo target is already named in the user question, the chair may run `deep-research` and `deep-analyze` **in parallel**, then merge. If one stage's queries depend on the other, stay serial.

### 3. Close

Write the chat report with `references/report-shape.md`. If `discussion` ran, its recommendation is the answer. If it did not, the last factual brief is the answer. Do not invent a panel after the fact.

## Tools

The chair classifies, launches, and synthesizes. Stage work uses the tools that stage already allows. No paid orchestrator product. No `plan.json` on disk.

## Stop

Stop when the path is done, or when a child skill stopped because evidence is insufficient. Do not add a consolation stage to look complete.
