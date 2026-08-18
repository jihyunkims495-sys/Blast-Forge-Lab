# Blast-Forge-Lab

> A lab where ideas explode, failures teach, and successful ventures are forged.

개발 학습, AI Agent 실험, 학습 자동화, 커머스 × AI 아이디어를 실제 결과물로 축적하는 개인 실험 저장소입니다.

현재는 **AI Agent 엔지니어링 학습 과정**을 중심으로, 매일의 학습 기록을 남기고 반복 업무를 Workflow와 Agent 구조로 발전시키는 데 초점을 두고 있습니다.

---

## 1. Repository Goals

이 저장소의 목표는 단순한 공부 기록을 넘어 다음 과정을 하나의 시스템으로 연결하는 것입니다.

```text
학습
↓
실습
↓
오류와 질문 기록
↓
복습 / 평가
↓
TIL · WIL · README 정리
↓
GitHub 아카이빙
↓
반복 Workflow 발견
↓
자동화
↓
AI Agent 서비스로 확장
```

장기적으로는 Python, SQL, FastAPI, LLM, RAG, AI Agent 기술을 활용해 **직접 사용할 수 있는 AI 서비스와 개인 멀티에이전트 운영 시스템**을 구축하는 것을 목표로 합니다.

---

## 2. Current Structure

```text
Blast-Forge-Lab/
│
├── README.md
│
├── TIL/
│   └── 일일 학습 기록 및 학습 결과물
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
            │   │   └── WORKFLOWS.md
            │   ├── 02_학습_아카이브_매니저/
            │   │   └── WORKFLOWS.md
            │   ├── 03_MD_커리어_전략실/
            │   │   └── WORKFLOWS.md
            │   └── 04_시장_AI_리서치_센터/
            │       └── WORKFLOWS.md
            │
            ├── wiki/
            └── workspace/
                ├── inbox/
                ├── working/
                └── output/
```

---

## 3. TIL — Learning Archive

[`TIL/`](./TIL)에는 매일 학습한 내용을 날짜별로 기록합니다.

단순히 수업 내용을 복사하는 것이 아니라 다음 흐름을 기준으로 정리합니다.

1. 오늘 학습 전체 구조
2. 중요 개념 정리
3. 수업 중 헷갈렸던 내용과 오류
4. 문제 풀이 및 오답 분석
5. 최종 개념 정리
6. TIL 기록

현재 학습 로드맵:

```text
Python
→ SQL
→ FastAPI
→ AI Literacy
→ LLM / RAG
→ AI Agent Development
```

---

## 4. AGENT — Personal AI Operating System

[`AGENT/AGENT-GPT-Orchestrator/AGENT`](./AGENT/AGENT-GPT-Orchestrator/AGENT)는 GPT를 메인 Orchestrator로 두고 여러 AI와 Workflow를 역할별로 운영하기 위한 실험 공간입니다.

### Core Documents

| Document | Role |
|---|---|
| [`README.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/README.md) | AGENT 시스템 전체 개요 |
| [`AGENTS.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/AGENTS.md) | GPT / Gemini / Claude 역할 정의 |
| [`USER_GUIDE.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/USER_GUIDE.md) | 사용자 배경과 공통 협업 원칙 |
| [`ORCHESTRATOR.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/ORCHESTRATOR.md) | 요청 라우팅, Handoff, 자동화 판단 기준 |
| [`WORKFLOWS.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/WORKFLOWS.md) | 프로젝트를 넘나드는 시스템 Workflow 관리 |

---

## 5. Agent Roles

현재 멀티에이전트 구조는 다음 역할 분리를 기준으로 설계하고 있습니다.

```text
                    User
                     │
                     ▼
              GPT Orchestrator
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
      GPT         Gemini       Claude
   Orchestrator   Researcher    Reviewer
        │            │            │
        └────────────┼────────────┘
                     ▼
              Final Integration
                     │
                     ▼
             Files / GitHub / Tools
```

- **GPT Orchestrator**: 요청 분석, 작업 분해, 라우팅, 최종 판단 및 통합
- **Gemini Researcher**: 최신 정보 조사와 자료 비교를 담당할 전문 Agent 후보
- **Claude Reviewer**: 긴 문서 검토, 논리 점검, 누락 및 반론 탐색을 담당할 전문 Agent 후보

모든 작업에 여러 AI를 사용하는 것이 아니라, **역할이 필요한 경우에만 전문 Agent를 호출하는 구조**를 지향합니다.

---

## 6. Project Architecture

Agent 시스템 안의 프로젝트는 각각 하나의 전문 업무 영역을 담당합니다.

| Project | Responsibility |
|---|---|
| [`01_AI_학습_코치`](./AGENT/AGENT-GPT-Orchestrator/AGENT/projects/01_AI_학습_코치/WORKFLOWS.md) | 개념 학습, 코드 실행 흐름, 오류 분석, 평가와 복습 |
| [`02_학습_아카이브_매니저`](./AGENT/AGENT-GPT-Orchestrator/AGENT/projects/02_학습_아카이브_매니저/WORKFLOWS.md) | TIL/WIL/README 및 학습 결과 아카이빙 |
| [`03_MD_커리어_전략실`](./AGENT/AGENT-GPT-Orchestrator/AGENT/projects/03_MD_커리어_전략실/WORKFLOWS.md) | 채용, 직무 적합도, 역량 Gap, 포트폴리오 전략 |
| [`04_시장_AI_리서치_센터`](./AGENT/AGENT-GPT-Orchestrator/AGENT/projects/04_시장_AI_리서치_센터/WORKFLOWS.md) | 시장·산업·AI 최신 정보 조사와 기회 탐색 |

### Design Principle

```text
Project
= 누가 어떤 업무를 담당하는가

Workflow
= 그 업무를 어떤 순서로 처리하는가

Trigger
= 언제 작업을 시작하는가

Task
= 예약되어 실행되는 작업

Skill
= 반복 작업을 어떤 규칙으로 처리하는가

Tool
= 실제 외부 작업을 수행하는 수단
```

---

## 7. Active Workflow — Daily Learning Pipeline

현재 가장 먼저 운영 중인 시스템 Workflow는 **일일 학습 파이프라인**입니다.

```text
07:50 Daily Task
↓
오늘 교안 입력
↓
01_AI_학습_코치
↓
교안 전체 분석
↓
오늘 학습 전체 구조
↓
중요 개념 정리
↓
수업 중 질문 / 코드 / 오류 누적
↓
헷갈렸던 내용 리뷰
↓
"오늘 수업 끝"
↓
5지선다 + 서술형 문제 10개
↓
풀이 / 채점 / 오답 분석
↓
취약 개념 재학습
↓
최종 개념 정리
↓
02_학습_아카이브_매니저
↓
TIL 작성
↓
Blast-Forge-Lab 반영
```

이 Workflow의 목적은 단순 진도 관리가 아니라 **교안을 읽는 것 → 이해하는 것 → 스스로 설명하고 문제를 푸는 것 → 기록하는 것**까지 하나의 학습 사이클로 만드는 것입니다.

자세한 내용은 [`AGENT/WORKFLOWS.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/WORKFLOWS.md)에서 관리합니다.

---

## 8. Development Roadmap

현재는 ChatGPT Project와 Workflow를 활용해 업무 구조를 먼저 설계하고 있습니다.

향후 발전 순서:

```text
Phase 1
ChatGPT Projects + Instructions + Tasks + Workflows

↓

Phase 2
Python 함수로 Workflow 구현

↓

Phase 3
FastAPI + API + 상태 관리

↓

Phase 4
OpenAI Agent / Tool 연결

↓

Phase 5
GPT Orchestrator + Gemini + Claude

↓

Phase 6
Multi-Agent + MCP / Shared Tools + Evaluation
```

처음부터 복잡한 멀티에이전트 시스템을 만드는 대신, **실제로 반복되는 개인 업무를 먼저 발견하고 하나씩 자동화**하는 방식을 사용합니다.

---

## 9. Working Principles

- 결과보다 **왜 그렇게 동작하는지 이해하는 것**을 우선합니다.
- 반복 작업은 관찰한 뒤 Workflow로 정의합니다.
- 자동화는 실제 시간 절감 효과가 있을 때 적용합니다.
- 최신 정보는 기억보다 원문과 공식 자료를 우선 확인합니다.
- AI 결과를 그대로 채택하지 않고 검증 단계를 둡니다.
- GitHub를 학습 기록과 Agent 운영 문서의 장기적인 Source of Truth로 발전시킵니다.

---

## 10. Current Focus

현재 집중하고 있는 두 가지 축은 다음과 같습니다.

### Learning
Python 기초부터 시작해 AI Agent 서비스를 직접 기획하고 구현할 수 있는 기술 기반을 쌓습니다.

### Agent System
매일 반복되는 학습·리서치·아카이빙·커리어 업무를 Workflow로 구조화하고, 이후 Python과 API를 통해 실제 Agent 서비스로 구현합니다.

---

## Status

**Active Development**

이 저장소는 완성된 결과물 저장소라기보다, 학습과 실험을 통해 구조 자체가 계속 개선되는 **개인 AI Agent Lab**입니다.
