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
