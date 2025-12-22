<!--
✅ 좋은 ADR 제목을 작성하는 방법
기본 원칙:
ADR 제목은 해당 문서가 어떤 기술적 결정을 다뤘는지를 간결하고 명확하게 요약해야 합니다.
이해하기 쉬운 동사와 핵심 명사를 활용하여, 한눈에 "무엇을 왜 결정했는가"를 알 수 있도록 만드세요.

✍️ 제목 작명 가이드
행동 중심 동사로 시작하세요.
예: Use, Choose, Switch, Deprecate, Adopt

무엇을 결정했는지를 짧고 명확하게 표현하세요.
예: Use Airflow for DAG orchestration

가능하면 '왜' 혹은 '언제'에 대한 간단한 맥락도 포함하세요.
예: Adopt batch ingestion for MVP stability

일관된 스타일을 유지하세요.
예: Verb + 대상 + 맥락 형식

📚 예시
- Use Airflow for DAG orchestration
- Adopt batch ingestion for low-volume data
- Switch from S3 to Delta Lake for data lake
- Reject real-time ingestion due to infra constraints
- Deprecate cron-based jobs in favor of managed scheduler
-->
# ADR-004: Separate Intermediate schema

## Status
<!-- 현재 이 결정의 상태는? -->
<!-- 예: Proposed, Accepted, Rejected, Superseded -->
Status: Accepted

## Date
<!-- 이 결정을 작성한 날짜는? -->
2025-12-22

---

## 1. Context (배경 및 문제 정의)
dbt 모델링 구조가 다음과 같이 되어 있는데, 중간 가공 데이터가 원본 데이터와 섞이지 않도록 별도 스키마로 분리하고자 함
- stgaing(stg_) : raw_data 스키마에 view 생성
- intermediate(int_) : raw_data 스키마에 table 생성
- marts(fact_, dim_) : analytics 스키마에 table 생성


## 2. Decision (내린 결정)
intermediate 스키마를 생성하여 분리
- stgaing(stg_) : raw_data 스키마에 view 생성
- intermediate(int_) : intermediate 스키마에 table 생성
- marts(fact_, dim_) : analytics 스키마에 table 생성

## 3. Alternatives Considered (고려했던 대안들)
- intermediate(int_) : analytics 스키마에 view 생성

## 4. Rationale (결정의 이유)
- view로 생성할 경우, 데이터가 많아지면 성능이 저하됨

## 5. Consequences (영향 및 결과)
- 원본 데이터와 가공 중인 데이터가 물리적으로 분리되어 스키마 관리가 명확해짐

## 6. Related Decisions (관련 ADR 문서)


## 7. References (참고 자료)
