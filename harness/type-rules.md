<!-- 원본: 블루엠 표준 하네스 v0.5.0 (homepage). 이 파일은 고치지 말고 원본에서 고친 뒤 다시 설치. -->
# 2층 홈페이지 규칙 (homepage)

## 페이지 기본
* 모든 페이지에 `<html lang="..">`, `<title>`, `<meta name="description">`, `<meta name="viewport">`를 넣는다.
* 언어별 페이지는 같은 내용을 같은 구조로 둔다. 한 언어만 고치면 다른 언어도 고쳐야 하는지 확인한다.
* 번역은 초안이다. 외국어 문장은 "(번역 검수 필요)"로 대표에게 알린다.
* 이미지는 웹용으로 줄여서 쓴다 (한 장 500KB 이하 권장). `alt`를 꼭 쓴다.
* 러시아어·독일어처럼 단어가 긴 언어가 있으면 제목(h1~h4)에 `overflow-wrap: break-word; hyphens: auto;`를 넣는다. 휴대폰에서 긴 단어가 화면 밖으로 넘친다 (실제 프로젝트에서 발생).

## 오픈 전·후
* 정식 오픈 전에는 모든 페이지에 `<meta name="robots" content="noindex">`를 넣어 검색에 안 나오게 한다.
* 오픈할 때 `launched`를 `true`로 바꾸고 noindex를 뺀다. 검사가 두 상태를 모두 확인한다.
* 사이트 설정 파일에 이미 `launched`가 있으면 `harness.config.json`에 `"launchedFrom": "그 파일"`로 적어 한 곳에서만 관리한다.
* 오픈 시 도메인 연결, 검색엔진 등록은 사람이 한다.

## 개인정보·법적 표시
* 문의 양식이 있으면 개인정보처리방침 페이지와 수집 동의 문구가 있어야 한다.
* 사업자 정보(상호, 대표자, 사업자등록번호 등) 표시는 고객이 준 내용만 그대로 쓰고, 추측해서 채우지 않는다.

## 화면 검사
* 큰 화면 변경 뒤에는 `node harness/checks/screenshots.mjs`로 언어×기기 스크린샷을 찍는다.
* 기본 기기는 휴대폰·PC 2종이다. 태블릿이 중요한 사이트만 `devices`에 `"tablet"`을 더한다 (장수가 1.5배로 늘어 느려짐).
* 결과는 `_workspace/screenshots/`에 저장된다(GitHub에 올라가지 않음). GitHub Actions에서는 실행 결과의 "Artifacts"에서 받는다.
* 휴대폰 화면에서 글자 넘침, 겹침, 가로 스크롤이 없는지 먼저 본다.

## 검사 명령
`gate.sh`가 `buildCommand`(예: `node tools/build.mjs`)로 빌드한 뒤 검사한다. 스크린샷은 빌드된 결과로 찍으므로 먼저 빌드한다.

| 검사 | 명령 |
|---|---|
| 관문 (빌드+전체 검사) | `bash harness/checks/gate.sh` |
| 기본 검사만 | `bash harness/checks/check-basic.sh` |
| 홈페이지 검사만 | `node harness/checks/check-homepage.mjs` |
| 화면 검사 | `node harness/checks/screenshots.mjs` (Playwright 필요) |

`package.json`이 있는 프로젝트는 짧은 명령을 넣어 두면 편하다.
```json
"check": "bash harness/checks/gate.sh",
"shots": "node tools/build.mjs && node harness/checks/screenshots.mjs"
```

## 배포 막기
* 자동 배포 워크플로의 배포 단계 앞에 `bash harness/checks/gate.sh`를 넣는다. 예시: 하네스 원본의 `types/homepage/examples/deploy-cloudflare-pages.yml`.
* 배포 과정에서 이미 빌드했다면 `bash harness/checks/gate.sh --skip-build`로 검사만 돌린다.
* `bluem-homepage-gate` 워크플로는 PR에서 미리 알려 주고 스크린샷을 남기는 용도다. 이것만으로는 배포가 멈추지 않는다.
