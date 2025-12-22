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
# ADR-001: self-hosted runner를 이용한 ec2 자동 배포

## Status
<!-- 현재 이 결정의 상태는? -->
<!-- 예: Proposed, Accepted, Rejected, Superseded -->
Status: Accepted

## Date
2025-12-10

---

## 1. Context (배경 및 문제 정의)
- aws 개인 계정으로, ec2 위에서 docker로 airflow 띄우는 작업을 연습하던 중, git pull을 계속 수동으로 해줘야 하는 것에 불편함을 느낌
- github main에 push 되면 바로 ec2에서 빌드 및 배포되는 방법을 찾아보게 됨

## 2. Decision (내린 결정)
EC2에 GitHub Actions Runner(self-hosted runner) 설치

## 3. Alternatives Considered (고려했던 대안들)
1. GitHub Actions → EC2로 SSH 접속 → docker compose build/run 실행
2. Cron(잡 스케줄러)을 사용해서 EC2가 스스로 주기적으로 git pull 과 docker compose build/run 실행

## 4. Rationale (결정의 이유)
1. EC2로 접속하기 위해서는 Github Actions Runners의 IP 대역을 보안그룹에 등록해줘야함
self-hosted runner를 이용하면 ec2 내부에 서비스를 등록해서 사용하는 것이기 때문에 인바운드를 열 필요가 없음
2. 즉시 배포가 아니고 반복 주기에 따라 지연 발생

## 5. Consequences (영향 및 결과)
* 장점
CI/CD 파이프라인이 ec2 내부에서 완성되므로 outbound 연결만 필요
즉시 배포 가능
* 단점
runner가 돌아가는 동안 ec2 cpu를 조금씩 계속 사용하고 있음

## 6. Related Decisions (관련 ADR 문서)
<!--
- 이 결정과 직접 연결되거나 영향을 주고받는 ADR이 있는가?
- 만약 있다면 번호와 제목을 함께 명시하자.
-->

## 7. References (참고 자료)
<!--
- 이 결정을 내리는 데 참고한 문서, 회의록, 외부 글 등이 있다면 모두 정리
- 내부 위키 문서, 기술 블로그, 테스트 결과, 회의 기록 등을 포함
-->
테스트 결과
https://github.com/hanbyeolkang/settingTest
