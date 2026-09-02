# 출력 가이드 (HTML + PDF)

SKILL.md STEP 6(완성도 체크 & 출력)에서 참고한다. 출력은 기본적으로 **HTML + PDF** 두 가지.

## 저장 위치 & 파일명

- 현재 작업 디렉토리(또는 사용자가 지정한 폴더)에 저장한다.
- 파일명: `<프로젝트명>_case-study.html` / `<프로젝트명>_case-study.pdf` (프로젝트명은 공백 대신 하이픈, 한글 가능).

## 1. HTML 작성

`references/html-template.html`을 베이스로 복사해 `{{...}}` 자리표시자를 채운다. 제목/섹션 위계·표·KPI 카드·페르소나 카드·플로우 다이어그램·비교 매트릭스·인라인 CSS가 이미 들어간 자체 완결형 단일 파일이다.

- **한글 폰트**: 템플릿은 Noto Sans KR 웹폰트를 우선 쓰고, 오프라인/로컬 폰트 부재 시 시스템 CJK 폰트로 폴백하도록 `font-family` 스택이 짜여 있다. **이 폰트 설정을 지우지 말 것** — 지우면 한글 폰트 없는 환경에서 PDF 글자가 깨진다.
- **이미지**: 사용자가 스크린샷을 주면 `<figure><img>`로 넣되, PDF에 안전하게 포함되도록 가능하면 base64 data URI로 인라인한다.

## 2. PDF 변환

주 대상은 **Windows와 macOS**, 여기에 **Linux/WSL 폴백**을 둔다. Chrome·Edge·Chromium은 같은 엔진이라 헤드리스 자동 변환이 되고, Safari는 CLI 헤드리스 변환을 지원하지 않으므로 수동 저장 폴백으로만 쓴다.

**자동 변환 명령 형식** (Chrome·Edge·Chromium 공통):

```
"<실행파일>" --headless --disable-gpu --no-pdf-header-footer --virtual-time-budget=10000 --print-to-pdf="출력.pdf" "file:///절대경로/문서.html"
```

- A4·배경색 포함해 렌더된다.
- `--virtual-time-budget=10000`은 웹폰트 로딩을 기다리게 하는 **베스트에포트** 옵션이다. 최신 Chrome의 새 헤드리스 모드에서는 무시될 수 있으니 **폰트를 이 옵션에 의존하지 않는다** — 한글이 안 깨지는 실질적 보장은 템플릿의 **CJK 폴백 스택**이다(그래서 지우면 안 된다). 웹폰트가 안 잡혀도 시스템 한글 폰트로 정상 출력된다.
- **`--no-sandbox`**: Windows/macOS에서는 **붙이지 않는다**(불필요하고 보안상 권장되지 않음). Linux 컨테이너·root 실행에서 sandbox 오류로 실패할 때만 붙인다.

### file:// URL 만들기 (변환 실패 1순위)

`--print-to-pdf`는 **절대경로 file:// URL**을 요구한다. 상대경로나 평범한 파일 경로를 주면 빈 PDF가 나오거나 조용히 실패한다.

- macOS/Linux: 절대경로 앞에 `file://`를 붙이면 끝 — `file:///Users/me/work/문서.html`
- **Windows: 역슬래시를 그대로 쓰면 안 된다.** `\`를 `/`로 바꾸고 드라이브 문자를 포함한다.
  - ✗ `file:///C:\Users\me\문서.html`
  - ✓ `file:///C:/Users/me/문서.html`
- 경로에 공백이 있으면 URL 전체를 따옴표로 감싼다. 한글 경로는 대개 그대로 동작하지만, 실패하면 영문 경로(예: 홈 디렉토리 바로 아래)로 옮겨 변환한 뒤 결과 파일만 되돌린다.

### OS별 실행 파일

**Windows** — 아래에서 존재하는 첫 실행 파일로 자동 변환:
1. Chrome: `C:\Program Files\Google\Chrome\Application\chrome.exe` (없으면 `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`)
2. Edge: `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe` (없으면 `C:\Program Files\Microsoft\Edge\Application\msedge.exe`) — Edge는 윈도우에 기본 설치돼 있어 Chrome이 없어도 대부분 성공한다.

**macOS** — Chrome이 있으면 자동 변환, 없으면 Safari 수동 폴백:
1. Chrome: `/Applications/Google Chrome.app/Contents/MacOS/Google Chrome` 로 자동 변환
2. Chrome이 없으면 HTML을 Safari로 열어(`open -a Safari 문서.html`) 사용자에게 **`Cmd+P → PDF로 저장`**(또는 파일 → PDF로 내보내기)을 안내한다. Safari는 맥에 항상 있다.

**Linux / WSL** — PATH에서 아래 순서로 찾아 자동 변환:
1. `google-chrome` → `google-chrome-stable` → `chromium` → `chromium-browser`
   (`command -v google-chrome || command -v chromium` 식으로 존재 확인)
2. 하나도 없으면 HTML만 전달하고 브라우저 수동 저장을 안내한다 (아래 폴백과 동일).
- 컨테이너·root 실행에서 sandbox 오류가 나면 그때만 `--no-sandbox`를 붙인다.
- WSL에서 Windows 쪽 Chrome(`/mnt/c/Program Files/...`)을 호출할 수도 있는데, 이 경우 **file:// URL도 Windows 형식**(`file:///C:/...`)이어야 한다. 리눅스 경로(`/mnt/c/...`)를 그대로 주면 실패한다.

**어느 쪽도 안 되면**: HTML만 전달하고 브라우저에서 `Ctrl/Cmd+P → PDF로 저장`을 안내한다. 이때 인쇄 설정에서 **"배경 그래픽" 옵션을 켜야** KPI 카드·표 헤더 배경이 나온다.

## 3. 전달

두 파일 모두 사용자에게 전달한다 — HTML은 화면 확인·수정용, PDF는 제출·공유용. 사용자가 마크다운이나 다른 형식을 원하면 그에 따른다.
