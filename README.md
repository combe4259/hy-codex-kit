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

## Playwright MCP

- 저장소: https://github.com/microsoft/playwright-mcp (공개, Apache-2.0)
- Codex가 브라우저를 직접 조작(이동·클릭·입력·스냅샷·스크린샷)해서 내가 만든 웹 서비스를 E2E로 확인하는 MCP. 용도는 본인 서버 테스트로만 (외부 사이트 탐색 X).
- 응시 환경은 화면 없는 리눅스라 `--headless` 필수, 메모리 아끼려고 `--isolated`.
- 기준 커밋: `0c4107acbecb75472b23c05c0e42471a0011874f` / npm `@playwright/mcp@0.0.83`

설치 (MCP 탭 JSON):

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@playwright/mcp@0.0.83", "--headless", "--isolated", "--browser", "chromium", "--no-sandbox"]
    }
  }
}
```

브라우저 없다고 나오면: `npx -y playwright@1.64.0-alpha-1790635538000 install chromium` (안 되면 `npx playwright install chromium`)

Codex CLI 직접 설정:

```bash
codex mcp add playwright -- npx -y @playwright/mcp@0.0.83 --headless --isolated --browser chromium --no-sandbox
```

사용: `서버 0.0.0.0:3000 띄우고 playwright로 http://localhost:3000 들어가서 추가 버튼 동작 확인해줘`

## Playwright Skill (OpenAI 공식, webapp-testing 대체)

- 저장소: https://github.com/openai/skills (공개, OpenAI 공식 Codex Skill 카탈로그)
- `skills/.curated/playwright`: 터미널에서 `playwright-cli`로 브라우저 자동화 (이동·폼 입력·스크린샷·UI 흐름 디버깅). MCP 대신 CLI 방식이라 가벼움.
- 기준 커밋: `49f948faa9258a0c61caceaf225e179651397431`

설치 (1순위): Codex에서 `$skill-installer playwright`

설치 (수동):

```bash
git clone https://github.com/openai/skills.git ~/.codex/openai-skills
git -C ~/.codex/openai-skills checkout 49f948faa9258a0c61caceaf225e179651397431
mkdir -p ~/.agents/skills && ln -s ~/.codex/openai-skills/skills/.curated/playwright ~/.agents/skills/playwright
```

## grill-me / handoff (Matt Pocock skills)

- 저장소: https://github.com/mattpocock/skills (공개, MIT, Codex용 `agents/openai.yaml` 포함)
- `grill-me`: 계획·설계를 AI가 집요하게 질문해서 빈틈을 찾아줌. 구현 전 요구사항 정리용. 내부적으로 `grilling` 스킬을 호출하므로 둘 다 설치.
- `handoff`: 현재 대화를 다음 세션/에이전트가 이어받을 수 있는 인수인계 문서로 압축 (컨텍스트 꽉 찼을 때).
- 기준 커밋: `a496f5513d4a4cf889bc48e189e579f4b0bdf6aa`

설치:

```bash
git clone https://github.com/mattpocock/skills.git ~/.codex/mattpocock-skills
git -C ~/.codex/mattpocock-skills checkout a496f5513d4a4cf889bc48e189e579f4b0bdf6aa
mkdir -p ~/.agents/skills
for s in grill-me grilling handoff; do ln -s ~/.codex/mattpocock-skills/skills/productivity/$s ~/.agents/skills/$s; done
```

사용: `$grill-me` / `$handoff 다음 세션은 테스트 작성용`
