## 📘 Architecture Decision Records (ADR)

### 🧭 목적 (Purpose)

이 리포지토리는 우리 팀의 **기술적 아키텍처 결정**을 기록하기 위해 존재합니다.
모든 중요한 기술 결정은 그 당시의 맥락, 고려했던 대안, 근거, 결과 등을 문서화하여
**지속 가능한 협업, 빠른 온보딩, 일관된 기술 판단**을 가능하게 합니다.

### 📚 ADR이란?

**ADR (Architecture Decision Record)** 는 특정 기술적 문제에 대해 **무엇을, 왜, 어떻게 결정했는지를 기록하는 문서**입니다.
짧고 명확한 문서로, 이후에 팀원들이 같은 결정을 반복하거나 질문하지 않도록 도와줍니다.

> 참고: [Architecture Decision Record](https://continuous-architecture.org/docs/practices/architecture-decision-records.html)

### 🔖 ADR 목록

| 번호      | 제목                                                                                  | 상태            | 요약                   |
| ------- | ----------------------------------------------------------------------------------- | ------------- | -------------------- |
| ADR-001 | [Deprecate cron in favor of scheduler](./adr-001-deprecate-cron.md)                 | 🔁 Superseded | cron 대신 Airflow로 전환  |
| ADR-002 | [Use Airflow for DAG orchestration](./adr-002-use-airflow-for-dag-orchestration.md) | ✅ Accepted    | 워크플로우 도구로 Airflow 채택 |
| ADR-003 | [Adopt batch processing for ETL](./adr-003-adopt-batch-processing.md)               | 🟡 Proposed   | 배치 기반 파이프라인 선택       |

> 새로운 ADR을 작성하면 이 표에도 추가해주세요. (상태 이모지는 변경 가능)

### 🛠️ 작성 및 사용법

#### 📁 디렉토리 구조

```
/adr
  ├── docs
    ├── adr-001-deprecate-cron.md
    ├── adr-002-use-airflow-for-dag-orchestration.md
    ├── adr-003-adopt-batch-processing.md
  ├── template
    ├── ADR-000-template.md
```

#### 🧱 파일 작명 규칙

* `adr-XXX-short-title.md` 형식 (번호는 순차적으로 증가)
* 제목은 \[Verb + 대상 + 맥락] 형식으로 짧게

예시:

* `adr-004-adopt-prefect-for-orchestration.md`

#### ✅ 상태 관리

* 🟡 `Proposed`: 제안된 상태, 아직 검토 중
* ✅ `Accepted`: 채택됨, 실행 중이거나 완료됨
* ❌ `Rejected`: 검토되었지만 채택되지 않음
* 🔁 `Superseded`: 다른 결정에 의해 대체됨

### ✍️ 템플릿

[`template.md`](./template/ADR-0000-template.md)를 복사해 새 ADR을 작성하세요.
각 항목에 대해 다음과 같은 질문에 답하며 작성합니다:

| 항목                | 질문                          |
| ----------------- | --------------------------- |
| Context           | 왜 이 결정이 필요한가? 어떤 문제가 있었나?   |
| Decision          | 우리는 무엇을 결정했는가?              |
| Alternatives      | 다른 대안은 무엇이 있었고, 왜 선택하지 않았나? |
| Rationale         | 이 선택이 가장 적합하다고 판단한 이유는?     |
| Consequences      | 이 결정으로 인해 발생할 영향은?          |
| Related Decisions | 관련된 다른 ADR이 있는가?            |
| References        | 참고한 문서, 회의 기록 등은?           |

### 🧪 예시 문서
{TBD}
* [adr-001-deprecate-cron.md](./adr-001-deprecate-cron.md)
* [adr-002-adopt-batch-processing.md](./adr-002-adopt-batch-processing.md)

### 🤝 기여 가이드

* 새 ADR을 작성할 경우 `template.md`를 복사해 번호를 붙이세요.
* 팀 내에서 논의 후 `Status`를 `Accepted`로 바꾸어 병합합니다.
* 기존 ADR을 대체할 경우, `README.md`의 ADR 목록의 상태를 `🔁 Superseded`로 변경하세요.
* **반드시 위 ADR 목록에도 항목을 추가**하세요.

> 🧠 *“기억은 흐려지지만, 기록은 남는다.” — 의사결정을 미래의 팀원에게 선물하세요.*
