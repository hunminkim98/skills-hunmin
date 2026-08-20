# deep-research

[English](../en/deep-research.md) · [문서 홈](README.md) · [SKILL.md](../../cursor/deep-research/SKILL.md)

주제를 관련 웹 각도로 나눈다. 그 각도를 병렬로 검색한다. 채팅에 근거 있는 브리프를 남긴다. 무엇이 버티는지, 출처가 어디서 싸우는지, 아직 모르는 것.

## 왜 만들었나

검색 한 번은 첫 SERP를 답한다. 에이전트 일에는 옆 질문도 필요한 경우가 많다. 공식 이야기, 반대, 올해 바뀐 것, 실제로 돌아간 사례. 그걸 한 답에서 목소리 다섯 개로 흉내 내면 연기다. Firecrawl 키 하나로 포장하면 제품 광고다.

이 근처의 공개 스킬은 대개 셋 중 하나로 간다. 플레이북 파일을 쓰거나(webcpu 쪽). P0–P7을 돌리며 `research-notes/`에 수천 단어를 쌓거나(daymade 쪽). 아니면 유료 API를 감싼다(AnyCap, Gemini Deep Research, Firecrawl 전용 팜).

이건 **채팅**에 남긴다. **실제 병렬 레인 에이전트**를 띄운다. 링크 나열은 실패다. 벤더는 필요 없다. 커버리지는 각도의 수이지 페이지 길이가 아니다.

[deep-analyze](deep-analyze.md)가 아니다. 그쪽은 질문 하나, 종종 이 레포, 범위를 넓히면 버그다. 여기서 넓히는 것은 일이다.

## 원리

슬래시로만 켠다. 주제가 없으면 시작하지 않는다.

1. 질문을 한 문장으로 고정한다. 레포 감사와 "뭘 출시할까"는 범위 밖.
2. 레인 4개(다른 영역이 정말 끼면 5개). 기본 일: **Core**, **Counter**, **Now**, **Practice**. 다섯 번째는 **Limits**. 규칙: [`references/lanes.md`](../../cursor/deep-research/references/lanes.md).
3. 레인을 **한 번의** Task 배치로 띄운다 (`web-researcher`가 있으면 그것, 없으면 `generalPurpose`). 레인마다 서로 다른 질의 셋 이상, URL 둘에서 넷. 프로토콜: [`references/search-protocol.md`](../../cursor/deep-research/references/search-protocol.md).
4. 빈약한 레인은 질의를 바꿔 **한 번만** 다시 돌린다. 같은 단어를 두 번 치는 것은 2파가 아니다. 그다음엔 `insufficient evidence`.
5. 채팅 보고: [`references/report-shape.md`](../../cursor/deep-research/references/report-shape.md). 아는 것, 충돌, 불확실, 다음에 읽을 것, 실제로 연 URL.

인용: [`references/citations.md`](../../cursor/deep-research/references/citations.md). 안 연 제목은 출처가 아니다. 의견이 갈리면 보고서에 남긴다. 페이월을 우회하지 않는다. 챕터를 붙여 넣지 않는다.

`research/` 폴더 없음. 플레이북 마크다운 없음. 위키 없음. 나중에 남기려면 [wiki-for-llm](wiki-for-llm.md).

## 언제 쓰나

웹에서 그 주제의 쓸모 있는 그림을 보고 싶을 때 `/deep-research`를 쓴다. 서로 반박하는 부분까지.

"이 함수가 배치 행에 락을 거나"는 [deep-analyze](deep-analyze.md). 출시 결정은 [discussion](discussion.md). 프롬프트 작업과 남은 파일 정리는 이쪽이 아니다.

이 스킬은 **슬래시로만** 켠다.

## 설치

```bash
npx skills add hunminkim98/skills-hunmin --skill deep-research --agent cursor
```

프로젝트와 전역은 [문서 홈](README.md).

## 사용

1. 새 Agent 채팅.
2. `/deep-research`와 주제 ("2026년에 하이브리드 검색을 어떻게 쓰고, 어디서 깨지나?").
3. 레인 명단을 본다. 레인을 고르겠다고 하지 않는 한 승인은 필요 없다.
4. 병렬 파를 기다린다. 빈 레인이 있으면 재검색은 최대 한 번.
5. What we know → Conflicts → Uncertain → What to read next.

레포에 새 마크다운이 생기면 스킬을 안 지킨 것이다.

## 다른 스킬과

- **이** 코드베이스의 사실은 [deep-analyze](deep-analyze.md). 바깥세상이 남으면 그때 여기로.
- 브리프 다음의 가치 싸움은 [discussion](discussion.md).
- 이 스킬과 레포 감사와 패널을 의장이 고르게 하려면 [ultra-research](ultra-research.md).
- 다음 에이전트가 써야 하면 [wiki-for-llm](wiki-for-llm.md).
- 남은 렌더를 치울 때는 [output-debt](output-debt.md)이지 이쪽이 아니다.

## 한계

병렬 레인은 시간과 토큰을 쓴다. 사회자는 3파를 열지 않는다. 인터넷이 빈약하면 보고도 그렇게 적어야 한다. 찾은 라이브러리를 구현하지 않는다. 해로운 이중 용도는 한 문단으로 거절한다.
