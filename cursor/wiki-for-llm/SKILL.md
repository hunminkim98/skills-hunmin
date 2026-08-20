---
name: wiki-for-llm
description: Records agent work into a project wiki so the user does not have to re-explain context later. Use when the user invokes /wiki-for-llm, or when a session changes code, docs, architecture, workflow, Git state, or makes a decision the next agent must know. Write task, decision, cleanup, and improvement notes before the final reply. Do not use for read-only questions, typos, or exploration that leaves no durable state. This is not Karpathy LLM wiki and does not ingest external articles into raw/.
---

# Wiki for LLM

The user should not carry the session in their head. If this turn produced durable work, write it down before you answer. The chat stays short. The wiki holds the detail the next agent will need.

This skill records **this conversation and this change set**. It does not ingest papers, URLs, or other outside sources into `raw/`. That is a different workflow.

## When to write

Write without being asked when any of these are true:

- Code, docs, architecture, workflow policy, or Git state changed
- A decision was made that a future agent must follow
- Something was removed or simplified and must not come back
- A durable improvement should be reused

Skip when the turn was only a read-only question, a typo, or exploration that did not change durable project state — unless it produced an important decision.

Do not claim the work is done until the notes exist.

## Find or create the vault

1. Search the current project for an existing work wiki. Reuse it if you find any of:
   - `llm-wiki/`
   - a folder that already has `tasks`, `02-Tasks`, `decisions`, or `03-Decisions`
   - a project `AGENTS.md` that already names a wiki closeout path
2. If a vault already exists, follow **that** folder layout, filenames, and templates. Do not invent a second tree.
3. If none exists, create this portable layout and nothing else:

```text
llm-wiki/
  tasks/
  decisions/
  cleanup/
  improvements/
  templates/
  index.md
```

Copy the templates from this skill's `references/` into `llm-wiki/templates/`. Write a one-line index that lists note types and the vault root.

Default vault root is `llm-wiki/` at the project root. Never hardcode another project's paths. Never write UmFit-only paths such as `llm-wiki/UmFit/02-Tasks` unless that is what this repo already uses.

## What to record

Use the matching note type. One session may produce more than one note.

| Kind | Folder (new vault) | When |
|------|--------------------|------|
| Task | `tasks/` | The work itself: request, changes, skipped work, verification, follow-ups |
| Decision | `decisions/` | Architecture, source of truth, API contract, security, Git, or workflow policy |
| Cleanup | `cleanup/` | Removed or simplified code or process, plus why it must stay gone |
| Improvement | `improvements/` | A durable better way of working that should be reused |

New-vault filenames:

- Task / cleanup / improvement: `YYYY-MM-DD-descriptive-slug.md`
- Decision: `YYYY-MM-DD-descriptive-slug.md` unless the repo already numbers ADRs

If this repo already uses date prefixes, ADR numbers, or numbered folders, keep that convention.

Every note must include, in the repo's template shape or the portable templates:

1. User request
2. Decisions locked in during the conversation
3. Affected paths
4. What changed
5. What was intentionally not changed
6. Verification commands and results — or an explicit `needs-verification` mark
7. Follow-ups

Do not put secrets, credentials, or machine-local absolute paths in notes.

## Chat vs wiki

Write for two readers.

- **Wiki:** enough that a cold agent can continue without asking the user to recap
- **Chat:** what changed, how to verify, and the note path. Do not paste the wiki body back into chat

The user should be able to ignore the wiki and still stay unblocked. The next agent should open the note instead of asking the user.

## New-repo opt-in

When this skill is the closeout mechanism for a repo that has no wiki rule yet, add one short pointer to `AGENTS.md` if that file exists or the user asked to set the repo up. Use `references/agents-md-snippet.md`. Do not replace a richer closeout that the repo already has. Do not edit UmFit's existing wiki rule unless that repo is the current workspace **and** it already points at this skill.

## Quality bar

- Prefer updating an open note for the same task over starting a duplicate
- Link related task, decision, cleanup, and improvement notes
- Today's date for `created` / `updated` / filenames
- If you did not run verification, say so. Do not invent command output
