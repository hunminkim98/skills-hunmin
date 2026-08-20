# output-debt

[English](../en/output-debt.md) · [문서 홈](README.md) · [SKILL.md](../../cursor/output-debt/SKILL.md)

에이전트가 남긴 산출물에 1부터 5까지 점수를 매긴다. 3 미만은 `garbage/`로 옮기고 메모를 붙인다. 3 이상은 그대로 둔다. 지우지는 않는다.

## 왜 만들었나

에이전트 일은 시험을 많이, 빨리 도는 쪽에 가깝다. 시험마다 파일이 생긴다. 하루가 지나면 `render.png`, `render2.png`, `render_final.png`가 있고, README가 가리키는 파일이 무엇인지 아무도 모른다. 그게 인지 부채다. 사람도, 다음 에이전트도 추측해야 한다.

공개된 cleanup 스킬은 대개 둘 중 하나다. tmp와 스크린샷을 지우거나, KEEP/ARCHIVE로 가른 뒤 확인을 묻는다. 삭제는 너무 빠르다. 지킬지 말지 이분법은 다음 주에 다시 볼 파일에는 거칠다.

이 스킬은 **점수**를 남긴다. 5는 지금 쓰는 산출물. 1은 실패한 출력. **3 미만**만 작업 트리에서 나가고, 목적지는 `/dev/null`이 아니라 `garbage/`다. 그 폴더를 비우는 것, 또는 메모에 적힌 경로로 되돌리는 것은 나중이다.

코드 청소가 아니다. [wiki-for-llm](wiki-for-llm.md)도 아니다. 위키 노트는 위키에 둔다.

## 원리

슬래시로만 켠다. `git status`가 지저분하다고 스스로 시작하지 않는다.

1. 범위: 지정한 폴더, 또는 프로젝트 루트에서 never-move 트리(`node_modules`, `.git`, 제품 소스)를 뺀 곳.
2. 산출물만 고른다. 추적 안 된 덤프, `tmp/`, 더 새 파일 옆의 `*_v2*`, README가 안 가리키는 렌더. `src/` 아래 추적 안 된 `.ts`는 미완 작업이지 렌더가 아니다.
3. 1–5점과 근거 한 줄. 규칙은 [`references/scoring.md`](../../cursor/output-debt/references/scoring.md). 판단이 안 되면 **3**을 주고 그대로 둔다.
4. 1과 2를 `garbage/YYYY-MM-DD/`로 옮긴다. 원래 상대 경로는 유지한다. `MEMO.md`를 쓴다. 배치: [`references/garbage-layout.md`](../../cursor/output-debt/references/garbage-layout.md).
5. `.gitignore`가 있고 `garbage/`가 아직 추적되지 않으면 `garbage/` 한 줄을 넣는다. git status는 실제 작업만 보이게.
6. 채팅 보고: 개수, 옮긴 것, 메모 경로. [`references/report-shape.md`](../../cursor/output-debt/references/report-shape.md).

건드리면 안 되는 목록: [`references/never-move.md`](../../cursor/output-debt/references/never-move.md). 시크릿은 `garbage/`로 복사하지 않는다. 소스, `AGENTS.md`, `llm-wiki/`는 후보에 넣지 않는다.

## 언제 쓰나

실험을 한동안 돌린 뒤, 커밋 전에, 또는 어느 CSV가 맞는지 에이전트와 말이 엇갈릴 때 `/output-debt`를 쓴다.

`node_modules` 삭제, 죽은 코드 리팩터, 작업 일지, 프롬프트 다시 쓰기에는 쓰지 않는다.

이 스킬은 **슬래시로만** 켠다.

## 설치

```bash
npx skills add hunminkim98/skills-hunmin --skill output-debt --agent cursor
```

모든 Cursor 프로젝트에 넣으려면 `--global`. 피커는 [문서 홈](README.md).

## 사용

1. 새 Agent 채팅.
2. `/output-debt`. 폴더를 적어도 된다 (`tmp/`, `demo/`).
3. Stayed와 Moved를 본다. 옮긴 게 있으면 `garbage/YYYY-MM-DD/MEMO.md`를 연다.
4. 되돌리려면 메모의 원래 경로로 옮긴다. `garbage/`에서 지우는 것은 그럴 작정일 때만.

제품 소스가 옮겨지면 스킬을 안 지킨 것이다. 되돌리면 된다.

## 다른 스킬과

- [wiki-for-llm](wiki-for-llm.md)는 결정을 적는다. 이쪽은 파일을 옮긴다. 격리 규칙을 남기고 싶으면 위키 노트를 따로 요청하면 된다.
- 폴더가 무엇인지 알기만 하고 옮기지 않으려면 [deep-analyze](deep-analyze.md).
- "어떤 디자인을 출시하나"는 [discussion](discussion.md)이지 이쪽이 아니다.

## 한계

`garbage/`를 대신 비우지 않는다. 애매해서 3을 준 파일은 일부러 남는다. `garbage/`를 gitignore하면 원격에는 안 보인다. 로컬 인지 부하를 줄이려는 동작이다. 격리를 원격에도 남기려면 gitignore를 빼고 직접 커밋하면 된다.
