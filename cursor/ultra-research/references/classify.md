# Classify

Fill three marks. Then pick stages and order. Do not use a hidden fourth mark like "be thorough."

| Mark | Yes when the question needs | Stage if yes |
|---|---|---|
| **Web** | Outside practice, market, versions, incidents, law, "how do others" | `deep-research` |
| **Repo** | This codebase, a named file, our pipeline, "what do we do today" | `deep-analyze` |
| **Decision** | Should we, A vs B, a costly or hard-to-reverse choice, stakeholders disagree | `discussion` |

A mark is **no** when that work would not change what you can say. "What port is Postgres on?" is no / no / no if the answer is in the repo or a single doc — then answer directly, no stage.

## Order

Once the marks are set:

1. If only one mark is yes, run that one stage.
2. If **repo** is yes and the search terms are local names, APIs, or "what we actually run," do `deep-analyze` first. The web stage then searches the thing you found, not a generic category.
3. If **web** is yes and you cannot name a repo target yet ("should we adopt hybrid search" with no file), do `deep-research` first. `deep-analyze` then looks only where the brief points, still inside the user's question.
4. If **web** and **repo** are both yes and the user already named the target (file, job, endpoint), run those two stages in parallel.
5. **Decision** is always last among the stages you chose. It needs the briefs. Skip it when the facts leave one obvious path and no stakeholder trade-off remains. `discussion` itself will also refuse a simple fact — believe it.

## Examples

| Ask | Marks | Path |
|---|---|---|
| Does finalize lock on the batch row or the object key? | repo | `deep-analyze` |
| How are teams doing hybrid search in 2026, and where does it fail? | web | `deep-research` |
| We have the briefs. Ship p75 names or change the filter? | decision | `discussion` |
| Should we put hybrid search into our batch pipeline? | web, repo, decision | `deep-research` then `deep-analyze` (target unknown) then `discussion` |
| Our `storage.py` finalize vs how others publish canonical objects — should we change it? | web, repo, decision | `deep-analyze` then `deep-research` then `discussion` |
| What does `storage.py` finalize do, and what did vendors change this year? | web, repo | parallel `deep-analyze` + `deep-research` |

## Ambiguity

Two unrelated products in one sentence: ask which target, then classify. Do not run two ultra-research paths in one go.

If you cannot tell web from repo, prefer **repo** when the workspace is a real project and the question uses "our / this / the function." Prefer **web** when there is no useful tree or the question is industry-level.

Show the path as one line before you start, for example: `Path: deep-analyze → deep-research → discussion (repo names the search).`
