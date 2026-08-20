# skills-hunmin

[한국어](#한국어)

Personal Cursor agent skills. Add more skill folders over time; installers pick only the ones they want.

`meta-prompting` uses sibling `prompt-optimizer` to rewrite a draft, then asks Y or N before using it. If you want that flow, select both.

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

- [meta-prompting](meta-prompting/SKILL.md)
- [prompt-optimizer](prompt-optimizer/SKILL.md)

---

# 한국어

개인용 Cursor 에이전트 스킬 모음입니다. 스킬 폴더를 계속 추가할 수 있고, 설치하는 사람은 원하는 것만 고릅니다.

`meta-prompting`은 옆에 있는 `prompt-optimizer`로 초안을 고친 뒤, 쓰기 전에 Y 또는 N을 묻습니다. 이 흐름을 쓰려면 둘 다 선택하세요.

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

- [meta-prompting](meta-prompting/SKILL.md)
- [prompt-optimizer](prompt-optimizer/SKILL.md)
