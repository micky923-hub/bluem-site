# bluem-site

bluem-partners.com 회사 소개 사이트. **공개 저장소**다.

## 블루엠 표준 하네스
* 이 저장소에는 블루엠 표준 하네스(homepage 유형)가 설치돼 있다. 이 파일이 3층(이 사이트만의 규칙)이고, 공통 규칙은 `harness/core-rules.md`(1층), `harness/type-rules.md`(2층)에 있다. 이 파일과 다르면 이 파일이 먼저다.
* `harness/`, `.github/workflows/bluem-*`, `.claude/skills/bluem-*`는 설치본이다. 여기서 고치지 않는다.
* 고친 뒤 `bash harness/checks/gate.sh`(비밀 정보·필수 태그·검색 노출·내부 링크·언어별 페이지)를 돌린다. 화면 확인은 `node harness/checks/screenshots.mjs` → `_workspace/screenshots/`(GitHub에 올라가지 않음).
* 이 사이트는 `main`이 바로 GitHub Pages로 배포된다. 그래서 머지 전에 PR의 `bluem-basic-checks`, `bluem-homepage-gate`가 초록불인지 확인하고, 빨간불이면 머지하지 않는다.

## 규칙
* 회사 내부 자료를 넣지 않는다: 수수료율·가격, 파트너사·고객사 이름(예외: K20은 2026-10-23 대표가 소개서 내용 공개 허락을 받음. 단가는 "문의"로 두고, 사례 속 브랜드 이름은 쓰지 않는다), 법인등록번호·사업자등록번호·주소 상세, 개인 연락처. 화면에 안 보이는 주석·파일에도 넣지 않는다.
* 옥외광고(`ooh/`): 매체사·영업대행 파트너 이름, 단가, 다른 광고주 집행 데이터, 매체 사진은 넣지 않는다. 매체는 종류·지역으로만 소개한다. 이름 공개는 계약 후 대표가 허락하면 바꾼다.
* 공개 연락처는 `contact@bluem-partners.com`만 쓴다.
* 실적·숫자는 근거가 있는 것만, 과장 표현("최고", "업계 1위", "100% 보장")은 쓰지 않는다.
* 빌드 도구 없이 정적 HTML로 유지한다. 페이지: `index.html`(소개), `contact/`(문의 양식), `privacy/`(개인정보처리방침), `404.html`(없는 주소 안내), `ooh/`·`en/ooh/`·`ja/ooh/`·`zh/ooh/`(옥외광고 소개, 주력 사업), `build/`·`en/build/`·`ja/build/`·`zh/build/`(홈페이지·서비스 구축 소개. 고객사 이름·서비스명은 넣지 않는다), `fast/`·`en/fast/`·`ja/fast/`·`zh/fast/`(K20 FAST 광고 소개), `en/`·`ja/`·`zh/`(영문·일본어·중국어 간체 소개, 문의는 메일 중심, 답변은 한국어·영어). 소개 문구를 바꾸면 네 언어를 함께 고친다. 하위 페이지 공통 스타일은 `assets/sub.css`.
* 공식 채널: 유튜브 `https://www.youtube.com/@bluem-partners` (바닥글 링크, 구조화 데이터 sameAs).
* 문의 양식은 Web3Forms로 contact@bluem-partners.com에 전달한다. 받는 항목·보관 기간·위탁 업체를 바꾸면 `privacy/`와 양식의 동의 문구를 함께 고친다.
* 쿠키·방문자 분석 등 추적 도구를 넣으면 개인정보처리방침에 먼저 반영한다.
* 색: 네이비 `#0C2340`, 블루 `#307FE2`, 라이트블루 `#71B0E8`. 글꼴: Pretendard.
* 야간 모드: 방문자 기기 설정(`prefers-color-scheme`)을 자동으로 따른다(전환 버튼 없음). 색은 변수로만 쓴다. 글자색 네이비는 `--title`, 흰 카드 바탕은 `--card`. 야간 색은 각 페이지 `:root`와 `assets/sub.css`의 `@media (prefers-color-scheme: dark)`에서 정한다. 새 요소를 만들 때 `#fff`·`var(--navy)` 글자색을 직접 쓰지 않는다.
* 작업 브랜치에서 고치고, 대표가 "머지해줘"라고 하면 PR을 만들어 `main`에 머지한다.
