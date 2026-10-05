<div align="center">

# OlThing

### 복잡한 하루를 실행 가능한 계획으로

**OlThing은 일정과 할 일을 한곳에 모으고, 직접 관리하거나 AI의 제안을 확인하고 승인해 실행 가능한 계획으로 만드는 모바일 앱입니다.**

`API 설계 준비` · `온라인 전용 모바일 앱` · `개인 일정과 할 일`

</div>

## 어떤 경험을 만들고 있나요?

| 기능 | 경험 |
| --- | --- |
| 🗓️ Today · Calendar | 오늘의 고정 일정과 할 일, 주간 계획을 함께 봅니다. |
| ✅ Task · Goal | 할 일을 목표에 연결하고 진행 상태와 예상 시간을 관리합니다. |
| ✨ AI 제안 | 자연어 입력으로 기록 후보를 만들고, 별도 계획 요청으로 한 주의 빈 시간에 작업 블록을 제안받습니다. |
| 👀 미리보기와 승인 | AI 후보는 확인·수정·승인한 뒤 반영합니다. 수동 관리는 AI 없이도 가능합니다. |
| 🛍️ 쇼핑 · 사진 · 보관함 | 쇼핑 체크리스트와 사진을 기록하고, 보관한 항목을 날짜별로 모아 봅니다. |
| 📱 온라인 연결과 복구 | 연결 중단 전 작성·전송 중인 내용을 보호하고, 재연결 시 저장 결과를 확인합니다. 오프라인 신규 조회·편집은 제공하지 않습니다. |

> **현재는 구현 전 설계 단계입니다.** 위 내용은 출시된 기능 목록이 아니라 제품 목표입니다. 최신 기준은 [확정 정책](https://github.com/OlThing/docs/blob/main/requirements/approved-policies-2026-10-04.md)과 [기능 명세 목차](https://github.com/OlThing/docs/blob/main/planning/feature-spec-backlog-2026-10-04.md)에서 관리합니다.

## 출시 범위

| 단계 | 범위 |
| --- | --- |
| MVP · 무료 베타 | Task·Goal·Today·주간 Calendar, 자연어 기록 후보·주간 계획 승인, 쇼핑 체크리스트·사진 첨부·개인 보관함 |
| V1 | 월·일 Calendar·Board, 요청·승인에 따른 재계획, AI 조회·목표 분해·사진 인식, 기기 내 기본 알림, 개인 유료 상품 한 종류 |

가격·AI 사용량 한도·구매 채널은 보류 중입니다. V1 알림은 기본 꺼짐이며, 원격 푸시는 현재 범위에 포함하지 않습니다.

## 현재 진행 상황

2026-10-05 기준입니다. 문서·로컬 DB 검증과 앱 구현·출시 검증을 구분합니다.

| 작업 | 상태 |
| --- | --- |
| 요구사항·기능 명세 | 기능·사업성·공통 품질 문서 총 20개의 작성과 정책 대조 완료 |
| ERD · PostgreSQL | 35개 테이블·41개 관계 정제, 로컬 SQL 검증과 스키마 백업·복원 검증 완료 |
| API 계약 | 작성 순서와 목차 정리 완료. 다음 작업은 공통 규칙과 Task API 작성·검토 |
| 기술 선택 · 앱 구현 | 기술 비교·ADR·구현 준비는 후속이며, 앱 코드는 아직 없음 |
| 제품 · 운영 검증 | AI 벤치마킹·사용자 시험, 성능·동시성·실제 스토리지·운영 이전 검증은 후속 |

[ERD와 DB 검증 결과](https://github.com/OlThing/docs/blob/main/planning/erd-closeout-2026-10-05.md) · [API 계약과 구현 준비 방향](https://github.com/OlThing/docs/blob/main/planning/api-implementation-direction-2026-10-05.md)

## 기술 검토 방향

API 계약을 정리한 뒤 기술 비교와 ADR로 채택 근거를 남깁니다. 아래 구성은 검토 후보이며, 로컬 PostgreSQL 검증을 운영 인프라 구축 완료로 해석하지 않습니다.

| 영역 | 검토 방향 |
| --- | --- |
| 모바일 | React Native · Expo · TypeScript 후보. 로컬 저장은 연결 중단 시 입력 보호 등 온라인 정책에 맞춰 검토 |
| 서버 · 데이터 | Java 21 · Spring Boot · PostgreSQL 기반 단일 서버 후보 |
| AI · 계획 | 외부 AI는 기록 후보·해석을 담당하고, 시간 배치·소유권·승인 적용은 서버 규칙으로 처리 |
| 알림 | V1 기기 내 알림. Expo Notifications 후보 |
| 배포 · 운영 | Docker · GitHub Actions, 관리형 컨테이너·PostgreSQL 후보. AWS 세부 서비스는 비용·운영 검토 후 결정 |

[기능별 기술 후보](https://github.com/OlThing/docs/blob/main/architecture/feature-technology.md) · [API 명세 작성 목차](https://github.com/OlThing/docs/blob/main/design/api/README.md)

## 개발 저장소

- [OlThing/olthing](https://github.com/OlThing/olthing) — 앱·서버 구현용 저장소. 현재는 안내 문서만 있음
- [OlThing/docs](https://github.com/OlThing/docs) — 요구사항과 설계 문서

두 저장소는 팀 전용일 수 있어 접근 권한이 필요합니다.
