<div align="center">

# OlThing

### 복잡한 하루를 실행 가능한 계획으로

**OlThing은 일정과 할 일을 한곳에 모으고, 직접 관리하거나 AI의 제안을 확인하고 승인해 실행 가능한 계획으로 만드는 모바일 앱입니다.**

`서버 핵심 기능 개발 중` · `온라인 전용 모바일 앱` · `개인 일정과 할 일`

</div>

## 어떤 경험을 만들고 있나요?

<table width="100%">
  <thead>
    <tr><th width="220" align="left">기능</th><th align="left">경험</th></tr>
  </thead>
  <tbody>
    <tr><td>🗓️ Today · Calendar</td><td>오늘의 고정 일정과 할 일, 주간 계획을 함께 봅니다.</td></tr>
    <tr><td>✅ Task · Goal</td><td>할 일을 목표에 연결하고 진행 상태와 예상 시간을 관리합니다.</td></tr>
    <tr><td>✨ AI 제안</td><td>자연어 입력으로 기록 후보를 만들고, 별도 계획 요청으로 한 주의 빈 시간에 작업 블록을 제안받습니다.</td></tr>
    <tr><td>👀 미리보기와 승인</td><td>AI 후보는 확인·수정·승인한 뒤 반영합니다. 수동 관리는 AI 없이도 가능합니다.</td></tr>
    <tr><td>🛍️ 쇼핑 · 사진 · 보관함</td><td>쇼핑 체크리스트와 사진을 기록하고, 보관한 항목을 날짜별로 모아 봅니다.</td></tr>
    <tr><td>📱 온라인 연결과 복구</td><td>연결 중단 전 작성·전송 중인 내용을 보호하고, 재연결 시 저장 결과를 확인합니다. 오프라인 신규 조회·편집은 제공하지 않습니다.</td></tr>
  </tbody>
</table>

> **설계·API 계약을 정리하고 서버 핵심 기능을 구현하는 단계입니다.** 위 내용은 제품이 지향하는 경험이며, 전체 기능이 출시된 상태는 아닙니다. 모바일 앱 구현과 실제 기기·외부 서비스·출시 검증은 남아 있습니다. 제품 기준은 [확정 정책](https://github.com/OlThing/docs/blob/main/requirements/approved-policies-2026-10-04.md)과 [설계·계약 정리 결과](https://github.com/OlThing/docs/blob/main/planning/design-final-closeout-2026-10-10.md)에서 관리합니다.

## 한눈에 보는 아키텍처

<p align="center">
  <a href="https://github.com/OlThing/.github/blob/main/profile/assets/olthing-architecture.svg">
    <img src="https://raw.githubusercontent.com/OlThing/.github/main/profile/assets/olthing-architecture.svg" alt="OlThing 아키텍처: 개발 중인 단일 API 서버와 PostgreSQL·Mailpit은 실선, 모바일 앱과 AI·SES·S3 후속 연동은 점선으로 구분" width="100%" />
  </a>
</p>

**실선은 현재 개발 구현, 점선은 채택한 방향과 후속 구현입니다.** 그림의 박스는 책임과 연결을 나타내며, 각각 별도 서버를 뜻하지 않습니다. [SVG 원본 보기](https://github.com/OlThing/.github/blob/main/profile/assets/olthing-architecture.svg)

## 출시 범위

<table width="100%">
  <thead>
    <tr><th width="160" align="left">단계</th><th align="left">범위</th></tr>
  </thead>
  <tbody>
    <tr><td>MVP · 무료 베타</td><td>Task·Goal·Today·주간 Calendar, 자연어 기록 후보·주간 계획 승인, 쇼핑 체크리스트·사진 첨부·개인 보관함</td></tr>
    <tr><td>V1</td><td>월·일 Calendar·Board, 요청·승인에 따른 재계획, AI 조회·목표 분해·사진 인식, 기기 내 기본 알림, 개인 유료 상품 한 종류</td></tr>
  </tbody>
</table>

가격·AI 사용량 한도·구매 채널은 보류 중입니다. V1 알림은 기본 꺼짐이며, 원격 푸시는 현재 범위에 포함하지 않습니다.

## 현재 진행 상황

2026-10-18 기준입니다. 서버 구현 현황은 개발 통합 브랜치인 `dev`를 기준으로 합니다.

<table width="100%">
  <thead>
    <tr><th width="220" align="left">작업</th><th align="left">상태</th></tr>
  </thead>
  <tbody>
    <tr><td>요구사항 · API 계약</td><td>22개 명세와 API·ERD의 연결 검토, 현재 설계·계약 범위 정리 완료. 기능별 실제 구현과 검증은 계속 진행합니다.</td></tr>
    <tr><td>ERD · PostgreSQL</td><td>46개 테이블·73개 관계 정제, SQL·새 DB·백업/복원 검증 완료. 개발 DB와 Flyway 마이그레이션 구성도 반영했습니다.</td></tr>
    <tr><td>서버 · 인증</td><td>개발 프로필에서 이메일 가입·로그인, Bearer 세션 인증·계정/세션 조회·로그아웃 구현. 외부 메일 발송은 후속입니다.</td></tr>
    <tr><td>Task 핵심 API</td><td>생성·목록·상세·부분 수정·상태 변경·완료·재개를 dev에 반영했습니다. 소유권·버전 충돌·중복 요청·트랜잭션 검증을 포함합니다.</td></tr>
    <tr><td>테스트 · CI</td><td>최근 로컬 Maven verify 332개 통과 기록과 10월 18일 dev 병합 커밋의 원격 CI 성공을 확인했습니다. PostgreSQL·Mailpit 통합 테스트를 포함합니다.</td></tr>
    <tr><td>모바일 · 나머지 기능</td><td>모바일 기술 방향을 채택했습니다. 앱 구현·실기기 시험, 나머지 도메인과 AI·계획 기능 구현은 후속입니다.</td></tr>
    <tr><td>배포 · 운영</td><td>WSL/Docker 로컬 개발·테스트 기반을 구성했습니다. 원격 서버 생성·공개 배포·실제 외부 메일 검증은 지인 테스트 준비 시점에 진행합니다.</td></tr>
  </tbody>
</table>

[설계·계약 검토 결과](https://github.com/OlThing/docs/blob/main/planning/design-final-closeout-2026-10-10.md) · [Task 상태 변경 구현](https://github.com/OlThing/olthing-server/blob/dev/docs/task-status-development.md) · [최신 병합·CI](https://github.com/OlThing/olthing-server/pull/14)

다음은 Task 삭제·복원·보관 등 남은 수명주기 구현과 로컬 배포 준비입니다. AI 품질·실제 기기·운영 부하·출시 검증은 별도로 진행합니다.

## 기술 구성

기술 방향은 ADR로 기록하고, 서버는 실제 코드와 CI에 적용하고 있습니다. 모바일·외부 연동의 기술 선택과 실제 서비스 연결 상태는 구분합니다.

<table width="100%">
  <thead>
    <tr><th width="220" align="left">영역</th><th align="left">구성 · 적용 상태</th></tr>
  </thead>
  <tbody>
    <tr><td>서버</td><td>Java 21 · Spring Boot 4.1.1 · Maven Wrapper. DDD 기반 모듈형 단일 서버로 개발 중입니다.</td></tr>
    <tr><td>데이터 · 인증</td><td>PostgreSQL · Flyway · JPA/명시 SQL · Spring Security. 계정·세션과 Task API에 적용 중입니다.</td></tr>
    <tr><td>모바일</td><td>React Native · Expo · TypeScript · Expo Router 방향 채택. 앱 초기 구성·빌드·기기 검증은 후속입니다.</td></tr>
    <tr><td>테스트 · 품질</td><td>GitHub Actions · Testcontainers · ArchUnit · JaCoCo 구성. Sonar 분석 연결은 후속입니다.</td></tr>
    <tr><td>외부 연동</td><td>메일은 SES, 사진은 S3 연동 방향을 정했습니다. 현재 메일 시험은 로컬 Mailpit을 사용하며 실제 공급자 연결·전달·삭제 검증은 남아 있습니다.</td></tr>
    <tr><td>배포 · 운영</td><td>WSL2 · Docker 로컬 준비 우선. 이미지·환경 분리·백업/복원·롤백을 준비한 뒤 원격 호스팅을 확정합니다.</td></tr>
  </tbody>
</table>

[기술 선택과 ADR](https://github.com/OlThing/docs/blob/main/planning/technology-final-closeout-2026-10-11.md) · [API 계약 목차](https://github.com/OlThing/docs/blob/main/design/api/README.md) · [최신 인프라 준비 계획](https://github.com/OlThing/docs/issues/49)

## 우리는 이렇게 처리합니다

<details open>
<summary><strong>01 · 서버는 하나로, 기능의 책임은 나누기로 했습니다</strong> — 적용 중</summary>

Java·Spring Boot와 PostgreSQL로 시작하고, 계정·작업·계획·사진 등의 책임을 모듈별로 나눕니다. 현재는 인증과 Task를 구현하고 있습니다. 초기에 서비스·DB를 여러 개로 늘리지 않아 배포와 운영 부담을 줄이고, 함께 바뀌어야 하는 데이터는 하나의 트랜잭션으로 처리합니다.

[DDD와 트랜잭션 경계](https://github.com/OlThing/docs/blob/main/architecture/ddd-boundaries-2026-10-11.md)

</details>

<details>
<summary><strong>02 · AI는 후보를 만들고, 사용자가 반영을 결정합니다</strong> — 설계 결정</summary>

수동 기록은 AI 없이도 사용할 수 있게 합니다. 자연어·사진 인식은 확인·수정할 후보를 만들고, 사용자가 승인한 뒤 서버가 검증해 반영합니다. 시간 배치·겹침·소유권은 서버 규칙으로 판정하며, 기록 저장과 계획·재계획 요청도 구분합니다. AI·계획 기능의 실제 구현은 후속입니다.

[수동·AI·계획의 담당 구분](https://github.com/OlThing/docs/blob/main/requirements/manual-ai-boundaries.md)

</details>

<details>
<summary><strong>03 · 같은 요청은 중복 저장하지 않고, 오래된 수정은 충돌로 안내합니다</strong> — Task에 적용</summary>

Task 변경은 계정 소유권·현재 세션·기준 버전을 확인합니다. 같은 요청 키와 같은 본문은 보존된 최초 결과를 재현하고, 다른 본문이나 오래된 버전은 충돌로 처리합니다. Task·연관 예약·변경 표시·요청 결과는 함께 커밋하거나 롤백해, 일부만 저장되는 상황을 막습니다. 완료·재개 시 예약 처리도 확정한 규칙을 따릅니다.

[Task 수정](https://github.com/OlThing/olthing-server/blob/dev/docs/task-update-development.md) · [상태 변경과 원자 저장](https://github.com/OlThing/olthing-server/blob/dev/docs/task-status-development.md)

</details>

<details>
<summary><strong>04 · 온라인으로 사용하되, 연결 중단으로 작성 내용을 잃지 않게 합니다</strong> — 앱 복구 설계</summary>

연결이 끊기면 신규 조회·편집을 제공하지 않고, 끊기기 전 작성·전송 중인 내용과 요청 ID를 보호합니다. 재연결 후 기존 요청의 처리 결과부터 확인하며 서버 성공 확인 전에는 저장 완료로 표시하지 않습니다. 오프라인 변경 대기열을 쌓는 방식으로 확장하지 않습니다. 서버의 중복 요청 처리와 별개로 앱 복구 화면·기기 검증은 남아 있습니다.

[온라인 요청·복구 계약](https://github.com/OlThing/docs/blob/main/design/api/sync-recovery.md)

</details>

<details>
<summary><strong>05 · 사진은 비공개로 두고, 접근과 삭제를 서버가 확인합니다</strong> — 연동 방향 채택</summary>

사진 저장은 비공개 S3를 초기 방향으로 정했습니다. 앱에 저장소 키나 공개 URL을 주지 않고, 서버가 현재 계정과 참조 권한을 검사해 업로드·조회를 중계합니다. 보관·복원·다른 항목의 참조를 확인한 뒤 파일을 정리하며, 일부 삭제 실패를 완료로 표시하지 않습니다. 실제 S3 연결과 업로드·삭제 시험은 후속입니다.

[사진 계약](https://github.com/OlThing/docs/blob/main/design/api/photos.md) · [외부 공급자 선택](https://github.com/OlThing/docs/blob/main/architecture/provider-sdk-selection-2026-10-11.md)

</details>

<details>
<summary><strong>06 · 로컬에서 검증하고, 지인 테스트 준비 때 원격으로 옮깁니다</strong> — 현재 운영 방향</summary>

지금은 WSL/Docker와 PostgreSQL·Mailpit으로 개발하고, PR마다 테스트·리뷰·원격 CI를 확인해 dev에 통합합니다. 다음은 이미지·환경/비밀값 분리·백업/복원·롤백 준비입니다. 유료 서버 생성과 도메인·HTTPS·실제 외부 메일 검증은 지인 테스트 준비 시점에 진행하기로 했습니다. 호스팅 상품은 아직 확정하지 않았습니다.

[개발 브랜치 운영](https://github.com/OlThing/olthing-server/blob/dev/docs/branching.md) · [최신 인프라 계획](https://github.com/OlThing/docs/issues/49)

</details>

## 개발 저장소

- [OlThing/olthing-server](https://github.com/OlThing/olthing-server/tree/dev) — 서버 코드·테스트·마이그레이션. `dev`에서 개발을 통합하고 `main`으로 운영 릴리스를 승격
- [OlThing/olthing](https://github.com/OlThing/olthing) — 모바일 앱 저장소. 현재는 초기 안내·협업 설정 단계
- [OlThing/docs](https://github.com/OlThing/docs) — 요구사항과 설계 문서

개발·문서 저장소는 팀 전용일 수 있어 접근 권한이 필요합니다.
