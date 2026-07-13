# Grokmate

> **권한 안에서 대화·검색·코딩·서버 관리를 끝까지 해내는 Grok 4.3 기반 디스코드 AI 봇.**

_비공식 독립 프로젝트 · 이 저장소는 **소스 비공개** 프로젝트의 **소개·문서** 공간이며 봇 구동 코드는 포함하지 않습니다._

## 1. 소개 (Introduction)

Grokmate는 xAI Grok 4.3 위에서 동작하는 디스코드 봇으로, **범용 AI(작문·코딩·추론·검색)** 와 **권한 기반 서버 관리** 를 한 봇에 통합합니다. 카미봇급 관리 기능이 필요하지만 AI의 유연함도 원하는 서버를 위해, **인가와 안전을 약속이 아니라 코드로 강제**하는 것을 목표로 합니다.

**주요 기능**

- **대화·AI** — `그록아` / `Hey Grok` / 멘션 / DM / **전용 AI 채널**(지정 시 멘션 없이 대화) 호출. 발화 단위로 일반·검색·코딩 모드 자동 판정, 반말 친근체(한국어·영어, 서버별 존댓말 설정 가능). `/reset`으로 대화 맥락 초기화.
- **검색·코딩** — 웹 / X 실시간 검색 + 출처 표기, 코드 작성·디버깅(긴 코드는 파일 첨부).
- **멀티모달·연동** — 이미지·파일 분석(SFW)·이미지 번역(`/translate`), URL 요약(`/fetch`), GitHub 조회(`/repo`·`/gh-user`·`/gh-file`).
- **서버 관리·모더레이션** — 자연어·슬래시 관리(슬로우모드·역할·채널·밴/차단 해제·타임아웃/해제·잠금), 자동 모더레이션, 경고·사면(누적 시 자동 타임아웃), 모더레이션 로그 채널, `/config` 서버 설정(전용 AI 채널·존댓말·자동 모더·스탭/관리 역할·자연어 관리·전체 초기화).
- **커뮤니티 유틸** — 레벨/리더보드, 환영·작별, 자동 역할, 반응 역할, 임시 음성채널, 투표(`/poll`, 시간 자동 마감), 진단(`/debug` — 시각·핑·RAM·디스크·CPU·네트워크 속도·채널 수, 동일인 1분 쿨타임).
- **게이팅된 성인 모드** — 연령제한 채널 + 서버 활성 + 연령 인증 + 성적 의도의 **4중 게이트**를 모두 통과해야만.
- **24/7 운영** — 점검 모드(`/maintenance`, 점검 중 '점검 중입니다' 안내)·단일 인스턴스 잠금·우아한 종료·업스트림 타임아웃 방어, 운영자 관측(`/cost`·`/health`·`/audit`).

**차별점 — 안전을 코드로 강제**: 모든 관리 액션은 봇이 아니라 **요청자 권한**으로 단일 게이트를 거치고(권한 상승 0), 미성년 성적 콘텐츠는 어떤 모드에서도 무조건 차단하며, 모르면 모른다고 말합니다(거짓 성공 보고 0). 상세는 [ARCHITECTURE.md](ARCHITECTURE.md#보안-모델).

## 2. 기술 스택 (Tech Stack)

- **런타임 · 언어**: Node.js 20+ (ESM) · JavaScript + JSDoc (`tsc --checkJs --strict`)
- **디스코드**: discord.js v14
- **AI**: xAI Grok 4.3 (`@ai-sdk/xai` · `ai`)
- **데이터**: SQLite + Drizzle ORM
- **기타**: tesseract.js (OCR) · undici (안전한 URL fetch)
- **품질**: Vitest (569 tests) · ESLint (+ `eslint-plugin-boundaries` 경계 강제) · Prettier · GitHub Actions CI(불변식 회귀 게이트 포함)

## 3. 봇 추가·사용 (Quick Start)

호스팅형 봇이라 설치·빌드가 필요 없습니다. 서버에 추가해서 바로 씁니다.

**요구 사항**: 봇을 추가할 권한(서버 관리)이 있는 디스코드 서버

1. **봇 추가 (Invite)**

   [**디스코드에 추가**](https://discord.com/oauth2/authorize?client_id=1515195451253592247&permissions=8&integration_type=0&scope=bot%20applications.commands)

2. **호출 (Call)** — 아래 중 하나로 부르면 응답합니다.

   ```text
   그록아 ...        # 한국어
   Hey Grok ...      # 영어
   @Grokmate ...     # 멘션
   DM                # 봇에게 다이렉트 메시지
   ```

3. **시작 (Try)** — `/help` 로 명령을 보고 바로 사용합니다.

   ```text
   /help
   그록아 오늘 xAI 관련 뉴스 검색해줘
   /poll 점심 뭐먹지 김밥 라면 햄버거
   ```

명령어 전체는 [COMMANDS.md](COMMANDS.md) 참고.

## 4. 저장소 구조 (Structure)

이 저장소는 **소개·문서 전용**입니다(봇 구동 코드는 비공개).

```text
깃허브 공개용 파일폴더/
├── index.html        # 소개 랜딩 페이지 (GitHub Pages)
├── README.md         # 이 문서
├── COMMANDS.md       # 전체 명령어
├── ARCHITECTURE.md   # 설계·보안 모델
├── PRIVACY.md        # 개인정보 요약
├── SECURITY.md       # 취약점 제보
├── LICENSE           # 독점 라이선스
├── legal/            # 게시용 약관·개인정보 (HTML)
│   ├── terms.html
│   └── privacy.html
├── docs/             # 디자인백서 · ADR(구조적 결정 기록)
└── assets/           # 스크린샷 (예정)
```

## 5. 정보 (Info)

- **License**: 독점 · All Rights Reserved ([LICENSE](LICENSE)). 문서·랜딩은 소개 목적이며 무단 복제·재사용을 허용하지 않습니다.
- **약관·개인정보**: [이용약관](legal/terms.html) · [개인정보 처리방침](legal/privacy.html) (요약 [PRIVACY.md](PRIVACY.md))
- **보안 제보**: [SECURITY.md](SECURITY.md)
- **더 보기**: [설계·보안 모델](ARCHITECTURE.md) · [디자인백서](docs/디자인백서.md) · [ADR](docs/adr/)
- **Contact**: [jtech-bryan@proton.me](mailto:jtech-bryan@proton.me)

---

비공식 독립 프로젝트로 xAI · X · Discord 와 제휴·보증 관계가 없습니다. Grok · xAI · X 는 각 소유자의 상표입니다.
