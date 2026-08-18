# Agent Wiki

AI Agent와 멀티에이전트 시스템을 만들면서 알게 된 개념, 사용법, 시행착오를 기록합니다.

처음에는 이 파일을 인덱스로 사용하고, 중요한 운영 기록과 학습 내용은 개별 파일로 분리합니다.

## Library Index

### 2026-08-18
- [`Automation Milestones`](./2026-08-18-automation-milestones.md) — 일일 학습 파이프라인, GPT Orchestrator, 프로젝트별 Workflow, README 아카이브 체계 정리

## Agent
목표를 받아 판단하고 필요한 행동이나 도구 사용을 통해 결과를 만드는 AI 시스템.

## Orchestrator
여러 Agent 또는 Tool의 작업 순서와 역할을 관리하는 중앙 관리자.

현재 구조에서는 GPT가 Orchestrator 역할을 맡습니다.

## Multi-Agent
여러 Agent가 서로 다른 역할을 맡아 하나의 목표를 해결하는 구조.

```text
User
 ↓
GPT Orchestrator
 ├─ Gemini Researcher
 └─ Claude Reviewer
 ↓
Final Output
```

## Tool Calling
AI 모델이 외부 함수나 도구를 선택해서 사용하도록 연결하는 방식.

## MCP
AI와 외부 도구 또는 데이터 소스를 연결하기 위한 표준화된 방식.

## Lessons Learned

### YYYY-MM-DD
-
