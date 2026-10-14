# Git 협업 중 작업 보관과 브랜치 전환

## 학습 목표

- 커밋하지 않은 변경 사항이 있을 때 브랜치를 전환하기 어려운 이유를 설명한다.
- `git stash`와 `git stash pop`으로 작업을 안전하게 보관하고 복원한다.
- 작업 보관이 필요한 협업 상황을 기록한다.

## 왜 작업 보관이 필요한가

기능 브랜치에서 문서를 작성하는 도중에는 변경 사항이 아직 커밋되지 않을 수 있다.
이 상태에서 다른 브랜치의 PR을 로컬로 검토하거나, 긴급하게 `main`의 변경을
확인해야 하면 현재 작업이 브랜치 전환을 막거나 섞일 수 있다. 이때 진행 중인
변경을 stash에 임시 보관하면 작업 디렉터리를 깨끗한 상태로 만들 수 있다.

## 기본 흐름

```bash
# 현재 작업 내용을 이름과 함께 임시 보관한다.
git stash push -m "docs: 학습 노트 작성 중 PR 검토를 위한 작업 보관"

# 다른 브랜치로 전환해 필요한 작업을 수행한다.
git switch review/pr-4

# 원래 브랜치로 돌아와 보관했던 내용을 적용하고 stash 항목을 제거한다.
git switch feature/4-additional-git-learning-note
git stash pop
```

## 확인 방법

1. `git status`로 stash 전에는 학습 노트 파일이 수정 상태인지 확인한다.
2. `git stash push` 후 `git status`가 깨끗한지, `git stash list`에 보관 항목이 있는지 확인한다.
3. 원래 브랜치에서 `git stash pop`을 실행한 뒤 `git status`와 파일 내용으로 변경이 복원됐는지 확인한다.

## 주의점

- `git stash pop` 중 같은 파일이 다른 브랜치에서 변경되었다면 충돌이 발생할 수 있다.
- 충돌을 해결하기 전에는 stash 항목이 남아 있을 수 있으므로 `git stash list`로 상태를 확인한다.
- 공유 브랜치의 커밋을 되돌리는 용도에는 stash가 아닌 `git revert`를 사용한다.

## 부록: PR #4 검토를 위해 수행한 stash 실습 기록

### 상황

이슈 #4 브랜치 `feature/4-additional-git-learning-note`에서 추가 학습 노트
`src/kwon-additional-git-learning-note.md`를 작성하던 중, PR #4의 변경을 로컬에서
확인하고 리뷰 코멘트를 남겨야 했다. 파일은 아직 커밋하지 않았지만 `git add`로
스테이징된 상태였으므로, 브랜치를 전환하기 전에 stash에 보관했다.

### 수행한 명령과 확인 결과

```bash
# 1. stash 전: 새 파일이 스테이징된 상태인지 확인
git status
git diff --cached --stat

# 2. 스테이징된 작업을 이름과 함께 보관
git stash push -m "docs: 학습 노트 작성 중 PR 4 검토를 위한 작업 보관"

# 3. 보관 결과 확인
git status
git stash list

# 4. PR #4 검토 브랜치로 전환하고 변경 이력 확인
git switch review/pr-4
git status
git log --oneline -5

# 5. GitHub PR #4에 파일과 명령어를 근거로 한 리뷰 코멘트 작성 후 원래 브랜치로 복귀
git switch feature/4-additional-git-learning-note
git stash pop

# 6. 복원 결과 확인
git status
git stash list
```

### 실제 실행 결과

아래는 위 절차에서 확인한 터미널 출력이다.

```text
$ git status
On branch feature/4-additional-git-learning-note
Changes to be committed:
  new file:   src/kwon-additional-git-learning-note.md

$ git diff --cached --stat
 src/kwon-additional-git-learning-note.md | 40 ++++++++++++++++++++++++++++++++
 1 file changed, 40 insertions(+)

$ git stash push -m "docs: 학습 노트 작성 중 PR 4 검토를 위한 작업 보관"
Saved working directory and index state On feature/4-additional-git-learning-note: docs: 학습 노트 작성 중 PR 4 검토를 위한 작업 보관

$ git status
On branch feature/4-additional-git-learning-note
nothing to commit, working tree clean

$ git stash list
stash@{0}: On feature/4-additional-git-learning-note: docs: 학습 노트 작성 중 PR 4 검토를 위한 작업 보관

$ git switch review/pr-4
Switched to branch 'review/pr-4'

$ git status
On branch review/pr-4
nothing to commit, working tree clean

$ git log --oneline -5
9e08232 (HEAD -> review/pr-4, origin/feature/2-learningFile) docs: 깃 기초 학습자료 문서 추가(jang)
7dffbf3 (origin/main, origin/HEAD, feature/4-additional-git-learning-note) Merge pull request #3 from jhj9109/feature/1-add-git-guide
3f77ad5 (origin/feature/1-add-git-guide, feature/1-add-git-guide) docs: add git fundamentals guide (kwon.md)
78c5f1f (main) chore: initialize team repository

$ git switch feature/4-additional-git-learning-note
Switched to branch 'feature/4-additional-git-learning-note'

$ git stash pop
On branch feature/4-additional-git-learning-note
Changes to be committed:
  new file:   src/kwon-additional-git-learning-note.md

Dropped refs/stash@{0}

$ git stash list
# 출력 없음: stash 목록이 비어 있음
```

### 결과와 배운 점

`git stash push`는 스테이징된 변경도 함께 보관한다. 따라서 작업 폴더를 깨끗하게
유지한 채 PR #4 검토 브랜치로 전환할 수 있었고, `git stash pop`으로 돌아온 뒤에는
작성 중이던 학습 노트가 스테이징 상태까지 그대로 복원되었다. 새 파일을 아직
`git add`하지 않은 상태라면 기본 stash는 보관하지 않으므로, `git add` 후 stash를
사용하거나 `git stash push -u`로 untracked 파일까지 포함해야 한다.
