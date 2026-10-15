# Git commit --amend 학습내용 및 실습결과

## 1. 학습 목적

Git의 `git commit --amend` 명령어를 이해하고, 가장 최근에 작성한 커밋 메시지를 수정하는 방법을 실습한다.

커밋 수정 전후의 차이를 확인하고, 팀 협업에서 사용할 때 주의해야 할 사항을 학습한다.

## 2. git commit --amend란?

`git commit --amend`는 **가장 최근에 생성한 커밋을 수정하여 새로운 커밋으로 교체하는 명령어**이다.

주로 다음과 같은 경우에 사용한다.

- 최근 커밋 메시지에 오타가 있는 경우
- 커밋 메시지를 더 명확하게 변경하고 싶은 경우
- 최근 커밋에 빠뜨린 파일이나 수정 사항을 추가하고 싶은 경우

예를 들어 다음과 같이 커밋했다고 가정한다.

```bash
git commit -m "docs: add study"
```

커밋 메시지를 더 구체적으로 변경하려면 다음 명령어를 사용한다.

```bash
git commit --amend -m "docs: add git amend study notes"
```

이렇게 하면 가장 최근 커밋의 메시지가 변경된다.

## 3. amend의 동작 원리

`amend`는 기존 커밋을 직접 수정하는 것이 아니라, **수정된 내용을 반영한 새로운 커밋을 생성하여 기존 커밋을 대체**한다.

따라서 커밋 메시지만 변경하더라도 커밋 ID(Hash)가 달라진다.

예시:

| 구분 | 커밋 ID | 커밋 메시지 |
|---|---|---|
| 수정 전 | `a1b2c3d` | docs: add study |
| 수정 후 | `e4f5g6h` | docs: add git amend study notes |

※ 위 커밋 ID는 설명을 위한 예시이며, 실제 실습에서는 다른 값이 생성된다.

## 4. 주요 명령어

### ① 최근 커밋 확인

```bash
git log -1 --oneline
```

가장 최근 커밋의 ID와 메시지를 확인한다.

### ② 최근 커밋 메시지 수정

```bash
git commit --amend -m "docs: add git amend study notes"
```

최근 커밋 메시지를 변경한다.

### ③ 메시지를 유지하면서 파일 변경 사항 추가

```bash
git add 파일명
git commit --amend --no-edit
```

새로 수정한 파일을 최근 커밋에 추가하되, 기존 커밋 메시지는 그대로 유지한다.

### ④ 수정 결과 확인

```bash
git log -1 --oneline
```

커밋 메시지와 ID가 변경되었는지 확인한다.

## 5. 실습 과정

이번 실습은 팀 프로젝트의 Issue #12 작업 브랜치에서 진행한다.

**실습 목표:** 커밋 메시지를 일부러 간단하게 작성한 뒤 `amend`로 수정하고, 수정 전후의 커밋 ID를 비교한다.

### Step 1. 작업 브랜치 확인

```bash
git branch --show-current
```

예상 브랜치 이름:

```text
feature/12-amend-practice
```

### Step 2. 학습자료 파일 추가 및 최초 커밋

```bash
git add git-amend-study.md
git commit -m "docs: add study"
```

※ 실제 파일 위치에 따라 `git add` 경로를 변경한다.

### Step 3. 수정 전 커밋 확인

```bash
git log -1 --oneline
```

출력된 커밋 ID와 메시지를 기록한다.

### Step 4. amend 실행

```bash
git commit --amend -m "docs: add git amend study notes"
```

### Step 5. 수정 후 커밋 확인

```bash
git log -1 --oneline
```

수정 전과 비교하여 커밋 ID 및 메시지가 변경되었는지 확인한다.

## 6. 실습 결과

※ 아래 표는 실제 실습 후 작성한다.

| 구분 | 커밋 ID | 커밋 메시지 |
|---|---|---|
| amend 실행 전 | 실습 후 입력 | 실습 후 입력 |
| amend 실행 후 | 실습 후 입력 | 실습 후 입력 |

**실습 결과 확인 사항**

- [ ] 가장 최근 커밋 메시지가 변경되었다.
- [ ] amend 실행 전후의 커밋 ID가 서로 다르다.
- [ ] 기존 파일 내용이 정상적으로 유지되었다.

## 7. 팀 협업 시 주의사항

`git commit --amend`는 커밋의 ID를 변경하므로, 이미 GitHub에 push한 커밋에 사용하면 문제가 발생할 수 있다.

특히 여러 팀원이 함께 사용하는 브랜치에서는 커밋 기록이 달라져 다른 사람의 작업에 영향을 줄 수 있다.

따라서 다음 원칙을 지켜야 한다.

1. 가능하면 **원격 저장소에 push하기 전의 개인 브랜치 커밋**에 사용한다.
2. 이미 push한 커밋을 수정해야 한다면 팀원과 먼저 협의한다.
3. 공유 브랜치인 `main`에서 임의로 커밋 기록을 변경하지 않는다.
4. 팀원과 합의하지 않은 강제 push는 사용하지 않는다.

## 8. 학습을 통해 이해한 내용

`git commit --amend`는 최근 커밋에 실수가 있을 때 유용하게 사용할 수 있는 명령어이다.

다만 기존 커밋을 수정하는 것이 아니라 새로운 커밋으로 교체하기 때문에 커밋 ID가 변경된다는 점이 중요하다.

특히 팀 프로젝트에서는 다른 팀원에게 영향을 주지 않도록, 원격 저장소에 push하기 전에 개인 브랜치에서 사용하는 것이 안전하다.

## 9. 참고 자료

- [Git 공식 문서 - git commit](https://git-scm.com/docs/git-commit)
- [Git 공식 학습자료 - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)