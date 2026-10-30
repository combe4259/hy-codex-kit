# hy-codex-kit

Codex에서 쓸 공개 Skill·Plugin·MCP 인덱스. 내용물은 각 원본 저장소에서 직접 받는다.

## ⚠️ 시험 환경 규칙 (먼저 읽기)

### 하면 안 되는 것
| 항목 | 규칙 |
|---|---|
| Git | `git push` 불가. 커밋만 한다. 허용되는 건 공개 저장소 `git clone`뿐 |
| 외부 전송 | 문제·파일·결과물의 외부 전송·공유 금지 (업로드, gist, pastebin, 외부 API로 전송 등). Outbound 모니터링됨 |
| 파일 업로드 | 개인 PC 파일·비공개 Skill 업로드 불가. 필요한 파일은 환경 안에서 작성 |
| 제한 우회 | 차단·감독·업로드 제한을 다른 도구·경로·설정 변경으로 우회 금지. 플랫폼 관리 설정·연결 프로세스 수정·종료 금지 |
| 설정 파일 | `~/.codex/config.toml`의 `probe-managed-mcp` 블록 수정 금지. MCP는 MCP 탭에서만 등록 |
| API 키 | 개인 API 키·유료 구독 사용 금지. 제공된 Codex만 사용. 키·토큰을 출력·공개하지 않음 |
| 모델 | Astra 사용 제한. 권장: Sol 6.1, Terra 5.6, Luna 6, Sol 6.0 |
| 자동 조작 | Computer Use(자동 조작) 전 단계 금지. 브라우저 자동화 도구 사용하지 않음 |
| 외부 브라우저 | 직접 검색·접속 금지. 정보는 Codex(웹 검색·fetch)를 통해서만 |
| 결과물 대체 | 외부 자료로 결과물을 통째로 대체 금지. 특히 제출 직전 대량 교체는 작업 이력 검토 대상 |
| 후속 서술형 | AI 사용 금지(다른 기기 포함), 복사·붙여넣기 불가, 본인이 직접 답변 |
| 감독 | 전체화면 유지, 화면 이탈·캡처 단축키 감지, 모니터 1대, 웹캠·휴대폰·화면 공유 유지 |
| 리소스 | 과도한 프로세스로 인한 메모리 부족(OOM)은 구제 대상 아님. 우측 상단 CPU/RAM 확인 |

### 기억할 것
- 수집 기록: Codex·실무자 대화, 터미널 세션, AI 도구 설정, git log·diff, 테스트 실행 결과, 작업 공간의 문서 → 과정 자체가 평가 대상
- 토큰 사용량은 추적되며 간접 평가에 활용될 수 있음
- 타이머는 멈추지 않음 (재접속·비활성·문의 중에도). 종료 10분 전 제출 시작 권장
- 제출물 확정 후 파일 수정 불가. 후속 서술형은 문항당 5분, 이전 문항으로 못 돌아감
- 서버는 `0.0.0.0`에 바인딩해야 Browser 미리보기 연결됨. 서버 띄운 터미널 탭은 닫지 않기
- 에디터 저장 충돌 시 내용 확인 후 "외부 변경 불러오기" (AI 수정이 날아가지 않게)
- 문제 신고 시 키·토큰·비밀번호 적지 않기. 사용법은 Cofa Helper, 업무 맥락은 실무자 에이전트에게
- 과제 안내 `README.md`는 덮어쓰지 않기
- 이 레포는 2차 예선 결과 통지까지 공개 유지, 시험 중 수정하지 않기

## 한눈에 보기

### 단계별 흐름
스킬 = 생각하는 도구, playbook = 기록·커밋 절차. 단계마다 둘을 이어서 쓴다.

| 단계 | 호출 | 용도 |
|---|---|---|
| 1. 실무자 대화 전 | `$to-questionnaire` | 모르는 것을 실무자에게 물을 질문으로 정리 |
| 2. 실무자 대화 후 | `docs/playbook/interview.md 절차대로 대화 내용 반영해` | 요구사항 → PLAN, 용어 → GLOSSARY |
| 3. 개념 조사 | `docs/playbook/research.md 절차대로 ○○ 조사해` (웹 검색 / fetch) | 반도체 개념 → GLOSSARY |
| 4. 용어 정리 | `$domain-modeling` | 대화·조사에서 확정된 용어를 GLOSSARY로 정돈 |
| 5. 목표 정의 | `$define-goal` | 측정 가능한 목표·성공 기준·검증 방법 → PLAN |
| 6. 설계 검증 | `$grill-me` | 계획의 빈틈을 질문으로 찾기 (구현 전에) |
| 7. 계획 | `/plan` 또는 `$writing-plans` | 작업 순서 확정 → PROGRESS 기능 목록 |
| 8. 구현 | `$test-driven-development` | 기능 하나씩 테스트 먼저 |
| 8-1. 데이터 분석이면 | `$jupyter-notebook` | CSV 탐색 분석 노트북 |
| 8-2. 막히면 | `$systematic-debugging` | 추측 말고 원인부터 찾기 |
| 9. 기능 완료마다 | `docs/playbook/checkpoint.md 절차대로 해` | 테스트 → PROGRESS·VERIFICATION 갱신 → 커밋 → 3줄 보고 |
| 10. 리뷰 | `/review` | 현재 변경의 버그 리뷰 |
| 11. 제출 전 | `docs/playbook/wrapup.md 절차대로 해` | 최종 점검 + 서술형 대비 요약 |
| 언제든 | `/compact` / `$handoff` | 대화가 길어지면 압축 / 새 세션으로 인수인계 |

### Skills
| 이름 | 호출 | 용도 |
|---|---|---|
| to-questionnaire | `$to-questionnaire` | 실무자에게 물을 질문을 순서대로 정리 |
| grill-me | `$grill-me` | 계획·설계의 빈틈을 집요하게 질문 (grilling 필요) |
| domain-modeling | `$domain-modeling` | 확정된 용어를 GLOSSARY로 축적 |
| define-goal | `$define-goal` | 모호한 요청 → 측정 가능한 목표·검증 방법 |
| jupyter-notebook | `$jupyter-notebook` | CSV 탐색 분석용 노트북 생성 |
| handoff | `$handoff 다음 세션 용도` | 컨텍스트 가득 찼을 때 인수인계 문서 |
| superpowers | `$brainstorming` `$test-driven-development` 등 | 계획 → TDD → 디버깅 → 검증 개발 방법론 묶음 |

### MCP (MCP 탭에서만 등록)
| 이름 | 호출 | 용도 |
|---|---|---|
| fetch | `fetch로 <URL> 읽고 요약해줘` | 웹페이지 하나를 마크다운으로 읽기 (도구 1개, 가벼움) |
| Context7 | `use context7 로 <라이브러리> 예시 찾아줘` | 라이브러리 최신 공식 문서·예시 |
| arXiv (선택) | `arxiv에서 <주제> 논문 찾아줘` | 논문 검색 (도구 19개, 무거움) |

### Codex 내장
| 명령 | 용도 |
|---|---|
| `/status` | 모델·권한·토큰 사용량 확인 |
| `/mcp` | 연결된 MCP 목록 확인 |
| `/skills` | 설치된 스킬 확인 |
| `/compact` | 대화가 길어졌을 때 컨텍스트 압축 |
| `/diff` | 현재 변경 확인 |
| 웹 검색 | `○○ 검색해서 알려줘` (꺼져 있으면 `codex --search`) |


## 반도체 과제용 라이브러리·자료

### 라이브러리 (모두 공개·유지 중, 2026-10-30 확인)
| 용도 | 이름 | 레포 | 라이선스 | 한 줄 사용 |
|---|---|---|---|---|
| 통계 검정·회귀 (SPC 보조) | statsmodels | https://github.com/statsmodels/statsmodels | BSD-3 | `statsmodels.stats.diagnostic.normal_ad(x)` |
| 기본 ML·이상 탐지 | scikit-learn | https://github.com/scikit-learn/scikit-learn | BSD-3 | `IsolationForest(contamination=0.01).fit(X)` |
| 센서 이상 탐지 (FDC) | PyOD | https://github.com/yzhao062/pyod | BSD-2 | `ECOD().fit(X).decision_scores_` (튜닝 불필요) |
| 시계열 이상 구간 | STUMPY | https://github.com/stumpy-dev/stumpy | BSD-3 | `stumpy.stump(ts, m=50)` → 최댓값 위치가 이상 구간 |
| 수율·불량 예측 | LightGBM | https://github.com/lightgbm-org/LightGBM | MIT | `LGBMClassifier(class_weight="balanced")` |
| 원인 변수 설명 | SHAP | https://github.com/shap/shap | MIT | `shap.TreeExplainer(model).shap_values(X)` |
| 드문 불량 (불균형) | imbalanced-learn | https://github.com/scikit-learn-contrib/imbalanced-learn | MIT | `SMOTE`, `BalancedRandomForestClassifier`. 지표는 PR-AUC·재현율 |
| 웨이퍼맵 이미지 특징 | scikit-image | https://github.com/scikit-image/scikit-image | BSD-3 | `transform.radon`, `measure.regionprops` |
| 장비 스케줄링 | OR-Tools | https://github.com/google/or-tools | Apache-2.0 | CP-SAT `NewIntervalVar` + `AddNoOverlap` |
| 팹 흐름 시뮬레이션 | SimPy | https://gitlab.com/team-simpy/simpy | MIT | `simpy.Resource(env, capacity=k)`로 장비군 모델링 |
| 대시보드 | Streamlit | https://github.com/streamlit/streamlit | Apache-2.0 | `streamlit run app.py --server.address 0.0.0.0` |
| 차트 | Plotly | https://github.com/plotly/plotly.py | MIT | `st.plotly_chart(fig)` |
| API 서버 | FastAPI | https://github.com/fastapi/fastapi | MIT | `uvicorn main:app --host 0.0.0.0 --port 3000` |
| 테스트 | pytest | https://github.com/pytest-dev/pytest | MIT | FastAPI는 `TestClient`로 테스트 |

설치:

```bash
pip install pandas numpy scikit-learn lightgbm shap pyod plotly streamlit fastapi uvicorn pytest
```

과제 유형별 추가: 스케줄링 `pip install ortools simpy` / 웨이퍼맵 `pip install scikit-image` / 시계열 `pip install stumpy statsmodels` / 불균형 `pip install imbalanced-learn`

### 공식 예제
- OR-Tools job-shop: https://github.com/google/or-tools/blob/stable/examples/python/jobshop_ft06_sat.py
- OR-Tools 설비 정비 포함 job-shop: https://github.com/google/or-tools/blob/stable/examples/python/jobshop_with_maintenance_sat.py

### 개념 자료 (fetch / 웹 검색으로 읽기)
| 주제 | URL |
|---|---|
| SPC·관리도 (공식 핸드북) | https://www.itl.nist.gov/div898/handbook/pmc/pmc.htm |
| 관리도 상세 | https://www.itl.nist.gov/div898/handbook/pmc/section3/pmc3.htm |
| 공정능력 Cp/Cpk | https://www.itl.nist.gov/div898/handbook/pmc/section1/pmc16.htm |
| 반도체 공정 흐름 | https://en.wikipedia.org/wiki/Semiconductor_device_fabrication |
| 웨이퍼 테스트·bin map | https://en.wikipedia.org/wiki/Wafer_testing |
| 다이 | https://en.wikipedia.org/wiki/Die_(integrated_circuit) |
| 수율 | https://en.wikipedia.org/wiki/Yield_(engineering) |
| SPC 개요 | https://en.wikipedia.org/wiki/Statistical_process_control |
| 이상 판정 규칙 | https://en.wikipedia.org/wiki/Western_Electric_rules |
| 공정능력지수 | https://en.wikipedia.org/wiki/Process_capability_index |
| APC | https://en.wikipedia.org/wiki/Advanced_process_control |
| 가상계측 (VM) | https://en.wikipedia.org/wiki/Virtual_metrology |
| 고장 탐지 (FDC) | https://en.wikipedia.org/wiki/Fault_detection_and_isolation |

## 하네스 (이 레포, `templates/`)

- `AGENTS.md`: 60줄 안팎의 지도. 명령어·작업 순서·완료 기준·docs 포인터·제약·커밋·토큰 절약·설명 규칙. 명령어 칸은 과제에 맞게 채운다. 수정하면 Codex 재시작해야 반영됨.
- `docs/`: 제출 문서 뼈대
  - `PLAN.md` 문제·요구사항·위험 시나리오·가정·성공 기준 / `DECISIONS.md` 결정·대안·충분한 이유·깨지는 조건·근거 코드 / `VERIFICATION.md` 검증(반복 횟수)·남은 한계
  - `GLOSSARY.md` 도메인 용어 / `PROGRESS.md` 기능 목록·통과 여부
  - `README_TEMPLATE.md` 결과물 README 뼈대 (한 명령 실행·테스트·헬스체크·환경과 가정·기능 요약). 과제 안내 README는 덮어쓰지 않는다.
- `docs/playbook/`: 부를 때만 읽는 절차 문서 (스킬 아님, 평소엔 컨텍스트에 안 올라감)
  - `interview.md` 실무자 대화 전 질문 정리 · 대화 후 PLAN 반영
  - `research.md` 도메인 개념 조사 → GLOSSARY
  - `checkpoint.md` 기능 하나 끝날 때: 테스트 → PROGRESS·VERIFICATION 갱신 → 커밋 → 3줄 보고
  - `wrapup.md` 제출 전 점검 + 후속 서술형 대비 요약
- `config.toml`: `~/.codex/config.toml`에 붙일 조각 (웹 검색 한 줄). 이미 있거나 관리 설정으로 막혀 있으면 추가하지 않음.

과제 작업 폴더에서:

```bash
git clone https://github.com/combe4259/hy-codex-kit.git ~/kit
cp ~/kit/templates/AGENTS.md . && cp -r ~/kit/templates/docs .
```


**MCP 규칙**: MCP는 MCP 탭에서만 등록한다. `config.toml` 직접 수정이나 Codex에게 MCP 등록을 시키지 않는다 (탭이 쓰는 `probe-managed-mcp` 블록과 이름이 겹치면 `duplicate key`로 Codex가 안 켜짐). 등록 전 Codex에서 `/mcp`로 이미 붙어 있는지 확인.

Codex가 안 켜지면: `python3 -c "import tomllib,os;tomllib.load(open(os.path.expanduser('~/.codex/config.toml'),'rb'));print('OK')"` 로 문제 줄 확인 → `probe-managed-mcp` 블록 밖의 중복만 삭제.

## Superpowers

- 저장소: https://github.com/obra/superpowers (공개, MIT)
- 계획 → TDD → 디버깅 → 검증 → 리뷰 흐름을 강제하는 개발 방법론 Skill 묶음 (brainstorming, writing-plans, test-driven-development, systematic-debugging, verification-before-completion 등).
- 기준 커밋: `2ce8aa15d05bd57213e6f746f953aafb7ded7a8b`

설치 (1순위): Codex CLI에서 `/plugins` → `superpowers` 검색 → Install Plugin

설치 (마켓 안 될 때):

```bash
git clone https://github.com/obra/superpowers.git ~/.codex/superpowers
git -C ~/.codex/superpowers checkout 2ce8aa15d05bd57213e6f746f953aafb7ded7a8b
mkdir -p ~/.agents/skills && ln -s ~/.codex/superpowers/skills ~/.agents/skills/superpowers
```

설치 후 Codex 재시작 → `/skills`로 확인

## Context7 (MCP)

- 저장소: https://github.com/upstash/context7 (공개, MIT)
- 라이브러리 최신 공식 문서·코드 예시를 Codex에 가져오는 MCP. 학습 데이터에 없는 최신 API를 확인할 때 사용.
- API 키 없이도 동작 (요청 한도만 낮음). 응시 환경에서는 개인 키 쓰지 말 것.
- 기준 커밋: `8a0289e4c5e28684b7c4ced5353af2893d1329f9` / npm `@upstash/context7-mcp@4.4.4`

설치 (MCP 탭 JSON):

```json
{
  "mcpServers": {
    "context7": {
      "url": "https://mcp.context7.com/mcp"
    }
  }
}
```

원격 URL이 안 되면 로컬 실행:

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp@4.4.4"]
    }
  }
}
```

사용: `use context7 로 FastAPI 라우터 예시 찾아줘` / AGENTS.md에 `When you need to search docs, use Context7.`

## OpenAI 공식 skills (define-goal / jupyter-notebook)

- 저장소: https://github.com/openai/skills (공개, 각 스킬 폴더에 Apache-2.0 LICENSE.txt)
- `define-goal`: 모호한 요청을 측정 가능한 목표·범위·검증 방법·종료 조건으로 정리. 계획 문서 맨 위에 사용. (`/goal` 연동, 0.139에서 동작 여부 미확인)
- `jupyter-notebook`: 수율·센서·결함 CSV 탐색 분석용 노트북을 템플릿 스크립트로 생성 (토큰 절약).
- 기준 커밋: `49f948faa9258a0c61caceaf225e179651397431`

설치 (1순위): Codex에서 `$skill-installer define-goal`, `$skill-installer jupyter-notebook`

설치 (수동):

```bash
git clone https://github.com/openai/skills.git ~/.codex/openai-skills
git -C ~/.codex/openai-skills checkout 49f948faa9258a0c61caceaf225e179651397431
mkdir -p ~/.agents/skills
for s in define-goal jupyter-notebook; do ln -s ~/.codex/openai-skills/skills/.curated/$s ~/.agents/skills/$s; done
```

## Matt Pocock skills (grill-me / grilling / handoff / to-questionnaire / domain-modeling)

- 저장소: https://github.com/mattpocock/skills (공개, MIT, Codex용 `agents/openai.yaml` 포함)
- `grill-me` (+ 내부에서 호출하는 `grilling`): 계획·설계를 AI가 집요하게 질문해서 빈틈을 찾아줌. 구현 전 요구사항 정리용.
- `to-questionnaire`: 내가 모르는 것을 실무자에게 물어볼 질문 목록으로 순서대로 정리. 메신저 대화 전에 사용.
- `domain-modeling`: 대화하며 확정된 용어를 `GLOSSARY.md`로 축적. 낯선 도메인(반도체) 용어 정리 + 후속 서술형 대비.
- `handoff`: 현재 대화를 다음 세션/에이전트가 이어받을 인수인계 문서로 압축 (컨텍스트 꽉 찼을 때).
- 기준 커밋: `a496f5513d4a4cf889bc48e189e579f4b0bdf6aa`

설치:

```bash
git clone https://github.com/mattpocock/skills.git ~/.codex/mattpocock-skills
git -C ~/.codex/mattpocock-skills checkout a496f5513d4a4cf889bc48e189e579f4b0bdf6aa
mkdir -p ~/.agents/skills
for s in productivity/grill-me productivity/grilling productivity/handoff productivity/to-questionnaire engineering/domain-modeling; do ln -s ~/.codex/mattpocock-skills/skills/$s ~/.agents/skills/$(basename $s); done
```

사용: `$to-questionnaire` / `$domain-modeling` / `$grill-me` / `$handoff 다음 세션은 테스트 작성용`

## Codex 내장 웹 검색 (설치 없음)

- 출처: https://github.com/openai/codex (Apache-2.0), `WebSearchMode = disabled | cached(기본) | live`
- 반도체 개념 딥리서치 1순위. MCP 도구 정의가 안 붙어서 토큰 부담 없음.
- 켜기: `codex --search` 또는 `~/.codex/config.toml` 최상단에 `web_search = "live"`
- 소스로만 확인. 응시 환경 관리자 설정으로 막혀 있을 수 있음 → 사전 체험 때 `/status` 확인 후 검색 한 번 시켜보기.

## fetch MCP

- 저장소: https://github.com/modelcontextprotocol/servers (공개, MIT) `src/fetch`
- URL 하나를 마크다운으로 읽어오는 도구 1개짜리 MCP. 위키피디아·공식 문서 읽기용, 웹 검색 막혔을 때 대안.
- 기준 커밋: `194cc86e3ae6400958555bd4116849d822d69263` / PyPI `mcp-server-fetch==2026.10.28` (로컬 테스트 완료)

```json
{
  "mcpServers": {
    "fetch": {
      "command": "uvx",
      "args": ["mcp-server-fetch==2026.10.28"]
    }
  }
}
```

`uvx` 없으면: `pip install mcp-server-fetch==2026.10.28` 후 `"command": "python", "args": ["-m", "mcp_server_fetch"]`

## arXiv MCP (선택)

- 저장소: https://github.com/blazickjp/arxiv-mcp-server (공개, Apache-2.0)
- 논문 검색·읽기 (wafer map defect, SPC 등). 도구 19개라 토큰 많이 듦 → 논문 수준으로 파야 할 때만 붙이기.
- 기준 커밋: `572e301bb3198962c025d5ed5e14becb86868daa` / PyPI `arxiv-mcp-server==0.8.2` (Python 3.11+, 로컬 테스트 완료)

```json
{
  "mcpServers": {
    "arxiv": {
      "command": "uvx",
      "args": ["arxiv-mcp-server==0.8.2"]
    }
  }
}
```
