# 전역 에이전트 지침 (Codex)

## AI PM 케이스 스터디 작성 스킬

사용자가 **"케이스 스터디", "PM 포트폴리오", "프로젝트 회고", "수익화 프로젝트 정리", "AI PM 프로젝트 문서화", "프로젝트를 문서로 정리해줘"** 같은 요청을 하면, 아래 스킬 파일들의 방법론을 그대로 따른다 (Claude용으로 작성됐지만 내용은 도구 무관하게 재사용 가능).

**스킬 위치**: `~/.claude/skills/ai-pm-case-study/` — 개인 폴더에 없으면 현재 프로젝트의 `.claude/skills/ai-pm-case-study/`에서 찾는다 (프로젝트 로컬 설치인 경우).

**읽을 파일 (순서대로)**
1. `~/.claude/skills/ai-pm-case-study/SKILL.md` — 전체 워크플로우(아이디어 접수 → 갭 분석 → 질문 → 입력 반영 → 문서 작성 → 완성도 체크·출력)
2. `~/.claude/skills/ai-pm-case-study/references/stage-templates.md` — 6단계 질문 목록 & 문서 섹션 템플릿
3. `~/.claude/skills/ai-pm-case-study/references/quality-principles.md` — 실무 품질 원칙(의사결정·원페이저·정량 데이터·본인 기여·용도별 강조)
4. `~/.claude/skills/ai-pm-case-study/references/checklist.md` — 최종 산출물 점검
5. `~/.claude/skills/ai-pm-case-study/references/html-template.html` — HTML 출력 베이스 템플릿
6. `~/.claude/skills/ai-pm-case-study/references/example-case-study.md` — 톤·분량 예시
7. `~/.claude/skills/ai-pm-case-study/references/output-guide.md` — HTML/PDF 출력 절차(OS별 변환·파일명 규칙)

**핵심 규칙 (요약)**
- 한 번에 다 묻고 다 쓰지 않는다. 먼저 갭 분석 → 단계별로 나눠 질문 → 답변 반영 후 작성.
- 사용자가 안 준 숫자·성과·고객 반응을 지어내지 않는다.
- 출력은 HTML + PDF. PDF는 Chrome/Edge 헤드리스(`--headless --print-to-pdf`)로 변환, 안 되면 브라우저 `Ctrl/Cmd+P → PDF로 저장` 안내. 자세한 OS별 실행 파일 경로·폴백 절차는 위 7번 `output-guide.md`에 있다 — SKILL.md에는 한 줄 요약만 있으므로 반드시 output-guide.md를 열 것.
