# Handoff

The chair carries a short packet between stages. Do not dump raw tool traces. Do not make the next skill re-discover the same facts.

## Packet

```text
Bound question: ...
Out of scope: ...
Prior stages: which ran, in what order
Web brief: What we know / Conflicts / Uncertain (or none)
Repo brief: Answer / Evidence / Gaps (or none)
Open user constraints: answers already given
```

## Into deep-research

Give the bound question plus any **local names** from a prior analyze (function, job type, file). Tell the lanes those names are clues for queries, not claims. Do not tell `deep-research` to stay inside the repo. Breadth is still its job.

## Into deep-analyze

Give one scoped question. If a web brief exists, name the files, symbols, or flows it pointed at — only as the **target**, not as extra questions. Do not paste the whole web report and say "also check everything." Widening is still forbidden.

If you cannot name a target after the web stage, ask one clarifying question and skip analyze. Do not scan the whole tree to look helpful.

## Into discussion

Give the bound decision, out of scope, and the two briefs as **shared evidence**. Experts may search, but they must not ignore an already verified repo fact or an opened URL. Keep discussion's seating, parallel rounds, and `AskQuestion` gates. The chair of ultra-research **is** the discussion chair in that stage. Do not launch a second persona to "oversee" the panel.

If the briefs collapsed the choice to one path with no leftover trade-off, skip discussion and say why in the closeout.

## Missing sibling

If the path needs a skill that is not on disk:

```text
Need sibling <name>. Install:
npx skills add hunminkim98/skills-hunmin --skill <name> --agent cursor
```

Skip that stage. Continue the rest of the path. Do not improvise a cheap copy of the missing skill.
