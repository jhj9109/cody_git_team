# Git 충돌 해결 기록

팀 전체 2건 이상 작성합니다. 최소 1건은 같은 hunk의 서로 다른 수정 또는 파일 이동/삭제와 내용 수정이 얽힌 비자명 충돌이어야 합니다.

## 사례 1
- 참여자 / 역할:
- Issue / PR 링크:
- 충돌 파일 및 충돌 전 두 브랜치의 차이:
- 재현 절차 및 명령어:
- 충돌 마커 / 에러 메시지:
- 해결 방식과 이유:
- 검증 명령 / 결과:
- 주의점:

## 사례 2
- 참여자 : Patrick-sangwook / jhj9109
- 상황 : 26-docs / SUBMISSION.md
- 충돌내용 : 업데이트 초안 공유 과정에서 의도치 않은 띄어쓰기 쪽 오류로 충돌
```text
<<<<<<< HEAD
- Patrick-sangwook
  - [docs: 개인학습자료 업로드](https://github.com/jhj9109/cody_git_team/pull/8)
  - [docs: 어맨드 학습정리](https://github.com/jhj9109/cody_git_team/pull/14)
=======
-  Patrick-sangwook
>>>>>>> origin/feature/26-docs
```
- 해결 방식과 이유: 명확히 올바른 쪽이 있기에, 한쪽을 선택
