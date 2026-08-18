# AGENT

GPT를 메인 오케스트레이터로 두고 Gemini, Claude 등 여러 AI를 역할별로 활용하기 위한 개인 멀티에이전트 운영 공간입니다.

## 목적
- GPT를 메인 Orchestrator로 사용
- 사용자 요청을 작업 단위로 분해
- 각 AI의 장점에 맞춰 업무 배정
- 중간 결과와 최종 결과를 workspace에 기록
- 반복되는 흐름을 발견한 뒤 Python으로 자동화

## 현재 구성
| 역할 | 모델 | 주요 업무 |
|---|---|---|
| Orchestrator | GPT | 요청 분석, 작업 분해, 배정, 검토, 최종 통합 |
| Researcher | Gemini | 최신 정보 조사, 자료 비교, Google 생태계 관련 업무 |
| Reviewer | Claude | 긴 문서 검토, 논리 점검, 누락 및 반론 탐색 |

## 기본 흐름
1. 사용자가 GPT에게 요청한다.
2. GPT가 직접 처리할지 다른 Agent에 넘길지 판단한다.
3. 필요한 경우 Gemini 또는 Claude에 작업을 배정한다.
4. 결과를 `workspace/working`에 기록한다.
5. GPT가 결과를 검토·통합한다.
6. 최종 결과를 `workspace/output`에 저장한다.

## 폴더 구조
```text
AGENT/
├─ README.md
├─ USER_GUIDE.md
├─ AGENTS.md
├─ agents/
│  ├─ gpt-orchestrator.md
│  ├─ gemini-researcher.md
│  └─ claude-reviewer.md
├─ wiki/
│  └─ README.md
└─ workspace/
   ├─ inbox/
   ├─ working/
   └─ output/
```
