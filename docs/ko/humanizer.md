# humanizer

[English](../en/humanizer.md) · [문서 홈](README.md) · [SKILL.md](../../cursor/humanizer/SKILL.md)

챗봇처럼 읽히는 글을 고친다. 영어 블록과 한국어 블록은 규칙이 다르다. 슬래시 하나다.

## 왜 만들었나

시중의 humanizer는 대개 한 언어만 본다. [blader/humanizer](https://github.com/blader/humanizer)는 영어 티(`delve`, 엠대시, "Great question!")를 잡고, [DaleSeo/korean-skills](https://github.com/DaleSeo/korean-skills)는 한국어 티(`에 대해`, `~것입니다`, `되어진다`)를 잡는다. `SKILL.md` 두 개를 붙이면 싸운다. 영어 대시 규칙이 한국어 문장에 들어가고, 한국어 쉼표 규칙이 영어에 들어가고, 짧은 문장에도 패턴 70개가 로드된다.

이 저장소 README처럼 **한 파일에 두 언어가 있는** 경우가 있어서, 설치할 스킬은 하나여야 했다. 어느 제목을 어느 humanizer가 맡는지 외우게 하지 않으려고 만들었다.

항상 켜 두지도 않는다. 채팅마다 윤문하면 설치 안내가 에세이가 된다. 필요할 때 `/humanizer`를 친다.

## 원리

에이전트는 섞는 쪽이 아니라 **라우터**다.

1. 붙여 넣은 글이나 파일 경로를 받는다. 둘 다 없으면 한 번 묻고 멈춘다.
2. 먼저 보호 구간을 가린다. 코드, 명령, frontmatter, 숫자, URL, 스킬 이름. [`references/leave-alone.md`](../../cursor/humanizer/references/leave-alone.md).
3. 나머지를 **언어 블록**으로 나눈다. 제목 아래 산문, 또는 같은 문자가 다수인 문단 묶음. 문장마다 언어를 뒤집지 않는다.
4. 라틴 문자 다수 블록만 [`references/en-patterns.md`](../../cursor/humanizer/references/en-patterns.md)를 연다. 한글 다수 블록만 [`references/ko-patterns.md`](../../cursor/humanizer/references/ko-patterns.md)를 연다. 안 쓰는 카탈로그는 닫아 둔다.
5. 상투어만 고치고 주장은 남긴다. 기술 문서는 담담하게. 없던 농담과 없던 사실은 넣지 않는다.
6. 부정문, 이름, 숫자를 다시 보고, 얼마나 바꿨는지 가늠한다. 절반이 넘으면 덮어쓰지 않고 묻는다.

내가 쓴 글 두세 문단을 샘플로 주면 리듬과 구두점은 그걸 따른다. 사실은 따르지 않는다.

탐지만 할 수도 있다. "고치지 말고 티만 찾아줘."

카탈로그는 짧은 작업 목록이다. 출처는 [`references/sources.md`](../../cursor/humanizer/references/sources.md). 업스트림 스킬을 통째로 벤더한 게 아니라서, 그쪽 버전을 따라가지 않는다.

## 언제 쓰나

말은 맞는데 기계처럼 들릴 때 `/humanizer`를 쓴다. README, 변경 기록, 블로그 한 단락, 영어를 옮긴 듯한 한국어 공지.

프롬프트가 필요하면 ([prompt-optimizer](prompt-optimizer.md) / [meta-prompting](meta-prompting.md)), 사실 확인이면 ([deep-analyze](deep-analyze.md)), 트레이드오프면 ([discussion](discussion.md)), 작업 기록이면 ([wiki-for-llm](wiki-for-llm.md)) 이쪽이 아니다. 코드도 아니고, "탐지기 통과"도 아니다.

이 스킬은 **슬래시로만** 켠다.

## 설치

```bash
npx skills add hunminkim98/skills-hunmin --skill humanizer --agent cursor
```

이 머신 모든 Cursor 프로젝트에 넣으려면 `--global`. 피커는 [문서 홈](README.md).

같은 에이전트에 `blader/humanizer`가 있으면 둘 다 `/humanizer`로 잡힐 수 있다. 메뉴가 헷갈리면 하나를 지운다.

## 사용

1. 새 Agent 채팅.
2. `/humanizer`와 초안, 또는 경로 (`docs/ko/README.md`).
3. 내 말투를 맞추려면 내가 쓴 글 두세 문단을 같이 넣는다.
4. 윤문본(또는 경로)을 본다. "무엇이 바뀌었나"는 몇 줄이면 된다. 논문이 나오면 스킬을 안 지킨 것이다.

한 파일에 영어·한국어가 같이 있으면, 한 번의 실행이 섹션을 나눠 처리한다.

채팅 안내는 요청한 언어를 따른다. 초안 언어는 그대로 둔다.

## 다른 스킬과

- 프롬프트는 먼저 만들고 ([prompt-optimizer](prompt-optimizer.md)), 그 프롬프트 문장이 상투적일 때만 윤문한다. 윤문 후 실행은 그렇게 시켰을 때만.
- [discussion](discussion.md) 권고를 밖으로 낼 때 문체를 다듬을 수는 있다. discussion 자체는 파일을 쓰지 않는다.
- [deep-analyze](deep-analyze.md) 대신 쓰지 않는다. 문장이 매끈한 것과 근거는 다른 일이다.

## 한계

원문에 없던 성격을 넣지 않는다. 기술 문서의 합니다체는 합니다체로 남는다. 보호 구간 때문에 페이지가 조금 딱딱해도, 설치 명령이 깨지는 쪽보다 낫다. 업스트림은 계속 바뀐다. 이 카탈로그는 이쪽 것이고, 일부러 따라가지 않는다.
