# Grokmate

Grok 4.3 기반 디스코드 AI 봇 — 대화·검색·코딩·이미지 분석부터 권한 기반 서버 관리까지, **인가와 안전을 코드로 강제**합니다.

> 비공식 독립 프로젝트입니다. xAI · X 와 제휴/보증 관계가 없습니다.
> 이 저장소는 **소스 비공개(클로즈드 소스)** 프로젝트의 **소개·문서** 공간입니다. 봇 구동 코드는 포함하지 않습니다.

## 무엇을 하는 봇인가

Grokmate는 xAI Grok 4.3 위에서 동작하는 디스코드 봇으로, 다음을 한 봇에 통합합니다.

- **대화·AI** — `그록아` / `Hey Grok` / 멘션 / DM 호출. 발화 단위로 일반·검색·코딩 모드 자동 판정. 기본 반말 친근체, 한국어·영어 응답.
- **검색·연구** — 웹 / X 실시간 검색 + 출처(citation) 표기.
- **코딩** — 코드 작성·디버깅, 긴 코드는 파일 첨부.
- **외부 연동** — `/fetch`(웹 페이지 읽기·요약, 자연어 링크도 가능), GitHub `/repo`·`/gh-user`·`/gh-file`.
- **멀티모달** — 이미지·텍스트/코드 파일 분석(SFW), 이미지 속 글자 번역(`/translate`).
- **서버 관리** — 권한 있는 사람의 자연어 지시(슬로우모드·역할·채널)와 슬래시 명령(밴·킥·타임아웃·청소·채널 잠금, 확인 버튼).
- **모더레이션·경고** — 자동 모더레이션(옵트인), 경고·사면(`/warn`·`/pardon`) + 누적 시 자동 타임아웃.
- **커뮤니티 유틸** — XP 레벨/리더보드, 환영·작별 메시지, 자동 역할, 반응 역할, 임시 음성채널, 투표(`/poll`), 합류 온보딩.
- **게이팅된 성인 모드** — 4중 게이트(연령제한 채널 + 서버 활성 + 연령 인증 + 성적 의도)를 모두 통과해야만.

명령어 전체는 [COMMANDS.md](COMMANDS.md), 설계·보안 모델은 [ARCHITECTURE.md](ARCHITECTURE.md), 소개 페이지는 [`index.html`](index.html)(GitHub Pages 호스팅 가능).

## 스크린샷

> [`assets/`](assets/)에 추가 예정 — 대화, 슬래시 명령 목록, 검색+출처, 관리 확인 버튼, 성인 게이트 안내 등.

## 안전·신뢰

7개 불변식(INVARIANTS)을 **약속이 아니라 테스트로** 고정합니다.

- 인가는 봇이 아니라 **요청자 권한**으로, 슬래시·자연어 모두 단일 게이트를 거칩니다(권한 상승 0).
- 미성년 성적 콘텐츠는 어떤 게이트·모드에서도 **무조건 차단**.
- 성인 콘텐츠는 4중 게이트를 모두 통과한 게이팅된 공간에서만.
- 모르면 모른다고 말합니다(거짓 성공 보고 0). 시크릿은 코드·로그에 노출되지 않습니다.

보안 모델 요약은 [ARCHITECTURE.md](ARCHITECTURE.md#보안-모델), 취약점 제보는 [SECURITY.md](SECURITY.md), 데이터 처리는 [PRIVACY.md](PRIVACY.md).

## 약관·개인정보

- **이용약관** — [legal/terms.html](legal/terms.html) (GitHub Pages 게시본)
- **개인정보 처리방침** — [legal/privacy.html](legal/privacy.html) · 요약 [PRIVACY.md](PRIVACY.md)

디스코드 개발자 포털의 Terms of Service URL·Privacy Policy URL 에는 위 HTML 게시본 링크를 사용합니다.

## 정직한 한계

- 실시간 정보는 검색 모드에서만. 이미지 분석은 SFW 전용(PDF/바이너리 미지원).
- 대화 기억은 단기·인메모리(재시작 시 초기화). 안전 필터는 규칙 기반이라 새로운 표현을 놓칠 수 있음.
- 연령 인증은 자가 인증 + Discord 연령 게이트(신분증 검증 아님).

## 기술

Node.js 20+ (ESM) · JavaScript + JSDoc(`tsc --checkJs --strict`) · discord.js v14 · xAI Grok 4.3(`@ai-sdk/xai`) · SQLite + Drizzle ORM · tesseract.js(OCR) · undici · Vitest(501 tests) · ESLint(+ `eslint-plugin-boundaries`).

## 더 보기

- [디자인백서](docs/디자인백서.md) — 페르소나·대화·UX·임베드 설계
- [ADR](docs/adr/) — 구조적 결정 기록(모델 선택·인가 단일 통제점·NSFW 게이팅·데이터 계층)

## 봇 추가

[**디스코드에 추가**](https://discord.com/oauth2/authorize?client_id=1515195451253592247&permissions=8&integration_type=0&scope=bot%20applications.commands)

## 라이선스

소스 비공개 · 독점(All Rights Reserved). [LICENSE](LICENSE) 참고. 이 저장소의 문서·랜딩은 소개 목적이며 무단 복제·재사용을 허용하지 않습니다.

---

Grok · xAI · X 는 각 소유자의 상표입니다.
