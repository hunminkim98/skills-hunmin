# prompt-optimizer

[한국어](../ko/prompt-optimizer.md) · [Docs home](README.md) · [SKILL.md](../../cursor/prompt-optimizer/SKILL.md)

Turn a rough draft, a vague idea, or a task description into one finished prompt you can paste into any chat model.

## Why it exists

Most "help me prompt this" answers are templates. They leave `[paste your product here]` in the middle and ask you to finish the work. That is useless the moment you wanted to hit send.

The output is a **complete user message**. Copy the code block, paste it into Claude, Codex, Copilot, or any other chat, and send. There is no system prompt to tune and no API `effort` knob. The prompt has to do all the work by itself.

It is also the engine under [meta-prompting](meta-prompting.md). That skill runs this optimizer, then stops for Y/N. If you only want the prompt, use this skill. If you want approval before anyone executes it, use meta-prompting.

## How it works

Two rules sit above everything else.

**No placeholders.** Square-bracket slots, `{topic}`, `<your_input>`, and blank lines that mean "fill me later" are forbidden. If you catch the model writing brackets around a noun, that is a placeholder and it must rewrite.

**Always ship a finished prompt.** There are two honest cases:

- **Case A: you already gave the content.** The numbers, the email, the offer letter, the product description go **inside** the prompt. The whole thing is one block.
- **Case B: you only described a class of task.** The prompt is still finished. It tells the *next* model to ask you for the missing inputs, or it says "I will paste the emails next; then do this." You are not asked to edit a template.

The skill then writes for how chat models actually read. Say the job and the output shape up front. Explain *why* a constraint exists. Prefer "write flowing paragraphs" over "don't use bullets." Use XML tags only when the prompt has several sections. Long documents go at the top; the question goes at the bottom. High-stakes answers get a last-pass self-check.

The only thing you should see in the chat is **one fenced code block**. No "here's your prompt," no changelog. The block ends with a short line that asks the receiving model to think carefully. If you later ask what changed, that is a follow-up turn, not part of the optimizer output.

## When to use it

Use `/prompt-optimizer` when you want a reusable prompt, not the answer to the task itself.

Examples: "rewrite this prompt," "make this a better prompt," "I want a prompt that triages email," or you paste a draft and ask for a sharper version.

Skip it when you want the agent to *do* the work (edit code, investigate a bug, record a wiki note). Skip it when you need a Y/N gate before anyone runs the prompt. That is meta-prompting.

## Install

In a real terminal, not Agent chat:

```bash
npx skills add hunminkim98/skills-hunmin --skill prompt-optimizer --agent cursor
```

Add `--global` to install for every Cursor project on this machine. See the [docs home](README.md) for the interactive picker.

## How to use it

1. Open a new Agent chat.
2. Type `/prompt-optimizer` and your draft or your task class.
3. Copy the single code block.
4. Paste it into the chat where you want the work done.

If your draft is Korean, the optimized prompt stays Korean unless you asked otherwise. The closing "think carefully" line can be adapted to that language.

You do not fill in blanks after the fact. If something essential is missing, the prompt itself tells the next model to ask you.

## With other skills

- Install next to [meta-prompting](meta-prompting.md). Meta-prompting reads `../prompt-optimizer/SKILL.md`.
- Do not mix this with [deep-analyze](deep-analyze.md) or [discussion](discussion.md). Those answer questions. This writes a prompt.

## Limits

The skill does not call a prompt API and does not tune tools. It will not execute the optimized prompt unless you are actually in meta-prompting and you pressed Y. It will not invent facts you never provided. In Case B it defers those questions to the next turn.
