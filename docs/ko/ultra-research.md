# ultra-research

[English](../en/ultra-research.md) · [문서 홈](README.md) · [SKILL.md](../../cursor/ultra-research/SKILL.md)

슬래시 한 번. 의장이 웹이 필요한지, 이 레포가 필요한지, 결정이 필요한지, 그리고 순서를 고른다. 그다음 형제 스킬을 그 스킬로 실행한다. 세 매뉴얼을 한 프롬프트에 붙이지 않는다.

## 왜 만들었나

`deep-research`, `deep-analyze`, `discussion`은 서로의 일을 훔치지 않게 썼다. 그건 그대로 맞다. 실제 질문은 일이 겹치는 경우가 많다. "하이브리드 검색을 우리 배치 파이프에 넣을까?"는 바깥세상, 이 트리, 결정이 같이 필요하다.

공개 오케스트레이터는 순서를 고정하거나(방법론 파이프), `plan.json`이나 debate 폴더를 쓰거나(클라우드 orchestrate, dialectic 키트), 파이프라인을 고르게 한다. 웹→코드→토론을 항상 돌리면, 범위를 좁히거나 패널을 거절하라고 만든 스킬이 죽는다.

이 스킬은 **의장**을 둔다. 의장이 분류하고, 건너뛰고, 가끔 순서를 뒤집는다. 자식 규칙은 그대로다.

## 원리

슬래시로만 켠다. 옆에 형제 셋이 있어야 한다 (`deep-research`, `deep-analyze`, `discussion`). 같이 설치하거나, CLI에서 넷을 같이 고른다.

1. 질문을 고정한다. **웹 / 레포 / 결정**을 표시한다. 규칙: [`references/classify.md`](../../cursor/ultra-research/references/classify.md).
2. 경로를 한 줄로 보여 주고 바로 시작한다. 승인은 기다리지 않는다. 서로 다른 대상이 두 개면 한 번만 묻는다.
3. 고른 단계마다 그 형제 `SKILL.md`를 먼저 읽는다. 핸드오프: [`references/handoff.md`](../../cursor/ultra-research/references/handoff.md).
4. 질문 안에 파일이나 심볼이 이미 있으면 웹과 레포를 병렬로 돌릴 수 있다. 결정은 마지막이고, 트레이드오프가 남을 때만. discussion의 `AskQuestion` 게이트는 유지한다.
5. 채팅 보고: [`references/report-shape.md`](../../cursor/ultra-research/references/report-shape.md). 경로, 답, 단계별 근거.

`research/` 없음. 플레이북 없음. 위키 없음. 형제가 없으면 설치 명령을 찍고 그 단계를 건너뛴다. 싸구려 복사본을 만들지 않는다.

## 언제 쓰나

파이프라인을 내가 고르기 싫고, 질문이 넓은 웹 / 이 레포 / 결정 중 둘 이상일 수 있을 때 `/ultra-research`를 쓴다.

단계를 이미 알면 그 스킬을 직접 부른다. 프롬프트 작업, 위키 closeout, 남은 파일 정리에는 쓰지 않는다.

이 스킬은 **슬래시로만** 켠다.

## 설치

```bash
npx skills add hunminkim98/skills-hunmin --skill ultra-research --agent cursor
npx skills add hunminkim98/skills-hunmin --skill deep-research --agent cursor
npx skills add hunminkim98/skills-hunmin --skill deep-analyze --agent cursor
npx skills add hunminkim98/skills-hunmin --skill discussion --agent cursor
```

또는 설치 UI에서 넷을 같이 고른다. [문서 홈](README.md).

## 사용

1. 새 Agent 채팅.
2. `/ultra-research`와 질문 ("하이브리드 검색을 우리 배치 파이프에 넣을까?").
3. 경로 한 줄을 본다. 대상이 헷갈리지 않으면 승인할 필요 없다.
4. discussion 단계가 열리면 중간 질문에 답한다. 자식 스킬이지 추가 의식이 아니다.
5. Path → Answer → 단계 블록.

매번 세 단계가 나오면 의장이 표시를 무시한 것이다.

## 다른 스킬과

- 일이 하나면 여전히 [deep-research](deep-research.md), [deep-analyze](deep-analyze.md), [discussion](discussion.md).
- 다음 에이전트가 결정을 써야 하면 뒤에 [wiki-for-llm](wiki-for-llm.md).
- 질문 자체가 흐리면 먼저 [meta-prompting](meta-prompting.md).
- [output-debt](output-debt.md)를 대신하지 않는다.

## 한계

한 자리에서 스웜을 세 번 여는 것은 비싸다. 의장은 맥스아웃 대신 단계를 건너뛰었어야 한다. 없는 형제는 스킵이지, 그 스킬을 다시 쓰는 일이 아니다. 시키지 않으면 구현하지 않는다. 해로운 이중 용도는 한 문단으로 거절한다.
