---
name: discussion
description: Runs a structured debate among parallel expert sub-agents on a complex problem, asks the user when a constraint would change the recommendation, and returns the most defensible path. Use when the user invokes /discussion, or wants a council, panel, or expert debate before choosing an approach. Do not use for simple facts, typo fixes, read-only audits (use deep-analyze), prompt rewriting, or work-wiki closeout.
disable-model-invocation: true
---

# Discussion

The chair (this agent) convenes real specialist sub-agents, lets them disagree, and keeps the user in the loop. The product is a recommended path, not a play.

This is not `deep-analyze` (facts only), not `wiki-for-llm` (session notes), and not Karpathy ingest. Do not implement the recommendation unless the user asks in the same request.

## Hard rules

1. **Complex problems only.** If the question has one obvious answer or a single source of truth, say so and offer a direct answer. Do not spin up a panel for a port number, a typo, or a file lookup.
2. **Real sub-agents, not voice acting.** Launch 3–5 specialist agents **in parallel** with the Task tool (`generalPurpose` unless the job is clearly codebase exploration, then `explore`). Each agent gets one job, one bias, and must argue against itself once. Do not write a fake transcript of seven personas in one reply.
3. **No clones.** Roles must differ in domain or incentive. Every panel includes a **specialist** (owns the domain) and a **contrarian** (attacks the leading idea). A third seat is a **operator** (cost, time, reversibility) or another specialist the problem actually needs.
4. **User stays in the debate.** After the first parallel round, stop and use `AskQuestion` when a missing preference, constraint, or risk tolerance would change the ranking. Do not finish the whole debate and only then ask. If nothing is missing, still offer `AskQuestion` once: continue, add a constraint, or conclude.
5. **Chair synthesizes. Experts do not talk to the user.** The user sees a short slate, the tensions, the questions, and the final recommendation. Paste expert excerpts only when a quote is load-bearing.
6. **No empty compromise.** Do not end with "both are valid" or "it depends" unless you name the decision factor and which side it favors. Label leftover conflict `contested`.
7. **No file writes.** Do not create `debate/` folders, HTML, or wiki notes. If the user later wants the decision recorded, that is `wiki-for-llm`.
8. **Match the user's language.**

Refuse harmful dual-use requests in one short paragraph. No steps.

## Workflow

### 1. Bind the problem

If there is no problem statement, ask once. Restate it in one sentence, name what is out of scope, and score complexity quickly:

- more than one stakeholder or domain
- real trade-offs
- costly or hard to reverse

If it looks simple, use `AskQuestion`: proceed with a panel, or answer directly. Then follow that choice.

### 2. Seat the panel

Name 3 experts by default (5 only if the problem spans three or more domains). Show the slate in one short list: role, what they optimize for, what they will attack. Do not wait for approval unless the user asked to pick the seats.

Read `references/roles.md` if the seating is unclear.

### 3. Round 1 — independent briefs

Launch all experts in **one** parallel Task batch. Each prompt must include:

- the bound problem and out-of-scope list
- that expert's job and forbidden overlap with the others
- a demand for: recommended path, strongest evidence, strongest case **against** their own path, what they need from the user
- no implementation, no file writes

Wait for all of them. Then write a tension map: agreements, conflicts, missing user facts.

### 4. User gate

Use `AskQuestion` (not a typed menu) for the **one or two** questions that would change the ranking. Options must be concrete. Always include a free-comment style option when the tool allows Other.

If the experts asked five things, pick the decisive ones. Do not dump the rest on the user.

### 5. Round 2 — informed rebuttal

Launch the same experts again in parallel. Each prompt includes the other briefs' headlines (not full dumps), the user's answers, and the open conflicts. Ask them to revise or stand pat, and to say what would falsify their view.

One rebuttal round is the default. A third round only if a conflict is still load-bearing and the user chose continue.

### 6. Recommend

Write the chat report using `references/report-shape.md`. Then `AskQuestion`: conclude, another round with a new constraint, or implement next (only if they want that handoff).

## Tools

- Chair: read/search as needed to brief experts; `AskQuestion` for the user; Task for experts
- Experts: may read and search; they must not edit the repo
- Do not require a paid debate product or a config file

Read `references/round-protocol.md` before writing expert prompts.
