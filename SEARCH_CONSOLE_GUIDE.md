# 🔍 검색엔진 등록 완전 가이드

> 사이트는 이미 SEO 최적화 완료. 이제 **검색엔진에 "내 사이트 있어!"라고 알려줘야** 1~2주 안에 검색됩니다.
> 아래 4개 검색엔진 전부 무료입니다. 각 5~10분.

---

## 📌 사전 준비 (한 번만)

배포된 사이트 URL을 메모장에 복사:
```
https://cruiselog-landing.vercel.app
```

---

## 1️⃣ Google Search Console (가장 중요 — 5분)

### 1단계: 접속
[https://search.google.com/search-console](https://search.google.com/search-console)

### 2단계: 속성 추가
- "속성 추가" → **"URL 접두어"** 선택 (Domain 아니라 URL prefix)
- URL 입력: `https://cruiselog-landing.vercel.app`
- "계속" 클릭

### 3단계: 소유권 확인
"HTML 태그" 방법 선택 → 다음과 같은 메타 태그 보임:
```html
<meta name="google-site-verification" content="aBcDeFgHiJkLmNoPqRsTuVwXyZ" />
```

여기서 **content="..." 안의 코드를 복사**.

### 4단계: 코드를 사이트에 박기

**나에게 채팅으로 코드만 보내주세요. 자동으로 사이트에 박고 재배포해드립니다.**

또는 직접 하실 거면:

```bash
# index.html, about/index.html 두 군데 수정
# 다음 줄 찾아서:
<meta name="google-site-verification" content="REPLACE_WITH_GSC_CODE" />
# REPLACE_WITH_GSC_CODE 부분만 받은 코드로 교체

# 그 후 push
git add -A
git commit -m "Add Google Search Console verification code"
git push
```

→ Vercel이 1~2분 안에 자동 재배포

### 5단계: 인증 클릭
GSC 페이지로 돌아가서 **"확인"** 클릭 → 성공 메시지

### 6단계: Sitemap 제출 (필수!)
좌측 메뉴 **"Sitemaps"** → "새 사이트맵 추가":
```
sitemap.xml
```
입력 후 "제출". 1~3일 안에 인덱싱 시작.

### 7단계: 색인 생성 요청 (즉시 색인용)
좌측 **"URL 검사"** → URL 입력 → "색인 생성 요청"
- 메인 페이지: `https://cruiselog-landing.vercel.app/`
- 소개 페이지: `https://cruiselog-landing.vercel.app/about/`

---

## 2️⃣ Naver Search Advisor (한국 검색 1위)

### 1단계: 접속
[https://searchadvisor.naver.com](https://searchadvisor.naver.com)

### 2단계: 사이트 등록
- 우측 상단 "웹마스터 도구" → 네이버 로그인
- "사이트 등록" → URL 입력: `https://cruiselog-landing.vercel.app`
- "확인"

### 3단계: 소유권 확인
"HTML 태그" 방법 → 코드 복사:
```html
<meta name="naver-site-verification" content="abc123def456..." />
```

**나에게 코드만 보내주세요.** 자동 적용해드립니다.

### 4단계: 사이트맵 제출
사이트 들어가서 좌측 "요청" → "사이트맵 제출":
```
sitemap.xml
```
"확인" 클릭.

### 5단계: RSS 등록 (옵션)
"RSS 제출"은 RSS 피드가 있을 때. 우리는 정적 사이트라 스킵.

### 6단계: 웹페이지 수집 요청
"요청" → "웹페이지 수집" → URL 입력 → 제출
- `/`
- `/about/`

→ 며칠 안에 네이버에서 검색됨.

---

## 3️⃣ Bing Webmaster Tools (영문 검색)

### 1단계: 접속
[https://www.bing.com/webmasters](https://www.bing.com/webmasters)

### 2단계: 빠른 가입
- "Get started" 클릭
- **Microsoft / Google / Facebook 중 하나로 로그인**
- 가입 시 **"Import from Google Search Console"** 옵션 선택하면 GSC 데이터 자동 가져옴 (가장 빠름)

### 3단계: 수동 추가 시
- "Add a site" → URL 입력
- HTML 메타 태그 방법 → content 코드 복사
- 메타 태그 이름: `<meta name="msvalidate.01" content="..." />`

**나에게 코드 보내주세요.** 자동 적용해드립니다.

### 4단계: Sitemap 제출
Sitemaps → Add → `https://cruiselog-landing.vercel.app/sitemap.xml`

---

## 4️⃣ Daum 검색 (네이버 다음으로 큰 한국 검색)

다음 검색은 네이버 → Yeti → Daumoa 순으로 크롤링되어,
**robots.txt에 이미 허용해둔 상태이므로 별도 등록 불필요.**

직접 등록하고 싶으면:
- [https://register.search.daum.net/index.daum](https://register.search.daum.net/index.daum)

---

## 🎯 추가 등록 (선택, 효과 작음)

| 검색엔진 | URL | 비고 |
|---|---|---|
| 줌 (Zum) | https://help.zum.com/submit | 한국 |
| 야후 재팬 | Bing 등록하면 자동 | 일본 시장 진출 시 |
| 얀덱스 | https://webmaster.yandex.com | 러시아 |
| 바이두 | https://ziyuan.baidu.com/site/index | 중국 (한국 사이트는 별 효과 X) |

---

## 📊 검색 노출 타임라인 (현실적 기대치)

| 시점 | 상태 |
|---|---|
| **Day 1~2** | GSC/Naver 등록 + 사이트맵 제출 완료 |
| **Day 3~7** | Google이 사이트 크롤링 시작 (검색 결과엔 아직 없음) |
| **Week 1~2** | "위시메이커", "오용택", "Austin Oh" 등 **고유 키워드**로 검색 시 노출 시작 |
| **Week 2~4** | "크루즈로그", "CruiseLog" 검색 시 1페이지 노출 |
| **Month 2~3** | 일반 키워드("크루즈 비용", "크루즈 예약") 부분 노출 시작 |
| **Month 3~6** | 안정적 SEO 트래픽 발생 (콘텐츠 + 백링크에 따라) |

---

## ✅ 완료 체크리스트

- [ ] Google Search Console 등록 + 사이트맵 제출 + URL 색인 요청
- [ ] Naver Search Advisor 등록 + 사이트맵 제출
- [ ] Bing Webmaster Tools 등록 (GSC 가져오기로 빠르게)
- [ ] 검증 코드 3개 받아서 채팅에 붙여넣기 → 사이트 자동 반영
- [ ] (선택) cruiselog.kr 도메인 구입 후 Vercel 연결
- [ ] (선택) Google Analytics 4 추가
- [ ] (선택) Google AdSense 신청 (콘텐츠 30개+ 발행 후)

---

## 💬 검증 코드 받아오면 다음과 같이 채팅에 붙여넣어주세요

예시:
```
Google: AbCdEfGhIjKlMnOpQrStUvWxYz123456789
Naver: 1234567890abcdef1234567890abcdef
Bing: A1B2C3D4E5F6G7H8I9J0
```

→ 그러면 사이트의 verification 메타 태그를 자동 교체 + Vercel 재배포 + 1~2분 후 검색엔진에서 확인 클릭 → 인증 완료

---

## 🔗 빠른 링크 모음

| 작업 | URL |
|---|---|
| Google Search Console | https://search.google.com/search-console |
| Naver Search Advisor | https://searchadvisor.naver.com |
| Bing Webmaster Tools | https://www.bing.com/webmasters |
| Daum 검색 등록 | https://register.search.daum.net |
| Google Analytics | https://analytics.google.com |
| Google AdSense | https://www.google.com/adsense |
| Schema 검증 (Rich Results Test) | https://search.google.com/test/rich-results |
| OG 검증 (카카오톡) | https://developers.kakao.com/tool/clear/og |

검증 코드 3개 받으시면 채팅에 보내주세요. 5분 안에 모든 인증 완료시켜 드립니다. 🚢
