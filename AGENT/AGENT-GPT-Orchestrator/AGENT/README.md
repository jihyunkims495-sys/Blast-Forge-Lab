# AGENT

GPT를 메인 오케스트레이터로 두고 Gemini, Claude 등 여러 AI를 역할별로 활용하기 위한 개인 멀티에이전트 운영 공간입니다.

## 목적
- GPT를 메인 Orchestrator로 사용
- 사용자 요청을 작업 단위로 분해
- 각 AI의 장점에 맞춰 업무 배정
- 프로젝트별 역할과 Workflow를 분리해 관리
- 중간 결과와 최종 결과를 workspace에 기록
- 반복되는 흐름을 발견한 뒤 Task, Python, API로 자동화

## 현재 구성
| 역할 | 모델 | 주요 업무 |
|---|---|---|
| Orchestrator | GPT | 요청 분석, 작업 분해, 배정, 검토, 최종 통합 |
| Researcher | Gemini | 최신 정보 조사, 자료 비교, Google 생태계 관련 업무 |
| Reviewer | Claude | 긴 문서 검토, 논리 점검, 누락 및 반론 탐색 |

## 핵심 개념
| 개념 | 의미 |
|---|---|
| Project | 특정 목적과 책임을 가진 업무 영역 |
| Workflow | 작업이 진행되는 반복 가능한 전체 순서 |
| Trigger | Workflow 또는 Task를 시작시키는 조건/신호 |
| Task | 특정 시간이나 조건에 실행되는 예약 작업 |
| Skill | 반복 작업을 수행하는 방법과 규칙 |
| Tool | 파일, GitHub, 웹, API 등 실제 외부 작업을 수행하는 수단 |

## 기본 흐름
1. 사용자가 GPT에게 요청한다.
2. GPT Orchestrator가 직접 처리할지 적절한 Project/Workflow/Agent로 보낼지 판단한다.
3. 필요한 경우 Gemini 또는 Claude에 전문 작업을 배정한다.
4. 필요한 Tool을 사용한다.
5. 중간 결과를 `workspace/working`에 기록한다.
6. GPT가 결과를 검토·통합한다.
7. 최종 결과를 `workspace/output` 또는 대상 저장소에 반영한다.

## 문서 역할
- `README.md`: 전체 시스템 개요와 구조
- `AGENTS.md`: GPT/Gemini/Claude 등 Agent의 역할과 책임
- `USER_GUIDE.md`: 사용자 협업 방식과 공통 지침
- `ORCHESTRATOR.md`: Project/Workflow/Agent/Tool 라우팅과 자동화 판단 규칙
- `WORKFLOWS.md`: 프로젝트를 넘나드는 시스템 수준 Workflow
- `projects/*/WORKFLOWS.md`: 각 Project 내부 Workflow
- `agents/*.md`: 모델별 세부 Agent 역할
- `workspace/`: 작업 입력, 진행 중 결과, 최종 산출물

## 프로젝트 구조
```text
projects/
├─ 01_AI_학습_코치/
│  └─ WORKFLOWS.md
├─ 02_학습_아카이브_매니저/
│  └─ WORKFLOWS.md
├─ 03_MD_커리어_전략실/
│  └─ WORKFLOWS.md
└─ 04_시장_AI_리서치_센터/
   └─ WORKFLOWS.md
```

## 시스템 Workflow
현재 첫 번째 정식 System Workflow는 `WF-001 일일 학습 파이프라인`입니다.

```text
교안 입력
↓
01_AI_학습_코치
↓
개념 학습 / 질문 / 코드 / 오류 누적
↓
평가 문제 / 채점 / 취약 개념 복습
↓
02_학습_아카이브_매니저
↓
TIL / 필요 시 README·WIL
↓
GitHub
```

상세 내용은 `WORKFLOWS.md`에서 관리합니다.

## 전체 폴더 구조
```text
AGENT/
├─ README.md
├─ USER_GUIDE.md
├─ AGENTS.md
├─ ORCHESTRATOR.md
├─ WORKFLOWS.md
├─ agents/
│  ├─ gpt-orchestrator.md
│  ├─ gemini-researcher.md
│  └─ claude-reviewer.md
├─ projects/
│  ├─ 01_AI_학습_코치/
│  │  └─ WORKFLOWS.md
│  ├─ 02_학습_아카이브_매니저/
│  │  └─ WORKFLOWS.md
│  ├─ 03_MD_커리어_전략실/
│  │  └─ WORKFLOWS.md
│  └─ 04_시장_AI_리서치_센터/
│     └─ WORKFLOWS.md
├─ wiki/
│  └─ README.md
└─ workspace/
   ├─ inbox/
   ├─ working/
   └─ output/
```

## 운영 원칙
- 역할을 모델보다 먼저 정의한다.
- 모든 작업에 여러 Agent를 사용하지 않는다.
- 단순 작업은 GPT가 직접 처리한다.
- 반복성이 확인된 작업만 Workflow/자동화로 승격한다.
- GitHub 문서를 운영 원본(Source of Truth)으로 사용한다.
- 기존 중요 파일을 덮어쓰거나 삭제할 때는 변경 범위를 먼저 확인한다.
- 현재 구조가 충분할 때 불필요한 계층이나 Agent를 추가하지 않는다.

## 발전 로드맵
```text
ChatGPT Project + Workflow + Task
↓
Python 함수와 상태 관리
↓
FastAPI + API + Tool
↓
GPT Orchestrator Agent
↓
Gemini / Claude API 연동
↓
역할 기반 Multi-Agent
↓
필요 시 MCP / 공통 Tool 계층
```
