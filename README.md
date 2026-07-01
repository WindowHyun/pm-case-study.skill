# ai-pm-case-study

AI PM(프로덕트 매니저) / 노코드+AI API 기반 수익화 프로젝트를 **케이스 스터디 · PM 포트폴리오 · 프로젝트 회고** 문서로 만들어 주는 Claude Code 스킬.

아이디어 한 줄만 던져도 **아이디어 접수 → 갭 분석 → 단계별 질문 → 입력 반영 → 문서 작성(HTML+PDF)** 순서로, 6단계 방법론(기획 검증 → UX 설계 → QA 검증 → 마케팅 런칭 → 성장 증명 → 데모데이 크리틱)에 맞춰 구조화된 문서를 만든다.

## 특징

- **한 번에 다 묻지 않음** — 먼저 빠진 부분을 분석하고 단계별로 나눠 질문
- **지어내지 않음** — 사용자가 안 준 수치·성과는 `[가정]` / `[추가 입력 필요]`로 표시
- **실무 품질 기준** — 원페이저 요약, 의사결정 서술, 경쟁 비교표, 구체적 페르소나, 정량 지표표 등 "합격하는" 케이스 스터디 요소 반영
- **HTML + PDF 출력** — Noto Sans KR 웹폰트 + CJK 폴백 스택 내장, 헤드리스 Chrome/Edge로 PDF 변환

## 구조

```
SKILL.md                          워크플로우 본체 (Claude가 읽는 진입점)
references/
├── stage-templates.md            6단계 질문 목록 & 문서 섹션 템플릿
├── quality-principles.md         실무 품질 원칙 + 깊이 기준
├── checklist.md                  최종 산출물 점검 리스트
├── html-template.html            시각 컴포넌트 포함 HTML 출력 템플릿
└── example-case-study.md         실무급 예시 (톤·깊이 기준점)
integrations/
├── codex-AGENTS.md               Codex 연동용 포인터 예시
└── gemini-GEMINI.md              Gemini 연동용 포인터 예시
```

## 설치 (Claude Code)

이 저장소를 개인 스킬 폴더로 복사한다:

```bash
git clone <this-repo> /tmp/pm-case-study.skill
mkdir -p ~/.claude/skills/ai-pm-case-study
cp -r /tmp/pm-case-study.skill/SKILL.md /tmp/pm-case-study.skill/references ~/.claude/skills/ai-pm-case-study/
```

특정 프로젝트에만 쓰려면 `~/.claude/skills/` 대신 해당 프로젝트의 `.claude/skills/`에 둔다.

## 사용

Claude Code에서 아래 같은 표현이면 자동 발동한다:

> "이 프로젝트 케이스 스터디로 정리해줘" · "PM 포트폴리오 만들어줘" · "프로젝트 회고 문서로 써줘"

## 다른 도구(Codex / Gemini)에서 쓰기

이 스킬 포맷은 Claude 전용이지만, 방법론 파일 자체는 도구 무관하게 재사용 가능하다. `integrations/`의 포인터 파일을 각 도구 규격 위치에 두면 같은 방법론을 공유한다:

- Codex: `integrations/codex-AGENTS.md` → `~/.codex/AGENTS.md` (또는 프로젝트 루트 `AGENTS.md`)
- Gemini: `integrations/gemini-GEMINI.md` → `~/.gemini/GEMINI.md`

두 파일은 `~/.claude/skills/ai-pm-case-study/`의 절대경로를 참조하므로, 스킬이 그 위치에 설치돼 있어야 한다.

## PDF 출력 참고

- 대상 OS: **Windows / macOS**
- Windows: Chrome → 없으면 Edge(기본 설치)로 자동 변환
- macOS: Chrome으로 자동 변환, 없으면 Safari로 열어 `Cmd+P → PDF로 저장`
- 어느 쪽도 안 되면 HTML만 전달 + 브라우저 `Ctrl/Cmd+P → PDF로 저장` 안내
