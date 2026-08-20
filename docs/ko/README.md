# skills-hunmin 문서

[English](../en/README.md)

사람이 읽고 쓰라고 적은 안내입니다. 에이전트가 따르는 지시는 각 `SKILL.md`입니다. 문서와 스킬 파일이 다르면 스킬 파일을 믿으세요.

Cursor용 스킬은 [`cursor/`](../../cursor/)에 있습니다. 원하는 것만 고르면 됩니다. 여기서 전부를 강제 설치하지는 않습니다.

## 어떤 스킬을 쓰나요?

| 하고 싶은 일 | 스킬 |
|---|---|
| 거친 아이디어를 아무 채팅에나 붙여 넣을 프롬프트로 만들기 | [prompt-optimizer](prompt-optimizer.md) |
| 프롬프트를 다듬고 Y/N으로 승인한 뒤 실행하거나 복사하기 | [meta-prompting](meta-prompting.md) |
| 작업 노트를 남겨 다음 에이전트가 맥락을 다시 묻지 않게 하기 | [wiki-for-llm](wiki-for-llm.md) |
| 파일은 건드리지 않고 질문 하나만 엄격히 조사하기 | [deep-analyze](deep-analyze.md) |
| 어려운 트레이드오프를 전문가 하위 에이전트와 토론하고, 나도 끼어들기 | [discussion](discussion.md) |
| 영어나 한국어 글이 챗봇처럼 들릴 때 문체만 고치기 | [humanizer](humanizer.md) |
| 남은 에이전트 산출물을 남길지 격리할지 나누기 | [output-debt](output-debt.md) |

이 일들을 서로 바꿔 쓰지 마세요. 사실 조사와 설계 선택은 다릅니다. 토론은 작업 일지가 아닙니다. 이 저장소에는 논문·아티클을 `raw/`에 쌓는 Karpathy식 위키가 없습니다. 챗봇 문체를 지우는 일은 따로 합니다. 옛 렌더를 격리하는 일은 죽은 코드를 지우는 일이 아닙니다.

## 설치

**실제 터미널**(Cursor 터미널 또는 iTerm)에서 실행하세요. Agent 채팅에서는 선택 UI가 뜨지 않습니다.

```bash
npx skills add hunminkim98/skills-hunmin
```

CLI는 `cursor/` 아래 스킬까지 찾아 목록으로 보여 줍니다. 검색하고, 스페이스로 고르고, 엔터로 확정합니다. 그다음 이 프로젝트만 설치할지 이 머신 모든 Cursor 프로젝트에 설치할지, 어느 에이전트에 넣을지 고릅니다.

자주 쓰는 변형:

```bash
# 스킬 하나, 이 프로젝트, Cursor만
npx skills add hunminkim98/skills-hunmin --skill meta-prompting --agent cursor

# 피커에 뜨는 스킬을 이 프로젝트 Cursor에
npx skills add hunminkim98/skills-hunmin --agent cursor

# 위와 같지만 모든 Cursor 프로젝트에서
npx skills add hunminkim98/skills-hunmin --agent cursor --global
```

설치 후 **새** Agent 채팅을 열고 `/` 다음에 스킬 이름을 입력하세요. 아래 페이지에서 "슬래시로만"이라고 한 스킬은 스스로 시작하지 않습니다.

`npx skills add`는 스킬 폴더만 복사합니다. `AGENTS.md`를 설치기가 직접 고치지는 않습니다. [wiki-for-llm](wiki-for-llm.md)은 더 자세한 closeout이 없는 레포에서 **처음 실행될 때** 한 줄을 넣을 수 있습니다.

## 모음이 나뉜 방식

```text
cursor/
  meta-prompting/     # 옆에 prompt-optimizer가 있어야 함
  prompt-optimizer/
  wiki-for-llm/
  deep-analyze/
  discussion/
  humanizer/
  output-debt/
```

`meta-prompting`은 형제 `prompt-optimizer`를 읽습니다. Y/N 흐름을 쓰려면 둘 다 설치하세요. 나머지는 혼자 동작합니다.

## 스킬 페이지

- [meta-prompting](meta-prompting.md)
- [prompt-optimizer](prompt-optimizer.md)
- [wiki-for-llm](wiki-for-llm.md)
- [deep-analyze](deep-analyze.md)
- [discussion](discussion.md)
- [humanizer](humanizer.md)
- [output-debt](output-debt.md)
