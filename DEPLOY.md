# 배포 및 수정 가이드

정적 HTML/CSS/JS 사이트. 빌드 도구·프레임워크·서버 없음. 파일을 그대로 GitHub에 올리면 끝.

---

## 1. 배포 (10분)

1. GitHub에서 새 저장소 생성 → 이름 **`Intro_YSH`**, Public
2. 이 폴더의 **내용물 전체**를 저장소 루트에 업로드
   (`index.html`이 저장소 최상단에 있어야 함. 폴더째 넣으면 주소가 한 단계 깊어짐)
3. 저장소 → **Settings → Pages**
   - Source: `Deploy from a branch`
   - Branch: `main` / `(root)` → **Save**
4. 1~2분 뒤 공개: **https://yang-soohyun.github.io/Intro_YSH/**

수정할 때는 파일 고쳐서 다시 push하면 30초~1분 내 반영된다.

### 저장소 이름을 바꾸고 싶다면
주소가 바뀌므로 `index.html`을 포함한 **9개 html 파일의 `<link rel="canonical">`·`og:url`·`og:image`**,
그리고 `sitemap.xml`, `robots.txt` 안의 URL을 새 주소로 바꿔야 한다.

> 저장소 이름을 **`yang-soohyun.github.io`** 로 만들면 주소가
> `https://yang-soohyun.github.io/` 로 짧아진다 (계정당 1개만 가능).

---

## 2. 로컬에서 미리보기

VS Code + **Live Server** 확장이 가장 쉽다. 또는:

```bash
cd Intro_YSH
python3 -m http.server 8000
# 브라우저에서 http://localhost:8000
```

---

## 3. 구조

```
index.html          홈 — 소개, 01 Research Interests, 02 Education, 03 News, 04 Selected Publications
vision.html         Pixel to Planet 철학 (3단계)
research.html       연구 4개 주제 + GLCD250-MOD 지표
publications.html   저널 논문
talks.html          학회 발표 11건
projects.html       수행 과제 9건
teaching.html       조교·멘토링
honors.html         수상·장학
others.html         스킬, 언어, 활동
css/style.css       스타일 전체 (색·폰트는 파일 상단 :root 변수에서 한 번에 조절)
js/main.js          모바일 메뉴 토글
figures/            사진, 로고, 파비콘, OG 이미지
assets/             공개용 CV (References 페이지 제외본)
sitemap.xml         검색엔진용
.nojekyll           GitHub Pages가 Jekyll 처리를 건너뛰게 함
```

---

## 4. 자주 하는 수정

### News 항목 추가
`index.html`의 `<ul class="news">` 맨 위에 블록 하나를 복사해 넣는다:

```html
<li>
  <span class="news__date">Oct 2026</span>
  <div class="news__body">
    <strong>제목 한 줄</strong>
    <span>부연 설명 · 저널명 · 역할</span>
  </div>
</li>
```

### 논문 추가
`publications.html`의 `<ol class="pubs">` 안에 항목을 복사해 넣고,
본인 이름은 `<span class="me">Yang, S.</span>`, 저널명은 `<span class="venue">…</span>` 로 감싼다.
상태 뱃지: `<span class="chip chip--review">In review</span>`, 링크 뱃지: `<a class="chip" href="…">DOI</a>`

### 색 바꾸기
`css/style.css` 최상단 `:root`의 `--brand` 값 하나만 바꾸면 사이트 전체 강조색이 바뀐다.
현재 값 `#014195` 는 서울시립대 엠블럼에서 추출한 파랑.

### CV 교체
`assets/` 에 새 PDF를 넣고, 9개 html의 CV 링크 경로를 새 파일명으로 바꾼다
(`grep -rn "CV_SooHyun" *.html` 로 위치 확인).

---

## 5. 남은 TODO

- [ ] `index.html` News의 IWA 항목 — 날짜가 `2026` 으로만 되어 있음. 학회 월 확정되면 `Aug 2026` 형식으로 교체 (해당 줄에 주석 표시해 둠)
- [ ] `others.html` 하단의 Military Service 블록은 주석 처리되어 있음. 넣으려면 `<!-- -->` 제거
- [ ] Google Scholar 프로필 ID 최종 확인 — 현재 `oVDOTsUAAAAJ`
- [ ] LinkedIn 계정이 있다면 `index.html` 의 `<ul class="social">` 에 항목 추가

---

## 6. 참고

- **공개용 CV**: REFERENCES 부분만 제거한 4쪽본이 들어 있다 (군복무 항목은 유지).
  교수님 6분의 개인 이메일·직통 전화번호가 담긴 페이지라 웹 공개 대상이 아니다.
  PDF 작성자 메타데이터도 함께 정리했다.
- 폰트는 Google Fonts CDN(Newsreader / Inter / IBM Plex Mono)에서 불러온다. 오프라인에선 시스템 폰트로 대체된다.
