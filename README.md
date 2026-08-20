# skills-hunmin

[한국어](#한국어) · [Docs (EN)](docs/en/README.md) · [문서 (KO)](docs/ko/README.md)

Personal agent skills, grouped by host. Cursor-specific skills live under `cursor/`. Add more folders over time; installers pick only the ones they want.

Full guides: [English](docs/en/README.md) and [한국어](docs/ko/README.md).

`meta-prompting` uses sibling `prompt-optimizer` to rewrite a draft, then asks Y or N before using it. If you want that flow, select both.

`wiki-for-llm` writes task, decision, cleanup, and improvement notes so the next agent can continue without asking the user to recap. It is not Karpathy-style source ingest.

`deep-analyze` is a read-only investigation of a user-specified question. It stays in scope, cites evidence, and does not change files.

`discussion` runs a real parallel expert debate on a complex problem, asks the user when a constraint would change the ranking, and returns one recommended path.

`humanizer` rewrites chatbot prose. English blocks and Korean blocks use different catalogs so the rules do not fight.

`output-debt` scores leftover agent outputs from 5 to 1. Scores below 3 go to `garbage/` with a memo. Nothing is deleted.

`deep-research` fans a topic into related web angles, searches them in parallel, and returns a cited brief in chat. It does not write a playbook file.

`ultra-research` is the chair for those three. It picks which of `deep-research`, `deep-analyze`, and `discussion` to run, and in what order. Install the siblings next to it.

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

- [meta-prompting](cursor/meta-prompting/SKILL.md) · [docs](docs/en/meta-prompting.md)
- [prompt-optimizer](cursor/prompt-optimizer/SKILL.md) · [docs](docs/en/prompt-optimizer.md)
- [wiki-for-llm](cursor/wiki-for-llm/SKILL.md) · [docs](docs/en/wiki-for-llm.md)
- [deep-analyze](cursor/deep-analyze/SKILL.md) · [docs](docs/en/deep-analyze.md)
- [discussion](cursor/discussion/SKILL.md) · [docs](docs/en/discussion.md)
- [humanizer](cursor/humanizer/SKILL.md) · [docs](docs/en/humanizer.md)
- [output-debt](cursor/output-debt/SKILL.md) · [docs](docs/en/output-debt.md)
- [deep-research](cursor/deep-research/SKILL.md) · [docs](docs/en/deep-research.md)
- [ultra-research](cursor/ultra-research/SKILL.md) · [docs](docs/en/ultra-research.md)

In a new repo, install `wiki-for-llm` (project or global) and add the one-line closeout from `cursor/wiki-for-llm/references/agents-md-snippet.md` to `AGENTS.md` if the repo has no richer wiki rule.

---

# 한국어

에이전트별로 나눠 둔 개인 스킬 모음입니다. Cursor 전용 스킬은 `cursor/`에 있습니다. 폴더를 계속 추가할 수 있고, 설치하는 사람은 원하는 것만 고릅니다.

동기·원리·설치·사용까지 적은 안내는 [한국어 문서](docs/ko/README.md)와 [English docs](docs/en/README.md)에 있습니다.

`meta-prompting`은 옆에 있는 `prompt-optimizer`로 초안을 고친 뒤, 쓰기 전에 Y 또는 N을 묻습니다. 이 흐름을 쓰려면 둘 다 선택하세요.

`wiki-for-llm`는 작업·결정·정리·개선 노트를 남겨, 다음 에이전트가 사용자에게 맥락을 다시 묻지 않게 합니다. 바깥 자료를 raw에 넣는 Karpathy 위키가 아닙니다.

`deep-analyze`는 사용자가 지정한 질문만 읽기 전용으로 조사합니다. 범위를 넓히지 않고, 근거를 붙이며, 파일은 바꾸지 않습니다.

`discussion`은 복잡한 문제를 실제 병렬 전문가 에이전트와 토론하고, 순위가 갈리는 지점에서 사용자에게 물은 뒤 하나의 권고안을 냅니다.

`humanizer`는 챗봇처럼 읽히는 글을 고칩니다. 영어 블록과 한국어 블록은 카탈로그가 달라서 규칙이 서로 싸우지 않습니다.

`output-debt`는 남은 에이전트 산출물에 1부터 5까지 점수를 매깁니다. 3 미만은 메모와 함께 `garbage/`로 갑니다. 지우지는 않습니다.

`deep-research`는 주제를 관련 웹 각도로 나눈 뒤 병렬로 검색하고, 채팅에 근거 있는 브리프를 남깁니다. 플레이북 파일은 쓰지 않습니다.

`ultra-research`는 그 셋의 의장입니다. `deep-research`, `deep-analyze`, `discussion` 중 무엇을 어떤 순서로 돌릴지 고릅니다. 형제를 옆에 설치하세요.

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

- [meta-prompting](cursor/meta-prompting/SKILL.md) · [문서](docs/ko/meta-prompting.md)
- [prompt-optimizer](cursor/prompt-optimizer/SKILL.md) · [문서](docs/ko/prompt-optimizer.md)
- [wiki-for-llm](cursor/wiki-for-llm/SKILL.md) · [문서](docs/ko/wiki-for-llm.md)
- [deep-analyze](cursor/deep-analyze/SKILL.md) · [문서](docs/ko/deep-analyze.md)
- [discussion](cursor/discussion/SKILL.md) · [문서](docs/ko/discussion.md)
- [humanizer](cursor/humanizer/SKILL.md) · [문서](docs/ko/humanizer.md)
- [output-debt](cursor/output-debt/SKILL.md) · [문서](docs/ko/output-debt.md)
- [deep-research](cursor/deep-research/SKILL.md) · [문서](docs/ko/deep-research.md)
- [ultra-research](cursor/ultra-research/SKILL.md) · [문서](docs/ko/ultra-research.md)

새 레포에서는 `wiki-for-llm`를 설치하고, 더 자세한 위키 규칙이 없을 때만 `AGENTS.md`에 `cursor/wiki-for-llm/references/agents-md-snippet.md`의 한 줄을 넣으면 됩니다.
