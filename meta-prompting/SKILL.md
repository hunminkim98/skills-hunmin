---
name: meta-prompting
description: Optimizes the user's draft prompt via prompt-optimizer, then asks Y or N before using it. On Y, uses the optimized prompt as-is. On N, offers 5 refinement directions plus 1 free-comment option and loops. Use when the user invokes /meta-prompting, asks for meta prompting, or wants to approve an optimized prompt before using it.
disable-model-invocation: true
---

# Meta Prompting

The user's draft is not the final prompt. Run it through prompt-optimizer, then get an explicit **Y** or **N**. This is meta prompting: improve the prompt, confirm, then use or refine.

## Optimizer pass

Before writing anything, read and follow `/Users/hunminkim/.codex/skills/prompt-optimizer/SKILL.md`.

If that file is missing, still produce a finished chat prompt with:

- no placeholders (`[paste X]`, `{topic}`, `<your_input>`, `___`)
- Case A: bake the user's real content into the prompt
- Case B: write a self-contained prompt that asks the user for missing inputs
- a closing reasoning line

**Override:** prompt-optimizer says "output only a code block." Do not do that here. Show the optimized prompt, then ask Y or N.

## Missing draft

If the user invoked this skill with no draft, ask them to paste the prompt or task they want optimized. Stop until they do.

## Show result, then Y or N

1. Put the optimized prompt in one fenced code block.
2. Do not explain what changed.
3. Ask with `AskQuestion` (not a typed "reply Y or N" in chat):

- **id:** `approve`
- **prompt:** `이 프롬프트를 이대로 쓸까요?`
- **options:**
  - `Y` — 그대로 사용
  - `N` — 다시 다듬기

Use those labels **Y** and **N** verbatim.

## Y — 그대로 쓰면 되고

Do not rewrite again. The approved prompt is final.

- If they wanted a reusable prompt to copy: reply with only that fenced prompt.
- If they wanted this chat to do the work: execute the approved prompt immediately as the user request.

## N — 선택지 5개 + 자유의견 1개

Generate **5** refinement directions from *this* draft and *this* optimized prompt. Each option must be a concrete edit, not a generic label.

Always add a 6th option for free comment.

Ask with `AskQuestion`:

- **id:** `refine`
- **prompt:** `어떤 식으로 다듬을까요?`
- **options:** the 5 generated directions, then:
  - `자유 의견` — 내가 직접 의견을 적을게요

If they pick `자유 의견` or Other, use their text as the refinement brief.

Then run the optimizer again with that constraint, show the new prompt, and ask **Y** or **N** again. Repeat until **Y**.

Do not invent a 6th refinement strategy. The 6th choice is only free comment.

## Rules

- Never skip the Y/N gate and start the real task.
- Never output placeholders in the optimized prompt.
- Keep the approval UI to Y/N only. Keep the refine UI to 5 directions + 1 free comment.
- Write user-facing questions in Korean. Write the optimized prompt in the same language as the user's draft, unless they asked otherwise.
