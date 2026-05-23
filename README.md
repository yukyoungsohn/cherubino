# Cherubino — GitHub Pages 이전 가이드

## 파일 구조
```
cherubino/
├── index.html       ← 메인 (4개 페이지 모두 포함)
├── css/
│   └── style.css
└── images/          ← Wix에서 저장한 이미지를 여기에
```

---

## 1단계 — GitHub 저장소 만들기

1. https://github.com 로그인
2. 우상단 [+] → **New repository**
3. Repository name: `cherubino` (또는 원하는 이름)
4. **Public** 선택 (GitHub Pages 무료 사용)
5. **Create repository** 클릭

---

## 2단계 — 파일 올리기

```bash
# 터미널에서 (Git 설치 필요)
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/cherubino.git
git push -u origin main
```

또는 GitHub 웹사이트에서 직접 파일 드래그&드롭도 가능해요.

---

## 3단계 — GitHub Pages 활성화

1. 저장소 → **Settings** 탭
2. 좌측 메뉴 **Pages**
3. Source: **Deploy from a branch**
4. Branch: `main` / `/ (root)`
5. **Save** 클릭
6. 약 1~2분 후 `https://YOUR_USERNAME.github.io/cherubino` 접속 가능

---

## 4단계 — Disqus 연동

1. https://disqus.com 가입
2. **Create a new site** → shortname 설정 (예: `cherubino-net`)
3. `index.html` 에서 아래 부분 교체:
   ```js
   s.src = 'https://YOUR_DISQUS_SHORTNAME.disqus.com/embed.js';
   ```
   → `YOUR_DISQUS_SHORTNAME` 자리에 본인 shortname 입력

---

## 5단계 — Wix 이미지 저장

Wix 이미지들은 `wixstatic.com`에 있어서 Wix 해지 후 사라져요.
지금 아래 URL들을 브라우저에서 열어 **이미지로 저장**해두세요:

- 편지 배경: `https://static.wixstatic.com/media/8e7785_c3b07adc284b46dd8fe36a6d06dc616e~mv2.png`
- Spring Edition 이미지: `https://static.wixstatic.com/media/8e7785_d7a4e01e67d1454eb32fb8980c74ef83~mv2.jpg`
- 소식 첨부 이미지들 (PNG 파일)

저장 후 `images/` 폴더에 넣고 `index.html`에서 경로 수정:
```html
<img src="images/letter-bg.png" alt="" class="letter-image" />
```

---

## 6단계 — 커스텀 도메인 연결 (cherubino.net)

### Wix에서 도메인 이전 신청
1. Wix 대시보드 → 도메인 관리
2. **Transfer domain** (도메인 이전) 선택
3. 이전할 레지스트라 선택 (Namecheap 추천)
4. 이전 완료까지 5~7일 소요

### GitHub Pages에 도메인 연결
1. 저장소 → Settings → Pages → **Custom domain**
2. `cherubino.net` 입력 후 Save
3. 저장소 루트에 `CNAME` 파일 생성:
   ```
   cherubino.net
   ```
4. 도메인 레지스트라에서 DNS 설정:
   ```
   A 레코드 4개 추가:
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153

   CNAME 레코드:
   www → YOUR_USERNAME.github.io
   ```

---

## 7단계 — Wix 해지

도메인 이전 완료 + GitHub Pages 정상 작동 확인 후:
- Wix 대시보드 → 계정 설정 → **Cancel subscription**
- ⚠️ 도메인 이전 전에 해지하면 도메인도 사라질 수 있어요!

---

## 소식 페이지 — 새 글 추가하는 법

`index.html`에서 `<div class="news-thread">` 안에 아래 형식으로 추가:

```html
<article class="news-post">
  <div class="news-meta">
    <span class="news-author">작성자 이름</span>
    <span class="news-date">날짜</span>
  </div>
  <div class="news-body">
    <p>내용...</p>
  </div>
</article>
```

음악 감상실에 곡 추가하려면 `<div class="music-grid">` 안에:

```html
<div class="music-card">
  <img class="music-thumb"
    src="https://i.ytimg.com/vi/유튜브ID/hqdefault.jpg"
    alt="곡 제목" loading="lazy" />
  <div class="music-card-body">
    <p class="music-card-title">작곡가 — 곡 제목</p>
    <a class="music-card-link"
      href="https://www.youtube.com/watch?v=유튜브ID"
      target="_blank" rel="noopener">
      ▶ 감상하기
    </a>
  </div>
</div>
```
