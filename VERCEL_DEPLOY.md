# 경희 미디어 업무 자동화 Portal — Vercel 배포 가이드

작성일: 2026-10-17

이 홈페이지는 `index.html`, CSS, JavaScript, 이미지로 구성된 정적 사이트입니다. Node.js 빌드, 데이터베이스, 서버 함수, 환경변수가 필요하지 않습니다. Vercel에서는 **Framework Preset을 `Other`로 선택하고 Build Command를 비워** 파일을 그대로 배포합니다.

공식 참고 문서:

- 프로젝트 생성 및 Git 가져오기: https://vercel.com/docs/projects/managing-projects
- Git 저장소 배포: https://vercel.com/docs/git
- 정적 사이트 빌드 설정: https://vercel.com/docs/builds/configure-a-build
- CLI 배포: https://vercel.com/docs/projects/deploy-from-cli
- 사용자 도메인 설정: https://vercel.com/docs/domains/set-up-custom-domain

---

## 0. 시작 전에 준비할 것

다음 항목을 먼저 확인합니다.

- 학과에서 관리할 Vercel 계정 또는 Vercel Team
- 학과 구성원이 접근할 수 있는 이메일
- 배포 파일: `vercel-배포용/` 또는 `vercel-배포용.zip`
- 사용자 도메인을 연결한다면 해당 도메인의 DNS를 수정할 수 있는 담당자
- Git 자동 배포를 사용할 경우 학과가 관리하는 GitHub 저장소

현재 배포 패키지의 필수 화면 파일은 다음과 같습니다.

```text
index.html
styles.css
script.js
khhu-main.jpeg
대학휘장-02.jpg
vercel.json
```

아래 파일은 운영 문서이므로 함께 보관하되 홈페이지 화면에는 사용되지 않습니다.

```text
README.md
DESIGN_RULES.md
VERCEL_DEPLOY.md
```

`vercel-배포용.zip`을 사용할 때는 먼저 압축을 풉니다. ZIP 파일 자체를 프로젝트 루트에 올리지 않습니다.

---

# 권장 방법: 학과 소유 Git 저장소와 Vercel 연결

이 방법은 파일을 수정해 Git에 올릴 때 Vercel이 자동으로 다시 배포하므로 장기 운영에 적합합니다. 개인 GitHub 계정 의존성을 없애려면 저장소도 학과 소유 계정이나 학과 Organization에서 관리하는 것이 좋습니다.

## 1단계. 학과용 Git 저장소 준비

1. 학과가 관리하는 GitHub 계정 또는 Organization에서 새 저장소를 만듭니다.
2. 저장소 이름은 예를 들어 `khu-media-automation-portal`로 지정합니다.
3. `vercel-배포용/` 폴더 안의 파일들을 저장소의 최상위에 올립니다.
4. 저장소 첫 화면에서 아래처럼 보여야 합니다.

```text
khu-media-automation-portal/
├─ index.html
├─ styles.css
├─ script.js
├─ khhu-main.jpeg
├─ 대학휘장-02.jpg
├─ vercel.json
├─ README.md
├─ DESIGN_RULES.md
└─ VERCEL_DEPLOY.md
```

> 작업 폴더 전체를 하나의 저장소로 운영하려면 `vercel-배포용/` 폴더를 그대로 올려도 됩니다. 이 경우 Vercel에서 Root Directory를 `vercel-배포용`으로 지정해야 합니다.

## 2단계. 학과 Vercel 계정으로 로그인

1. https://vercel.com/ 에 접속합니다.
2. 학과에서 관리할 계정으로 로그인합니다.
3. 화면 왼쪽 위의 계정/Team 선택 메뉴에서 **학과 Team**이 선택되어 있는지 확인합니다.
4. 개인 계정이 선택되어 있다면 프로젝트를 만들기 전에 학과 Team으로 전환합니다.

## 3단계. GitHub 연결

1. Vercel 대시보드에서 **Add New → Project**를 누릅니다.
2. **Import Git Repository** 영역에서 GitHub를 선택합니다.
3. 처음 연결하는 경우 GitHub 권한 화면이 열립니다.
4. 학과 저장소가 속한 계정 또는 Organization을 선택합니다.
5. 전체 저장소 접근 대신 필요한 학과 저장소만 허용할 수 있다면 해당 저장소만 선택합니다.
6. `khu-media-automation-portal` 저장소 옆의 **Import**를 누릅니다.

> 학과 저장소가 목록에 없다면 GitHub에서 Vercel 앱의 저장소 접근 권한을 확인합니다. 비공개 GitHub Organization 저장소와 Vercel 요금제·팀 구성에 따라 커밋 작성자의 Vercel Team 가입이 요구될 수 있습니다.

## 4단계. 프로젝트 설정

Import 다음 화면에서 아래와 같이 설정합니다.

| 항목 | 설정값 |
| --- | --- |
| Project Name | `khu-media-automation-portal` 또는 학과가 정한 이름 |
| Framework Preset | `Other` |
| Root Directory | 파일이 저장소 최상위에 있으면 비움 / 폴더째 올렸으면 `vercel-배포용` |
| Build Command | Override를 켜고 **빈 값** |
| Output Directory | 별도 지정하지 않음 |
| Install Command | 별도 지정하지 않음 |
| Environment Variables | 없음 |

Vercel 공식 안내에 따르면 HTML/CSS/JS만 있는 정적 프로젝트는 `Other`를 선택하고 Build Command를 비워 빌드 단계를 건너뛸 수 있습니다. `public` 폴더가 없으면 프로젝트 루트의 파일이 제공됩니다.

## 5단계. 첫 배포

1. 설정을 다시 확인합니다.
2. **Deploy**를 누릅니다.
3. 배포가 끝날 때까지 기다립니다.
4. 성공 화면의 **Visit** 또는 발급된 `*.vercel.app` 주소를 엽니다.
5. 이 주소는 아직 학과 도메인을 바꾸지 않은 검수용 주소로 사용합니다.

## 6단계. 기능 검수

새 Vercel 주소에서 다음을 순서대로 확인합니다.

- 상단 제목이 `경희 미디어 업무 자동화 Portal`인지
- 학생용 → 교수용 → 범용 탭 전환이 되는지
- 학생용 01번 `408호 스튜디오 강의실 예약`이 `이용 가능`인지
- 408호 타일을 눌렀을 때 경희대학교 Google Apps Script 신청 페이지로 이동하는지
- 학생용 02번 `졸업논문 제출`은 준비 중인지
- 교수용 01번 `교수 연구실적 제출`이 기존 Google Forms로 이동하는지
- PC와 휴대전화에서 글자나 타일이 잘리지 않는지
- 휘장과 캠퍼스 사진이 정상 표시되는지

Google Apps Script 주소에 `/a/macros/khu.ac.kr/`가 포함되어 있으므로 실제 이용 대상 계정에서 로그인 및 접근 가능 여부도 확인합니다.

## 7단계. 자동 배포 확인

Git 연결 방식에서는 Production Branch에 새 커밋이 들어오면 Vercel이 새 Production Deployment를 만듭니다.

1. `README.md`처럼 화면에 영향을 주지 않는 파일을 한 줄 수정해 커밋합니다.
2. GitHub에 push합니다.
3. Vercel 프로젝트의 **Deployments**에서 새 배포가 시작되는지 확인합니다.
4. 테스트 커밋은 원복하거나 그대로 관리 문구로 유지합니다.

이 확인이 끝나면 이후 운영은 다음 순서입니다.

```text
루트 관리 파일 수정
→ 패키지_동기화.ps1 실행
→ vercel-배포용 파일을 학과 Git 저장소에 반영
→ commit / push
→ Vercel 자동 배포 확인
```

---

# GitHub 없이 배포하는 방법: Vercel CLI

개인 GitHub와 완전히 분리해 바로 배포하려면 로컬 폴더에서 Vercel CLI를 사용할 수 있습니다. 다만 이후 수정 때도 담당자가 직접 배포 명령을 실행해야 합니다.

## 1단계. 배포 폴더 열기

PowerShell에서 다음을 실행합니다.

```powershell
cd "C:\Users\s2won\Desktop\경희대학교 미디어학과 업무 에이전트\vercel-배포용"
```

## 2단계. Vercel 로그인 및 연결

전역 설치 없이 실행하려면 다음 명령을 사용합니다.

```powershell
npx vercel login
```

브라우저가 열리면 학과 Vercel 계정으로 로그인합니다. 로그인 후 다음을 실행합니다.

```powershell
npx vercel
```

질문이 나오면 다음 기준으로 선택합니다.

- Scope: 학과 Team
- 기존 프로젝트 연결 여부: 처음이면 `No`
- 프로젝트 이름: `khu-media-automation-portal`
- 소스 폴더: 현재 폴더 `./`
- 설정 변경 여부: `vercel.json`을 사용하므로 기본값 유지

명령이 끝나면 Preview 또는 첫 Deployment 주소가 표시됩니다. 위의 **6단계 기능 검수**를 수행합니다.

## 3단계. Production 배포

검수가 끝나면 다음을 실행합니다.

```powershell
npx vercel --prod
```

이후 수정본을 배포할 때도 같은 폴더에서 `npx vercel --prod`를 실행합니다.

> `.vercel/` 폴더에는 연결된 Vercel 프로젝트 정보가 생성됩니다. 이 폴더를 공개 저장소나 배포 ZIP에 포함하지 않습니다.

---

# 학과 도메인 연결

Vercel 기본 주소에서 모든 검수가 끝난 뒤 진행합니다. 기존 GitHub Pages 주소나 도메인은 새 사이트가 확인되기 전에 중단하지 않습니다.

## 1단계. 도메인 추가

1. Vercel에서 학과 프로젝트를 엽니다.
2. **Settings → Domains**로 이동합니다.
3. 사용할 학과 도메인 또는 서브도메인을 입력하고 추가합니다.
4. Vercel이 표시하는 DNS 레코드와 소유권 확인 값을 기록합니다.

## 2단계. DNS 담당자에게 전달

- 루트 도메인은 일반적으로 A 레코드를 요구합니다.
- 서브도메인은 일반적으로 CNAME 레코드를 요구합니다.
- 다른 Vercel 계정이나 프로젝트에 이미 등록된 도메인은 TXT 소유권 확인을 요구할 수 있습니다.
- 실제 값은 일반 예시를 복사하지 말고 **현재 프로젝트의 Settings → Domains 화면에 표시되는 값**을 사용합니다.

학교가 외부 DNS 제공자를 사용한다면 Vercel 화면에서 직접 DNS를 추가하지 않고, 학교 DNS 관리자에게 표시된 레코드를 전달합니다.

## 3단계. 전환 확인

DNS 변경 후 Vercel의 Domains 화면이 `Valid Configuration` 또는 정상 상태가 될 때까지 기다립니다. Vercel은 DNS 확인 후 SSL 인증서를 자동으로 발급합니다.

다음 사항을 다시 확인합니다.

- `https://학과도메인` 접속
- 보안 인증서 경고 없음
- 학생용·교수용·범용 탭 정상 작동
- 408호 예약 및 교수 연구실적 제출 링크 정상 작동
- PC와 휴대전화 표시 정상

## 4단계. 기존 개인 배포 정리

새 도메인이 안정적으로 동작하는 것을 확인한 뒤에만 기존 개인 GitHub Pages 배포를 정리합니다.

- 기존 저장소를 즉시 삭제하지 말고 백업으로 보관
- GitHub Pages 설정을 해제하기 전에 새 사이트 최종 확인
- 기존 개인 Vercel 프로젝트가 있다면 학과 Team으로 프로젝트를 이전할 수도 있지만, 지금 제공한 정적 패키지로 새 프로젝트를 만드는 편이 계정 소유 관계를 명확히 관리하기 쉽습니다.
- 학과 담당자 최소 2명이 Vercel 프로젝트와 소스 저장소에 접근할 수 있는지 확인

---

# 문제 해결

## 배포 후 404가 표시됨

- `index.html`이 Vercel 프로젝트 Root Directory의 최상위에 있는지 확인합니다.
- 저장소 전체를 올렸다면 Root Directory가 `vercel-배포용`인지 확인합니다.
- Project Settings → Build and Deployment에서 Framework Preset이 `Other`인지 확인합니다.

## CSS 또는 이미지가 보이지 않음

- 파일명이 정확히 `styles.css`, `khhu-main.jpeg`, `대학휘장-02.jpg`인지 확인합니다.
- 대소문자와 한글 파일명이 Git 저장소에서 유지되었는지 확인합니다.
- 브라우저에서 강력 새로고침을 합니다.

## Git push 후 자동 배포가 되지 않음

- Vercel Settings → Git에서 연결 저장소와 Production Branch를 확인합니다.
- GitHub의 Vercel 앱이 해당 저장소에 접근할 수 있는지 확인합니다.
- 비공개 Organization 저장소라면 Vercel Team 및 요금제의 협업 제한을 확인합니다.

## 도메인이 다른 홈페이지를 보여줌

- DNS가 아직 기존 GitHub Pages 값을 가리키는지 확인합니다.
- Vercel Settings → Domains가 제시하는 레코드와 실제 DNS 값을 비교합니다.
- DNS 전파 중이면 기존 값과 새 값이 지역에 따라 다르게 보일 수 있습니다.

## 408호 신청페이지에서 권한 오류가 표시됨

- 경희대학교 Google 계정으로 로그인했는지 확인합니다.
- Google Apps Script 배포의 실행 사용자 및 접근 권한 설정을 확인합니다.
- 신청페이지 자체 문제는 포털 HTML이 아니라 Apps Script 배포 설정에서 수정합니다.

---

# 최종 완료 체크리스트

- [ ] 학과 Vercel Team에서 프로젝트 생성
- [ ] 개인 계정이 아닌 학과 소유 범위인지 확인
- [ ] Framework Preset `Other`
- [ ] Build Command 비움
- [ ] 올바른 Root Directory 선택
- [ ] `*.vercel.app` 주소에서 화면 검수
- [ ] 408호 예약 링크 검수
- [ ] 교수 연구실적 링크 검수
- [ ] Git 자동 배포 또는 CLI 재배포 절차 확인
- [ ] 학과 도메인 DNS 연결
- [ ] HTTPS 인증서 확인
- [ ] 담당자 2명 이상 접근 확인
- [ ] 새 사이트 확인 후 기존 개인 배포 정리
