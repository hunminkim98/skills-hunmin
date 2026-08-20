# meta-prompting

[한국어](../ko/meta-prompting.md) · [Docs home](README.md) · [SKILL.md](../../cursor/meta-prompting/SKILL.md)

Improve your draft with [prompt-optimizer](prompt-optimizer.md), show the result, and wait for an explicit **Y** or **N** before anyone uses it.

## Why it exists

An optimizer that immediately starts the real task is dangerous. You asked to *see* the prompt. The agent “helpfully” begins coding, or investigating, or rewriting the repo.

Meta-prompting splits those jobs. First the draft becomes a finished prompt. Then you get a button, not a paragraph that says “reply Y or N.” Until you press **Y**, the real work does not start. Until you press **N**, the agent does not invent a new direction.

The approval UI is Korean on purpose (`이 프롬프트를 이대로 쓸까요?`). The optimized prompt stays in the language of your draft.

## How it works

1. If you typed `/meta-prompting` with no draft, the agent asks you to paste one and stops.
2. It reads the sibling skill `cursor/prompt-optimizer/SKILL.md` and runs that optimizer. If that file is missing, it still writes a finished prompt: no placeholders, Case A or Case B, plus a closing reasoning line.
3. **Override:** prompt-optimizer wants “only a code block.” Meta-prompting still shows that block, then asks Y/N. It does not explain what changed.
4. `AskQuestion` appears with exactly two options: **Y** (use as-is) and **N** (refine). Those labels stay `Y` and `N`.
5. On **Y**, the approved prompt is frozen. If you wanted a prompt to copy, the agent returns only that block. If you wanted this chat to do the work, it executes the approved prompt as your request. It does not rewrite again.
6. On **N**, you get five *concrete* edits drawn from *this* draft and *this* optimized prompt, plus a sixth option `자유 의견` (write your own note). Generic labels like “make it shorter” are not allowed as the five directions. After you pick, the optimizer runs again under that constraint, and you see Y/N again. That loop continues until **Y**.

The sixth choice is only free comment. There is no sixth refinement strategy.

## When to use it

Use `/meta-prompting` when the draft is not the prompt you want executed yet: a messy task, a dangerous repo change, or anything you want to read once before the agent spends a lot of time.

Skip it when you already want the optimizer’s code block and nothing else (`/prompt-optimizer`). Skip it when the work is already specified and you just want it done.

This skill is **slash only** (`disable-model-invocation: true`). It will not start because you said the word “prompt” in passing.

## Install

Install **both** siblings. Meta-prompting will not see the optimizer if you only copied one folder.

```bash
npx skills add hunminkim98/skills-hunmin --skill meta-prompting --skill prompt-optimizer --agent cursor
```

Or pick both in the interactive picker. See the [docs home](README.md).

## How to use it

1. Open a new Agent chat.
2. Type `/meta-prompting` and the task or draft.
3. Read the fenced prompt. Do not expect a diff essay.
4. Press **Y** to use it, or **N** to steer the next rewrite.
5. If you pressed Y and the prompt was a request for *this* agent, watch it execute. If it was a prompt to take elsewhere, copy the block.

User-facing questions stay Korean. If the draft is English, the optimized prompt is English unless you asked otherwise.

## With other skills

- Depends on [prompt-optimizer](prompt-optimizer.md).
- After Y, the approved prompt might tell the agent to use [deep-analyze](deep-analyze.md), [discussion](discussion.md), or [wiki-for-llm](wiki-for-llm.md). That is the *content* of the prompt, not this skill starting those jobs before Y.

## Limits

The gate is only as strong as the agent following the skill. If the prompt is not shown and Y/N never appears, stop and ask for the block. The skill will not start the real task while it is still asking N-refine questions. It does not write wiki notes about the prompt itself.
