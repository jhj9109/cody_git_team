# Git 기본 구조와 동작 원리 (핵심 정리)

Git을 이해하는 핵심은 **"오브젝트(불변 데이터)"**와 **"포인터(주소 쪽지)"**가 어떻게 물리적으로 연결되어 움직이는가를 파악하는 것입니다.

---

## 1. Git의 3대 작업 영역 (Three Areas)

Git은 파일을 3개의 논리적 공간을 거쳐 저장합니다.

```text
[ Working Tree ]  --(git add)-->  [ Index (Staging) ]  --(git commit)-->  [ Repository (.git) ]
  (실제 작업 공간)                 (다음 커밋 준비소)                     (영구 저장된 스냅샷)
```

* **Working Tree**: 실제 눈에 보이고 편집하는 로컬 디렉터리.
* **Index (Staging Area)**: `.git/index` 파일. 다음 커밋에 담을 파일 목록과 메타데이터 준비 공간.
* **Repository**: `.git/` 디렉터리. 커밋, 트리, 블롭 등 객체들이 영구 저장되는 데이터베이스.

---

## 2. 포인터와 오브젝트의 연결 체인 (핵심 구조)

Git 데이터는 크게 두 가지로 나뉩니다:
* **오브젝트 (Object)**: `.git/objects/`에 압축 저장되는 알맹이 (**Commit, Tree, Blob**)
* **참조 (Ref / Pointer)**: 오브젝트 주소(해시값)를 적어둔 가벼운 텍스트 쪽지 (**HEAD, Branch**)

이 둘은 다음과 같이 **하나의 체인**으로 연결됩니다.

```text
[ .git/HEAD ]                 "현재 작업자는 main 브랜치를 보는 중"
      │
      ▼ (참조: refs/heads/main)
[ .git/refs/heads/main ]     "main의 최신 커밋 주소는 a1b2c3..."
      │
      ▼ (해시: a1b2c3...)
┌──────────────────┐
│  Commit Object   │  "이 시점의 루트 폴더는 d4e5f6, 이전 커밋은 987654"
│  (.git/objects)  │  - tree: d4e5f6... (루트 Tree)
└────────┬─────────┘  - parent: 987654... (부모 커밋)
         │
         ▼ (해시: d4e5f6...)
┌──────────────────┐
│   Tree Object    │  "폴더 내용: hello.py라는 파일(Blob)이 들어있음"
│  (.git/objects)  │  - 100644 blob 7g8h9i...  hello.py
└────────┬─────────┘  - 040000 tree 1a2b3c...  src/
         │
         ▼ (해시: 7g8h9i...)
┌──────────────────┐
│   Blob Object    │  "실제 파일 내용 자체"
│  (.git/objects)  │  print("Hello, Git!")
└──────────────────┘
```

---

## 3. Git 내부를 직접 열어보면? (텍스트 연결 확인)

Git 저장소 내부(`.git/`)를 확인해보면 모두 명확한 텍스트 주소로 이어져 있습니다.

1. **`cat .git/HEAD`**
   * 내용: `ref: refs/heads/main`
   * 의미: 현재 작업 위치가 `main` 브랜치임을 표시
2. **`cat .git/refs/heads/main`**
   * 내용: `a1b2c3d4...` (단 41바이트짜리 텍스트 파일)
   * 의미: `main` 브랜치 포인터가 가리키는 최신 **Commit 오브젝트의 해시값**
3. **`git cat-file -p a1b2c3d4` (Commit Object)**
   * 내용: 루트 디렉터리의 `tree <해시>`, 이전 커밋 `parent <해시>`, 작성자, 커밋 메시지
4. **`git cat-file -p d4e5f6` (Tree Object)**
   * 내용: 해당 디렉터리에 속한 파일명과 권한, 그리고 내용이 담긴 `blob <해시>` 매핑 목록
5. **`git cat-file -p 7g8h9i` (Blob Object)**
   * 내용: 순수한 파일 내용 (파일명 정보 없음. 파일명은 상위 Tree가 관리)

---

## 4. "브랜치가 움직인다"의 실체

새로운 작업을 하고 `git commit`을 실행했을 때 일어나는 내부 동작:

1. 수정한 파일 내용으로 새 **Blob** 생성
2. 프로젝트 폴더 구조를 스냅샷으로 뜬 새 **Tree** 생성
3. 이전 커밋을 `parent`로 지정한 새 **Commit** 생성
4. **브랜치 파일(`.git/refs/heads/main`) 속의 40자리 해시 텍스트를 새 커밋의 해시로 덮어쓰기!**

> 💡 **요약:**  
> 프로젝트 전체를 통째로 복사하는 것이 아니라, 새 스냅샷 객체들을 생성한 뒤  
> **브랜치 파일 속 40자리 해시 글자 하나를 새 커밋으로 바꿔치기(전진)**하는 것이 브랜치의 이동입니다.

---

## 5. 핵심 명령어와 영역 간 이동

* **`git add <file>`**: Working Tree의 변경 사항을 읽어 Blob 객체 준비 및 Index(Staging Area) 갱신
* **`git commit`**: Index 상태를 기반으로 Tree와 Commit 객체를 생성하고, 현재 브랜치 파일의 해시값을 새 커밋 해시로 갱신
* **`git switch <branch>`**: `.git/HEAD`의 참조 대상을 변경하고, 해당 커밋의 Tree/Blob을 읽어 Working Tree와 Index를 동기화
* **`git status`**: Working Tree, Index, HEAD가 가리키는 Commit 객체 간의 상태 차이를 비교 출력
