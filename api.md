Listed directory vibecoding
Ran command: `find Project_* -maxdepth 2`
Ran command: `grep -rn -E "fetch\(|http|api\.|https://" Project_* --exclude="*.min.js" --exclude="*.map"`
Viewed app.js:1-684
Viewed app.js:1-617
Viewed index.html:1-100
Viewed index.html:140-210
Ran command: `head -n 30 Project_03/js/*.js`
Viewed app.js:1-150
Viewed app.js:151-300
Viewed app.js:301-450
Viewed app.js:1-200
Viewed app.js:251-450
Viewed app.js:451-620
Viewed app.js:621-732
Viewed app.js:350-430
Viewed index.html:1-60
Viewed app.js:1-40
Viewed api.js:1-200
Viewed SPECIFICATION.md:1-60

`apps-core.com`을 제외한 본 폴더 내 **각 프로젝트(Project_01 ~ Project_07)**에서 사용된 **외부 REST API**, **브라우저 Web API**, 그리고 **프론트엔드 라이브러리 API**를 정리한 내용입니다.

---

### 1. [Project_01](file:///Users/creatorjoseph/Desktop/vibecoding/Project_01) — 위키백과 인터랙티브 웹 클론
* **프로젝트 개요**: 한국어 위키백과(Vector 2022 테마) 인터랙티브 문서 뷰어 및 편집기
* **외부 REST API**: **없음** (정적 내부 데이터베이스 객체 `ARTICLES_DATABASE`, `HOVER_PREVIEW_DATA` 기반 자체 구동)
* **브라우저 Web API**:
  * `DOM & Event API`: 탭 전환, 실시간 검색어 자동완성 하이라이트, 모달 제어
  * `Window.matchMedia API`: 시스템 다크/라이트 모드 자동 감지
  * `Window.scrollTo & Element.getBoundingClientRect`: 목차(TOC) 클릭 시 부드러운 스크롤 이동 및 스크롤스파이(Scrollspy) 위치 계산
  * `Selection API` (`selectionStart`, `selectionEnd`): 위키 마크업 편집기(굵게, 기울임, 링크 등 태그 삽입)

---

### 2. [Project_02](file:///Users/creatorjoseph/Desktop/vibecoding/Project_02) — 구글 스타일 시작 홈페이지
* **프로젝트 개요**: 포항 실시간/시간대별 날씨 및 강수 레이더와 명언이 포함된 Google 스타일 홈
* **외부 REST API & 외부 서비스**:
  * **Open-Meteo Weather API**:
    * 엔드포인트: `https://api.open-meteo.com/v1/forecast`
    * 사용 목적: 포항 지역(위도 36.019, 경도 129.3435)의 실시간 온도, 체감온도, 습도, 풍속 및 24시간 시간대별 날씨/강수확률 수신
  * **Windy Embed Map/Radar**:
    * 엔드포인트: `https://embed.windy.com/embed2.html`
    * 사용 목적: 한반도 및 포항 지역 실시간 강수량 레이더 및 위성 영상 iframe 임베드
  * **Google Search & Lens URL API**:
    * `https://www.google.com/search?q=...` (검색 및 I'm Feeling Lucky 연동)
    * `https://images.google.com/` (구글 렌즈 연동)
* **브라우저 Web API**:
  * `Web Speech API` (`SpeechRecognition` / `webkitSpeechRecognition`): 음성 검색 기능
  * `Clipboard API` (`navigator.clipboard.writeText`): 오늘의 명언 클립보드 복사
  * `Web Storage API` (`localStorage`): 다크/라이트 테마 설정 저장
  * `Window.matchMedia API`: 시스템 다크모드 감지

---

### 3. [Project_03](file:///Users/creatorjoseph/Desktop/vibecoding/Project_03) — 스마트 공학용 계산기 & 유틸리티
* **프로젝트 개요**: 공학용 수식 계산기 및 생활 도구(더치페이, 할인율 계산기, 단위 변환기)
* **외부 REST API**: **없음** (순수 클라이언트 사이드 자체 연산 엔진)
* **브라우저 Web API**:
  * **`Web Audio API` (`AudioContext` / `webkitAudioContext`, `OscillatorNode`, `GainNode`)**:
    * 별도 오디오 파일 없이 주파수 합성을 통해 키패드 입력 시 햅틱 효과음 실시간 생성
  * `Clipboard API` (`navigator.clipboard.writeText`): 계산 결과 및 정산 내역 복사
  * `Keyboard Event API` (`keydown`): 물리 키보드 입력 매핑 및 비주얼 키 프레스 피드백
  * `Web Storage API` (`localStorage`): 계산 히스토리 기록 영구 저장 및 음소거/테마 상태 저장

---

### 4. [Project_04](file:///Users/creatorjoseph/Desktop/vibecoding/Project_04) — URL2QR (스마트 QR코드 생성기)
* **프로젝트 개요**: 입력한 URL을 고해상도 QR코드로 생성하고 이미지(PNG/JPG/SVG)로 다운로드하는 도구
* **외부 REST API**: **없음** (클라이언트 측에서 독립적으로 QR 생성 및 렌더링)
* **외부 라이브러리**:
  * `qrcode.min.js`: 클라이언트 측 QR 코드 매트릭스 생성
* **브라우저 Web API**:
  * **`HTML5 Canvas API` (`canvas.toDataURL`, `CanvasRenderingContext2D`)**: QR 코드를 고해상도 PNG/JPG 래스터 이미지로 변환
  * **`Blob & URL API` (`new Blob`, `URL.createObjectURL`, `URL.revokeObjectURL`)**: 생성된 SVG/이미지 파일 가상 링크 다운로드 트리거
  * `Clipboard API` (`navigator.clipboard.readText`, `navigator.clipboard.writeText`): 클립보드 URL 붙여넣기 및 복사
  * `URL API` (`new URL(...)`): 사용자 입력 URL 유효성 검증 및 도메인 추출
  * `Web Storage API` (`localStorage`): 다국어(KO/EN/ZH/JA) 및 테마 상태 저장

---

### 5. [Project_05](file:///Users/creatorjoseph/Desktop/vibecoding/Project_05) — Re:Connect 동창회 모바일 초대장
* **프로젝트 개요**: 감성 벚꽃 인터랙션, 지도, BGM 신시사이저, 일정 등록을 갖춘 동창회 초대장
* **외부 지도 타일 및 외부 서비스**:
  * **OpenStreetMap Tile API**:
    * 엔드포인트: `https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png`
    * 사용 목적: 창경궁 오프라인 모임 장소 300x300 타일 맵 렌더링
  * **Google Calendar Template URL**:
    * 엔드포인트: `https://calendar.google.com/calendar/render?action=TEMPLATE&...`
    * 사용 목적: 구글 캘린더에 동창회 일정(일시, 장소, 링크) 원클릭 등록
  * **외부 지도 딥링크**: 네이버 지도(`https://naver.me/FFGMk3uS`), 카카오맵, 티맵 연동
* **외부 라이브러리**:
  * `Leaflet.js`: 인터랙티브 지도 생성 및 마커/팝업 렌더링
* **브라우저 Web API**:
  * **`Web Audio API` (`AudioContext`, `OscillatorNode`, `GainNode`)**: 피아노 아르페지오 멜로디 BGM 합성
  * **`HTML5 Canvas API` (`2D Context`) & `requestAnimationFrame`**: 벚꽃 꽃잎 파티클 물리 낙하 애니메이션
  * **`Web Share API` (`navigator.share`)**: 스마트폰 네이티브 공유 다이얼로그 호출
  * `Intersection Observer API`: 스크롤 시 각 섹션 부드러운 리빌(Reveal) 애니메이션
  * `Touch / Pointer Events API`: 모바일 사진 갤러리 터치 스와이프 제스처
  * `Blob & URL API`: iCalendar(`.ics`) 스마트폰용 캘린더 파일 즉석 생성 및 다운로드
  * `Web Storage API` (`localStorage`): 참석 여부(RSVP) 및 방명록 댓글 로컬 저장

---

### 6. [Project_06](file:///Users/creatorjoseph/Desktop/vibecoding/Project_06) — QR & URL Studio (단축 URL 및 QR 생성 포털)
* **프로젝트 개요**: URL2QR과 실시간 단축 URL 서비스(URLShort)를 통합 제공하는 허브
* **외부 REST API (단축 URL)**:
  * **is.gd API** (Engine 1):
    * 엔드포인트: `https://is.gd/create.php?format=json&url={targetUrl}`
    * 사용 목적: 중간 페이지 없는 즉시 리다이렉트(301) 단축 링크 생성
  * **spoo.me API** (Engine 2):
    * 엔드포인트: `https://spoo.me/` (POST, CORS 지원)
    * 사용 목적: is.gd 실패 시 폴백 및 안정적인 단축 링크 생성
* **외부 라이브러리**:
  * `qrcode.min.js`: 통합 QR 코드 생성 엔진
* **브라우저 Web API**:
  * **`Fetch API` & `AbortController`**: 6초 타임아웃 및 듀얼 엔진 비동기 HTTP 요청 처리
  * `HTML5 Canvas API` & `Blob/URL API`: QR 코드 PNG/JPG/SVG 내보내기
  * `Clipboard API` (`navigator.clipboard.readText`, `navigator.clipboard.writeText`)
  * `Web Storage API` (`localStorage`): 최근 생성된 단축 URL 히스토리 및 클릭 통계 저장

---

### 7. [Project_07](file:///Users/creatorjoseph/Desktop/vibecoding/Project_07) — MetalPulse (국제 귀금속/원자재 실시간 시세 대시보드)
* **프로젝트 개요**: 금, 은, 구리, 플래티넘, 팔라듐의 실시간 시세 및 기간별 시세 차트 대시보드
* **외부 REST API**:
  * **MetalpriceAPI Free Tier**:
    * 엔드포인트: `https://api.metalpriceapi.com/v1/latest?api_key={key}&base=USD&currencies=XAU,XAG,XCU,XPT,XPD,KRW`
    * 사용 목적: 귀금속 및 주요 산업 금속의 최신 국제 시세 및 USD/KRW 환율 실시간 수신 (15분 스마트 캐싱 적용)
* **외부 라이브러리**:
  * `Chart.js 4.x`: 기간별(1W, 1M, 3M, 6M, 1Y) 시세 인터랙티브 라인 차트 렌더링
  * `Lucide Icons`: 금융/원자재 UI 아이콘 렌더링
* **브라우저 Web API**:
  * `Fetch API`: 시세 API 통신
  * `HTML5 Canvas API` (`createLinearGradient`): 차트 영역 배경 그라데이션 시각화
  * `Web Storage API` (`localStorage`): 사용자 등록 API 키, 통화(USD/KRW), 무게 단위(oz/g), 15분 시세 캐시 및 과거 시세 누적 저장

---

### 요약 비교표

| 프로젝트 | 프로젝트 성격 | 주요 외부 REST API | 주요 브라우저 Web API / 라이브러리 |
| :--- | :--- | :--- | :--- |
| **Project_01** | 위키백과 인터랙티브 뷰어 | 없음 (내부 정적 DB) | Selection API, matchMedia, DOM |
| **Project_02** | 시작 페이지 (포항 날씨/레이더) | **Open-Meteo**, **Windy Embed** | Web Speech API, Clipboard, Storage |
| **Project_03** | 스마트 공학용 계산기 | 없음 (클라이언트 연산) | **Web Audio API (효과음 합성)**, Storage |
| **Project_04** | 스마트 QR코드 생성기 | 없음 | **Canvas API**, Blob/URL, `qrcode.js` |
| **Project_05** | 동창회 모바일 초대장 | **OpenStreetMap**, **Google Calendar** | **Web Audio API**, **Web Share**, Canvas, `Leaflet` |
| **Project_06** | QR & URL 단축 통합 포털 | **is.gd**, **spoo.me** | Fetch, AbortController, Canvas, Storage |
| **Project_07** | 귀금속/원자재 시세 대시보드 | **MetalpriceAPI** | Fetch, Canvas, Storage, `Chart.js` |
