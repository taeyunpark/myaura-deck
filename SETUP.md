# MYAURA Buyer Deck — GitHub Pages 배포 가이드

> **박 차장님 전용 단계별 가이드**
> 예상 소요 시간: **20~40분** (GitHub 계정 보유 시)

---

## 사전 준비물

| 항목 | 상태 |
|---|---|
| GitHub 계정 | □ 보유 / □ 신규 가입 필요 |
| myaura.co.kr DNS 관리 접근 권한 | □ 필요 |
| 본 패키지 (5개 파일 + 1개 폴더) | ✅ 준비 완료 |

---

## STEP 1 — GitHub Repository 생성 (5분)

### 1-1. GitHub 로그인
[https://github.com](https://github.com) 접속 후 로그인

### 1-2. 새 Repository 생성
1. 우측 상단 **`+`** 아이콘 → **New repository** 클릭
2. 설정값 입력:

| 항목 | 입력값 |
|---|---|
| Repository name | `myaura-deck` |
| Description | `MYAURA — K-Beauty Brand Deck` |
| Public / Private | **Public** ✅ (GitHub Pages 무료 사용 필수) |
| Add a README file | ❌ 체크 해제 (이미 패키지에 있음) |
| Add .gitignore | None |
| Choose a license | None |

3. **Create repository** 클릭

---

## STEP 2 — 파일 업로드 (3분)

### 2-1. 빈 Repository 화면에서 파일 업로드
1. **`uploading an existing file`** 링크 클릭
   (또는 "Add file" → "Upload files")

### 2-2. 패키지 파일 5개 모두 드래그앤드롭

| 파일명 | 역할 |
|---|---|
| `index.html` | 덱 본체 (336KB) |
| `CNAME` | Custom Domain 지정 |
| `.nojekyll` | Jekyll 비활성화 (HTML 그대로 노출) |
| `README.md` | Repository 설명 |
| `404.html` | 잘못된 경로 진입 시 메인으로 리다이렉트 |

> **⚠️ `.nojekyll` 파일은 점(.)으로 시작하여 숨김 파일로 취급될 수 있습니다.**
> Mac: Finder에서 `Cmd + Shift + .` 으로 숨김 파일 표시 후 드래그
> Windows: 탐색기 "보기" → "숨긴 항목" 체크 후 드래그

### 2-3. Commit 메시지
- Commit message: `Initial deck v4.2 deployment`
- **Commit changes** 클릭

---

## STEP 3 — GitHub Pages 활성화 (5분)

### 3-1. Settings 진입
Repository 메인 → 상단 **Settings** 탭

### 3-2. Pages 설정
좌측 메뉴 → **Pages**

### 3-3. Source 설정

| 항목 | 선택 |
|---|---|
| Source | **Deploy from a branch** |
| Branch | **main** / **(root)** |
| **Save** 클릭 | |

### 3-4. 1~10분 대기
페이지 상단에 빌드 상태 표시. 완료되면 다음 URL로 임시 접속 가능:

```
https://{username}.github.io/myaura-deck/
```

> ⚠️ 이 시점에서 한 번 접속해서 **덱이 정상 표시되는지 확인**하세요. 정상이라면 STEP 4 진행.

---

## STEP 4 — Custom Domain 연결 (15~30분)

### 4-1. myaura.co.kr DNS 관리 페이지 진입
도메인 등록 업체 (가비아 / 후이즈 / 카페24 / Cloudflare 등) DNS 관리 페이지 진입.

### 4-2. CNAME 레코드 추가

| 항목 | 입력값 |
|---|---|
| 호스트 (Host) / 이름 (Name) | `deck` |
| 타입 (Type) | `CNAME` |
| 값 (Value) / 대상 (Target) | `{username}.github.io` (마침표 끝에 포함) |
| TTL | 자동 또는 3600 |

> 예시: GitHub 사용자명이 `yeo-corp`라면 → 값에 `yeo-corp.github.io.` 입력
> **마침표(.) 끝에 포함하는 게 중요** (FQDN 표기)

### 4-3. GitHub Pages Custom domain 설정
1. Repository → Settings → Pages
2. **Custom domain** 입력란에 `deck.myaura.co.kr` 입력
3. **Save** 클릭
4. **Enforce HTTPS** 체크박스가 활성화되면 체크 ✅

### 4-4. DNS 전파 대기 (10분~24시간)
- 일반적으로 **10~30분** 안에 적용
- 최대 **24시간** 소요 가능
- 브라우저 캐시 이슈 가능 시 시크릿 창으로 테스트

### 4-5. 최종 확인
```
https://deck.myaura.co.kr
```

접속 시 덱 정상 노출 + 주소창에 🔒 자물쇠 (HTTPS) 표시되면 완료.

---

## 향후 업데이트 방법 (변경 발생 시)

### 방법 A — 웹에서 직접 수정 (간단)
1. Repository → `index.html` 클릭
2. 우측 상단 연필 아이콘 (Edit) 클릭
3. 직접 수정 → 하단 **Commit changes**
4. 1~2분 후 라이브 반영

### 방법 B — 새 버전 업로드 (덱 통째 교체)
1. Repository → `index.html` 클릭 → 우측 휴지통 아이콘으로 삭제
2. Repository → Add file → Upload files
3. 새 `index.html` 업로드 → Commit
4. 1~2분 후 라이브 반영

---

## 트러블슈팅

| 증상 | 원인 / 해결 |
|---|---|
| `https://deck.myaura.co.kr` 접속 안 됨 (NXDOMAIN) | DNS 전파 미완료 — 30분~24시간 대기 |
| HTTPS 인증서 오류 | Custom domain 입력 후 자동 발급 (10~30분 대기) |
| 페이지가 README만 보임 | `.nojekyll` 파일 누락 — 다시 업로드 |
| 404 페이지 표시 | `index.html` 대소문자 확인 (소문자 `index.html` 필수) |
| Custom domain 입력 후 "DNS check unsuccessful" | CNAME 레코드 전파 대기 또는 값 재확인 |
| 페이지 깨짐 / 폰트 미적용 | 브라우저 캐시 — 강제 새로고침 (`Ctrl + Shift + R`) |

---

## 추가 권장 사항 (선택)

### Organization 만들기 (장기 운영용)

GOOKIN 덱처럼 모든 와이이오 브랜드 덱을 한 곳에서 관리하려면:

1. GitHub → 우측 상단 `+` → **New organization**
2. 이름: `yeo-corp` 또는 `yeo-co` 등
3. Free plan 선택
4. 향후 `yeo-corp/myaura-deck`, `yeo-corp/gookin-deck`, `yeo-corp/bnbg-deck` 등 통합 관리

### 접근 분석 (Google Analytics 등)
필요 시 `index.html` `<head>`에 GA 코드 삽입 가능. 박 차장님 요청 시 작업 가능.

---

## 문의

본 가이드 진행 중 문제 발생 시 박 차장님이 직접 알려주십시오 (자체 처리 가능 범위 내에서 즉시 정정안 회신).

— Claude · 와이이오 마케팅 AI 파트너
