# Lanes

Default is **four** lanes. Use **five** only when the topic clearly spans another domain (law and engineering, clinic and product, two industries). Never six.

Each lane owns one angle. If two prompts would return the same SERP, merge them.

## Default slate

| Lane | Owns | Attacks |
|---|---|---|
| Core | Definitions, official docs, the current default story | Marketing pages that repeat the same slogan |
| Counter | Critiques, failed bets, minority views, "this does not work when" | Cheerleading the core lane |
| Now | What changed recently: releases, incidents, regulation, dates | Undated evergreen posts treated as news |
| Practice | How people actually do it: case writeups, postmortems, field reports | Hypothetical "you should" lists with no instance |

Fifth lane, only if needed:

| Lane | Owns |
|---|---|
| Limits | Measurement, cost, safety, what the method cannot see |

Rename the labels to fit the topic. Keep the jobs.

## Anti-clones

Bad slate for "vector databases":

- Overview of vector DBs
- Introduction to embeddings
- What is a vector database

Those are one lane.

Better:

- Core — ANN indexes and the official API shape
- Counter — when keyword or relational search still wins
- Now — 2026 releases, pricing, and known outages
- Practice — production postmortems (reindex, drift, hybrid)

## Chair prompt to each lane

The sub-agent cannot see this chat. Every launch includes:

1. The bound question, one sentence
2. Out of scope
3. This lane's name and what it must not cover (name the other lanes)
4. Today's date, so "recent" has a floor
5. The search-protocol output contract
6. Hard limits: no file writes, no implementation, no other lanes' jobs
