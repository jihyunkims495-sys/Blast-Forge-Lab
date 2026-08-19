# Blast-Forge-Lab

> **Learning → Workflow → Automation → AI Agent**
>
> A personal lab for turning daily learning, repeated work, and business ideas into reusable AI systems.

`Blast-Forge-Lab`은 AI Agent 엔지니어링 학습과 개인 업무 자동화를 하나의 흐름으로 연결하는 실험 저장소입니다.

현재는 **Python 기초 학습**, **학습 자동화 Workflow**, **GPT 중심 Orchestrator 구조**를 실제 문서와 GitHub 운영 방식으로 설계하고 있습니다.

---

## What I am building

이 저장소의 핵심은 단순한 TIL 기록이 아니라, 반복되는 개인 업무와 학습 패턴을 발견하고 다음 단계로 발전시키는 것입니다.

```text
Learning
↓
Practice
↓
Questions / Errors
↓
Review & Evaluation
↓
TIL / WIL / Learner State
↓
Reusable Workflow
↓
Automation
↓
AI Agent Service
```

장기적으로는 다음 기술을 연결해 **직접 사용할 수 있는 AI Agent 서비스**와 **개인 Multi-Agent 운영 시스템**을 구축하는 것이 목표입니다.

`Python → SQL → FastAPI → LLM → RAG → AI Agent → Multi-Agent`

---

# Learning System Architecture v2.0

**Version:** 2.0  
**Designed:** 2026-08-19  
**Effective Date:** 2026-08-20

## Why v2.0

초기 학습 Workflow에서는 `01_AI_학습_코치`와 `02_학습_아카이브_매니저`가 모두 학습 내용을 다루면서 역할과 데이터 소유권이 겹칠 가능성이 있었습니다.

v2.0에서는 책임을 다음과 같이 분리합니다.

```text
01_AI_학습_코치
= Learn

02_학습_아카이브_매니저
= Archive

GitHub
= Source of Truth
```

핵심 변경점은 다음과 같습니다.

1. 학습과 아카이빙 책임을 분리합니다.
2. 실습 문제는 정답 코드보다 설계를 먼저 수행합니다.
3. `LEARNER_STATE.md`를 01과 02 사이의 상태 전달 인터페이스로 사용합니다.
4. 01은 학습 상태 업데이트 후보를 만들고, 02가 기존 상태와 비교해 canonical 상태를 관리합니다.
5. 새로운 예제는 이미 학습한 개념을 기반으로 점진적으로 확장합니다.

---

## Daily Learning Loop v2.0

```text
01_AI_학습_코치
│
├─ 교안 입력
├─ 수업 내용 질문
├─ 개념 학습
├─ 복습
├─ 실습 문제 설계
├─ 코드 작성
├─ 오류 분석
└─ LEARNER_STATE 업데이트 후보 생성
        │
        ▼
02_학습_아카이브_매니저
│
├─ 기존 LEARNER_STATE 확인
├─ 오늘 학습 기록과 비교
├─ TIL 업데이트
├─ 학습 상태 변화 검증
├─ WIL 추적 항목 관리
└─ canonical LEARNER_STATE 갱신
        │
        ▼
GitHub
Source of Truth
```

### Daily usage

```text
학습 중
→ 01_AI_학습_코치

학습 종료
→ "오늘의 학습내용 정리해줘"
→ LEARNER_STATE 업데이트 후보 생성

기록 관리
→ 02_학습_아카이브_매니저
→ 기존 상태와 비교
→ TIL / WIL / LEARNER_STATE 갱신
→ 사용자 승인
→ GitHub 반영
```

---

## Project Responsibility

| Project | Primary Responsibility | Does Not Own |
|---|---|---|
| `01_AI_학습_코치` | 개념 학습, 문제 설계, 코드 실행 흐름, 오류 분석, 복습, 학습 상태 관찰 | GitHub 아카이빙, TIL/WIL 최종 관리 |
| `02_학습_아카이브_매니저` | TIL/WIL/README, 학습 상태, GitHub/Notion 기록 관리 | 새로운 개념 강의, 실습 문제 코칭 |

프로젝트를 분리하는 기준은 **역할과 책임의 분리(Separation of Concerns)** 입니다.

---

## Learner State

`LEARNER_STATE.md`는 전체 학습 기록을 복사한 문서가 아니라 **현재 학습 상태를 빠르게 파악하기 위한 compact state**입니다.

주요 내용:

- 현재 학습 트랙
- 개념별 이해 상태
- 반복 오류
- 문제 설계 취약 단계
- 현재 학습 전략
- 최근 학습 방식 변경
- 다음 복습 포인트

데이터 소유권:

```text
01
→ 업데이트 후보 생성

02
→ 기존 상태와 비교 및 검증

GitHub
→ canonical LEARNER_STATE 저장
```

canonical 파일 위치:

`AGENT/AGENT-GPT-Orchestrator/AGENT/projects/02_학습_아카이브_매니저/LEARNER_STATE.md`

---

## Design Principles v2.0

1. **Separation of Concerns**  
   학습과 기록 관리를 분리합니다.

2. **Single Source of Truth**  
   장기 기록의 최종본은 GitHub에서 관리합니다.

3. **State over Full History**  
   매번 모든 과거 TIL을 읽는 대신 현재 상태 요약을 사용합니다.

4. **Progressive Learning**  
   새로운 예제는 이전에 안정적으로 이해한 개념 1~2개와 연결하여 점진적으로 확장합니다.

5. **Design Before Code**  
   실습 문제는 `입력 → 출력 → 변수 → 연산 → 제어구조 → 코드` 순서로 설계합니다.

6. **Human Approval**  
   학습 상태와 GitHub 기록의 중요한 변경은 사용자 검토 후 반영합니다.

---

## Repository Architecture

```text
Blast-Forge-Lab/
│
├── README.md
│
├── TIL/
│   └── Daily learning archive
│
└── AGENT/
    └── AGENT-GPT-Orchestrator/
        └── AGENT/
            ├── README.md
            ├── AGENTS.md
            ├── USER_GUIDE.md
            ├── ORCHESTRATOR.md
            ├── WORKFLOWS.md
            │
            ├── agents/
            │   ├── gpt-orchestrator.md
            │   ├── gemini-researcher.md
            │   └── claude-reviewer.md
            │
            ├── projects/
            │   ├── 01_AI_학습_코치/
            │   ├── 02_학습_아카이브_매니저/
            │   │   ├── WORKFLOWS.md
            │   │   └── LEARNER_STATE.md
            │   ├── 03_MD_커리어_전략실/
            │   └── 04_시장_AI_리서치_센터/
            │
            ├── wiki/
            └── workspace/
```

---

## Learning Archive

[`TIL/`](./TIL)은 수업 내용을 단순 복사하는 공간이 아니라 **이해 과정과 시행착오를 남기는 기록**으로 운영합니다.

### Current Learning Track

```text
Python
  ↓
SQL
  ↓
FastAPI
  ↓
AI Literacy
  ↓
LLM / RAG
  ↓
AI Agent Development
```

---

## Development Roadmap

### Phase 1 — Workflow Design `In Progress`

```text
ChatGPT Projects
+ Instructions
+ Markdown Workflows
+ Learner State
```

현재 단계에서는 반복되는 업무를 먼저 관찰하고, Project와 Workflow 단위로 구조화합니다.

### Phase 2 — Python Automation

```text
Workflow
↓
Python Functions
↓
File / GitHub Automation
↓
State Management
```

현재 Markdown으로 정의한 업무 흐름을 코드로 이전합니다.

### Phase 3 — Agent Service

```text
FastAPI
+ LLM API
+ Tools
+ State
```

학습 파이프라인과 개인 업무 Workflow를 실제 서비스로 구현합니다.

### Phase 4 — Multi-Agent

```text
GPT Orchestrator
├── Learning Agent
├── Research Agent
├── Career Agent
└── Archive Agent
```

---

## What this repository demonstrates

- 문제를 **역할과 책임**으로 분해하는 능력
- 반복 작업을 **Workflow**로 구조화하는 능력
- 사람의 판단과 자동화 가능한 단계를 구분하는 능력
- 학습 중 발생하는 오류와 시행착오를 기록하고 개선하는 과정
- AI 출력물을 그대로 사용하지 않고 검증 단계를 설계하는 방식
- 상태를 전체 이력과 분리하여 관리하는 방식
- 학습한 Python / API / Agent 개념을 실제 개인 시스템에 연결하는 과정

---

## Working Principles

- 먼저 이해하고, 그 다음 자동화합니다.
- 반복되지 않는 작업을 성급하게 자동화하지 않습니다.
- 복잡한 Multi-Agent 구조보다 작은 Workflow 하나를 제대로 동작시키는 것을 우선합니다.
- AI의 결과는 검증 없이 최종 결과로 채택하지 않습니다.
- GitHub를 학습 기록과 Agent 운영 문서의 **Source of Truth**로 사용합니다.
- 학습 상태는 `LEARNER_STATE.md`로 요약하고, 상세 이력은 TIL/WIL로 분리합니다.

---

## Version History

| Version | Date | Change |
|---|---|---|
| v1.x | 2026-08 | Daily Learning Pipeline 및 Project 기반 학습·아카이빙 구조 구축 |
| **v2.0** | **2026-08-19** | 01/02 책임 분리 강화, Design-First 학습 도입, `LEARNER_STATE.md` 기반 Handoff 구조 설계 |

---

## Current Status

**Active Development**

현재는 Python 기초 학습과 동시에 `Daily Learning Loop v2.0`을 운영하며, 이를 향후 Python → FastAPI → AI Agent 서비스로 발전시키고 있습니다.

> **문제를 발견하고 → 구조화하고 → 학습하고 → 기록하고 → 자동화하고 → 실제 Agent로 발전시키는 과정**을 기록하는 개인 AI Engineering Lab입니다.
