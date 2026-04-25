# 🚀 크루즈로그 랜딩페이지 배포 가이드

## 📁 파일 구성

```
landing/
├── index.html       ← 랜딩페이지 본체 (단일 파일, CDN 의존)
├── og-image.html    ← OG 이미지 생성용 (1200×630)
└── DEPLOY.md        ← 이 문서
```

---

## ⚡ 5분 배포 — Vercel (가장 추천)

도메인 없이도 `cruiselog.vercel.app` 무료 배포 가능.

```
1. https://vercel.com 접속 → GitHub로 가입 (무료)
2. New Project → Import → "Upload Folder" 선택
3. landing/ 폴더 통째로 드래그
4. Project Name: cruiselog
5. Framework Preset: Other
6. Root Directory: ./
7. Deploy
8. 1~2분 후 https://cruiselog.vercel.app 발급됨
```

**자동으로 되는 것:**
- HTTPS 인증서
- 글로벌 CDN
- 실시간 미리보기
- Custom domain 연결 (cruiselog.kr 사면)

---

## 🌐 5분 배포 — GitHub Pages (대안)

도메인 `cruiselog-kr.github.io/cruiselog/` 형태.

```
1. https://github.com 접속 → 새 저장소 만들기
   - 저장소 이름: cruiselog
   - Public 선택
2. landing/ 폴더의 모든 파일을 저장소 root에 업로드
3. Settings → Pages → Source: main branch / root
4. 1~2분 후 https://[your-id].github.io/cruiselog/ 접속 가능
```

---

## 🌐 5분 배포 — Netlify (대안 2)

```
1. https://app.netlify.com 접속 → 가입
2. "Add new site" → "Deploy manually"
3. landing/ 폴더 드래그
4. Site name 변경: cruiselog
5. https://cruiselog.netlify.app 발급
```

---

## 🖼️ OG 이미지 만들기 (필수)

`og-image.html`을 1200×630 PNG로 변환해서 `og-image.png`로 저장하면 카카오톡/페북/트위터에서 미리보기로 보입니다.

### 방법 A — 무료 온라인 도구 (가장 쉬움)

```
1. https://htmlcsstoimage.com/ 또는 https://www.web2png.com/ 접속
2. URL: 배포한 https://cruiselog.vercel.app/og-image.html
3. Width: 1200, Height: 630
4. PNG로 다운로드
5. 다운받은 파일 이름을 og-image.png 로 변경
6. landing/ 폴더에 추가 후 다시 Vercel에 업로드
```

### 방법 B — 브라우저 스크린샷

```
1. og-image.html 을 브라우저에서 열기
   (간단히 더블클릭하면 열림)
2. F12 (개발자 도구)
3. Ctrl+Shift+M (모바일 모드)
4. 화면 크기를 1200×630으로 설정
5. Ctrl+Shift+P → "Capture full size screenshot"
6. 자동 다운로드된 PNG 파일을 og-image.png로 저장
```

### 방법 C — Chrome 헤드리스 (개발자용)

```bash
chrome --headless --disable-gpu --window-size=1200,630 \
       --screenshot=og-image.png \
       file:///path/to/og-image.html
```

---

## 🔧 index.html 에서 수정할 것 (배포 후)

배포한 도메인에 맞게 `index.html` 상단의 메타 태그 5곳 수정:

```html
<!-- 기존 -->
<meta property="og:url" content="https://cruiselog.kr/" />
<meta property="og:image" content="https://cruiselog.kr/og-image.png" />
<meta name="twitter:url" content="https://cruiselog.kr/" />
<meta name="twitter:image" content="https://cruiselog.kr/og-image.png" />
<link rel="canonical" href="https://cruiselog.kr/" />

<!-- Vercel 사용 시 → -->
<meta property="og:url" content="https://cruiselog.vercel.app/" />
<meta property="og:image" content="https://cruiselog.vercel.app/og-image.png" />
<meta name="twitter:url" content="https://cruiselog.vercel.app/" />
<meta name="twitter:image" content="https://cruiselog.vercel.app/og-image.png" />
<link rel="canonical" href="https://cruiselog.vercel.app/" />
```

---

## ✅ OG 미리보기 검증

배포 후 카카오톡/페북에서 제대로 보이는지 확인:

| 도구 | URL |
|---|---|
| **Facebook Debugger** | https://developers.facebook.com/tools/debug/ |
| **Twitter Card Validator** | https://cards-dev.twitter.com/validator |
| **카카오톡 디버거** | https://developers.kakao.com/tool/debugger/sharing |
| **LinkedIn Post Inspector** | https://www.linkedin.com/post-inspector/ |
| **종합 OG 검증** | https://www.opengraph.xyz/ |

각 도구에 배포된 URL 입력 → "Scrape Again" → 미리보기 확인.

---

## 🎨 도메인 연결 (선택)

`cruiselog.kr` 도메인 구입하면:

1. **가비아 / 후이즈 / Namecheap** 에서 `cruiselog.kr` 구입 (연 1~2만원)
2. Vercel 대시보드 → Settings → Domains → Add
3. DNS 설정 (Vercel이 안내):
   - `A` 레코드: `76.76.21.21`
   - `CNAME` 레코드: `cname.vercel-dns.com`
4. 30분~24시간 후 활성화

도메인 사기 전엔 `cruiselog.vercel.app` 그대로 써도 OK.

---

## 📊 배포 후 체크리스트

- [ ] 사이트 접속 확인 (https://cruiselog.vercel.app)
- [ ] 모바일에서도 확인 (반응형 디자인)
- [ ] OG 이미지 카카오톡 디버거로 검증
- [ ] 7개 채널 링크 전부 클릭 테스트
- [ ] index.html 의 OG 메타 태그 도메인 변경 완료
- [ ] Google Search Console 에 사이트 등록 (https://search.google.com/search-console)
- [ ] Naver Search Advisor 에 사이트 등록 (https://searchadvisor.naver.com/)
- [ ] sitemap.xml 생성 후 제출 (선택)

---

## 🎯 추천 우선순위

1. **지금 당장**: Vercel에 5분 배포 → 링크 발급
2. **오늘 안에**: OG 이미지 생성 + 메타 태그 도메인 수정 + 재배포
3. **이번 주 안에**: OG 검증 도구로 카카오톡 미리보기 확인
4. **선택**: 도메인 cruiselog.kr 구매 + 연결

배포 막히면 단계별로 도와드릴 수 있어요.
