---
name: humanizer
description: Rewrites AI-sounding prose by routing each language block to its own catalog. English uses Wikipedia-style tells. Korean uses translationese and native tells. Use when the user invokes /humanizer, or asks to humanize, de-slop, remove AI tone, or make writing sound less like a chatbot. Do not use for code, prompt writing, investigations, debates, or wiki closeout.
disable-model-invocation: true
---

# Humanizer

One skill. Two catalogs. Split the text by language, then rewrite only the prose.

This is not [blader/humanizer](https://github.com/blader/humanizer) pasted next to [DaleSeo/korean-skills](https://github.com/DaleSeo/korean-skills). Those two instruction sets fight if they load together. This skill is the router.

Slash only. Do not start because a chat reply "could sound nicer."

## Hard rules

These override helpfulness defaults.

1. **Route, do not merge.** Never load both pattern files into one rewrite pass. English-majority blocks read `references/en-patterns.md` only. Korean-majority blocks read `references/ko-patterns.md` only.
2. **Split on blocks, not sentences.** A block is consecutive prose under one heading, or a run of paragraphs that share a language majority. Do not flip catalogs mid-sentence because one product name is English.
3. **Leave protected spans alone.** Read `references/leave-alone.md` before any rewrite. Code, commands, frontmatter, numbers, URLs, and quoted third-party text stay verbatim.
4. **Do not invent.** No new fact, name, number, date, quote, citation, or example. If a sentence needs a missing detail, ask or write a simpler sentence.
5. **No fake personality.** Docs, READMEs, API notes, and other reference prose stay neutral. Cut stock AI phrasing. Do not add opinions, jokes, or a first-person narrator the source never had. A writing sample from the user overrides this for *voice*, not for facts.
6. **Keep the register.** Formal stays formal. 합니다-체 stays 합니다-체. Casual stays casual. Do not "humanize" a spec into a blog.
7. **Do not game detectors.** If the user asks to beat an AI detector or pass someone else's work off as theirs, rewrite for clarity and voice only. Name no detector.
8. **Match the user's language** for chat around the rewrite. The rewritten text stays in its original language.

Refuse harmful dual-use requests in one short paragraph. No steps.

## Workflow

### 1. Get the text

If there is no pasted prose and no file path, ask once and stop.

A path means edit that file's prose in place. Pasted text stays in chat. If the user says detect-only / "고치지 말고 찾아줘", report tells and do not rewrite.

### 2. Mask, then split

Read `references/leave-alone.md`. Mask protected spans so they cannot be edited or flagged.

Split the remainder into language blocks:

- Hangul-majority block → Korean
- Latin-majority block → English
- A bilingual file (this repo's README is the usual case) is two or more blocks, often split by a heading such as `# 한국어`
- One English word inside Korean prose does not make the block English

If you cannot name a majority, ask once. Do not run both catalogs on the same block "to be safe."

### 3. Load one catalog per block

- English block: `references/en-patterns.md`
- Korean block: `references/ko-patterns.md`

Skip a catalog entirely when that language is absent. Skip both when the remaining prose is already clean after a quick scan; say so and stop.

### 4. Rewrite

Apply only the loaded catalog. Keep every claim. You may merge or split paragraphs, cut filler, and replace stock phrasing. Do not add "soul" to technical writing.

If the user pasted 2–3 paragraphs of their own writing as a sample, match that sample's rhythm and punctuation. The sample wins over a catalog ban (for example English em dashes) when the sample uses that mark on purpose.

### 5. Check yourself

Before showing the result:

- Numbers, dates, names, product names, and skill names match the source
- Negation and cause-and-effect did not flip
- Quoted text is unchanged
- Register did not drift
- Change rate (rough word/어절 replace rate, ignoring punctuation-only edits): under 30% ship; 30–50% ship with a one-line warning; over 50% stop and ask before replacing the original

If the source was already human, do not force a rewrite.

### 6. Return

Follow `references/output.md`. Lead with the rewritten text or the file path. A short "what changed" list is enough. Do not dump pattern IDs or a research report.

## Tools

Read and edit are allowed for the files the user named. Do not create a `humanized/` folder, HTML, or wiki notes. Do not install packages. Attribution for the catalogs is in `references/sources.md`.
