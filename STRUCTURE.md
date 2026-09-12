# 사이트 구조 (포트폴리오/자기소개, 순수 HTML/CSS/JS)

빌드 도구·프레임워크 없이 브라우저에서 바로 여는 정적 다중 페이지 사이트.
이 저장소(`my-project`)를 그대로 확장해서 만든다 — 새 저장소를 따로 만들지 않고
기존 `index.html`/`style.css`(자기소개 랜딩페이지)를 이 구조에 맞게 다듬고
`about.html`/`projects.html`/`contact.html`을 추가하는 방식. 이미 Public +
GitHub Pages가 연결돼 있어서(https://whatsso12-code.github.io/my-project/),
`main` 브랜치에 push만 하면 자동으로 재배포된다.

## 사이트맵

| 페이지 | 파일 | 목적 |
|---|---|---|
| 홈 | `index.html` | 첫인상 — 이름/한줄소개 + 하이라이트, 다른 페이지로 유도 |
| 소개 | `about.html` | 자기소개, 경력/스킬 |
| 프로젝트 | `projects.html` | 작업물/프로젝트 목록 (카드 형태) |
| 연락처 | `contact.html` | 이메일/소셜 링크, (선택) 연락 폼 |

페이지가 늘어나면 이 표에 행만 추가하고, 아래 폴더 구조 규칙을 그대로 따르면 됨.

## 폴더 구조

```
my-project/                (저장소 루트)
├── index.html
├── about.html
├── projects.html
├── contact.html
├── css/
│   └── style.css        # 전체 공통 스타일 (:root 변수 + 페이지별 섹션)
├── js/
│   └── main.js           # 공통 스크립트 (모바일 메뉴 토글 등)
└── assets/
    └── images/           # 사진/아이콘 등 이미지 리소스
```

- CSS/JS는 파일 하나씩만 두고 모든 페이지가 공유 (페이지별로 CSS/JS를 쪼개야 할 만큼 커지면 그때 나눈다 — 지금은 과설계 방지)
- 이미지는 전부 `assets/images/` 아래에 모아서 경로 혼선을 방지

## 모든 페이지가 공유하는 레이아웃

각 `.html` 파일은 아래 뼈대를 반복한다 (프레임워크가 없으니 네비게이션 마크업은 각 파일에 중복 — 페이지 4개 수준에서는 이게 오히려 제일 단순함):

```html
<header class="site-header">
  <nav>
    <a href="index.html">홈</a>
    <a href="about.html">소개</a>
    <a href="projects.html">프로젝트</a>
    <a href="contact.html">연락처</a>
  </nav>
</header>

<main><!-- 페이지별 내용 --></main>

<footer class="site-footer">...</footer>
```

- 현재 페이지의 네비게이션 링크에는 `class="active"`를 붙여서 어디에 있는지 표시
- `css/style.css`의 `.site-header`, `.site-footer`, `nav` 규칙이 모든 페이지에 동일하게 적용됨

## CSS 설계 방향

- `style.css` 최상단 `:root`에 색상/폰트크기/여백을 변수로 모아둔다 (이전 `extract-config-vars` 스킬과 같은 원칙) — 톤을 바꿀 때 변수 몇 개만 수정하면 되게
- 모바일 폭(480px 이하) 기준 반응형 — `my-project`에서 쓴 것과 같은 패턴 재사용

## JS 사용 범위

빌드 도구 없이 `<script src="js/main.js">`만 사용. 지금 필요한 범위는:
- 화면 좁을 때 네비게이션 토글(햄버거 메뉴) — 필요해지면 추가, 페이지 수가 적을 땐 생략 가능
- 그 이상의 상태 관리/라우팅은 안 함 (정적 다중 페이지 방식이라 불필요)

## 다음 단계

이 구조대로 `index.html`부터 실제 마크업/스타일 작업 시작. 페이지가 늘거나 섹션이 바뀌면 이 문서를 먼저 갱신하고 코드를 맞춘다.
