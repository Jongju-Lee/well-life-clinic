# 🏥 웰라이프내과의원 - 의료기관 웹사이트
> 서울특별시 광진구에 위치한 호흡기내과 전문 클리닉 '웰라이프내과의원'의 반응형 웹사이트입니다.

🔗 **[웹사이트 바로가기 (Live Demo)](https://well-life-clinic.vercel.app/)**

---

## 👨‍💻 프로젝트 소개
2년 차 프론트엔드 퍼블리셔로서 실무 수준의 마크업 역량을 보여주기 위해 제작한 포트폴리오 프로젝트입니다.

가상의 내과 전문 클리닉을 주제로, 기획부터 디자인 시스템 설계, 퍼블리싱, 인터랙션 구현까지 전 과정을 직접 수행했습니다.

### 프로젝트 범위
| 구분 | 내용 |
|---|---|
| **페이지** | 메인 페이지(8개 섹션), 상담 및 예약 페이지 |
| **반응형** | 데스크탑(1280px 이상) · 태블릿(768px~1279px) · 모바일(767px 이하) 브레이크포인트 적용 |
| **기능** | 다크모드, 스크롤 애니메이션, 슬라이더, 캘린더 예약 폼, 폼 유효성 검증 |
| **기간** | 약 2주(하루 8시간 1인 작업) |

---

## 💡 핵심 구현 사항

### 1. CSS 변수 기반 디자인 시스템 설계
- **중앙 집중형 스타일 관리:** 컬러, 스페이싱(4px 단위), 타이포그래피, 레이아웃 등 100개 이상의 디자인 토큰을 `variables.css`에 CSS Custom Properties로 정의하여 전체 UI의 일관성을 유지했습니다. (👉 [코드 보기](css/common/variables.css))
- **Typography Scale:** Perfect Fourth(1.333배) 비율을 적용한 6단계 폰트 사이즈 시스템을 구성하고, 한글(SC-Dream) · 영문(Montserrat) · 숫자(GmarketSans)를 용도별로 분리 적용했습니다. 모든 `@font-face`에 `font-display: swap`을 설정하여 웹폰트 로딩 전 텍스트가 보이지 않는 FOIT 현상을 방지했습니다.
- **다크모드 연동:** `[data-theme='dark']` 선택자 하나로 배경, 텍스트, 테두리, 그림자 등의 색상 변수를 일괄 오버라이드하여 별도 CSS 파일 없이 다크모드를 구현했습니다. `localStorage`로 설정을 유지하고, 첫 방문 시에는 `prefers-color-scheme`으로 OS 다크모드 설정을 자동 감지합니다.

### 2. 웹 접근성(KWCAG) 지침을 고려한 시맨틱 마크업
- **문서 구조:** `<header>`, `<main>`, `<section>`, `<article>`, `<footer>` 등 시맨틱 태그로 문서 영역을 구분하고, ARIA landmark role(`banner`, `main`, `contentinfo`)을 명시했습니다.
- **키보드 접근성:** 스킵 네비게이션(`본문으로 바로가기`)을 제공하고, `:focus-visible` 선택자를 활용하여 키보드 탐색 시에만 포커스 아웃라인을 표시합니다.
- **스크린 리더 대응:** 모든 이미지에 의미를 담은 `alt` 텍스트를 작성하고, 장식적 요소는 `aria-hidden="true"` 처리했습니다. 아이콘 버튼에는 `aria-label`을, 그룹 입력 필드에는 `aria-labelledby`를 부여했습니다.

### 3. 3단 반응형 레이아웃
- **브레이크포인트 설계:** 1280px(태블릿), 768px(모바일), 480px(소형 모바일) 기준으로 레이아웃·폰트·여백 등의 CSS 변수를 재정의하여 자연스러운 화면 전환을 구현했습니다.
- **모바일 뷰포트 대응:** `100dvh`를 적용하여 모바일 브라우저의 주소창 높이 변화에 대응하고, 히어로 섹션이 항상 화면 전체를 채우도록 처리했습니다.
- **디바이스별 UI 분기:** PC에서는 그리드 레이아웃으로 진료과목을 배치하고, 태블릿·모바일에서는 Swiper 슬라이더로 전환하여 터치 환경에 최적화했습니다.

### 4. Vanilla JS 인터랙션 구현
- **스크롤 애니메이션:** `IntersectionObserver`를 활용하여 요소가 뷰포트에 진입할 때 fade-up/fade-down 애니메이션을 실행합니다. `data-anim`, `data-anim-duration`, `data-anim-delay` 속성으로 HTML에서 직접 제어할 수 있도록 설계했습니다.
- **카운트업 애니메이션:** `requestAnimationFrame`과 `easeOutQuad` 이징 함수를 적용한 숫자 카운트업을 구현하여, 통계 수치에 시각적 임팩트를 부여했습니다.
- **진료 예약 캘린더:** 외부 라이브러리 없이 순수 JavaScript로 캘린더를 직접 구현했습니다. 6주 × 7일 고정 그리드 렌더링, 과거 날짜·일요일 비활성화, 3개월 범위 제한, 당일 자동 선택까지 실제 예약 시스템에서 필요한 UX 흐름을 모두 포함합니다.
- **폼 유효성 검증:** 제출 시 전체 필드를 한 번에 검증하고 첫 번째 에러 위치로 자동 스크롤·포커스 처리합니다. 이름(2자 이상), 전화번호(정규식), 주민등록번호(형식 체크), 진료과목, 동의 체크박스를 각각 검증하며, 입력 즉시 에러 상태가 해제되는 UX를 적용했습니다.

### 5. 컴포넌트 분리 및 재사용 구조
- **Include 시스템:** Fetch API를 이용하여 Header, Sidebar, Footer를 별도 HTML 파일로 분리하고 동적으로 로드하는 구조를 적용했습니다. 페이지가 추가되어도 공통 영역의 수정 포인트가 한 곳으로 유지됩니다.
- **CSS 파일 구조:** `common/`(공통) → `pages/`(페이지별)로 스타일시트를 분리하고, variables · reset · font · common · responsive 순서로 계층화했습니다.

### 6. SEO 및 성능 최적화
- **메타 태그 및 Open Graph:** `description`, `keywords`, Open Graph(`og:title` · `og:description` · `og:image` · `og:locale`), `canonical`, `theme-color`, favicon, `apple-touch-icon`을 작성하여 검색 노출과 소셜 공유 시 링크 미리보기를 대응했습니다.
- **이미지 최적화:** 전체 이미지를 WebP 포맷으로 변환하고 `<img loading="lazy">`를 적용하여 초기 로딩 시 불필요한 이미지 요청을 줄였습니다.
- **리소스 로딩 최적화:** 외부 CDN에 `<link rel="preconnect">`를 선언하여 DNS 조회 시간을 단축하고, 모든 `<script>`에 `defer` 속성을 부여하여 HTML 파싱을 차단하지 않도록 처리했습니다.

---

## 🛠 사용 기술 (Tech Stack)

### Markup & Styling
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)

### Interaction
![JavaScript](https://img.shields.io/badge/JavaScript_(ES6+)-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Swiper](https://img.shields.io/badge/Swiper.js_11-6332F6?style=for-the-badge&logo=swiper&logoColor=white)

### Deployment & Tooling
![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)
![Git](https://img.shields.io/badge/GIT-E44C30?style=for-the-badge&logo=git&logoColor=white)

---

## 📁 폴더 구조

```
well-life/
├── index.html                          # 메인 페이지
├── pages/
│   └── appointment.html                # 상담 및 예약 페이지
├── includes/                           # 공통 컴포넌트 (Fetch로 동적 로드)
│   ├── header.html
│   ├── sidebar.html
│   └── footer.html
├── css/
│   ├── common/                         # 공통 스타일
│   │   ├── variables.css               # 디자인 토큰 (100+ CSS 변수)
│   │   ├── reset.css                   # HTML 초기화
│   │   ├── font.css                    # 웹폰트 정의
│   │   ├── common.css                  # 공통 컴포넌트 스타일
│   │   └── common-responsive.css       # 공통 반응형
│   └── pages/                          # 페이지별 스타일
│       ├── main-page/
│       └── appointment/
├── js/
│   ├── includes.js                     # 컴포넌트 로드 로직
│   ├── common.js                       # 다크모드, 애니메이션, Swiper
│   └── appointment.js                  # 캘린더, 폼 검증
├── font/                               # 로컬 웹폰트 (SC-Dream, Montserrat 등)
├── images/                             # WebP 포맷 이미지
└── mockup/                             # 태블릿·모바일 목업 참고 파일
```

---

## ⚙️ 로컬 실행 방법
별도 빌드 도구 없이 정적 HTML/CSS/JS로 구성되어 있습니다.

```bash
# 로컬 서버로 실행 (VS Code Live Server 등)
# index.html을 브라우저에서 열어 확인
```

---

## 📐 페이지 구성

### 메인 페이지 (`index.html`)
| 섹션 | 설명 |
|---|---|
| Hero | 전체 화면 배경 + 뱃지 + 카운트업 통계 (Glassmorphism 효과) |
| Intro | 병원 소개 + 진료 특징 3종 (이미지 교차 레이아웃) |
| Why | 병원 선택 이유 + 해시태그 뱃지 |
| Doctor | 의료진 소개 + 경력·학력·저서 정보 |
| Disease | 호흡기 대표질환 8종 아이콘 카드 + 검사항목 4종 |
| Subject | 진료과목 6종 (PC: 그리드 / 모바일: Swiper 슬라이더) |
| Gallery | 시설 둘러보기 (Swiper 루프 슬라이더 + 프로그레스 바) |
| Info & Direction | 진료시간·연락처 안내 + 오시는 길 지도 |

### 상담 및 예약 페이지 (`pages/appointment.html`)
- 커스텀 캘린더 (날짜 선택, 과거 날짜·일요일 비활성화, 3개월 제한)
- 시간대 선택 (오전 시간대 비활성화, 자동 선택)
- 환자 정보 입력 (이름, 주민등록번호, 전화번호, 진료과목)
- 실시간 유효성 검증 + 에러 위치 자동 스크롤
