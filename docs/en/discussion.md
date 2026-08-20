# discussion

[한국어](../ko/discussion.md) · [Docs home](README.md) · [SKILL.md](../../cursor/discussion/SKILL.md)

For a genuinely hard problem, run a short debate among real specialist sub-agents, ask you when a constraint would change the ranking, and return one recommended path.

## Why it exists

Most "panel" skills are theater: one model writes seven voices in a box-drawing transcript, then offers a menu after it has already decided. Other kits write a `debate/` directory of every round. That is expensive, hard to read, and easy to skip.

This skill treats debate as a **decision tool**. The chair (the agent you are talking to) launches **actual parallel sub-agents**. They disagree. You are pulled in when a preference would reorder the options, not after a ten-page play. You get a recommendation. You do not get a script.

Use it for irreversible or cross-domain choices: architecture, product constraints, "build vs buy," safety vs speed. Do not use it for "what port is Postgres on?"

## How it works

**Complex problems only.** If there is one obvious answer or a single source of truth, the chair says so and offers a direct answer. A panel is not started for a typo or a file lookup.

**Real sub-agents, not voice acting.** Three experts by default, five only if three or more domains are in play. They launch in **one** parallel Task batch (`generalPurpose`, or `explore` when the job is clearly codebase exploration). Each gets one job, one bias, and must argue against itself once. The chair does not impersonate them in one reply.

**No clones.** Seats must differ in domain or incentive. Required: a **specialist** (owns the domain) and a **contrarian** (attacks the leading idea). The third seat is an **operator** (cost, time, reversibility), a second specialist who can veto the first, or a concrete stakeholder proxy. There is no "visionary" seat and no extra synthesizer. The chair already synthesizes. See [`references/roles.md`](../../cursor/discussion/references/roles.md).

**You stay in the debate.** After round 1, the chair uses `AskQuestion` when a missing constraint would change the ranking. It does not finish the whole debate and only then ask. If nothing is missing, you still get one question: continue, add a constraint, or conclude. At most one or two decisive questions. Expert laundry lists are not dumped on you.

**Chair talks to you. Experts do not.** You see the slate, the tensions, the questions, and the recommendation. Quotes appear only when they carry weight.

**No empty compromise.** "Both are valid" and bare "it depends" are not allowed unless the decision factor is named and it is clear which side it favors. Leftover conflict is labeled `contested`.

**No file writes.** No `debate/` folder, no HTML, no wiki. Recording the decision later is [wiki-for-llm](wiki-for-llm.md). Implementation does not start unless you ask in the same request.

Flow:

1. Bind the problem in one sentence. Score complexity (stakeholders, trade-offs, reversibility). If it looks simple, `AskQuestion`: panel or direct answer.
2. Seat 3-5 experts. Show the slate. Do not wait for approval unless you asked to pick seats.
3. **Round 1:** independent briefs in parallel. Each returns a path, evidence, the case against itself, and at most two user questions.
4. **User gate:** `AskQuestion` on the ranking-changing items.
5. **Round 2:** same experts, now with the others' headlines and your answers. They revise or stand pat and name a falsifier. A third round only if a conflict is still load-bearing and you chose continue.
6. Report via [`references/report-shape.md`](../../cursor/discussion/references/report-shape.md), then `AskQuestion`: conclude, another round, or hand off to implementation.

Expert prompts follow [`references/round-protocol.md`](../../cursor/discussion/references/round-protocol.md). Experts may read and search. They must not edit the repo. No paid debate product is required.

## When to use it

Use `/discussion` when two competent people could disagree and the cost of being wrong is high.

Skip it for facts ([deep-analyze](deep-analyze.md)), for a wide web survey ([deep-research](deep-research.md)), for prompt crafting, and for writing the work log.

This skill is **slash only**.

## Install

```bash
npx skills add hunminkim98/skills-hunmin --skill discussion --agent cursor
```

See the [docs home](README.md) for project vs global.

## How to use it

1. New Agent chat.
2. `/discussion` plus the decision ("Should we keep p75 wire names while changing the filter?").
3. If the chair offers "panel vs direct," pick.
4. Read the slate and the first tensions.
5. Answer the mid-debate question. That answer is supposed to move the ranking.
6. Read Recommendation, Why not the alternatives, Constraints you set, Contested, Risks.

You should not get a novel-length transcript. If you do, the skill is being ignored.

## With other skills

- Use [deep-analyze](deep-analyze.md) first when the fight is actually about a fact.
- Use [deep-research](deep-research.md) when you need the outside web before you argue values.
- Use [wiki-for-llm](wiki-for-llm.md) after, if the decision should survive this chat.
- Use [meta-prompting](meta-prompting.md) if you want to approve the discussion brief before the panel starts.

## Limits

Parallel sub-agents cost time and tokens. The chair will refuse a panel for a simple lookup. Experts can be wrong; the report must show evidence or `unverified`. The skill will not implement the winner unless you ask. Harmful dual-use topics are refused in one paragraph.
