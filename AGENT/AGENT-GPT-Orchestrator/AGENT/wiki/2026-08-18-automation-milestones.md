# 2026-08-18 Automation Milestones

오늘 구축한 핵심 자동화 및 운영 체계를 기록합니다.

## 1. 일일 학습 파이프라인 자동화

### 목적
교안 입력부터 복습, 평가, TIL, GitHub 반영 준비까지 하나의 학습 사이클로 연결합니다.

### 핵심 흐름
```text
07:50 예약 Task
↓
오늘 교안 입력
↓
교안 분석
↓
오늘 학습 전체 구조 / 중요 개념 정리
↓
수업 중 질문 · 코드 · 오류 누적
↓
"오늘 수업 끝"
↓
5지선다 + 서술형 10문제
↓
채점 / 오답 분석 / 취약 개념 복습
↓
최종 개념 정리
↓
TIL
↓
GitHub 반영 준비
```

### 현재 자동화 수준
- 매일 07:50 학습 시작 Task: 자동
- 교안 전달 이후 학습 진행: 대화형
- `오늘 수업 끝` 이후 퀴즈 전환: 대화 신호 기반
- 답안 제출 이후 채점/복습: 대화형
- 중요 파일 변경: Human-in-the-loop

---

## 2. GPT Orchestrator 운영 구조

### 목적
사용자 요청을 분석해 적절한 Project, Workflow, Agent, Tool로 라우팅하고 결과를 통합합니다.

### 현재 역할 구조
```text
User
↓
GPT Orchestrator
├─ Project Routing
├─ Workflow Selection
├─ Tool Selection
├─ Gemini Researcher 후보
└─ Claude Reviewer 후보
↓
검증 및 최종 통합
```

### 핵심 운영 규칙
- 단순 작업은 GPT가 직접 처리
- 역할이 필요한 경우에만 전문 Agent 사용
- Project 간 Handoff 시 목표, 완료 내용, 남은 작업, 기대 출력 전달
- 반복 업무는 즉시 자동화하지 않고 빈도/효과/위험을 평가

---

## 3. 프로젝트별 Workflow 관리 체계

### 목적
시스템 전체 Workflow와 각 Project 내부 Workflow를 분리해 관리합니다.

### 구조
```text
AGENT/WORKFLOWS.md
= 여러 Project를 연결하는 System Workflow

projects/01_AI_학습_코치/WORKFLOWS.md
= 학습 코치 내부 Workflow

projects/02_학습_아카이브_매니저/WORKFLOWS.md
= 학습 기록 및 아카이빙 Workflow

projects/03_MD_커리어_전략실/WORKFLOWS.md
= 커리어 분석 Workflow

projects/04_시장_AI_리서치_센터/WORKFLOWS.md
= 시장/AI 리서치 Workflow
```

### 핵심 개념 분리
- Project: 누가 어떤 업무를 담당하는가
- Workflow: 업무를 어떤 순서로 처리하는가
- Trigger: 언제 Workflow를 시작하는가
- Task: 예약되어 실행되는 작업
- Skill: 반복 작업을 수행하는 규칙
- Tool: 외부 작업을 수행하는 수단
- Orchestrator: 전체 흐름을 판단하고 조정하는 관리자

---

## 4. README 버전 아카이브 체계

### 목적
루트 `README.md`는 항상 최신 포트폴리오 상태를 유지하고, 큰 구조 변경 전에는 이전 버전을 보존합니다.

### 운영 구조
```text
README.md
= 최신 포트폴리오

archive/README/
= 중요한 과거 버전 스냅샷
```

### 아카이브 기준
다음과 같은 중대한 변경 전에 이전 버전을 저장합니다.
- 저장소 목적 또는 방향 변경
- Agent / Workflow 구조 대규모 변경
- 포트폴리오 전면 개편
- 개발 Phase 변경

오타, 표현 수정, 작은 링크 수정 등은 별도 아카이브하지 않습니다.

### 첫 기준선
- `archive/README/2026-08-18_v1.md`

---

## 오늘의 핵심 의미

오늘의 결과는 단순히 몇 개의 문서를 만든 것이 아니라 다음 구조를 처음 운영 가능한 형태로 만든 것입니다.

```text
반복되는 개인 업무 발견
↓
Project로 역할 분리
↓
Workflow로 순서 정의
↓
Trigger / Task로 시작 조건 설정
↓
Orchestrator가 전체 흐름 관리
↓
GitHub에 운영 규칙과 결과 축적
```

즉, ChatGPT를 단순 질의응답 도구가 아니라 **개인 학습과 업무 흐름을 관리하는 Orchestrator**로 발전시키기 위한 첫 운영 버전입니다.

## 다음 발전 방향
1. Daily Learning Pipeline의 실제 사용 데이터 축적
2. 반복되는 수동 단계 식별
3. Python 함수로 Workflow 일부 구현
4. GitHub/File 자동화 강화
5. FastAPI 기반 상태 관리
6. Gemini / Claude API 연동
7. Multi-Agent Orchestration으로 확장
