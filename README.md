# Grokmate

> **권한 안에서 대화·검색·코딩·서버 관리를 끝까지 해내는 Grok 4.3 기반 디스코드 AI 봇.**

_비공식 독립 프로젝트 · 이 저장소는 **소스 비공개** 프로젝트의 **소개·문서** 공간이며 봇 구동 코드는 포함하지 않습니다._

## 1. 소개 (Introduction)

Grokmate는 xAI Grok 4.3 위에서 동작하는 디스코드 봇으로, **범용 AI(작문·코딩·추론·검색)** 와 **권한 기반 서버 관리** 를 한 봇에 통합합니다. 카미봇급 관리 기능이 필요하지만 AI의 유연함도 원하는 서버를 위해, **인가와 안전을 약속이 아니라 코드로 강제**하는 것을 목표로 합니다.

**호출** — `그록아` · `Hey Grok` · `@Grokmate` · DM · **전용 AI 채널**(지정 시 멘션 없이) 중 하나로 부르면 응답합니다. 메시지마다 일반·검색·코딩·서버 관리·성인 모드를 자동 판정하고, 반말 친근체로 답합니다(한국어·영어, 서버별 존댓말).

**주요 명령어** — 대표만 추렸습니다. 전체 41개와 자세한 설명은 [COMMANDS.md](COMMANDS.md) 또는 [소개 페이지](<https://jtech-co.github.io/Grokmate/>) 참고.

_누구나_

- `/help` 안내 · `/usage` 사용량·요금제 · `/reset` 대화 초기화 · `/debug` 진단(시각·핑·시스템·네트워크 속도)
- `/fetch` URL 요약 · `/translate` 이미지 번역(OCR) · `/repo` `/gh-user` `/gh-file` GitHub 조회
- `/poll` 투표 · `/level` `/leaderboard` 레벨 · `/voice` 임시 음성방 · `/verify-age` 성인 인증

_서버 관리 (스태프·관리자)_

- 모더레이션 — `/warn` `/pardon` `/timeout` `/kick` `/ban` `/unban` `/purge` `/slowmode` `/lock`
- 서버 설정 — `/config` `/nsfw-policy` `/welcome` `/autorole` `/reactionrole` `/voice-hub`
- 자연어로도 지시 가능(권한자 한정) — "슬로우모드 10초로", "역할 부여" 등. 밴·킥·타임아웃·청소는 슬래시 + 확인 버튼 전용.

_봇 운영자_

- `/maintenance` 점검 모드 · `/health` 상태 · `/cost` 토큰 집계 · `/audit` 감사 로그 · `/grant-tier` `/grant-list` 구독

**그 외** — 게이팅된 성인 모드(연령제한 채널 + 서버 활성 + 연령 인증 + 성적 의도 **4중 게이트**), 자동 모더레이션(옵트인)·모더 로그 채널, 서버 합류 온보딩, 웹·X 실시간 검색(출처 표기), 24/7 운영(점검 모드·단일 인스턴스·우아한 종료·업스트림 타임아웃).

**차별점 — 안전을 코드로 강제**: 모든 관리 액션은 봇이 아니라 **요청자 권한**으로 단일 게이트를 거치고(권한 상승 0), 미성년 성적 콘텐츠는 어떤 모드에서도 무조건 차단하며, 모르면 모른다고 말합니다(거짓 성공 보고 0). 상세는 [ARCHITECTURE.md](ARCHITECTURE.md#보안-모델).

## 2. 기술 스택 (Tech Stack)

- **런타임 · 언어**: Node.js 20+ (ESM) · JavaScript + JSDoc (`tsc --checkJs --strict`)
- **디스코드**: discord.js v14
- **AI**: xAI Grok 4.3 (`@ai-sdk/xai` · `ai`)
- **데이터**: SQLite + Drizzle ORM
- **기타**: tesseract.js (OCR) · undici (안전한 URL fetch)
- **품질**: Vitest (584 tests) · ESLint (+ `eslint-plugin-boundaries` 경계 강제) · Prettier · GitHub Actions CI(불변식 회귀 게이트 포함)

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
- **약관·개인정보**: [이용약관](<https://jtech-co.github.io/Grokmate/legal/terms.html>) · [개인정보 처리방침](<https://jtech-co.github.io/Grokmate/legal/privacy.html>) (요약 [PRIVACY.md](PRIVACY.md))
- **보안 제보**: [SECURITY.md](SECURITY.md)
- **더 보기**: [설계·보안 모델](ARCHITECTURE.md) · [디자인백서](docs/디자인백서.md) · [ADR](docs/adr/)
- **Contact**: [jtech-bryan@proton.me](mailto:jtech-bryan@proton.me)

---

비공식 독립 프로젝트로 xAI · X · Discord 와 제휴·보증 관계가 없습니다. Grok · xAI · X 는 각 소유자의 상표입니다.
