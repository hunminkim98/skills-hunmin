# wiki-for-llm

[한국어](../ko/wiki-for-llm.md) · [Docs home](README.md) · [SKILL.md](../../cursor/wiki-for-llm/SKILL.md)

Record the work of this conversation so you do not have to recap it later. The chat stays short. The wiki holds what the next agent needs.

## Why it exists

Long agent sessions create **cognitive debt**. You remember the constraints, the thing you told it not to touch, the test that was skipped. The next chat starts cold and asks you again.

This skill moves that debt onto disk. The user should be able to ignore the wiki and still stay unblocked. The next agent should open the note instead of interviewing you.

It is **not** a Karpathy LLM wiki. It does not fetch papers into `raw/` and compile concept pages. The material is **this chat and this change set**.

It is also not UmFit-specific. Default folders are portable. If a repo already has `llm-wiki/UmFit/02-Tasks` or another living convention, the agent follows that tree and does not invent a second one.

## How it works

The agent writes **without being asked** when the turn changed code, docs, architecture, workflow, Git state, or a decision the next agent must follow — or when something was removed and must stay gone, or a durable improvement should be reused.

It skips read-only questions, typos, and exploration that left no durable state, unless that exploration produced an important decision.

It looks for an existing vault (`llm-wiki/`, folders named `tasks` / `02-Tasks` / `decisions` / `03-Decisions`, or an `AGENTS.md` closeout path). If it finds one, it uses that layout and those templates.

If it finds nothing, it creates only this:

```text
llm-wiki/
  tasks/
  decisions/
  cleanup/
  improvements/
  templates/
  index.md
```

Templates are copied from the skill’s `references/`. New notes use `YYYY-MM-DD-descriptive-slug.md` unless the repo already numbers ADRs.

Every note, in the repo’s shape or the portable templates, includes: the user request, decisions locked in chat, affected paths, what changed, what was intentionally not changed, verification commands and results (or `needs-verification`), and follow-ups. Secrets and machine-local absolute paths stay out.

Chat vs wiki:

- Wiki: enough for a cold agent to continue
- Chat: what changed, how to verify, and the note path — not the wiki body pasted back

Prefer updating the open note for the same task over starting a duplicate. Link related notes. Do not invent command output.

### First run and AGENTS.md

`npx skills add` does **not** edit `AGENTS.md`.

The first time this skill actually **runs** in a repo that has no richer wiki closeout, it may add a one-line pointer from `references/agents-md-snippet.md` — if `AGENTS.md` already exists, or you asked to set the repo up. It will not replace a richer rule. It will not rewrite a project’s existing closeout unless that project already points at this skill.

## When to use it

Let it run after real work. You can also type `/wiki-for-llm` if you want a note written now.

Skip it for “what does this function do?” unless you made a lasting decision. Skip Karpathy-style “ingest this URL into raw/.”

Unlike the slash-only skills, this one **may start itself** when the description matches. A short `AGENTS.md` pointer makes that reliable in a new repo.

## Install

```bash
npx skills add hunminkim98/skills-hunmin --skill wiki-for-llm --agent cursor
```

Add `--global` if every project on this machine should see it. For a new template repo with no wiki rule, you can paste the snippet from [`references/agents-md-snippet.md`](../../cursor/wiki-for-llm/references/agents-md-snippet.md) yourself.

## How to use it

Do the work as usual. At the end you should see a short chat summary and a path like `llm-wiki/tasks/2026-08-20-....md`. Open that path if you want the full record.

If you start a new repo, either wait for first run to add the `AGENTS.md` line, or add it yourself. Then later agents load the skill without you typing `/wiki-for-llm` every time.

## With other skills

- After [discussion](discussion.md), ask to record the decision if you want it on disk. Discussion itself writes no files.
- [deep-analyze](deep-analyze.md) is read-only and will not write these notes.
- Do not use this skill to ingest outside articles.

## Limits

The vault is only as good as what was written. If verification was skipped, the note must say so. The skill will not create UmFit paths in a repo that does not already use them. It will not keep a second wiki next to an existing one.
