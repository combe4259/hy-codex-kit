# AGENTS.md

## 프로젝트
- 문제: (실무자 요청 한 줄 요약)
- 결과물: (무엇을 만들어 제출하는가)
- 세부 내용은 `docs/PLAN.md`가 기준이다.

## 명령어
- 실행: (예: `docker compose up --build -d`)
- 테스트: (예: `python3 -m pytest -q`)
- 스모크 확인: (예: `curl -s -o /dev/null -w '%{http_code}\n' http://localhost:3000`)

## 작업 순서
1. 구현 전에 `docs/PLAN.md`를 채운다. 요구사항이 모호하면 추측하지 말고 멈춰서 질문 목록을 만든다.
2. `docs/PROGRESS.md`의 기능을 한 번에 하나씩 진행한다.
3. 기능마다 테스트를 먼저 쓰고, 통과하는 최소 코드를 작성한다.
4. 기능이 끝나면 `docs/playbook/checkpoint.md` 절차를 따른다.

## 단계별 도구
설치된 스킬은 단계에 맞을 때 사용한다. 없는 스킬은 건너뛰고 같은 목적을 직접 수행한다.
- 실무자 대화 전: `to-questionnaire` → 대화 후 `docs/playbook/interview.md`
- 도메인 개념: `docs/playbook/research.md` (웹 검색 / fetch) → 용어 정돈 `domain-modeling`
- 목표 정의: `define-goal` → 설계 빈틈 점검 `grill-me` (요구사항이 모호할 때만)
- 계획: `writing-plans` 또는 `/plan` → `docs/PROGRESS.md` 기능 목록
- 구현: `test-driven-development`, 데이터 분석이면 `jupyter-notebook`, 막히면 `systematic-debugging`
- 기능 완료: `docs/playbook/checkpoint.md` / 제출 전: `docs/playbook/wrapup.md`
- 대화가 길어지면 `handoff`

## 완료 기준
- 테스트와 스모크 확인을 이번 변경 이후 실제로 실행했고, 출력에서 통과를 확인했다.
- 명령 출력 없이 "완료", "동작함"이라고 말하지 않는다.
- 테스트를 수정하거나 삭제해서 통과시키지 않는다.

## 문서 (필요할 때만 읽기)
- `docs/PLAN.md`: 문제·요구사항·성공 기준. 범위가 헷갈릴 때.
- `docs/GLOSSARY.md`: 도메인 용어. 비즈니스 로직을 건드리기 전에.
- `docs/DECISIONS.md`: 설계·기술 선택을 할 때마다 한 항목 추가.
- `docs/VERIFICATION.md`: 검증 결과와 남은 한계.
- `docs/PROGRESS.md`: 기능 목록과 통과 여부.
- `docs/playbook/*.md`: 위 "단계별 도구"의 해당 단계에 도달했거나 사용자가 요청할 때 읽고 그 절차를 따른다.

## 제약
- 웹 서버는 `0.0.0.0`에 바인딩하고 실행 포트를 출력한다.
- 서버를 띄운 터미널은 종료하지 않는다.
- 새 의존성은 이유를 말하고 추가한다. 개인 API 키·유료 외부 서비스는 쓰지 않는다.
- `~/.codex/config.toml`과 `probe-managed-mcp` 블록은 수정하지 않는다.

## 커밋
- 동작하는 작은 단위마다 커밋. 형식: `feat:`, `fix:`, `test:`, `docs:`, `refactor:`
- 메시지에는 무엇보다 왜를 적는다. 테스트 실패 상태로 커밋하지 않는다.

## 토큰 절약
- 큰 파일·데이터는 통째로 읽지 말고 검색하거나 필요한 범위만 읽는다.
- 긴 명령 출력은 요약해서 보고한다. 코드 전체를 다시 출력하지 않는다.
- 같은 명령을 반복 실행하지 않는다.

## 사람이 이해할 수 있게
- 각 단계를 마치면 무엇을, 왜 바꿨는지 3줄 이내로 설명한다.
- 도메인 용어가 처음 나오면 한 줄 정의를 붙이고 `docs/GLOSSARY.md`에 추가한다.
