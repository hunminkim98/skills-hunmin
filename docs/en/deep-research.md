# deep-research

[한국어](../ko/deep-research.md) · [Docs home](README.md) · [SKILL.md](../../cursor/deep-research/SKILL.md)

Split a topic into related web angles. Search those angles in parallel. Come back with a cited brief: what holds, where sources fight, what is still unknown.

## Why it exists

A single search answers the first SERP. Agent work often needs the neighboring questions too: the official story, the critique, what changed this year, and a case that actually shipped. Doing that as one chat turn with five fake voices is theater. Doing it as one Firecrawl key is a product pitch.

Public skills in this neighborhood usually take one of three exits. They write a playbook file (webcpu-style). They run a P0–P7 pipeline into `research-notes/` and aim for thousands of words (daymade-style). Or they wrap a paid API (AnyCap, Gemini Deep Research, Firecrawl-only farms).

This one stays in **chat**. It uses **real parallel lane agents**. It refuses a link dump. It does not need a vendor. Coverage means angles, not page count.

It is not [deep-analyze](deep-analyze.md). That skill stays inside one question and often the repo. Widening there is a bug. Widening here is the job.

## How it works

Slash only. No topic, no run.

1. Bind the question in one sentence. Repo audits and "which should we ship" are out of scope.
2. Name 4 lanes (5 only if another domain is really in play). Default jobs: **Core**, **Counter**, **Now**, **Practice**. Optional fifth: **Limits**. Rules: [`references/lanes.md`](../../cursor/deep-research/references/lanes.md).
3. Launch every lane in **one** Task batch (`web-researcher` if the host has it, else `generalPurpose`). Each lane runs at least three different queries and opens two to four URLs. Protocol: [`references/search-protocol.md`](../../cursor/deep-research/references/search-protocol.md).
4. A thin lane gets **one** rewrite wave with new queries. Same keywords twice is not a second wave. After that, `insufficient evidence`.
5. Chat report: [`references/report-shape.md`](../../cursor/deep-research/references/report-shape.md). What we know, conflicts, uncertain, what to read next, URLs actually opened.

Citations: [`references/citations.md`](../../cursor/deep-research/references/citations.md). Unread titles do not count. Disagreement stays in the report. No paywall bypass. No pasted chapters.

No `research/` folder. No playbook markdown. No wiki. Recording later is [wiki-for-llm](wiki-for-llm.md).

## When to use it

Use `/deep-research` when you want the web's useful picture of a topic, including the parts that argue with each other.

Skip it for "does this function lock on the batch row" ([deep-analyze](deep-analyze.md)), for a shipping decision ([discussion](discussion.md)), for prompt work, and for cleaning leftover files.

This skill is **slash only**.

## Install

```bash
npx skills add hunminkim98/skills-hunmin --skill deep-research --agent cursor
```

See the [docs home](README.md) for project vs global.

## How to use it

1. New Agent chat.
2. `/deep-research` plus the topic ("How are teams doing hybrid search in 2026, and where does it fail?").
3. Read the lane slate. You do not have to approve it unless you asked to pick lanes.
4. Wait for the parallel wave. If a lane was empty, there is at most one rewrite.
5. Read What we know → Conflicts → Uncertain → What to read next.

You should not see a new markdown file in the repo. If you do, the skill was ignored.

## With other skills

- A fact about *this* codebase is [deep-analyze](deep-analyze.md), then come here only if you still need the outside world.
- A values fight after the brief is [discussion](discussion.md).
- Keep the brief with [wiki-for-llm](wiki-for-llm.md) if the next agent will need it.
- Do not run this instead of [output-debt](output-debt.md) when the mess is leftover renders.

## Limits

Parallel lanes cost time and tokens. The chair will not start a third wave. A thin internet stays thin; the report should say that. The skill will not implement a library it found. Harmful dual-use topics are refused in one paragraph.
