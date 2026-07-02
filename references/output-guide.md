# 출력 가이드 (HTML + PDF)

SKILL.md 6단계(완성도 체크 & 출력)에서 참고한다. 출력은 기본적으로 **HTML + PDF** 두 가지.

## 저장 위치 & 파일명

- 현재 작업 디렉토리(또는 사용자가 지정한 폴더)에 저장한다.
- 파일명: `<프로젝트명>_case-study.html` / `<프로젝트명>_case-study.pdf` (프로젝트명은 공백 대신 하이픈, 한글 가능).

## 1. HTML 작성

`references/html-template.html`을 베이스로 복사해 `{{...}}` 자리표시자를 채운다. 제목/섹션 위계·표·KPI 카드·페르소나 카드·플로우 다이어그램·비교 매트릭스·인라인 CSS가 이미 들어간 자체 완결형 단일 파일이다.

- **한글 폰트**: 템플릿은 Noto Sans KR 웹폰트를 우선 쓰고, 오프라인/로컬 폰트 부재 시 시스템 CJK 폰트로 폴백하도록 `font-family` 스택이 짜여 있다. **이 폰트 설정을 지우지 말 것** — 지우면 한글 폰트 없는 환경에서 PDF 글자가 깨진다.
- **이미지**: 사용자가 스크린샷을 주면 `<figure><img>`로 넣되, PDF에 안전하게 포함되도록 가능하면 base64 data URI로 인라인한다.

## 2. PDF 변환

대상 OS는 **Windows와 macOS**다. Chrome·Edge는 크롬 엔진이라 헤드리스 자동 변환이 되고, Safari는 CLI 헤드리스 변환을 지원하지 않으므로 수동 저장 폴백으로만 쓴다.

**자동 변환 명령 형식** (Chrome·Edge 공통):

```
"<실행파일>" --headless --disable-gpu --no-pdf-header-footer --virtual-time-budget=10000 --print-to-pdf="출력.pdf" "file:///절대경로/문서.html"
```

- A4·배경색 포함해 렌더된다.
- `--virtual-time-budget=10000`은 웹폰트(Noto Sans KR) 로딩을 기다리게 하는 옵션 — 빼면 폴백 폰트로 찍힐 수 있다.
- **`--no-sandbox`는 붙이지 않는다** — 일반 Windows/macOS 환경에선 불필요하고 보안상 권장되지 않는다.

**Windows** — 아래에서 존재하는 첫 실행 파일로 자동 변환:
1. Chrome: `C:\Program Files\Google\Chrome\Application\chrome.exe` (없으면 `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`)
2. Edge: `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe` (없으면 `C:\Program Files\Microsoft\Edge\Application\msedge.exe`) — Edge는 윈도우에 기본 설치돼 있어 Chrome이 없어도 대부분 성공한다.

**macOS** — Chrome이 있으면 자동 변환, 없으면 Safari 수동 폴백:
1. Chrome: `/Applications/Google Chrome.app/Contents/MacOS/Google Chrome` 로 자동 변환
2. Chrome이 없으면 HTML을 Safari로 열어(`open -a Safari 문서.html`) 사용자에게 **`Cmd+P → PDF로 저장`**(또는 파일 → PDF로 내보내기)을 안내한다. Safari는 맥에 항상 있다.

**둘 다 안 되면**: HTML만 전달하고 브라우저에서 `Ctrl/Cmd+P → PDF로 저장`을 안내한다.

## 3. 전달

두 파일 모두 사용자에게 전달한다 — HTML은 화면 확인·수정용, PDF는 제출·공유용. 사용자가 마크다운이나 다른 형식을 원하면 그에 따른다.
