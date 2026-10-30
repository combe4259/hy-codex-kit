# hy-codex-kit

Codex에서 쓸 공개 Skill·Plugin·MCP 인덱스. 내용물은 각 원본 저장소에서 직접 받는다.

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

Codex CLI 직접 설정 (`~/.codex/config.toml`):

```bash
codex mcp add context7 -- npx -y @upstash/context7-mcp@4.4.4
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
