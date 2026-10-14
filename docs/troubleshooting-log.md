# Git 트러블슈팅 실습 기록

네 시나리오 모두 수행합니다. 모든 팀원은 최소 1개 시나리오의 해결 기록에 참여하고 자신의 이름 및 역할을 남깁니다.

실습은 안전한 개인 브랜치에서 수행합니다. 이미 공유된 커밋에 대한 amend/reset 및 무단 강제 Push를 금지합니다.

## 1. git commit --amend (최근 커밋 메시지 수정)

### 참여자 / 역할
- Patrick-sangwook
- 역할: `git commit --amend` 명령어를 이용한 최근 커밋 메시지 수정 실습 및 결과 기록

### 발생시킨 상황 / 기대한 복구
- 개인 학습자료를 작성한 후 커밋 메시지를 `어맨드 학습정리`로 등록함.
- 팀의 커밋 메시지 작성 규칙에 맞춰 `docs:` 접두어를 추가하고자 함.
- 기존 커밋의 파일 내용을 유지하면서 최근 커밋 메시지만 `docs: 어맨드 학습정리`로 수정하는 것을 목표로 함.

### 재현 절차 및 실제 실행 명령
1. `feature/12-amend-practice` 브랜치에서 최근 커밋을 확인함.
2. `git commit --amend`를 이용하여 커밋 메시지를 수정함.
3. 수정 후 `git log`로 커밋 메시지 및 커밋 ID 변경 여부를 확인함.

실습 명령어:

```bash
git log
git commit --amend -m "docs: 어맨드 학습정리"
git log
```

※ 가운데 `git commit --amend` 명령어는 제공된 실행 전후 로그를 바탕으로 정리한 재현용 명령어임.

### 실행 전 `git log`

**git log**

```text
commit ac8e2009dfa5aaa29b81d8c6d62abf0a80c27936 (HEAD -> feature/12-amend-practice)
Author: Patrick-sangwook <netlee12@naver.com>
Date:   Wed Oct 14 22:03:48 2026 +0900

    어맨드 학습정리
```

### 실행 후 `git log`

**git log**

```text
commit e41fc0a28abc98759a165a7b98ad902aba387113 (HEAD -> feature/12-amend-practice)
Author: Patrick-sangwook <netlee12@naver.com>
Date:   Wed Oct 14 22:03:48 2026 +0900

    docs: 어맨드 학습정리
```

### 결과 / 검증

| 구분 | 수정 전 | 수정 후 |
|---|---|---|
| 커밋 ID | `ac8e2009` | `e41fc0a2` |
| 커밋 메시지 | 어맨드 학습정리 | docs: 어맨드 학습정리 |
| 브랜치 | feature/12-amend-practice | feature/12-amend-practice |

**검증 결과**

- 최근 커밋 메시지가 정상적으로 변경됨.
- 커밋 ID가 `ac8e2009`에서 `e41fc0a2`로 변경됨.
- 작업 브랜치는 동일하게 유지됨.
- `git commit --amend`가 기존 커밋을 새로운 커밋으로 교체한다는 것을 확인함.

### 주의점
- `git commit --amend`는 최근 커밋을 새로운 커밋으로 교체하므로 커밋 ID가 변경됨.
- 이미 원격 저장소에 push한 커밋을 수정하면 다른 팀원의 Git 작업에 영향을 줄 수 있음.
- 가급적 원격 저장소에 push하기 전 개인 브랜치에서 사용해야 함.
- 공유 브랜치인 `main`에서는 팀원과 협의 없이 커밋 기록을 변경하거나 강제 push하지 않아야 함.
- 이번 실습을 통해 커밋 메시지 작성 규칙을 지키는 것의 중요성을 이해함.

## 2. git reset --soft HEAD~1 (로컬 커밋 취소, 변경 유지)
- 참여자 / 역할:
- 발생시킨 상황 / 기대한 복구:
- 재현 절차 및 실제 실행 명령:
- 실행 전 `git log` / `git status`:
- 실행 후 `git log` / `git status`:
- 결과 / 검증:
- 주의점:

## 3. git revert (원격에 Push한 커밋 변경 취소)
- 참여자 / 역할:
- 원격 브랜치와 취소 대상 커밋(해시/링크):
- 발생시킨 상황 / 기대한 복구:
- 재현 절차 및 실제 실행 명령:
- 실행 전 이력 / 파일 내용:
- 실행 후 이력 / 파일 내용:
- 결과 / 검증:
- 주의점:

## 4. git stash / git stash pop (작업 임시 보관·복원)

### 참여자 / 역할

- `wp230`: 이슈 #4 학습 노트 작성, PR #4 로컬 검토 및 리뷰 코멘트 작성, stash 실습 수행 및 기록 작성
- 실습일: 2026-10-14

### 발생시킨 상황 / 기대한 복구

`feature/4-additional-git-learning-note`에서 새 학습 노트를 작성하던 중,
다른 팀원의 PR #4를 로컬에서 검토해야 했다. 작성 중인 파일을 커밋하기 전에
보관하고 `review/pr-4`로 전환한 뒤, 원래 브랜치에서 작업을 복원하는 것이 목표였다.

처음에는 새 파일이 untracked 상태여서 기본 `git stash push`를 실행했을 때
`No local changes to save`가 출력되었다. 아래 명령으로 새 파일을 스테이징한 뒤
실습을 진행했다. `git add`는 커밋을 생성하지 않는다.

```bash
git add src/kwon-additional-git-learning-note.md
```

### 재현 절차 및 실제 실행 명령

실습은 아래 순서로 수행했다. `review/pr-4`는 실습 전에 PR #4의 head를
`git fetch origin pull/4/head:review/pr-4`로 가져와 준비한 로컬 브랜치다.
재현 시에는 해당 브랜치가 있는지 확인하고, 없으면 이 명령으로 준비한다.

```bash
git status
git diff --cached --stat
git stash push -m "docs: 학습 노트 작성 중 PR 4 검토를 위한 작업 보관"
git status
git stash list
git switch review/pr-4
git status
git log --oneline -5
# 로컬 파일 검토 후 GitHub PR #4에 리뷰 코멘트 작성
git switch feature/4-additional-git-learning-note
git stash pop
git status
git stash list
```

### 실행 전 `git status` / 작업 내용

다음은 실습 당시의 실제 출력이다. 당시 초안은 40줄이며, 이후 설명과 부록을
추가한 현재 학습 노트의 길이와는 다르다. 아래 코드 블록의 `$`는 프롬프트 표시다.

```text
$ git status
On branch feature/4-additional-git-learning-note
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   src/kwon-additional-git-learning-note.md

$ git diff --cached --stat
 src/kwon-additional-git-learning-note.md | 40 ++++++++++++++++++++++++++++++++
 1 file changed, 40 insertions(+)
```

새 파일이 스테이징되어 있었지만 아직 커밋되지 않은 상태였다.

### 보관 후 상태 및 PR 검토 브랜치 전환

```text
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
```

작업을 보관한 뒤 작업 폴더가 깨끗해지고 stash 항목이 1개 생성된 것을 확인했다.
`review/pr-4`에서는 PR #4의 커밋 `9e08232`를 확인했다.

### 실행 후 `git status` / 복원 확인

PR #4에 리뷰 코멘트를 작성한 뒤 작업 브랜치로 돌아왔다.

```text
$ git switch feature/4-additional-git-learning-note
Switched to branch 'feature/4-additional-git-learning-note'
$ git stash pop
On branch feature/4-additional-git-learning-note
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   src/kwon-additional-git-learning-note.md

Dropped refs/stash@{0} (174702226d7ac69d67e56bb3c050da885d42c884)
$ git status
On branch feature/4-additional-git-learning-note
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   src/kwon-additional-git-learning-note.md

$ git stash list
```

마지막 `git stash list`에는 출력이 없었다. 이는 보관 항목이 제거됐다는 뜻이다.

### 결과 / 검증

- 보관 직후 작업 폴더가 깨끗해지고 stash 항목이 생성됐다.
- PR 검토 브랜치로 전환하여 다른 팀원의 학습 자료를 확인했다.
- 원래 브랜치에서 학습 노트가 복원됐으며, 이번 실행에서는 새 파일이 스테이징 상태로 돌아왔다.
- `Dropped refs/stash@{0}` 출력과 빈 stash 목록으로 적용 후 항목 제거를 확인했다.

### 주의점

- 기본 stash는 untracked 파일을 포함하지 않는다. 새 파일은 `git add`로 스테이징하거나
  `git stash push -u`로 포함할 수 있다. 이번 실습에서는 `git add`를 사용했다.
- 이번 새 파일의 스테이징 복원 결과를 모든 변경에 일반화하지 않는다.
  기존 스테이징 상태까지 복원하려는 경우 `git stash pop --index`를 사용한다.
- `git stash pop` 중 충돌이 발생하면 stash 항목이 유지될 수 있다. 충돌을 해결하고
  파일 내용과 `git stash list`를 확인한 뒤 필요한 경우 해당 항목을 제거한다.
- 로그의 브랜치 포인터와 해시는 실습 당시 상태다. 이후 PR 병합으로 현재 이력은 달라질 수 있다.

### 관련 링크

- [이슈 #4: 추가 Git 학습 노트 및 stash 실습](https://github.com/jhj9109/cody_git_team/issues/4)
- [PR #4: 검토한 팀원의 Git 학습 자료](https://github.com/jhj9109/cody_git_team/pull/4)
- [PR #7: stash 학습 노트 추가](https://github.com/jhj9109/cody_git_team/pull/7)
- [학습 노트 및 실습 부록](../src/kwon-additional-git-learning-note.md)
