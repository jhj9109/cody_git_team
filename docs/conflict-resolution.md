# Git 충돌 해결 기록

팀 전체 2건 이상 작성합니다. 최소 1건은 같은 hunk의 서로 다른 수정 또는 파일 이동/삭제와 내용 수정이 얽힌 비자명 충돌이어야 합니다.
<br>
## 사례 1
### 참여자 / 역할: <김상준> / 충돌 발생 및 해결 담당 <br>
### Issue / PR 링크: (작업 브랜치: `feature/16-reset-practice`) <br>
### 충돌 파일 및 충돌 전 두 브랜치의 차이:
- 충돌 파일: `src/reset_summary.md` (64~81줄 부근, 같은 hunk)
- 내 로컬 `feature/16-reset-practice`: `### 실행 전 그림` 아래에 `[실행 전]` 블록과 이미지(`../screenshot/reset_실습전.png`)를 추가하고 `[실행 후]` 블록을 작성함 (커밋: `docs: git reset 실습 후 관련 내용정리 추가`)
- 원격 `origin/feature/16-reset-practice`: 팀원이 같은 위치의 `[실행 전]` 코드 블록을 다른 구조로 작성함 (커밋: `docs: reset 학습정리`, `docs: 어맨드 학습정리`, PR #14 병합 포함)
- 같은 줄을 서로 다르게 수정해 Git이 자동으로 합칠 수 없었던 **같은 hunk의 서로 다른 수정** 충돌

### 재현 절차 및 명령어:
1. 로컬에서 `reset_summary.md`를 수정하고 커밋: `git add src/reset_summary.md` → `git commit -m "docs: git reset 실습 후 관련 내용정리 추가"`
2. 그 사이 팀원이 같은 파일의 같은 부분을 수정해 원격에 푸시
3. `git push` 시 원격과 기록이 갈라져 거부되거나, `git pull` 시 병합을 시도하면서 충돌 발생
4. 재현이 필요하면 `git fetch` → `git merge origin/feature/16-reset-practice`

### 충돌 마커 / 에러 메시지:
```
<<<<<<< HEAD (현재 변경 사항)
### [실행 전]
...내 로컬 내용...
=======
...원격에서 들어온 내용...
>>>>>>> 490557027c64982af8b040b034b587deb325e41e (수신 변경 사항)
```
- VS Code 소스 제어에서 `reset_summary.md`가 `↓A, !`(충돌) 상태로 표시됨
- 병합 메시지: `Merge branch 'feature/16-reset-practice' of https://github.com/jhj9109/cody_git_team into feature/16-reset-practice`
- <터미널 메시지가 있다면 붙여넣기: `CONFLICT (content): Merge conflict in src/reset_summary.md` / `Automatic merge failed; fix conflicts and then commit the result.`>

### 해결 방식과 이유:
- 방식: VS Code 병합 편집기에서 두 변경 사항을 비교한 뒤 <현재 변경 사항 수락 / 두 변경 사항 모두 수락 / 직접 수정 중 실제로 한 것>을 선택하고, `<<<<<<<`, `=======`, `>>>>>>>` 마커가 남지 않게 정리함
- 이유: 팀원이 쓴 내용을 불필요하게 지우지 않으면서, 코드 블록(```)이 중복되거나 닫히지 않는 구조 문제를 바로잡기 위해 <실제 이유로 수정>
- 마무리: `git add src/reset_summary.md` → `git commit`(병합 커밋) → `git push`

### 검증 명령 / 결과:
- `git status`: `Unmerged paths`가 없고 충돌 해결 완료 상태 확인
- `grep -n "<<<<<<<\|=======\|>>>>>>>" src/reset_summary.md`: 결과 없음
- `git log --oneline --graph --all`: 로컬과 원격 두 갈래가 하나의 병합 커밋으로 합쳐짐 <실행 결과 붙여넣기 또는 스크린샷>
- VS Code 미리보기(`Cmd + K` 후 `V`)에서 이미지와 코드 블록이 정상 표시됨

### 주의점:
- 충돌을 해결하고도 **병합 커밋을 만들지 않으면** 병합이 끝나지 않아 그래프에 로컬/원격이 갈라진 채 남음
- "현재 변경 사항 수락"만 누르면 팀원이 쓴 내용이 사라질 수 있으니 양쪽을 읽고 판단할 것
- 마커가 남은 채 커밋하지 않도록 저장 후 반드시 검색해서 확인
- 꼬였을 때는 `git merge --abort`로 병합 전 상태로 돌아가 다시 시도
- 이미 공유된 커밋을 reset/amend하거나 무단 강제 push하지 않음

## 사례 2
- 참여자 / 역할:
- Issue / PR 링크:
- 충돌 파일 및 충돌 전 두 브랜치의 차이:
- 재현 절차 및 명령어:
- 충돌 마커 / 에러 메시지:
- 해결 방식과 이유:
- 검증 명령 / 결과:
- 주의점:
