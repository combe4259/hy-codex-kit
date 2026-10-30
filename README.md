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
