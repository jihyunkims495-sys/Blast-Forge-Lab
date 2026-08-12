# 1장 2강: Git 환경 설정과 GitHub 인증
## 핵심 정리
---
1. git config --global로 user.name, user.email, editor를 설정하면 모든 저장소에 적용됩니다.
2. config 범위는 system < global < local 순서로 좁아질수록 우선순위가 높습니다.
3. SSH 키는 비공개키/공개키 쌍으로 동작하며, 공개키만 GitHub에 등록합니다.
4. PAT는 토큰 발급 후 자격 증명 매니저에 저장하여 사용합니다.
5. `ssh -T git@github.com`으로 인증이 성공적으로 설정되었는지 확인할 수 있습니다.
---
## 개념 정리
- Bash : 명령어를 입력받아 컴퓨터에 전달하는 셸(Shell)
- Shell : 사용자와 운영체제 사이에서 명령을 전달하는 프로그램
- Git Bash : Windows에서 Bash와 Git을 함께 사용할 수 있도록 만든 프로그램
    - Git Bash의 역할 : Git 명령어와 Linux 스타일 명령어를 입력하고 실행하는 환경
- Git : 버전 관리 프로그램

[별첨.] 명령 프롬프트 vs 파워쉘 vs 터미널
