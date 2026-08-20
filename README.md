# skills-hunmin

[한국어](#한국어)

Personal agent skills, grouped by host. Cursor-specific skills live under `cursor/`. Add more folders over time; installers pick only the ones they want.

`meta-prompting` uses sibling `prompt-optimizer` to rewrite a draft, then asks Y or N before using it. If you want that flow, select both.

`wiki-for-llm` writes task, decision, cleanup, and improvement notes so the next agent can continue without asking the user to recap. It is not Karpathy-style source ingest.

`deep-analyze` is a read-only investigation of a user-specified question. It stays in scope, cites evidence, and does not change files.

## Install

Use the [skills](https://github.com/vercel-labs/skills) CLI. Run this in a real terminal (Cursor Terminal or iTerm), not inside an Agent chat. Agent shells skip the picker.

```bash
npx skills add hunminkim98/skills-hunmin
```

That opens a terminal UI:

1. Search and checkbox-select skills (type to filter, space to toggle, enter to confirm)
2. Choose this project or global
3. Choose Cursor (and any other agents)

**One skill, no UI**

```bash
npx skills add hunminkim98/skills-hunmin --skill meta-prompting --agent cursor
```

**This project only, skip the scope prompt**

```bash
npx skills add hunminkim98/skills-hunmin --agent cursor
```

**All Cursor projects**

```bash
npx skills add hunminkim98/skills-hunmin --agent cursor --global
```

Start a new Agent chat afterwards and type `/` plus the skill name.

## Skills

Cursor (`cursor/`):

- [meta-prompting](cursor/meta-prompting/SKILL.md)
- [prompt-optimizer](cursor/prompt-optimizer/SKILL.md)
- [wiki-for-llm](cursor/wiki-for-llm/SKILL.md)
- [deep-analyze](cursor/deep-analyze/SKILL.md)

In a new repo, install `wiki-for-llm` (project or global) and add the one-line closeout from `cursor/wiki-for-llm/references/agents-md-snippet.md` to `AGENTS.md` if the repo has no richer wiki rule.

---

# 한국어

에이전트별로 나눠 둔 개인 스킬 모음입니다. Cursor 전용 스킬은 `cursor/`에 있습니다. 폴더를 계속 추가할 수 있고, 설치하는 사람은 원하는 것만 고릅니다.

`meta-prompting`은 옆에 있는 `prompt-optimizer`로 초안을 고친 뒤, 쓰기 전에 Y 또는 N을 묻습니다. 이 흐름을 쓰려면 둘 다 선택하세요.

`wiki-for-llm`는 작업·결정·정리·개선 노트를 남겨, 다음 에이전트가 사용자에게 맥락을 다시 묻지 않게 합니다. 바깥 자료를 raw에 넣는 Karpathy 위키가 아닙니다.

`deep-analyze`는 사용자가 지정한 질문만 읽기 전용으로 조사합니다. 범위를 넓히지 않고, 근거를 붙이며, 파일은 바꾸지 않습니다.

## 설치

[skills](https://github.com/vercel-labs/skills) CLI를 씁니다. Cursor 터미널이나 iTerm 같은 **실제 터미널**에서 실행하세요. Agent 채팅에서 실행하면 선택 UI가 뜨지 않습니다.

```bash
npx skills add hunminkim98/skills-hunmin
```

터미널 UI가 열립니다.

1. 스킬을 검색하고 체크박스로 고릅니다 (입력으로 필터, 스페이스로 선택, 엔터로 확정)
2. 이 프로젝트만 설치할지, 전역으로 설치할지 고릅니다
3. Cursor와 필요한 다른 에이전트를 고릅니다

**UI 없이 스킬 하나만**

```bash
npx skills add hunminkim98/skills-hunmin --skill meta-prompting --agent cursor
```

**이 프로젝트만, 범위 질문 생략**

```bash
npx skills add hunminkim98/skills-hunmin --agent cursor
```

**이 머신 모든 Cursor 프로젝트**

```bash
npx skills add hunminkim98/skills-hunmin --agent cursor --global
```

설치 후 새 Agent 채팅을 열고 `/` 다음에 스킬 이름을 입력하세요.

## 스킬

Cursor (`cursor/`):

- [meta-prompting](cursor/meta-prompting/SKILL.md)
- [prompt-optimizer](cursor/prompt-optimizer/SKILL.md)
- [wiki-for-llm](cursor/wiki-for-llm/SKILL.md)
- [deep-analyze](cursor/deep-analyze/SKILL.md)

새 레포에서는 `wiki-for-llm`를 설치하고, 더 자세한 위키 규칙이 없을 때만 `AGENTS.md`에 `cursor/wiki-for-llm/references/agents-md-snippet.md`의 한 줄을 넣으면 됩니다.
