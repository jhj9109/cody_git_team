# 팀 Git 협업 실습

3~5명이 GitHub Flow, PR 리뷰, 충돌 해결, Git 복구 명령을 연습하는 팀 프로젝트입니다.

## 결과물

- 선택 유형: 학습 정리 노트 (`src/`)
- [Git 기본 구조와 동작 원리](src/kwon.md)
- [Git 객체와 파일 버전 저장 방식](src/jang.md)
- [GitHub 팀 협업 저장소 생성 방식 비교](src/sang.md)
- [Git 협업 중 작업 보관과 브랜치 전환](src/kwon-additional-git-learning-note.md)

## 팀원

| GitHub ID | 담당 파일 |
|---|---|
| wp230 | [Git 기본 구조](src/kwon.md), [작업 보관과 브랜치 전환](src/kwon-additional-git-learning-note.md) |
| jhj9109 | [Git 객체와 파일 버전 저장](src/jang.md) |
| Patrick-sangwook | [팀 협업 저장소 생성 방식 비교](src/sang.md) |

## 제출물 및 협업 문서

- [제출물 인덱스](SUBMISSION.md): 팀원별 기여와 증빙을 모으는 문서
- [협업 규칙](docs/CONTRIBUTING.md): 브랜치, 커밋, PR 및 리뷰 규칙
- [충돌 해결 기록](docs/conflict-resolution.md): 충돌 상황과 해결 과정
- [Git 트러블슈팅 기록](docs/troubleshooting-log.md): amend, reset, revert, stash 실습 기록

## 협업 방식

- `main`은 안정적인 상태로 유지합니다.
- 작업은 Issue → `feature/*` 브랜치 → PR → 리뷰·수정 → 승인 → Merge 순서로 진행합니다.
- [협업 규칙](docs/CONTRIBUTING.md)을 따릅니다.
