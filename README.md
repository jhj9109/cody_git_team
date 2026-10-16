# 팀 Git 협업 실습

4명이 GitHub Flow, PR 리뷰, 충돌 해결, Git 복구 명령을 연습하는 팀 프로젝트입니다.
Git에 관한 학습 정리 노트(Markdown)를 작성하며 GitHub 협업을 실습합니다.
개인 저장소에 Collaborator를 초대하는 방식으로 진행합니다.

## 결과물
**깃허브에 관한 학습 정리 노트(md) (`src/`)**

| GitHub ID | 담당 학습 노트 |
|---|---|
| wp230 | [Git 기본 구조](src/kwon.md), [작업 보관과 브랜치 전환](src/kwon-additional-git-learning-note.md) |
| jhj9109 | [Git 객체와 파일 버전 저장](src/jang.md) |
| Patrick-sangwook | [팀 협업 저장소 생성 방식 비교](src/sang.md), [commit --amend](src/sang-commit-amend-learning-note.md) |
| roiker7 | [git reset](src/reset_summary.md) |

## 제출물 및 협업 문서

- [제출물 인덱스](SUBMISSION.md): 팀원별 기여와 증빙을 모으는 문서
- [협업 규칙](docs/CONTRIBUTING.md): 브랜치, 커밋, PR 및 리뷰 규칙
- [충돌 해결 기록](docs/conflict-resolution.md): 충돌 상황과 해결 과정
- [Git 트러블슈팅 기록](docs/troubleshooting-log.md): amend, reset, revert, stash 실습 기록

## 협업 방식

- `main`은 안정적인 상태로 유지합니다.
- 작업은 Issue → `feature/*` 브랜치 → PR → 리뷰·수정 → 승인 → Merge 순서로 진행합니다.
- [협업 규칙](docs/CONTRIBUTING.md)을 따릅니다.

## GITHUB FLOW 선택이유
GitHub Flow는 브랜치 생성부터 PR, 코드 리뷰, Merge까지의 협업 과정을 간결하게 경험할 수 있어 선택했다.
main 브랜치를 안정적으로 유지하면서 기능별 브랜치에서 독립적으로 작업할 수 있다.
복잡한 브랜치 관리 없이 Git 협업의 핵심인 코드 리뷰와 변경 이력 관리에 집중할 수 있다.
