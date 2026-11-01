# 프로젝트 규칙

> 이 파일은 Antigravity·Cline 같은 AI 도구가 이 프로젝트에서 대화할 때마다 읽는 약속입니다. 수강생은 직접 고치지 않고, 각 회차 첫 프롬프트가 그 회차 약속을 이 파일 끝에 덧붙입니다.
> 이 브랜치는 4회차까지 끝낸 상태입니다. 코드가 아래 약속과 다르면 코드를 따르세요.

## 일하는 방식
- 병렬·서브 에이전트를 사용하지 말고 현재 에이전트가 순서대로 직접 수행하세요.
- 사용자는 코딩을 처음 배우는 수강생입니다. 설명은 짧고 쉬운 한국어로 하고, 전문 용어는 풀어서 말하세요.
- 한 번에 요청한 일만 하고, 요청하지 않은 파일은 고치지 마세요. 더 나은 방법이나 기능이 떠올라도 더하지 마세요.
- 프롬프트에 따옴표로 적힌 화면 글자는 한 글자도 바꾸지 말고 그대로 쓰세요. 프롬프트 안의 "---- 아래 글 그대로 ----" 줄은 표시일 뿐이니 파일에 넣지 말고 그 아래 글만 그대로 쓰세요.
- 이 파일에 적힌 이름(파일·폴더·주소·키·함수·화면 요소)은 그대로 쓰고, 적히지 않은 이름은 스스로 정하세요. 한 번 만든 이름은 바꾸지 마세요. 프롬프트가 "생산 카드"처럼 화면 이름으로 가리키면 코드에서 찾아 씁니다.
- 이미 있는 코드의 방식을 새 기능에도 그대로 따르세요. 같은 일을 하는 함수가 이미 있으면 새로 만들지 말고 그것을 쓰세요.
- 이미 있는 CSS 규칙을 바꿀 때는 그 규칙을 고치고, 같은 규칙을 파일 끝에 다시 더하지 마세요.
- 일을 마치면 사용자가 화면이나 터미널에서 무엇을 보면 되는지 한 줄로 알려 주세요.
- .env, .clasp.json 파일은 열지 말고 내용을 출력하지 마세요. Google 웹 앱 주소, 배포 ID, Discord 웹훅 주소는 채팅·코드·문서에 옮겨 적지 마세요(웹 앱 주소는 5회차 배포 명령만 public/config.js에 씁니다).
- 터미널 명령은 Windows PowerShell 기준으로 npm.cmd, npx.cmd, curl.exe를 씁니다.
- 서버 켜기·끄기(npm.cmd start), backend 폴더의 설치·빌드, npm.cmd run gas:로 시작하는 명령(Google 로그인·코드 올리기·배포)은 사용자가 직접 합니다. 실행하지 마세요.
- 브라우저를 열어 확인하지 마세요. 화면 확인, Google 로그인과 권한 승인, Apps Script 편집기 작업은 사용자가 직접 합니다.
- 요청에 없는 패키지는 더하지 말고 버전을 바꾸지 마세요. npm audit fix도 실행하지 마세요. 화면은 외부 라이브러리·CDN·웹 글꼴 없이 만듭니다.

## 앱의 기본 약속
- 텀블공장(텀블러 공장)의 생산·출고를 보는 운영 대시보드입니다. 화면 글은 모두 한국어입니다.
- 폴더 배치: 화면 파일은 public 폴더, 화면 서버는 scripts/serve.mjs, 내 서버(NestJS)는 4회차부터 backend 폴더, Google Apps Script 코드는 5회차부터 gas 폴더에 둡니다.
- 화면은 public/index.html 한 페이지와 public/styles.css 한 파일입니다(2회차부터 JavaScript는 public/app.js 한 파일). 없는 주소용 화면은 public/404.html입니다.
- 강사가 준 파일은 이름과 위치를 바꾸지 않습니다: 로고 public/assets/tumble-factory-logo.png, 현장 사진 public/assets/approved/factory.png·warehouse.png, 맨 위 API_CONTRACT.md.
- package.json: name "tumble-dashboard", version "1.0.0", private true, scripts는 "start": "node scripts/serve.mjs" 하나입니다. 설치하는 패키지는 없고 npm init 같은 자동 생성 명령은 쓰지 않습니다.
- 화면 서버는 Node.js 기본 모듈(node:http, node:fs, node:path)만 씁니다. 127.0.0.1에서만 열고, 포트는 환경 변수 PORT, 없으면 4173입니다. 켜지면 "http://127.0.0.1:<실제 포트>" 한 줄을 출력합니다.
- public 폴더는 명령을 실행한 폴더가 아니라 serve.mjs가 있는 폴더 기준(../public)으로 찾습니다. serve.mjs가 있는 폴더는 기본 모듈 셋만 쓰도록 import.meta.dirname으로 구합니다. 주소의 ? 뒤는 무시하고 경로를 decodeURIComponent로 푼 뒤 판단합니다. / 는 index.html입니다.
- Content-Type은 html text/html, css text/css, js text/javascript(셋 다 뒤에 ; charset=utf-8), png image/png, 그 밖은 text/plain; charset=utf-8입니다. 모든 응답에 Cache-Control: no-store를 붙입니다.
- /api/로 시작하는 경로는 파일을 찾지 않고 상태 404, application/json; charset=utf-8로 {"error":"이 서버는 화면 파일만 보냅니다. 화면은 public/config.js의 apiBaseUrl로 API 서버를 직접 부릅니다."}를 보냅니다.
- 없는 파일, 풀 수 없는 경로, public 밖을 가리키는 경로는 상태 404로 404.html 내용(text/html; charset=utf-8)을 보냅니다. 404.html은 CSS를 /styles.css로 연결하고 오늘 운영 링크는 /#/today입니다.
- 화면 주소는 주소 끝 # 부분으로 나눕니다: #/today 오늘 운영(기본), #/records/factory 오늘 생산 기록, #/records/warehouse 오늘 출고 기록, #/queries/factory 생산 데이터 조회 기록, #/queries/warehouse 출고 데이터 조회 기록. 1회차에는 링크만 두고 화면 나누기는 2회차에 합니다.
- index.html은 lang="ko", charset utf-8, viewport width=device-width, initial-scale=1, 빈 아이콘(href="data:,")입니다. 화면 틀(머리 부분, 카드, 제목, 칸)은 index.html에 두고, 2회차부터 JavaScript는 그 요소의 글자·숨김·class·값만 바꿉니다.
- 오늘 운영 영역 순서: 먼저 확인할 일, 생산·출고 카드(공장·창고), 운영 상태(공장·창고·알림 카드 세 장), 기록 처리 상태(공장·창고), 데이터 조회 기록(공장·창고).
- 운영 상태 카드 세 장에서 class meta는 맨 아래 작은 시각 글 하나에만 붙입니다. 카드의 설명 문장에는 붙이지 않습니다.
- 화면 요소 이름(이 이름 그대로 씁니다. 창고 쪽은 factory를 warehouse로 바꾼 같은 이름): 본문 건너뛰기 링크 class skip-link(href "#main"), 로고 홈 링크 class brand, 머리 부분 오른쪽 묶음 class header-actions, 기준 시각 선택 id view-time, 조회 상태 id freshness, 새로고침 버튼 id refresh-btn, 다음 조회 글자 id countdown-text, 알림 버튼 id header-alerts-link와 그 글자 id header-alerts-text, 알림 목록 id notification-dropdown.
- 화면 요소 이름(계속): 본문 묶음 main id main(tabindex="-1", 건너뛰기 링크가 여기로 초점을 옮김), 그 안의 본문 section id page-content, 제목 id page-title, 오늘 운영 영역 id today-view, 먼저 확인할 일 상자 class hero와 제목 id hero-title, 생산·출고 카드 묶음 class "grid kpis", 수량 줄 id factory-quantity, 달성률 글 id factory-progress-text, 진행 막대 progress 요소(max 100) id factory-progress, 목표 초과 글 id factory-exceeded, 사진 figure id factory-photo(사진 대신 글자를 넣는 칸은 class photo-placeholder), 그래프 자리 id factory-graph(안에 class loading-graph 조회 중 글자, class graph-scroll 그래프 칸), 운영 상태 카드 id factory-status·alerts-status, 기록 처리 상태 카드 id factory-flow, 조회 기록 카드 글 id factory-query와 작은 글 id factory-query-meta. 카드는 class card, 작은 회색 글은 class meta, 안내 상자는 class notice, 카드 아래 링크는 class card-link, 배지는 class badge입니다. 수량 줄(id factory-quantity) 안은 실적 글자 요소와 목표 글자 요소를 공백이나 줄바꿈 없이 붙여 쓰고, 간격은 CSS로 줍니다.
- 상태 색은 class 네 개로 나타냅니다: good(초록), warning(노랑), danger(빨강), neutral(회색). 배지, 알림 버튼, 조회 상태 점, 먼저 확인할 일 상자가 같은 이름을 씁니다. 노란 안내 상자는 class "notice warning"입니다.
- 화면 폭: PC는 생산·출고 카드 두 열, 폭 700px 이하는 한 열입니다(휴대폰 확인은 375px). 701~1199px에서는 머리 부분 오른쪽 묶음이 로고 아래 줄로 내려갑니다. 375px에서 페이지 가로 스크롤이 생기지 않습니다.
- 버튼, 카드 아래 링크, 입력 칸은 높이 44px 이상, 키보드 초점은 초록 테두리로 보이게 합니다. 숨길 요소는 hidden 속성으로 숨기고 CSS에 [hidden] { display: none !important; }를 둡니다.
- 움직임 줄이기 설정(prefers-reduced-motion: reduce)에서는 버튼 눌림, 도는 아이콘 같은 움직임을 끕니다.

## 2회차 약속
- 예시 자료는 public/sample-data.js입니다. API_CONTRACT.md 5절 예시 응답을 글자 그대로 window.SAMPLE_SNAPSHOT = { … }; 로, 6절 예시 기록을 window.SAMPLE_RECORDS = { production: […], shipment: […] }; 로 둡니다. 이 파일은 3회차에 지웁니다.
- 화면 JavaScript는 public/app.js 한 파일입니다(모듈·프레임워크 없이). index.html head에서 sample-data.js, app.js 순서로 defer를 붙여 부릅니다.
- 자료의 필드 이름과 값은 API_CONTRACT.md 2·3절을 따릅니다. 화면의 "지금"은 자료의 viewTime이고 브라우저 시계는 쓰지 않습니다.
- 화면 그리기는 자료 하나로 화면 전체를 채우는 함수 하나(render)가 맡습니다. 마지막 자료를 기억해 두고 인자 없이 부르면 그 자료로 다시 그립니다. 공장과 창고는 같은 함수를 함께 씁니다. 버튼이나 주소 바뀜 처리에서는 직접 그리지 말고 render를 부릅니다.
- 안을 통째로 새로 그려도 되는 곳은 기록 처리 상태 카드 안, 그래프 칸 안, 기록 표 자리, 조회 기록 화면, 알림 목록 안뿐입니다. 나머지는 index.html의 요소를 찾아 바꿉니다.
- 시각 글자는 한국 시간 "2026. 10. 26. 09:00:00" 꼴입니다(Intl.DateTimeFormat("ko-KR"), timeZone "Asia/Seoul", year numeric, 나머지 2-digit, hourCycle "h23". hour12는 쓰지 않음). 그래프 아래는 "09시"입니다. 시각이 아니면 "기록 없음"입니다.
- 수량은 0 이상의 안전한 정수(Number.isSafeInteger)만 수로 보고 toLocaleString("ko-KR")로 씁니다. 아니면 "확인 불가"이고 0으로 바꾸지 않습니다. 한 현장 값이 틀려도 다른 현장은 그대로 보입니다.
- 달성률은 실적 ÷ 목표 × 100을 소수 첫째 자리까지 씁니다. 실적·목표가 수가 아니거나 목표가 0이면 달성률 대신 안내를 쓰고 진행 막대와 "목표 초과"를 숨깁니다. 막대 값은 반올림하지 않고 100을 넘지 않습니다.
- 상태 값과 배지(글자, 색): normal 정상 good, warning 확인 필요 warning, error 오류 danger, sent 전송 성공 good, failed 실패 danger, unknown 확인 불가 warning, waiting 대기 warning입니다. 목록에 없는 값은 "확인 필요" warning입니다.
- 늦은 기록: 마지막 발생 시각(lastEventAt)이 없거나 "지금"보다 늦으면 missing, 30분 넘게 지났으면 stale, 그 밖은 fresh입니다. 공장·창고 배지는 missing이면 waiting, stale이면 warning, fresh면 자료의 status입니다. "몇 분 전"은 내림한 분입니다.
- 현장 status가 error면 그 운영 상태 카드에, 알림 status가 failed면 알림 카드에 danger class를 더합니다.
- 서버 처리 시각이 없으면 "기록 대기", 단 processingState가 paused면 "처리 중단"입니다. 기록 상태는 completed 완료, receipt-wait 접수 대기, 그 밖 처리 대기입니다.
- 기록 처리 상태 카드(id factory-flow) 안의 시각 세 줄은 dl 하나에 dt(기록 발생, 서버 접수, 서버 처리)와 dd(시각 글자) 세 쌍으로 둡니다.
- 그래프는 라이브러리 없이 SVG로 그립니다. 한 시간에 막대 하나, 첫 시각부터 시간 차만큼 오른쪽으로 옮기고, 기록이 없는 시간은 빈자리로 둡니다. quantity 0은 높이 0 막대와 수량 "0"입니다. 다시 그릴 때는 SVG만 바꾸고 가로 스크롤 위치를 지킵니다.
- 막대는 막대마다 rect 하나이고 그래프 SVG에 다른 rect를 두지 않습니다. 막대 칸 간격은 90px이고, 그래프 칸에서 좌우 방향키는 한 번에 90px 움직입니다.
- 알림 목록과 먼저 확인할 일은 자료의 incidents로 채웁니다. id "PREDICTION-JOB"은 빼고, 같은 id는 한 번만, level "error"를 앞에 둡니다. 알림 버튼 색은 error 항목이 있으면 danger, 항목이 있으면 warning, 없으면 good입니다. 목록 항목은 class notification-item입니다.
- 먼저 확인할 일의 안내 고르기: scope factory 또는 id FACTORY-FEED는 생산 기록 안내, scope warehouse 또는 id WAREHOUSE-FEED는 출고 기록 안내, id ALERT-DELIVERY는 알림 전송 기록 안내, 그 밖은 안내 없음입니다.
- 화면 나누기: 기본 약속의 다섯 주소 가운데 맞는 영역 하나만 보입니다(오늘 운영 id today-view, 기록 화면 id records-view, 조회 기록 화면 id queries-view). 그 밖 주소는 오늘 운영과 안내 id route-notice를 함께 보입니다. 오늘 운영이 아니면 돌아가기 링크 id back-link를 보입니다. 주소가 바뀌면(hashchange) 다시 그리고 맨 위로 스크롤합니다.
- 기록 화면 요소 이름: 양식 id record-filter, 시작 칸 id record-from, 종료 칸 id record-to, 조회 버튼 id record-submit, 표 자리 id records-result, 표를 감싼 칸 class table-scroll. 기록 표는 머리글 한 줄을 thead에, 기록 줄을 tbody에 둡니다. 시작·종료 칸은 datetime-local(step 1)이고 한국 시간으로 읽습니다(값 뒤에 "+09:00"을 붙여 Date로). 기본값과 범위는 "지금" 날짜의 00:00:00부터 "지금"까지입니다. 시작·종료 칸은 required입니다.
- 도움말 "?"는 class help-wrap 안에 버튼 class help-btn과 설명 class help-popover를 둡니다. 한 번에 하나만 열리고, 설명은 카드나 화면 밖으로 나가지 않습니다.
- 도움말 버튼은 aria-expanded로 열림을 나타냅니다. 클릭해 고정하면 data-pinned "true"이고, 어떤 방법으로 닫히든 "false"로 돌립니다. 알림 버튼도 목록을 열고 닫을 때 aria-expanded를 맞춥니다.
- 화면 이벤트(클릭, 키, 창 크기)는 페이지를 열 때 한 번만 붙이고 그릴 때마다 다시 붙이지 않습니다. Escape는 document의 keydown 하나에서 받아 열린 알림 목록과 도움말을 함께 닫습니다. 바깥을 눌러 닫는 처리와 부딪히지 않게 도움말 버튼의 클릭·키 처리에서 이벤트 전파를 막지 않습니다(stopPropagation을 쓰지 않음).
- 같은 화면을 다시 그릴 때는 표와 막대 줄의 가로 스크롤 위치와 초점을 지키고, 그릴 내용이 지난번과 같으면 표를 다시 만들지 않습니다. 주소가 바뀐 뒤 처음 그릴 때는 지키지 않습니다.
- 검증표는 맨 위 검증표.md입니다(sample-data.js에서 바꿀 값, 기대 화면, 되돌릴 값을 한 줄씩). 시험값 여덟 개: 생산 실적 null, 생산 실적 0, 생산 실적 130(목표 120), 생산 목표 0, 공장 마지막 기록 시각 null, 공장 서버 처리 시각 null과 처리 중단, 알림 상태 실패, 공장 시간별 기록 빈 목록.

## 3회차 약속
- 연결 설정은 public/config.js 네 줄입니다: `window.DASHBOARD_CONFIG = {` / `  apiBaseUrl: "주소",` / `  timeoutMs: 5000` / `};`. 키 이름·큰따옴표·줄 모양을 바꾸지 말고 다른 키를 넣지 않습니다. 뒤 회차에서는 이 두 값만 바뀝니다.
- apiBaseUrl은 API_CONTRACT.md 9절 1단계 주소를 끝에 / 없이 씁니다. index.html에서 config.js를 app.js보다 먼저 defer로 부르고, 설정은 페이지를 열 때 한 번 읽습니다(window.DASHBOARD_CONFIG, 없으면 빈 객체).
- 요청 주소 만들기: 주소 끝 / 하나를 뗍니다. 주소가 /exec로 끝나면 주소 + "?path=" + 경로(쿼리가 있으면 + "&" + 쿼리), 아니면 주소 + 경로(쿼리가 있으면 + "?" + 쿼리)입니다. 쿼리는 URLSearchParams로 만듭니다. 5회차의 GAS 웹 앱 주소가 /exec로 끝나기 때문입니다.
- 요청은 두 가지입니다(API_CONTRACT.md 1·3절): GET /api/v1/snapshot(과거 시각이면 at), GET /api/v1/records(kind production 또는 shipment, at은 마지막 snapshot의 viewTime, from·to는 고른 때만). 시각 쿼리는 toISOString() 글자입니다.
- apiBaseUrl이 http:// 또는 https://로 시작하지 않으면 요청하지 않고 실패로 봅니다.
- 받기: fetch GET, cache "no-store", 헤더 Accept: application/json. timeoutMs(숫자가 아니면 5000)가 지나면 AbortController로 멈추고, 타이머는 성공·실패 모두 finally에서 지웁니다.
- 받은 snapshot에 viewTime이 없으면 serverTime을 기준 시각("지금")으로 씁니다. 받은 자료를 다듬는 단계가 생기기 전, 처음 API 자료로 화면을 채울 때부터 이렇게 합니다.
- 실패는 갈래마다 정해진 문장을 씁니다(문장은 프롬프트에 있음): 시간 초과, 연결 실패, JSON 아님, HTTP 오류(본문은 읽지 않음. 400, 404, 그 밖 400번대, 500번대). 응답 맨 바깥에 글자로 된 error가 있으면 200이어도 실패입니다. 시간 초과 문장의 N초는 timeoutMs ÷ 1000을 소수 첫째 자리까지 반올림한 수입니다(5000이면 5, 100이면 0.1. 5.0처럼 0을 붙이지 않음).
- 받은 snapshot·records는 API_CONTRACT.md 4절 순서대로 검사해 처음 틀린 칸 하나를 그 절의 문장 꼴로 알리고 실패로 봅니다. 과거 시각 요청이면 응답 viewTime이 at과 같은 시각이어야 합니다.
- 검사를 통과한 snapshot은 틀린 칸만 비웁니다: viewTime이 없으면 serverTime, target·completed는 0 이상 정수가 아니면 null, status는 normal·warning·error 밖이면 unknown, note가 글자가 아니면 "기록 대기", processingState는 completed·paused·waiting 밖이면 processedAt이 있을 때 completed 아니면 waiting입니다.
- 이어서: lastEventAt·receivedAt·processedAt은 시각이 아니거나 viewTime보다 늦으면 null, image는 url·alt가 모두 글자일 때만, history는 배열이고 24개 이하이며 모든 점이 맞을 때만 시각 순으로(하나라도 틀리면 그 현장만 빈 배열), 알림 status는 sent·failed 밖이면 unknown입니다.
- 조회 상태는 마지막 성공 자료, 마지막 성공 시각, 지금 오류 문장 셋으로 둡니다. 실패해도 마지막 성공 자료는 지우지 않고 화면에 남깁니다. 첫 조회부터 실패하면 빈 자료로 그려 "조회 중"이 남지 않게 합니다.
- 응답 전(자료도 오류도 없음)에는 숫자 대신 "조회 중" 글자를 보이고 0을 보이지 않습니다. 배지에 loading을 주면 neutral "조회 중"입니다. 그동안 id page-content에 aria-busy="true"를 두고, 자료나 오류가 생기면 aria-busy="false"로 바꿉니다(속성을 지우지 않음).
- 조회는 함수 하나(poll)로 합니다. 조회 중이면 새로 보내지 않고, 응답이 온 뒤(성공·실패 모두) 10초 뒤 조회를 예약합니다. 예약은 늘 하나이고, 새로고침 버튼은 예약을 지우고 바로 조회합니다.
- 조회 중 새로고침 버튼은 disabled 대신 aria-disabled="true"·aria-busy="true"를 두고 class loading을 붙입니다. 조회 중에는 새로고침 아이콘이 1초에 한 바퀴 돌고, 움직임 줄이기 설정에서는 돌지 않습니다. 조회가 끝나면 두 속성을 "false"로 바꾸고(지우지 않음) class loading을 뗍니다. 버튼에 초점을 두고 Enter를 누르고 있어도 요청이 이어 나가지 않게, 되풀이되는 Enter(event.repeat)는 막습니다. 헤더의 새로고침 버튼으로 다시 조회하게 만들 때 이 줄을 함께 만듭니다.
- 움직임 줄이기(prefers-reduced-motion: reduce)로 움직임을 끄는 규칙은 끄려는 규칙보다 styles.css 뒤쪽에 둡니다. 앞쪽에 있는 묶음에 넣으면 뒤의 움직임 규칙이 이깁니다.
- 다음 조회까지의 초는 0.25초마다 글자만 고칩니다. 예약 시각이 이미 지났거나, 탭이 다시 보일 때(visibilitychange) 예약 시각이 지났으면 바로 조회합니다.
- 조회가 실패한 동안은 알림 목록 맨 앞에 id "API-QUERY", scope "service", level "error" 항목을 더합니다(글은 프롬프트). 순서는 API-QUERY, level error, 나머지입니다.
- 기준 시각 목록은 "현재"(value "")와 한국 시간 오늘 00:00부터 지금까지의 정시(value는 그 시각의 toISOString())입니다. "지금"과 "오늘"은 마지막 성공 자료의 serverTime, 없으면 브라우저 시계입니다. 목록에 초점이 있는 동안은 다시 만들지 않고, 값을 바꾼 그때(change)는 한 번 다시 만듭니다.
- 과거 시각에서는 snapshot에 at을 붙이고 자동 조회를 멈추며, 다음 조회 글자(id countdown-text)는 hidden 속성으로 숨깁니다. 현재로 돌아오면 hidden을 풉니다. 새로고침 버튼은 같은 시각으로 조회합니다. 기준 시각 안내 id view-context, 현재로 돌아가기 버튼 class inline-button, 노란 실패 안내 id data-errors입니다.
- 조회 정보 줄은 main 맨 앞(본문 section 위)의 두 칸입니다: 마지막 조회 시각(id updated-at), 기준 시각 안내(id view-context). 앞 칸에 글이 있으면 그 뒤에 쉼표를 붙입니다.
- "현재로 돌아가기"를 눌러도 열린 알림 목록은 닫히지 않습니다. 바깥 클릭 처리에서 눌린 요소가 그 버튼인지는 event.target.closest로 찾고, 문서에 아직 있는지(contains)나 위치로 판단하지 않습니다(버튼이 누르는 순간 다시 그려져 문서에서 떨어지기 때문).
- 기준 시각이나 화면 주소가 바뀔 때마다 번호를 올리고, 번호가 바뀐 뒤 도착한 응답은 성공·실패 모두 화면에 쓰지 않고 버립니다. 시각을 바꾸면 이전 자료·성공 시각·오류·기록·고른 시간대를 비웁니다. 조회 중에 시각이나 주소가 바뀌면 새 요청은 바로 보내지 않고, 진행 중인 조회가 끝나자마자 10초를 기다리지 않고 새 시각(주소만 바뀌었으면 같은 시각)으로 다시 조회합니다. 기준 시각을 바꾸는 기능을 만들 때 이 줄을 함께 만듭니다.
- 기록 화면에 있으면 snapshot 조회가 성공할 때마다 기록도 따로 받고, 기록 화면으로 들어오면 조회 중이 아닐 때 바로 조회합니다. 기록 요청에도 처음부터 번호를 매겨, 다른 화면으로 옮기거나 "시간대 조회"를 누르기 전에 보낸 기록 요청의 응답은 늦게 와도 버립니다. "시간대 조회"를 누르면 앞서 받은 표를 비워, 새 응답을 기다리는 동안 표 자리에 기록을 받기 전 안내가 보이게 합니다(이 동작은 그 버튼을 만들 때 함께 넣습니다).
- from·to는 "시간대 조회"를 누른 값만 보냅니다(칸 글자 + "+09:00"을 toISOString()). 다른 화면으로 옮기면 고른 시간대와 받은 기록을 비웁니다. 종료가 시작보다 이르면 종료 칸에 setCustomValidity로 안내를 겁니다. 칸 값이 바뀔 때(input)와 칸을 다시 채울 때마다 다시 계산하고, 안내가 있으면 요청하지 않습니다.
- 칸에 보일 값은 사용자가 고친 값, 없으면 "시간대 조회"로 기억한 값, 없으면 기본값(기준 시각 날짜의 00:00:00, 기준 시각)입니다. 초점이 있는 칸은 덮어쓰지 않습니다. 기준 시각은 마지막 snapshot의 viewTime, 없으면 고른 과거 시각, 없으면 브라우저 시계입니다.
- 현장 사진은 snapshot의 sites.(현장).image.url을 고치지 않고 img의 src에 씁니다. 현장 사진 칸(figure) 안은 통째로 새로 그려도 됩니다(2회차의 "통째로 새로 그려도 되는 곳"에 더함). 주소와 alt가 지난번과 같으면 다시 만들지 않습니다. public/assets/approved의 사진은 지우지 않습니다(5회차에 다시 씁니다).
- 조회 기록은 poll 한 번마다 한 건입니다: requestedAt(요청 시작, ISO), at(현재면 ""), ok, durationMs(정수), available { factory, warehouse }(그 현장 completed와 target이 둘 다 0 이상 정수면 true), error(실패 문장의 첫 문장. ". "까지 자르고 60자가 넘으면 60자 + "…"). 버린 응답도 남깁니다.
- 조회 기록은 최근 200건만 sessionStorage의 "tumble-query-log"에 JSON 배열로 저장하고, 페이지를 열 때 모양이 맞는 항목만 읽어 옵니다. 읽거나 쓰지 못하면 메모리의 배열로 이어 갑니다.
- 페이지를 떠나는 중(beforeunload·pagehide에서 켜고, timeoutMs 뒤나 pageshow에서 끔)에 실패한 조회는 오류로 쓰지 않고 기록에도 남기지 않습니다. beforeunload에서 확인 창을 띄우지 않습니다.
- 조회 기록 화면: 결과는 실패면 "조회 실패" danger, 성공이고 그 현장 값이 있으면 "자료 제공" good, 값이 없으면 "현장 값 누락" warning입니다. 막대(button, class history-bar, data-at에 requestedAt)는 오래된 것부터, 표는 최신부터입니다(기록 표처럼 class table-scroll 안, 머리글 thead, 줄 tbody). 고른 막대 글은 class history-detail, 성공률 줄은 class history-range(굵은 성공률 글은 그 안 strong)입니다. 막대를 누를 때마다(이미 고른 막대를 Enter로 다시 눌러도) history-detail 글을 그 막대 글로 다시 씁니다.
- 3회차 끝에는 public/sample-data.js와 그것을 부르는 줄을 지우고 app.js에 SAMPLE_로 시작하는 이름을 남기지 않습니다. 검증표.md는 남깁니다.
- 다음 조회 글자(id countdown-text)는 min-width 88px로 폭을 고정해, 글자가 "조회 중…"으로 바뀌어도 머리 부분이 움직이지 않게 합니다.

## 4회차 약속
- 1단계 정리: package.json scripts에 "check": "node --check public/app.js && node --check public/config.js && node --check scripts/serve.mjs"를 더합니다.
- 시험용 응답 파일(확장자 없음): public/test/error/api/v1/snapshot 내용 {"error":"시험용 오류입니다."}, public/test/not-json/api/v1/snapshot 내용은 JSON이 아닌 글 한 줄(예: 시험용 글자입니다)입니다. public/test 폴더는 사용자가 지우라고 할 때 지웁니다.
- README.md 끝에 "실행", "검사", "화면 주소", "단계별 public/config.js 값" 절을 더합니다. 단계별 값은 API_CONTRACT.md 9절 표와 같고 3단계 주소는 "<GAS 웹앱 주소>" 그대로 둡니다. 웹 앱 주소를 받아도 README에 옮겨 적지 않습니다(5회차 배포 명령이 public/config.js에 씁니다).
- 내 서버는 backend 폴더의 NestJS(TypeScript)입니다. nest new나 npm init을 쓰지 않고 파일을 직접 만듭니다. 화면 코드는 고치지 않고, 마지막에 public/config.js의 apiBaseUrl만 "http://127.0.0.1:3000"으로 바꿉니다(timeoutMs 5000 그대로).
- backend/package.json: name "aiops-dashboard-student-api", version "1.0.0", private true, description "학생용 텀블러 생산·출고 교육 API", engines node ">=22", scripts build "tsc -p tsconfig.json", start "node dist/main.js", start:local "node --env-file=.env dist/main.js".
- 패키지는 이것만, 버전 앞에 ^·~ 없이 씁니다: dependencies @nestjs/common 11.2.7, @nestjs/core 11.2.7, @nestjs/platform-express 11.2.7, reflect-metadata 0.2.2, rxjs 7.8.2 / devDependencies @types/node 24.4.0, typescript 5.9.3.
- backend/tsconfig.json: target ES2022, module CommonJS, moduleResolution Node, lib ["ES2022", "DOM"], outDir dist, rootDir src, include ["src/**/*.ts"], strict·skipLibCheck·esModuleInterop·experimentalDecorators·emitDecoratorMetadata·forceConsistentCasingInFileNames true. backend/.gitignore는 node_modules/, dist/, var/, .env 네 줄입니다.
- src/main.ts 첫 줄은 import "reflect-metadata";입니다. CORS는 origin "*", methods ["GET"], credentials false입니다. 포트는 PORT, 없으면 3000(1~65535 정수가 아니면 "PORT 값이 잘못되었습니다." 오류), 주소는 HOST, 없으면 127.0.0.1입니다. 전역 주소 접두어·검증 파이프·예외 필터·환경 설정 패키지는 넣지 않습니다.
- 주소는 GET 네 개입니다: /api/v1/health(상태 확인), /api/v1/snapshot(오늘 운영 자료), /api/v1/records(기록 목록), /api/v1/images/:id(현장 사진). images 말고는 응답 헤더 Cache-Control: no-store를 붙입니다. health는 { status: "ok", releaseId: 환경 변수 RELEASE_ID, 없으면 "local" }입니다.
- 응답 모양은 API_CONTRACT.md 2·3·5절과 같습니다. 잘못된 요청은 NestJS 기본 400 모양({"message": 문장, "error": "Bad Request", "statusCode": 400})이고, 정하지 않은 주소는 NestJS 기본 404입니다. 예외 필터는 만들지 않습니다.
- 상태 파일은 환경 변수 STATE_FILE, 없으면 서버를 켠 폴더 기준 ./var/state.json입니다. 없으면 처음 켤 때 폴더와 함께 만들고, 있으면 읽은 내용을 그대로 씁니다. 저장은 2칸 들여쓴 JSON 끝에 줄바꿈을 붙여 같은 이름 + ".next"에 쓴 뒤 이름을 바꿔 옮깁니다.
- 상태 파일 맨 위 키는 sessionId("lesson-" + 만든 시각 ISO + "-1"), records, scenarioId("normal"), revision(1), changedAt(만든 시각)입니다. 화면이 쓰지 않는 예측 상태(services.prediction)와 그 이력은 만들지 않아도 됩니다.
- 상태 파일이 잘못되면 파일을 고치거나 지우지 않고 오류를 내서 서버가 켜지지 않게 합니다. scenarioId가 "normal"이 아니거나 revision이 1 이상 정수가 아니거나 changedAt이 시각이 아니면 "STATE_FILE 내용이 잘못되었습니다. 기존 파일을 보존하고 확인해 주세요.", 기록이 틀리거나 id가 겹치면 "저장된 기록을 확인해 주세요."입니다.
- 기록 한 건은 id(영문·숫자·_·- 1~100자), kind("production"·"shipment"), quantity(1 이상 정수), occurredAt, receivedAt, processedAt(없으면 null) 순서의 키입니다. 시각은 Z로 끝나는 ISO 글자이고 발생 ≤ 접수 ≤ 처리, 처리가 있으면 접수도 있습니다.
- 시드 기록(상태 파일을 만들 때): 오늘 한국 0시부터 지금보다 2분 이른 시각까지를 같은 간격 점으로 나눕니다(점 개수 = 올림(구간 ÷ 20분) + 1, 첫 점 0시, 마지막 점 구간 끝). 생산을 모두 만든 뒤 출고를 잇습니다.
- 시드 수량은 생산 합계 100, 출고 합계 75를 점 개수로 나눈 몫이고 나머지는 앞 기록부터 1씩 더합니다. id는 "seed-production-0"…, "seed-shipment-0"…입니다. 생산 발생은 점 그대로, 출고 발생은 점보다 1초 뒤이고, 두 종류 모두 접수는 발생 2초 뒤, 처리는 접수 3초 뒤입니다. 어느 시각도 지금보다 늦지 않습니다.
- 기준 시각 at(없으면 지금)은 "2026-11-09T"처럼 날짜와 T로 시작하고 끝이 Z나 +09:00 꼴이며, 시각으로 읽히고, 지금 이전이고, 한국 날짜가 오늘이어야 합니다. 아니면 400 "오늘의 현재 이전 시각을 선택해 주세요."입니다. at=처럼 값이 빈 at은 없는 것이 아니라 이 400입니다. 통과하면 Z로 끝나는 ISO로 바꿔 씁니다.
- records는 kind가 production·shipment가 아니면 시각을 보기 전에 400 "생산 또는 출고 기록을 선택해 주세요."입니다. from(없으면 기준 날짜 한국 0시)·to(없으면 기준 시각, from=·to=처럼 값이 비어도 없는 것으로 봄)는 Z나 +09:00 꼴이고 기준 날짜와 같은 한국 날짜이며 from ≤ to ≤ 기준 시각이어야 하고, 아니면 400 "조회 시간 구간을 확인해 주세요."입니다.
- records 결과는 { sessionId, viewTime(기준 시각), records }입니다. 그 kind이고 발생 시각이 from~to(양 끝 포함)인 기록을 발생 시각 순으로 담습니다. 기준 시각보다 늦은 접수·처리 시각은 null로 바꾸고 status를 더합니다(처리가 있으면 completed, 접수만 있으면 processing-wait, 둘 다 없으면 receipt-wait). 시각은 글자가 아니라 숫자로 바꿔 비교합니다.
- snapshot은 schemaVersion 1, scenarioId, revision, changedAt(상태 파일 값, 단 기준 시각보다 늦으면 기준 시각), serverTime(지금), trainingOnly true, sites, services, incidents 뒤에 viewTime(기준 시각), mode(at이 없으면 "current", 있으면 "past"), sessionId를 붙입니다.
- sites.factory는 label "텀블공장", target 120, 생산 기록이고 sites.warehouse는 label "물류창고", target 100, 출고 기록입니다. completed는 발생 시각의 한국 날짜가 기준 날짜와 같고 처리 시각이 기준 시각 이전인 기록의 수량 합이며, 합이 0이면 null입니다.
- lastEventAt·receivedAt·processedAt은 0시~기준 시각 기록 목록(records와 같은 계산)의 마지막 기록 값(없으면 null)이고, processingState는 그 마지막 기록에 처리 시각이 있으면 "completed", 아니면 "waiting"입니다.
- history는 같은 목록에서 처리 시각이 있는 기록을 발생 시각의 UTC 정시(ISO)별로 더한 { timestamp, quantity } 배열(시각 순)입니다. image는 { url: (PUBLIC_BASE_URL 끝 / 뗀 값, 없으면 "http://127.0.0.1:" + (PORT 또는 3000)) + "/api/v1/images/factory"(창고 warehouse), alt: "생산 라인 참고 사진"(창고 "물류창고 참고 사진") }입니다.
- 현장 status는 마지막 기록이 없거나, 기준 시각이 마지막 발생보다 30분 넘게 늦거나, processingState가 completed가 아니면 "warning", 아니면 "normal"입니다. note는 normal이면 "기록이 반영되고 있습니다."입니다. warning이면 마지막 기록이 없으면 label + "의 기록이 없습니다.", 마지막 기록에 처리 시각이 없으면 label + " 기록 처리를 기다리고 있습니다.", 30분 넘게 늦으면 label + " 기록이 30분 넘게 들어오지 않았습니다." 순서로 먼저 맞는 것 하나입니다.
- warning 현장마다 incidents에 { id: "FACTORY-FEED"(창고 "WAREHOUSE-FEED"), scope: "factory"(창고 "warehouse"), level: "warning", title: 그 note, owner: "공장 데이터 담당자"(창고 "창고 데이터 담당자"), action: "기록 수집과 처리 상태를 확인해 주세요." }를 넣습니다.
- services는 api { status: "normal", note: "조회 서비스가 정상입니다." }, alerts { status: "sent", lastAttemptAt: 그 snapshot의 changedAt보다 1분 이른 시각, note: "모의 전송 성공 기록입니다. 실제 알림을 보내지 않았습니다." }입니다.
- images는 id가 factory나 warehouse면 backend/assets/(id).png를 Content-Type image/png로 보냅니다(빌드된 dist 폴더 기준 ../assets). 다른 id는 문장 없이 NestJS 기본 404입니다. 사진은 사용자가 public/assets/approved에서 backend/assets로 복사해 둡니다. 파일은 StreamableFile(createReadStream)로 보내고 res.sendFile은 쓰지 않습니다.
- 이 서버에는 기록을 더하는 기능이 없습니다. 기록을 지금 기준으로 다시 만들 때는 사용자가 서버를 끄고 backend/var/state.json을 지운 뒤 다시 켭니다.
