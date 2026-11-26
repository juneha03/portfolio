# DESIGN — 이준하 포트폴리오 디자인 규칙

> ⚠ 작업 시작 시점에 이 폴더에는 `DESIGN.md`가 **없었다**. 그래서 §1~§6 '기존 디자인 규칙'은 새로 지어낸 것이 아니라,
> 레퍼런스 측정 기록 `research/tokens-and-motion.md`와 `index.html`의 원본 스타일시트를 **그대로 옮겨 적은 것**이다.
> 원래 쓰던 DESIGN.md가 따로 있다면 [확인 필요] — 그 파일의 §1~§6을 우선하고, 이 파일의 §7(추가분)만 붙인다.
>
> 규칙: §1~§6은 **고치지 않는다**. 새 섹션 · 컴포넌트는 §7에만 더한다.

---

## 1. 색 토큰 (`:root`) — 기존

| 토큰 | 값 | 쓰임 |
|---|---|---|
| `--bg` | `#07111f` | 페이지 배경 |
| `--text` | `#e9f2ff` | 본문 · 제목 |
| `--text-soft` | `#a8bbd1` | 보조 글 · eyebrow |
| `--text-dim` | `#7188a2` | 캡션 |
| `--accent` | `#91d5ff` | 마침표 · 번호 · 화살표 · 밑줄 |
| `--accent-strong` | `#b7e5ff` | 포커스 링 · 강조 기술 |
| `--header-ink` | `#ffffff` | 헤더 메뉴 |
| `--gutter` | `clamp(1.1rem, 4.25vw, 4.75rem)` | 좌우 여백 |

리터럴 색(원본 그대로): `#b7c9de` 키커, `#64809e` 슬래시, `#c5d6e9` 히어로 요약, `#dcecff`/`#7790aa` 매니페스토 글/흐린 단어, `#aec1d6` 카드 본문, `#748ba5` 푸터 라벨, `#b8c9dd` 푸터 링크 등.

## 2. 글꼴 — 기존

- 본문: **Manrope Variable** (200–800), 기본 굵기 350
- 제목(display): **Space Grotesk Variable** (300–700)
- 한글은 두 글꼴에 글리프가 없어 시스템 산세리프(맑은 고딕 · Apple SD 고딕 등)로 대체되어 표시된다.

## 3. 글자 크기 (@1440) — 기존

| 요소 | 값 |
|---|---|
| hero-title | `clamp(1.8rem,3.2vw,3.8rem)` / lh .97 / ls −.075em / w500 / 대문자 |
| manifesto-copy | `clamp(1.55rem,2.75vw,3.3rem)` / lh 1.16 / ls −.05em / w350 |
| process h3 | `clamp(3.2rem,4.65vw,5.7rem)` / w380 |
| section-title | `clamp(3.8rem,6.7vw,7.3rem)` / w370 / ls −.08em |
| service h3 | `clamp(2rem,3.2vw,4rem)` |
| closing-copy | `clamp(2rem,3.8vw,4.4rem)` / lh 1.13 |
| contact h2 | `clamp(3.15rem,6.25vw,7rem)` / lh .97 / ls −.075em |
| eyebrow | `clamp(.55rem,.67vw,.68rem)` / w550 / ls .105em / 대문자 |

## 4. 레이아웃 — 기존

- 섹션 순서 골격: Hero → Manifesto → Process(3 패널, 좌·우·좌) → Services(3카드, 데스크톱 고정 핀) → Skills(2단 그리드) → Closing manifesto → Contact footer
- 브레이크포인트: `1600 / 900 / 760 / 640 / 370px`
- 모바일(≤640): `--gutter: 1.1rem`, 그리드는 1단, 카드 너비 72~80%

## 5. 움직임 — 기존 (값 변경 금지)

| 대상 | 규칙 |
|---|---|
| 부드러운 스크롤 | Lenis duration 1.15, `t => min(1, 1.001 − 2^(−10t))`, wheelMultiplier .5 |
| 로더 | 진행 .45s power2.out → 페이드 1.1s power2.inOut |
| 히어로 등장 | `.hero-char` 글자별 opacity·blur(1.1px) 2s sine.out, 무작위 stagger 1.2 / `[data-hero-reveal]` y10, 1.05s |
| 헤더 | 아래로 스크롤(>100px) 시 숨김, 위로 스크롤 시 표시 (.9s) |
| `[data-section-kicker]` | y7 · opacity .58 · 자간 .17em → 원래값, 1.2s, 화면 90% 지점 1회 |
| `[data-rise]` | y15 · opacity 0 → 1, 1.05s power2.out, 88% 지점 1회 |
| `[data-scroll-words]` | 단어별 색·opacity 스크럽 (매니페스토 stagger .018 / 클로징 .012) |
| `[data-blur-reveal]` | blur 12 → 0, #services 85%→25% 스크럽 |
| 서비스 카드 | 데스크톱 핀(1.8×vh) 동안 순서대로 등장 / 모바일은 개별 등장 |
| 메뉴 클릭 | 잉크 원 전환 1.4s, 0.7s에 점프 |
| 커서 글로우 | 단색 배경 섹션에서 반경 그라디언트가 커서를 따라옴 (τ 190/380ms) |
| 감속 모드 | `prefers-reduced-motion`이면 모든 애니메이션 끔 |

## 6. 공통 컴포넌트 — 기존

`eyebrow` + `eyebrow-rule`(점) · `accent-period`(제목 끝 파란 마침표) · `text-link`(작은 대문자 링크 + ↗) · `service-card`(번호 · 유형 · h3 · 본문 · `service-link`) · `phase-tags`(슬래시로 구분한 태그) · `skill-group` · `contact-cta`(밑줄이 늘어나는 링크) · `footer-label`.

---

## 7. 추가 섹션 · 컴포넌트 (2026-11-26, 이준하 내용으로 교체하며 추가)

> 원칙: **새 색 · 새 글꼴 · 새 애니메이션을 만들지 않는다.** 아래는 모두 §1~§6의 토큰과 클래스를 재사용한다.
> CSS 위치: `index.html` `<style>` 맨 아래 `/* ===== portfolio additions ===== */` 블록.

### 7-1. 메뉴 6개로 확장

| 메뉴 | 연결 | 섹션 |
|---|---|---|
| Home | `#home` | Hero |
| About | `#manifesto` | 소개 + 인물 사진 |
| Process | `#process` | 일하는 방식 3단계 |
| Focus | `#services` | 관심 분야 3카드 (id는 JS 핀 로직 때문에 `services` 유지) |
| **Work** (신규) | `#work` | 대표 프로젝트 |
| Contact | `#contact` | 푸터 |

- 활성 메뉴 감지(IntersectionObserver) 목록에 `work` 추가.
- 375px 폭에서 메뉴 전체 폭 345px — 가로 넘침 없음.

### 7-2. 섹션 순서 (변경 후)

Hero → About(01) → Process(02) → Focus(03) → **Work(04, 신규)** → Skills(05) → Closing(06) → Contact(07)

### 7-3. `.about-portrait` — About 인물 사진 (신규 컴포넌트)

| 속성 | 값 |
|---|---|
| 위치 | `.manifesto-main` 안, `manifesto-foot` 아래 |
| 너비 | `clamp(6.5rem, 9vw, 9.5rem)` / 모바일 6rem |
| 이미지 | `images/profile.jpg` (1080×1376), `aspect-ratio:1080/1376`, `object-fit:cover`, `loading="lazy"` |
| 캡션 | `figcaption` — `--text-dim`, .55rem, w550, ls .12em (manifesto-foot와 같은 규칙) |
| 움직임 | `data-rise` (기존 §5 규칙) |

### 7-4. `.work-section` — 대표 프로젝트 섹션 (신규 섹션)

| 속성 | 값 |
|---|---|
| 그리드 | `.skills-section`과 동일: `minmax(0,31vw) minmax(0,39vw)`, gap 4vw, padding 12vh/15vh, 배경 `--bg` |
| 왼쪽 `.work-intro` | eyebrow 키커 `04 / FEATURED PROJECT` + `section-title` "Work." + `.work-intro-copy`(= skills-intro-copy 규칙) |
| 오른쪽 `.work-card` | `.service-card` 재사용 (번호 `P-1`, 유형 `AI TAROT · WEB APP`, h3, 본문) |
| 커서 글로우 | `.work-section:before` — services/skills/closing과 같은 그라디언트, JS `solid` 목록에 추가 |
| 반응형 | ≤900: `34vw / 42vw` · ≤640: 1단, 카드 너비 88% 오른쪽 정렬 |
| 움직임 | 제목 · 소개 · 카드 모두 `data-rise`, 키커는 `data-section-kicker` |

### 7-5. `.work-meta` — 프로젝트 정보 목록 (신규 컴포넌트)

- `<dl>` 2단 그리드(`auto | 1fr`), 위쪽 1px 선 `#a8bbd126`
- `dt` = `footer-label` 규칙(#748ba5, .53rem, w600, ls .1em) — FLOW / PRIVACY / DOCS / BUILT WITH
- `dd` = 푸터 링크 색 `#b8c9dd`, .78rem (모바일 .7rem)

### 7-6. `.work-links` — 카드 하단 링크 묶음

- `service-link` 2개를 가로로 (gap 2.2rem, 줄바꿈 허용)
- 외부 링크(배포 사이트)는 `target="_blank" rel="noopener noreferrer"`

### 7-7. `.footer-email-pending` — 연락처 자리표시

- 공개 이메일이 [확인 필요]라서 링크 대신 글자만 표시. 글자 규칙은 `.footer-email>a`와 같다.
- 이메일이 정해지면 `<a href="mailto:…">`로 바꾸고 이 클래스는 지운다.

### 7-8. 한글 줄바꿈

- `html:lang(ko){word-break:keep-all; overflow-wrap:break-word}` — 어절 가운데서 줄이 끊기지 않게. 글꼴 · 크기 · 색은 그대로.

### 7-9. 에셋 경로

| 에셋 | 이전 | 이후 |
|---|---|---|
| 하늘 텍스처 | `oussamaaz.dev/textures/milky8.webp` | `images/milky8.webp` (같은 파일 로컬 사본) |
| 파비콘 | 레퍼런스 사이트 favicon.ico | 인라인 SVG "J" (`--bg` 배경, `--text` 글자, `--accent` 점) |
| 글꼴 · 배경 사운드 | 레퍼런스 사이트 주소 | **그대로** (REVIEW.md 참고, [확인 필요]) |
