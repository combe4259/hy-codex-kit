# Codex 사용법 (Claude Code → Codex)

codex-cli 0.139 소스 기준. 시험 환경 버전은 다를 수 있으니 `/` 입력해서 실제 목록 확인.

## 시작·세션
| Claude Code | Codex | 비고 |
|---|---|---|
| `claude` | `codex` | |
| `claude -p "..."` | `codex exec "..."` | 대화창 없이 한 번 실행 |
| `claude --continue` / `--resume` | `codex resume --last` / `codex resume`, 안에서 `/resume` | |
| `/clear` | `/clear` 또는 `/new` | 새 대화 |
| `/exit` | `/exit` 또는 `/quit` | |
| `/cost`, `/context` | `/status` | 모델·권한·토큰 사용량 |
| `/doctor` | `/debug-config` | 설정 출처 확인 |
| `/export` | `/copy` | 마지막 응답 마크다운 복사 |

## 권한·자동 승인
| Claude Code | Codex | 비고 |
|---|---|---|
| `/permissions` | `/permissions` | 권한 수준 선택 |
| Shift+Tab (자동 수락) | `/permissions`에서 넓은 단계 선택, 또는 승인 창에서 "계속 허용" | |
| (실행 옵션) | `-a` / `--ask-for-approval`: `untrusted` / `on-request` / `never` | `on-request`: 모델이 필요할 때 질문. `never`: 묻지 않고 실패는 그대로 반환 |
| (실행 옵션) | `-s` / `--sandbox`: `read-only` / `workspace-write` / `danger-full-access` | 파일 쓰기·실행 범위 |
| `--dangerously-skip-permissions` | `--dangerously-bypass-approvals-and-sandbox` | 시험에서 사용 금지 |

시험: 기본 설정(필요할 때 승인 요청) 그대로 사용. 승인이 잦으면 처음 묻는 명령에서 "계속 허용" 선택 또는 `/permissions`로 한 단계만 넓힘. `bypass`·`danger-full-access`는 제한 우회처럼 보이므로 쓰지 않음.

## 작업 모드
| Claude Code | Codex | 비고 |
|---|---|---|
| Plan 모드 (Shift+Tab) | `/plan` | 계획 모드 전환 |
| `/model` | `/model` | 모델 + 추론 강도 선택 |
| `/compact` | `/compact` | 대화 요약으로 컨텍스트 확보 |
| `/review` | `/review` | 현재 변경의 버그 리뷰 |
| `/init` | `/init` | AGENTS.md 생성 |
| CLAUDE.md | AGENTS.md | 수정 후 Codex 재시작해야 반영 |

## 입력·조작
| Claude Code | Codex | 비고 |
|---|---|---|
| Esc (중단) | Esc | |
| 실행 중 메시지 | 실행 중 Enter = 방향 수정(steer), Tab = 다음 메시지로 대기 | |
| `@파일` | `@파일` 또는 `/mention` | |
| `!명령` | `!명령` | 셸 명령 바로 실행 (사전 체험 때 확인) |
| Esc Esc (되감기) | Esc Esc (이전 메시지 수정) | 사전 체험 때 확인 |

## 확장
| Claude Code | Codex | 비고 |
|---|---|---|
| Skills (`/스킬명`) | `/skills` 목록, `$스킬명` 호출 | 커스텀 슬래시 명령 없음 → 스킬로 대체 |
| `/mcp` | `/mcp` (`/mcp verbose` 상세) | 등록은 MCP 탭에서만 |
| `/hooks` | `/hooks` | 시험에선 사용하지 않음 |
| 서브에이전트 `/agents` | `/agent` (에이전트 스레드 전환) | 토큰 많이 씀 |
| 플러그인 | `/plugins` | |
| WebSearch 도구 | `codex --search` 또는 `web_search = "live"` | |
| `--add-dir` | `--add-dir`, `/sandbox-add-read-dir <경로>` | |

## Codex에만 있는 것
| 명령 | 용도 |
|---|---|
| `/diff` | git diff (추적 안 된 파일 포함). 커밋 전 확인 |
| `/goal` | 긴 작업의 목표 설정·확인 |
| `/side` (`/btw`) | 본 대화를 오염시키지 않는 곁가지 질문 (임시 분기) |
| `/fork` | 대화 복제해서 다른 방향 시도 |
| `/ps` / `/stop` | 백그라운드 터미널 목록 / 전부 종료 |
| `/rename`, `/archive` | 대화 이름 변경, 보관 |
| `/raw` | 복사하기 편한 화면 모드 |
| `/personality` | 응답 말투 선택 |
| `codex -c key=value` | 파일 수정 없이 이번 실행만 설정 변경 (예: `-c model_reasoning_effort=high`) |
| `codex exec --output-schema` | 결과를 JSON 스키마로 강제 |

## 시험에서 자주 쓸 것
| 시점 | 명령 |
|---|---|
| 시작 | `/status`, `/model`, `/skills`, `/mcp` |
| 작업 중 | `/plan`, 실행 중 Enter(방향 수정), `/diff`, `/compact`, `/side` |
| 마무리 | `/review` |
