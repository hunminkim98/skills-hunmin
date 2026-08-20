---
name: deep-research
description: Fans a topic into related web angles and searches them in parallel, then synthesizes a cited brief. Use when the user invokes /deep-research, or wants wide internet research across several related questions. Do not use for a single-repo fact check (deep-analyze), a design debate (discussion), prompt rewriting, or output cleanup.
disable-model-invocation: true
---

# Deep research

The chair (this agent) splits a topic into related web angles, searches those angles in parallel, and writes a cited brief. Breadth is the point. A single query is not a run.

This is not `deep-analyze` (one scoped question, often the repo, stay narrow). It is not `discussion` (a decision with user gates). It is not a playbook writer and not a paid research API wrapper.

Slash only. Do not start because someone said "look this up."

## Hard rules

1. **Need a topic.** If `/deep-research` has no question, ask once and stop.
2. **Fan out, then search.** Split into 4 lanes by default (5 if the topic spans more than one domain). Lanes must not clone each other. Read `references/lanes.md`.
3. **Real parallel agents.** Launch the lanes in **one** Task batch. Prefer `web-researcher` when the host has it. Otherwise `generalPurpose`. Do not use `explore` (that is for the local repo). Do not impersonate five voices in one reply.
4. **Live web only.** Each lane must search and open URLs. Training memory is not a finding. If a tool cannot search, say so and stop; do not invent a literature review.
5. **Cite or drop.** A load-bearing claim needs a URL you opened. Unread titles are not sources. Conflicts stay visible. Read `references/citations.md`.
6. **Chat only.** No `research/`, no playbook file, no wiki note, no commit. The product is the report in this chat.
7. **One rewrite wave.** If a lane comes back thin, change the queries and search again once. Same keywords twice is not a second wave. After that, write `insufficient evidence` and move on.
8. **Match the user's language.**

Do not bypass paywalls or logins. Do not paste copyrighted chapters, lyrics, or papers. Refuse weapons, CSAM, malware, and doxxing in one short paragraph. No steps.

## Workflow

### 1. Bind

Restate the question in one sentence. Name what is out of scope (repo audits, "which should we ship," implementation). If the words name two unrelated products, ask which one.

### 2. Name the lanes

Show a short slate: lane name and the angle it owns. Do not wait for approval unless the user asked to pick lanes.

### 3. Wave 1 — parallel search

Launch every lane in one parallel Task batch. Each prompt is self-contained. Follow `references/search-protocol.md`.

Wait for all of them. Drop findings with no URL. Keep conflicts.

### 4. Wave 2 — only if thin

A lane is thin when it has fewer than two opened URLs, or every URL is the same domain repeating the same claim. Rewrite that lane's queries and relaunch **only those** lanes, once. Do not relaunch a lane that already has coverage.

### 5. Report

Write the chat report with `references/report-shape.md`. Lead with what is known. Then conflicts, gaps, and what to read next. A bullet list of links with no synthesis is a failed run.

## Tools

- Chair: bind the question, launch lanes, synthesize. May search to fill a single hole the lanes missed. Do not replace the swarm with one chair search.
- Lanes: search and fetch only. No repo edits. No talking to the user.
- Use whatever web tools this session already has (search, fetch, Bright Data, Exa, GitHub). Do not require Firecrawl, AnyCap, Gemini Deep Research, or a headless `claude -p` farm.

## Stop

Stop after at most two waves, or when another search would not change the brief. Name the leftover gaps. Volume is coverage of *angles*, not a longer page.
