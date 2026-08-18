# Blast-Forge-Lab

> **Learning → Workflow → Automation → AI Agent**
>
> A personal lab for turning daily learning, repeated work, and business ideas into reusable AI systems.

`Blast-Forge-Lab`은 AI Agent 엔지니어링 학습과 개인 업무 자동화를 하나의 흐름으로 연결하는 실험 저장소입니다.

현재는 **Python 기초 학습**, **학습 자동화 Workflow**, **GPT 중심 Orchestrator 구조**를 실제 문서와 GitHub 운영 방식으로 설계하고 있습니다.

---

## What I am building

이 저장소의 핵심은 단순한 TIL 기록이 아니라, 반복되는 개인 업무를 발견하고 다음 단계로 발전시키는 것입니다.

```text
Learning
↓
Practice
↓
Questions / Errors
↓
Review & Evaluation
↓
TIL / WIL / README
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

## Current Highlights

### 1. Daily Learning Pipeline

매일 교안 입력부터 복습, 평가, TIL 기록까지 연결하는 학습 Workflow를 운영하고 있습니다.

```text
07:50 Task
↓
오늘 교안 입력
↓
교안 구조 분석
↓
핵심 개념 정리
↓
수업 중 질문 / 코드 / 오류 누적
↓
"오늘 수업 끝"
↓
5지선다 + 서술형 10문제
↓
채점 / 오답 분석
↓
취약 개념 재학습
↓
최종 개념 정리
↓
TIL
↓
GitHub Archive
```

이 Pipeline의 목적은 단순히 진도를 빠르게 나가는 것이 아니라,

> **읽기 → 이해 → 설명 → 문제 해결 → 기록**

까지 하나의 학습 사이클로 만드는 것입니다.

자세한 설계는 [`AGENT/WORKFLOWS.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/WORKFLOWS.md)에서 관리합니다.

---

### 2. GPT Orchestrator Architecture

GPT를 메인 Orchestrator로 두고 업무 유형에 따라 전문 Agent 또는 Project로 라우팅하는 구조를 설계하고 있습니다.

```text
                         User
                          │
                          ▼
                  GPT Orchestrator
                          │
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
       Projects        Gemini          Claude
          │           Researcher       Reviewer
          │               │               │
          └───────────────┼───────────────┘
                          ▼
                   Final Integration
                          │
                          ▼
                GitHub / Files / Tools
```

현재 역할 정의:

- **GPT Orchestrator** — 요청 분석, 작업 분해, 라우팅, 검증, 최종 통합
- **Gemini Researcher** — 최신 정보 조사와 자료 비교를 담당할 전문 Agent 후보
- **Claude Reviewer** — 긴 문서 검토, 논리 점검, 누락 및 반론 탐색을 담당할 전문 Agent 후보

핵심 원칙은 **모든 작업에 여러 AI를 호출하지 않는 것**입니다. 필요한 역할이 있을 때만 전문 Agent를 사용합니다.

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
            │   ├── 03_MD_커리어_전략실/
            │   └── 04_시장_AI_리서치_센터/
            │
            ├── wiki/
            └── workspace/
                ├── inbox/
                ├── working/
                └── output/
```

---

## Project Architecture

각 Project는 하나의 전문 업무 영역을 담당합니다.

| Project | Responsibility |
|---|---|
| [`01_AI_학습_코치`](./AGENT/AGENT-GPT-Orchestrator/AGENT/projects/01_AI_학습_코치/WORKFLOWS.md) | 개념 학습, 코드 실행 흐름, 오류 분석, 퀴즈와 취약 개념 복습 |
| [`02_학습_아카이브_매니저`](./AGENT/AGENT-GPT-Orchestrator/AGENT/projects/02_학습_아카이브_매니저/WORKFLOWS.md) | TIL, WIL, README 및 학습 결과 아카이빙 |
| [`03_MD_커리어_전략실`](./AGENT/AGENT-GPT-Orchestrator/AGENT/projects/03_MD_커리어_전략실/WORKFLOWS.md) | 채용, 직무 적합도, 역량 Gap, 포트폴리오 전략 |
| [`04_시장_AI_리서치_센터`](./AGENT/AGENT-GPT-Orchestrator/AGENT/projects/04_시장_AI_리서치_센터/WORKFLOWS.md) | 시장·산업·AI 최신 정보 조사 및 기회 탐색 |

프로젝트를 분리하는 기준은 **역할과 책임의 분리(Separation of Concerns)** 입니다.

---

## Core Operating Documents

| Document | Purpose |
|---|---|
| [`AGENT/README.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/README.md) | Agent System 전체 개요 |
| [`AGENTS.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/AGENTS.md) | GPT / Gemini / Claude 역할 정의 |
| [`USER_GUIDE.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/USER_GUIDE.md) | 사용자 배경과 공통 협업 원칙 |
| [`ORCHESTRATOR.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/ORCHESTRATOR.md) | Routing, Handoff, 자동화 판단 기준 |
| [`WORKFLOWS.md`](./AGENT/AGENT-GPT-Orchestrator/AGENT/WORKFLOWS.md) | 프로젝트를 넘나드는 System Workflow 관리 |

---

## System Design Concepts

이 저장소에서는 다음 개념을 분리해 관리합니다.

| Concept | Meaning |
|---|---|
| **Project** | 누가 어떤 업무를 담당하는가 |
| **Workflow** | 업무를 어떤 순서로 처리하는가 |
| **Trigger** | 언제 Workflow를 시작하는가 |
| **Task** | 특정 시간/조건에 실행되는 예약 작업 |
| **Skill** | 반복 작업을 수행하는 방법과 규칙 |
| **Tool** | GitHub, Files, API 등 실제 외부 작업 수단 |
| **Orchestrator** | 어떤 Project / Agent / Tool을 사용할지 결정하고 결과를 통합하는 관리자 |

이 구조는 향후 Python과 FastAPI로 Agent 서비스를 구현할 때 그대로 코드 구조로 발전시킬 예정입니다.

---

## Learning Archive

[`TIL/`](./TIL)은 수업 내용을 단순 복사하는 공간이 아니라 **이해 과정과 시행착오를 남기는 기록**으로 운영합니다.

기본 기록 구조:

1. 오늘 학습 전체 구조
2. 중요 개념
3. 코드 실행 흐름
4. 질문과 오류
5. 헷갈렸던 개념
6. 문제 풀이 / 오답
7. 최종 개념 정리
8. TIL

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
+ Scheduled Tasks
+ Markdown Workflows
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

### Phase 5 — Multi-Model Orchestration

```text
GPT Orchestrator
├── OpenAI
├── Gemini
├── Claude
└── Shared Tools / MCP
```

각 모델을 단순 비교하는 대신 **역할 기반 Specialist**로 사용합니다.

---

## What this repository demonstrates

이 저장소에서 보여주고자 하는 것은 단순히 "AI 도구를 사용했다"는 사실이 아닙니다.

- 문제를 **역할과 책임**으로 분해하는 능력
- 반복 작업을 **Workflow**로 구조화하는 능력
- 사람의 판단과 자동화 가능한 단계를 구분하는 능력
- 학습 중 발생하는 오류와 시행착오를 기록하고 개선하는 과정
- AI 출력물을 그대로 사용하지 않고 검증 단계를 설계하는 방식
- 학습한 Python / API / Agent 개념을 실제 개인 시스템에 연결하는 과정

---

## Working Principles

- 먼저 이해하고, 그 다음 자동화합니다.
- 반복되지 않는 작업을 성급하게 자동화하지 않습니다.
- 복잡한 Multi-Agent 구조보다 작은 Workflow 하나를 제대로 동작시키는 것을 우선합니다.
- 최신 정보는 공식 자료와 원문을 기준으로 확인합니다.
- AI의 결과는 검증 없이 최종 결과로 채택하지 않습니다.
- GitHub를 학습 기록과 Agent 운영 문서의 **Source of Truth**로 발전시킵니다.

---

## Current Status

**Active Development**

현재는 Python 기초 학습과 동시에 `Daily Learning Pipeline`을 운영하며, 이를 향후 Python → FastAPI → AI Agent 서비스로 발전시키고 있습니다.

이 저장소는 완성된 결과물만 보여주는 공간이 아니라,

> **문제를 발견하고 → 구조화하고 → 학습하고 → 자동화하고 → 실제 Agent로 발전시키는 과정**

을 기록하는 개인 AI Engineering Lab입니다.
