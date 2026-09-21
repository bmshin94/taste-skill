# Taste Skill 전수조사 & 활용 전략 정리 (한국어)

> 이 문서는 `taste-skill` 레포지토리를 전수조사하고 나눈 대화를 정리한 기록입니다.
> 분석 대상 폴더 전체(`skills/`, `research/`, `.claude-plugin/`, `.github/`, `scripts/`)를 직접 확인한 결과를 담았습니다.

## 저장소 주소

- 원본: https://github.com/Leonxlnx/taste-skill
- 포크(본 저장소): https://github.com/bmshin94/taste-skill
- 공식 사이트: https://tasteskill.dev
- 라이선스: MIT (Copyright (c) 2026 Leonxlnx)

---

## 목차

1. [이게 뭐하는 프로젝트인가](#1-이게-뭐하는-프로젝트인가)
2. [쉽게 다시 설명](#2-쉽게-다시-설명)
3. [질문 7가지 정밀 답변](#3-질문-7가지-정밀-답변)
4. [수익화 아이디어](#4-수익화-아이디어)
5. [핵심 요약 카드](#5-핵심-요약-카드)

---

## 1. 이게 뭐하는 프로젝트인가

### 한 줄 정의

**AI가 만든 웹 UI가 촌스러워지는 현상(AI slop)을 막는, 마크다운 기반 디자인 지침서 모음집.**

코드 라이브러리가 아니다. 설치해도 실행되는 패키지는 없다. 실체는 `SKILL.md` 텍스트 파일 13개다.

### 실제 폴더 구조

```
taste-skill/
├── skills/                          # 핵심. 여기가 제품 그 자체
│   ├── taste-skill/SKILL.md              (1,206줄)  메인 v2 experimental
│   ├── taste-skill-v1/SKILL.md           (226줄)    구버전 보존
│   ├── gpt-tasteskill/SKILL.md           (74줄)     GPT/Codex 전용
│   ├── image-to-code-skill/SKILL.md      (1,228줄)
│   ├── imagegen-frontend-web/SKILL.md    (987줄)
│   ├── imagegen-frontend-mobile/SKILL.md (1,465줄)
│   ├── brandkit/SKILL.md                 (798줄)
│   ├── redesign-skill/SKILL.md           (178줄)
│   ├── soft-skill/SKILL.md               (98줄)
│   ├── minimalist-skill/SKILL.md         (85줄)
│   ├── brutalist-skill/SKILL.md          (92줄)
│   ├── output-skill/SKILL.md             (49줄)
│   ├── stitch-skill/SKILL.md + DESIGN.md
│   └── llms.txt                          스킬 목록 색인(AI가 읽는 요약)
├── .claude-plugin/
│   ├── plugin.json                       Claude Code 플러그인 메타
│   └── marketplace.json                  Claude Code 마켓플레이스 등록
├── .github/
│   ├── copilot-instructions.md           GitHub Copilot 전역 규칙
│   └── FUNDING.yml                       후원 링크
├── research/laziness/                    "LLM은 왜 게으른가" 연구 자료
│   ├── root-causes/      (4개 문서)
│   ├── remediation/      (4개 문서)
│   └── findings/         (2개 문서)
├── scripts/                              스폰서 로고 webp 변환 유틸(.mjs)
├── assets/ · examples/                   README 이미지, 결과물 샘플
├── skill.sh                              스킬 경로 조회 bash 헬퍼
└── README.md · CHANGELOG.md · LICENSE · CLAUDE.md
```

전체 마크다운 약 6,927줄. 실행 코드는 메인테이너용 이미지 변환 스크립트 4개뿐이다.

### 해결하려는 문제 — "AI slop"

| AI의 고질적 기본값 | 원인 |
| --- | --- |
| 폰트는 무조건 `Inter` | 학습 데이터 최빈값 |
| 아이콘은 무조건 `Lucide` | 위와 동일 |
| 가운데정렬 히어로 → 3칸 카드 그리드 → FAQ | 통계적 최다 패턴 |
| `shadow-lg` 남용, 보라-핑크 그라데이션 | 프레임워크 기본값 |
| "Elevate", "Seamless", "Next-Gen" 카피 | AI 클리셰 |
| em-dash(—) 남발 | 모델 선호 문장부호 |
| `// TODO: 나머지 구현` 후 중단 | 토큰 절약 편향 |

### 실제 규칙 예시 (메인 SKILL.md 발췌)

```
§9.G EM-DASH BAN    페이지 어디에도 '—' 금지 (헤드라인/버튼/alt 텍스트 포함)
§4.7 히어로 규율     헤드라인 ≤ 2줄, 서브텍스트 ≤ 20단어 & ≤ 4줄, CTA는 스크롤 없이 노출
§9.C 레이아웃 반복 금지  8개 섹션이면 최소 4가지 다른 레이아웃 패밀리 사용
§4.2 Color Lock     페이지 전체 accent 컬러 1개 고정
§6.B Reduced Motion 접근성 필수
§8   Dark Mode      소비자용 페이지는 듀얼 모드 기본

기타 금지: "00 / INDEX" 섹션번호 라벨, "↓ Scroll" 유도문구, 가짜 대시보드 div,
          도시/시간 스트립, 이미지 위 pill 라벨, 장식용 상태 점(dot),
          마케팅 페이지의 버전 푸터(v1.4.2), 손으로 그린 SVG 아이콘
```

### 시그니처 기능 — 3개의 다이얼

```
DESIGN_VARIANCE:  8   (1=완벽 대칭 ~ 10=예술적 카오스)
MOTION_INTENSITY: 6   (1=정적 ~ 10=시네마틱 물리엔진)
VISUAL_DENSITY:   4   (1=미술관처럼 여백 ~ 10=조종석처럼 빽빽)
```

대화창에서 "variance 3으로 낮춰줘"처럼 즉시 조정 가능하다.

### 스킬 13개 용도표

**코드 생성 스킬**

| 폴더 | install name | 용도 |
| --- | --- | --- |
| taste-skill | `design-taste-frontend` | 기본값. 랜딩/포폴/리디자인 범용 (v2 experimental) |
| taste-skill-v1 | `design-taste-frontend-v1` | 구버전 고정용 |
| gpt-tasteskill | `gpt-taste` | GPT/Codex용 강화판. 레이아웃 랜덤화 강제 |
| redesign-skill | `redesign-existing-projects` | 기존 프로젝트 감사 후 개선 |
| soft-skill | `high-end-visual-design` | 애플/Linear 톤, 부드럽고 고급스러운 |
| minimalist-skill | `minimalist-ui` | 노션/Linear 톤, 모노크롬 에디토리얼 |
| brutalist-skill | `industrial-brutalist-ui` | 스위스 타이포 + 군용 터미널 (베타) |
| output-skill | `full-output-enforcement` | AI가 코드 생략할 때 특효 |
| stitch-skill | `stitch-design-taste` | 구글 Stitch용 DESIGN.md 생성 |

**이미지 생성 전용 스킬 (코드 미출력)**

| 폴더 | install name | 용도 |
| --- | --- | --- |
| imagegen-frontend-web | `imagegen-frontend-web` | 섹션별 웹 시안. 8섹션 = 이미지 8장 강제 |
| imagegen-frontend-mobile | `imagegen-frontend-mobile` | 모바일 화면/플로우, 폰 목업 프레임 |
| brandkit | `brandkit` | 로고/팔레트/타이포 브랜드 보드 |
| image-to-code-skill | `image-to-code` | 이미지 생성 → 분석 → 코드 구현 원스톱 |

### 사용자에게 주는 이득

1. 디자이너 없이도 퍼블리싱 퀄리티 결과물 확보
2. "Inter 쓰지 마, 여백 늘려" 같은 반복 프롬프트 제거
3. 프레임워크 무관 (React/Vue/Svelte/PHP/순수 HTML)
4. 에이전트 무관 (Claude Code/Cursor/Codex/Copilot)
5. `output-skill`만으로도 코드 생략 방지 효과
6. MIT 라이선스로 개조·상업적 이용 자유

### 한계 (공식 Out of Scope)

- 대시보드, 데이터 테이블, 다단계 폼/위저드, 코드 에디터, 네이티브 모바일, 실시간 협업 UI는 범위 밖
- 메인 v2는 experimental. v2.0.0 stable 미도달
- `§12 Block Library`는 계약(schema)만 정의되고 구현체는 비어 있음
- 규칙 분량이 커서 컨텍스트 소모가 큼
- README가 스폰서 배너 중심 (Kimi, Fluxion AI 등)

---

## 2. 쉽게 다시 설명

### 비유

AI는 실력은 좋지만 취향이 없는 요리사다. "밥 해줘"라고 하면 학습 데이터에 제일 많았던 김치볶음밥만 만든다.

**taste-skill은 그 요리사에게 주는 "우리 집 규칙 메모"다.**

```
- 김치볶음밥 금지
- 참기름은 마지막에 반 스푼만
- 사각 접시 사용
- 플레이팅 여백 3cm 확보
- 반쯤 만들고 중단 금지
```

이 메모를 주방 벽에 붙여두면(= 프로젝트 폴더에 SKILL.md를 두면) 요리사가 알아서 따른다.

### 작동 순서

```
1) 사용자: "랜딩페이지 만들어줘"
2) AI가 프로젝트 폴더에서 SKILL.md 발견
3) AI: "Inter 금지, 여백 크게, 레이아웃 다양화..." 규칙 인식
4) 규칙을 지키며 코드 작성
5) 결과: 템플릿 같지 않은 페이지
```

설치라는 건 결국 "폴더에 마크다운 파일 넣기"다.

### Before / After

**스킬 없을 때**

```jsx
<section className="text-center py-20 bg-gradient-to-r from-purple-500 to-pink-500">
  <h1 className="text-5xl font-bold text-white font-inter">
    Elevate Your Workflow — Seamlessly
  </h1>
  <p>Transform how your team works with next-gen AI</p>
  <div className="grid grid-cols-3 gap-4">{/* shadow-lg 카드 3개 */}</div>
</section>
```

보라-핑크 그라데이션, Inter, 가운데정렬, 3칸 카드, "Elevate", em-dash. 전형적인 AI 산출물.

**스킬 적용 시**

```jsx
<section className="grid grid-cols-12 min-h-[88vh] px-[clamp(1.5rem,5vw,6rem)]">
  <div className="col-span-7 self-end pb-[clamp(4rem,10vh,9rem)]">
    <h1 className="font-[Geist] text-[clamp(3rem,7vw,6.5rem)] leading-[0.92] tracking-[-0.03em]">
      Ship design reviews in one pass
    </h1>
    <p className="max-w-[46ch] mt-6 text-neutral-500">
      구체적인 문장, 20단어 이내
    </p>
  </div>
  <div className="col-span-5">{/* 비대칭 배치 */}</div>
</section>
```

비대칭 12칼럼, 유동 타이포그래피, 구체적 카피.

### 다이얼을 이퀄라이저로 이해하기

| 다이얼 | 1로 내리면 | 10으로 올리면 |
| --- | --- | --- |
| VARIANCE | 은행 홈페이지처럼 정형적 | 미대생 포트폴리오처럼 실험적 |
| MOTION | 정지 화면 | 스크롤 연동 시네마틱 |
| DENSITY | 애플 홈페이지처럼 여백 위주 | 커머스처럼 정보 밀집 |

기본값 `8 / 6 / 4`.

### 스킬 조합은 도시락처럼

- 밥(기본): `taste-skill`
- 메인반찬(택1): `soft` / `minimalist` / `brutalist`
- 사이드: `redesign`, `output`
- 디저트: `imagegen-*`, `brandkit` (이미지 전용)

전부 설치할 필요 없다. 필요한 것만 고른다.

---

## 3. 질문 7가지 정밀 답변

### Q1. 설치 및 사용법

**방법 A — npx skills add (권장)**

```bash
# 전체 설치
npx skills add https://github.com/Leonxlnx/taste-skill

# 단일 스킬 설치
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"

# 포크에서 설치
npx skills add https://github.com/bmshin94/taste-skill
```

주의: `--skill` 값은 폴더명이 아니라 frontmatter의 `name:` 값이다.

| 폴더명 | install name |
| --- | --- |
| taste-skill | design-taste-frontend |
| soft-skill | high-end-visual-design |
| minimalist-skill | minimalist-ui |
| brutalist-skill | industrial-brutalist-ui |
| output-skill | full-output-enforcement |
| redesign-skill | redesign-existing-projects |
| gpt-tasteskill | gpt-taste |
| stitch-skill | stitch-design-taste |
| image-to-code-skill | image-to-code |

**방법 B — Claude Code 플러그인 마켓플레이스**

```bash
/plugin marketplace add bmshin94/taste-skill
/plugin install taste-skill@taste-skill
```

**방법 C — 수동 복사**

```bash
mkdir -p 내프로젝트/.claude/skills
cp -r skills/taste-skill 내프로젝트/.claude/skills/
```

ChatGPT 대화창에 SKILL.md 내용을 그대로 붙여넣어도 동작한다.

**도구별 설치 위치**

| 도구 | 경로 |
| --- | --- |
| Claude Code (프로젝트) | `.claude/skills/<이름>/SKILL.md` |
| Claude Code (전역) | `~/.claude/skills/<이름>/SKILL.md` |
| Cursor | `.cursor/rules/` 또는 `AGENTS.md` 병합 |
| Codex / ChatGPT | 대화 붙여넣기 또는 `AGENTS.md` |
| GitHub Copilot | `.github/copilot-instructions.md` |

**사용 예시**

```
"요가 스튜디오 랜딩페이지 만들어줘. 차분하고 고급스럽게. variance 4, motion 3."
→ AI가 SKILL.md 로드 → Design Read 한 줄 출력 → 다이얼 반영
→ 구현 → §14 Pre-Flight 체크리스트로 자가검증
```

특정 스킬을 강제하려면 이름을 직접 부른다: "redesign-skill 써서 감사부터 해줘".

### Q2. 플러그인 / 스킬 / MCP 중 무엇인가

**본질은 Skill, 배포 포장은 Plugin, MCP는 전혀 아니다.**

| 구분 | 해당 여부 | 설명 |
| --- | --- | --- |
| Skill | 본체 | SKILL.md 13개. 실체 |
| Plugin | 포장지 | `.claude-plugin/plugin.json`으로 마켓 등록 |
| MCP | 아님 | 서버·프로토콜·JSON-RPC 일절 없음 |

```
SKILL  = 지식/지침   마크다운. 모델 컨텍스트에 들어감. 실행되지 않음
PLUGIN = 배포 단위   skills + commands + agents + hooks 묶음
MCP    = 도구/연결   별도 서버 프로세스가 모델에게 실제 능력 제공
```

비유: Skill은 요리책(지식), MCP는 가스레인지(능력), Plugin은 배송 박스(포장).

검증: `plugin.json`에 `mcpServers` 필드 없음, 레포 내 MCP 설정 파일 없음, `skills/` 하위에 실행 파일 없음.

### Q3. API 토큰이 필요한가

**필요 없다.**

| 항목 | 토큰 필요 |
| --- | --- |
| 설치 | 불필요 |
| 사용 | 불필요 |
| 회원가입/결제 | 불필요 |

실행되는 코드가 없어 네트워크 호출 자체가 발생하지 않는다.

README 상단의 Kimi API 키 안내, Fluxion AI 크레딧 안내는 **스폰서 광고**이며 기능과 무관하다. 클릭하지 않아도 정상 작동한다.

실제로 필요한 것은 이미 사용 중인 AI 도구(Claude/ChatGPT/Cursor 구독)와, `npx` 사용 시 Node.js뿐이다. 추가 비용은 0원.

보안 관점: 텔레메트리 없음, 외부 통신 없음, postinstall 스크립트 없음. 폐쇄망에서도 md 파일 복사만으로 동작한다.

### Q4. 왜 GitHub에서 유명한가

1. **보편적 통증을 정확히 타격** — "AI UI는 다 똑같다"는 개발자 전원이 체감하는 문제인데, 최초로 문서 형태 해결책 제시
2. **"Anti-slop" 네이밍** — 유행어에 접두사를 붙여 정체성을 한 단어로 압축
3. **진입장벽 0** — 설치 1줄, 빌드/의존성 없음, 삭제도 1초. 밑져야 본전
4. **Before/After가 시각적** — 디자인 레포는 스크린샷 한 장이 설명 100줄을 이김. SNS 확산에 최적
5. **타이밍** — Agent Skills 표준화 + `npx skills add` CLI 등장 시점에 정확히 진입. 생태계 초기 선점
6. **에이전트 중립성** — GPT 전용 변형, Copilot instructions까지 제공해 사용자 풀 확대
7. **운영 품질** — research 폴더로 근거 제시, CHANGELOG로 투명성, v1 보존, 전용 사이트, Vercel OSS 프로그램 선정

요약: 모두가 아는 문제 + 제로 코스트 해결책 + 즉시 확인 가능한 결과 + 완벽한 타이밍.

### Q5. 로컬 에이전트 구축에 도움이 되는가

**된다. 단 "부품"이 아니라 "교과서"로.**

**도움 되는 부분**

프롬프트 설계 교본으로서의 가치:

| 테크닉 | 구현 위치 |
| --- | --- |
| Negative Constraint | "하지 마" 목록이 "해라"보다 김 |
| Progressive Disclosure | 섹션 번호 체계로 부분 참조 |
| Self-Verification Loop | §14 Pre-Flight 자가검증 체크리스트 |
| Parameterization | 3개 다이얼로 행동 제어 |
| Few-shot Skeleton | GSAP 코드 뼈대 통째 제공 |
| Scope Declaration | §13에서 능력 한계 명시 |

`research/laziness/`는 LLM 출력 절단의 원인(RLHF 경제학, 학습 데이터 편향, 컨텍스트 비대칭)과 해결법(파라미터 튜닝, XML 프롬프트 구조, 아키텍처 패턴)을 정리한 자료로, 로컬 에이전트 개발 시 첫 난관의 참고서가 된다.

`skills/llms.txt` + 개별 `SKILL.md` 구조는 lazy loading 패턴이며, 컨텍스트 절약 설계로 그대로 차용할 수 있다.

Ollama/LM Studio 등 로컬 LLM의 system prompt에도 그대로 투입 가능하다.

**불가능한 부분**

툴 호출, 메모리/RAG, 멀티 에이전트 오케스트레이션, 상태 관리, 프론트엔드 외 도메인은 전혀 다루지 않는다.

**결론**

```
로컬 에이전트 = [LLM] + [도구(MCP)] + [메모리] + [오케스트레이션] + [지침]
                                                                  ↑ taste-skill
```

권장 조합: Claude Agent SDK(뼈대) + Playwright MCP(검증) + taste-skill(디자인 규칙) + 자체 RAG(프로젝트 디자인 토큰).

### Q6. 수익화 가능성

가능하다. 상세 내용은 4장 참조.

핵심 인사이트:
1. MIT 라이선스라 상업적 이용/개조/재배포가 합법
2. 원본은 의도적으로 수익화를 하지 않음(스폰서십만) → 빈 공간이 넓음
3. 규칙 자체는 공짜지만, 적용된 결과물과 자동화는 유료화 가능

### Q7. React나 PHP로 만들 수 있는가

**해석 A: taste-skill을 적용해 React/PHP 사이트를 만들 수 있는가 → 가능하다**

README FAQ에 명시: "Does it work with React, Vue, Svelte? Yes. Rules target design intent, not a single framework API."

| 스택 | 적용도 | 비고 |
| --- | --- | --- |
| React / Next.js | 최상 | 스킬 내부 예제가 React + Tailwind + GSAP |
| Vue / Nuxt | 높음 | 규칙 100% 적용, 코드 예제만 변환 |
| Svelte | 높음 | 동일 |
| PHP (Laravel Blade) | 높음 | Blade + Tailwind면 거의 그대로 |
| PHP (순수/WordPress) | 보통 | 타이포·컬러·레이아웃 규칙 유효, GSAP은 script 태그 |
| 순수 HTML/CSS | 높음 | 문제없음 |

이유: 규칙이 프레임워크 API가 아니라 디자인 의도를 기술하기 때문이다.

PHP 사용 시 팁 — 스킬 §3.A 기본 스택이 React/Next이므로 프롬프트에 명시한다:
"taste-skill 규칙 적용하되 Laravel Blade + Tailwind로 출력. React 코드 금지."

**해석 B: taste-skill 같은 제품을 우리가 만들 수 있는가 → 가능하다**

스킬 자체는 마크다운이라 언어가 필요 없고, 만들 것은 그것을 둘러싼 제품이다.

```
[React/Next.js] 프론트엔드
  다이얼 슬라이더 UI / 실시간 프리뷰 / 스킬 조합 선택 / SKILL.md 다운로드
[PHP(Laravel) 또는 Node] 백엔드
  인증·결제 / 커스텀 스킬 저장 / LLM API 프록시 / 팀 공유·버전 관리
[마크다운] 스킬 엔진
  taste-skill 규칙 + 자체 규칙
```

| 만들 것 | 스택 | 난이도 |
| --- | --- | --- |
| 스킬 빌더 웹앱 | React + Next.js | 낮음 |
| 한국어판 포크 | 마크다운 | 매우 낮음 |
| VS Code 익스텐션 | TypeScript | 중간 |
| WordPress 플러그인 | PHP | 중간 |
| 디자인 감사 SaaS | React + Node/PHP | 높음 |
| 에이전시용 브랜드 스킬 생성기 | Next.js + Claude API | 높음 |

---

## 4. 수익화 아이디어

### 전략 프레임

```
팔면 안 되는 것: 규칙 문서 그 자체 (MIT 공개. 복사 1초. 가격 방어 불가)

팔아야 하는 것:
  1) 적용된 결과물 (Output)
  2) 자동화/워크플로우 (Automation)
  3) 고유 데이터/브랜드 (Proprietary)
  4) 검증/보증 (Verification)
  5) 커뮤니티/교육 (Community)
```

황금률: 복붙으로 훔칠 수 있는 건 팔지 않는다. 훔쳐도 재현되지 않는 것을 판다.

### TIER 1 — 즉시 실행 가능, 저비용

**아이디어 1. 한국어 프리미엄 스킬팩 판매 (1순위 추천)**

| 항목 | 내용 |
| --- | --- |
| 상품 | 한글 폰트 최적화 + 국내 트렌드 반영 SKILL.md 팩 |
| 근거 | 원본은 100% 영어 + 서구권 폰트. 한글 타이포는 규칙 체계가 다름 |
| 차별점 | Pretendard/SUIT 폰트 스택, 한글 음수 자간, `word-break: keep-all`, 한국형 랜딩 구조 |
| 가격 | 39,000~89,000원 (평생 이용) |
| 채널 | Gumroad, 크몽, 인프런 |
| 제작기간 | 2~3주 |

```markdown
# 한국어판 규칙 예시
## 한글 타이포그래피
- 폰트: Pretendard Variable 기본. Noto Sans KR 금지(과다 사용)
- 자간: 제목 -0.035em, 본문 -0.015em
- 줄바꿈: word-break: keep-all + overflow-wrap: break-word
- 한 줄 길이: 한글 기준 28~34자 (영문 65자 기준 아님)
- 금지 카피: "지금 바로", "혁신적인", "최고의", "원스톱"
```

경쟁자가 거의 없고 수요가 확실하며, 한국어 역량 자체가 해자가 된다.

**아이디어 2. AI 랜딩페이지 제작 서비스 (Productized Service)**

| 항목 | 내용 |
| --- | --- |
| 상품 | "5일 안에 프리미엄 랜딩페이지" 고정가 패키지 |
| 근거 | taste-skill로 제작 시간이 대폭 단축 → 마진 확대 |
| 가격 | Basic 80만 / Standard 200만 / Premium 500만원 |
| 채널 | 크몽, 숨고, 위시켓, X, 링크드인 |

```
전통 외주: 기획3일 + 디자인5일 + 퍼블7일 = 15일
AI 활용:   기획0.5일 + 생성0.5일 + 다듬기2일 = 3일
→ 고객 단가는 낮추고 시급은 올리는 구조
```

상품 개발 없이 즉시 시작 가능해 현금흐름 확보에 가장 빠른 경로다.

**아이디어 3. 유료 디자인 플레이북**

| 항목 | 내용 |
| --- | --- |
| 상품 | "AI로 어워드급 프론트엔드 만들기" 가이드 + 프롬프트 50개 + 스킬팩 |
| 가격 | 29,000~59,000원 |
| 근거 | 스킬 파일은 공짜여도 조합법·적용 시점은 노하우 |
| 구성 | 스킬별 실전 시나리오 / 다이얼 프리셋 20종 / Before-After 30쌍 / 실패 사례집 |

### TIER 2 — 1~3개월, SaaS 제품화

**아이디어 4. 스킬 빌더 웹앱**

```
DESIGN_VARIANCE   ●────────  8
MOTION_INTENSITY  ──●──────  6
VISUAL_DENSITY    ─●───────  4
브랜드 컬러 [#0A84FF]  폰트 [Pretendard]  업종 [SaaS]
[ 실시간 프리뷰 ]  [ SKILL.md 다운로드 ]
```

| 항목 | 내용 |
| --- | --- |
| 스택 | Next.js + Tailwind + Claude API + Supabase |
| 수익모델 | Free(월 3회) / Pro $12월 / Team $49월 |
| 차별점 | 실시간 프리뷰, 브랜드 토큰 주입, 팀 공유 |
| 개발기간 | 4~8주 |

**아이디어 5. 디자인 감사(Audit) SaaS**

```
URL 입력 → 크롤링 → taste-skill 규칙 채점 → 리포트

Taste Score: 42/100
 - Inter 폰트 사용            -12
 - em-dash 17개 발견          -8
 - 레이아웃 반복 6/8 섹션      -15
 - CTA 대비 3.1:1 (AA 미달)   -10
 - 히어로 헤드라인 4줄         -8
 + 다크모드 지원              +5
[ 수정 코드 받기 → Pro ]
```

| 항목 | 내용 |
| --- | --- |
| 강점 | 점수는 공유되고 공유는 바이럴을 만듦 (PageSpeed Insights 모델) |
| 수익 | 무료 스캔 → Pro($19/월) 수정 코드 + CI 연동 + 팀 대시보드 |
| B2B | 에이전시용 화이트라벨 리포트 (월 $199) |
| 스택 | Next.js + Playwright + Claude API |

바이럴 잠재력이 가장 크다.

**아이디어 6. 에이전시 브랜드 스킬 생성기 (B2B)**

| 항목 | 내용 |
| --- | --- |
| 상품 | 브랜드 가이드 업로드 → 해당 브랜드 전용 SKILL.md 자동 생성 |
| 타겟 | 디자인 에이전시, 인하우스 디자인팀 |
| 가격 | 초기 셋업 300~800만원 + 유지보수 월 50만원 |
| 근거 | 에이전시는 "AI가 자사 브랜드 톤을 지키게 하는 것"에 지불 의사가 큼 |
| 핵심 기술 | PDF/피그마 파싱 → 디자인 토큰 추출 → 규칙 문서 생성 |

객단가가 가장 높다.

### TIER 3 — 장기/고위험

**아이디어 7. 스킬 마켓플레이스** — 창작자 업로드 + 수수료 30%. 확장성은 크지만 닭-달걀 문제와 "무료 스킬 대비 지불 이유" 확보가 관건.

**아이디어 8. 자동화 파이프라인 SaaS** — 피그마 링크 → 분석 → taste-skill 적용 → Next.js 코드 → 배포. v0/Lovable/Bolt와 경쟁하되 "슬롭 없는 생성" 포지셔닝으로 차별화.

**아이디어 9. 콘텐츠(유튜브/뉴스레터)** — "AI 디자인 슬롭 해부" 시리즈. 광고 + 제휴 + 자체 상품. 원본 레포가 실제로 쓰는 모델.

### 법적 체크 (MIT 라이선스)

| 허용 | 금지 |
| --- | --- |
| 상업적 사용 | 라이선스/저작권 고지 삭제 |
| 수정·개조 | "Taste Skill 공식" 사칭 |
| 재배포·판매 | 원저작자 보증 주장 |
| 클로즈드소스 전환 | 상표권 침해 소지 있는 명칭 |

필수: 배포물에 LICENSE 포함 및 `Copyright (c) 2026 Leonxlnx` 고지 유지.
권장: "Based on taste-skill (MIT)" 크레딧 명시.
주의: README에 공식 토큰/코인/크립토가 없음이 명시되어 있으므로 코인 관련 사업은 배제한다.

### 추천 로드맵

```
1개월차   한국어 스킬팩 제작 + 랜딩 제작 서비스 오픈 → 현금흐름 확보
2-3개월차 반복 작업 자동화 → 스킬 빌더 웹앱 MVP (Next.js)
4-6개월차 디자인 감사 SaaS 런칭 → 무료 스캔 바이럴 → Pro 전환
6개월+    B2B 에이전시 계약으로 객단가 상승
```

순서의 근거:
1. 1단계에서 수익과 도메인 지식을 동시에 확보한다
2. 2단계는 검증된 수요 위에 제품을 얹는 자연스러운 자동화다
3. 3단계는 마케팅비 없는 유입 엔진이다
4. 4단계는 앞 단계 레퍼런스를 활용한 수확이다

핵심 원칙: 규칙을 파는 것이 아니라 결과를 판다. taste-skill은 원가를 낮추는 무기이지 상품 자체가 아니다.

---

## 5. 핵심 요약 카드

| 질문 | 답 |
| --- | --- |
| 정체 | AI 프론트엔드 슬롭 방지용 마크다운 지침서 13종 |
| 분류 | Skill(본체) + Plugin(포장). MCP 아님 |
| 설치 | `npx skills add https://github.com/Leonxlnx/taste-skill` |
| API 토큰 | 불필요. 추가 비용 0원 |
| 지원 스택 | React/Vue/Svelte/PHP/순수 HTML 전부 |
| 지원 에이전트 | Claude Code / Cursor / Codex / Copilot |
| 라이선스 | MIT (상업 이용·개조·재판매 가능) |
| 범위 밖 | 대시보드, 데이터 테이블, 다단계 폼, 네이티브 앱 |
| 최고 강점 | 설치 즉시 결과물 품질 상승, 진입장벽 0 |
| 최고 약점 | v2 experimental, Block Library 미구현, 컨텍스트 소모 |
| 수익화 1순위 | 한국어 스킬팩 + 랜딩 제작 서비스 |
| 수익화 최대치 | 디자인 감사 SaaS / B2B 브랜드 스킬 생성기 |

---

## 참고 링크

- 원본 저장소: https://github.com/Leonxlnx/taste-skill
- 본 포크: https://github.com/bmshin94/taste-skill
- 공식 사이트: https://tasteskill.dev
- 체인지로그: https://www.tasteskill.dev/changelog
- Agent Skills CLI: https://github.com/vercel-labs/agent-skills
- 라이선스: MIT
