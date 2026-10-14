# GitHub 팀 협업 저장소 생성 방식 비교

## 1. 학습 목적

GitHub에서 여러 사람이 하나의 프로젝트를 공동으로 작업하는 방법을 알아본다.

이번 미션에서 제시된 두 가지 저장소 운영 방식인 **GitHub Organization 저장소**와 **개인 저장소의 Collaborator 초대 방식**을 비교하고, 각각의 특징과 차이점을 이해한다.

## 2. 방법 A: GitHub Organization 저장소

### 개념

Organization은 여러 사람이 공동으로 프로젝트를 관리할 수 있도록 GitHub에서 제공하는 조직 계정이다.

개인 한 명이 아닌 조직이 저장소를 소유하며, 팀원들에게 역할과 권한을 부여할 수 있다.

### 생성 방법

1. GitHub에 로그인한다.
2. 프로필 메뉴에서 `Your organizations`로 이동한다.
3. `New organization`을 선택한다.
4. 요금제와 조직 이름을 설정하고 조직을 생성한다.
5. 조직에 팀원을 초대한다.
6. 조직 소유의 새로운 Repository를 생성한다.
7. 팀원에게 필요한 저장소 접근 권한을 부여한다.

### 특징

- 저장소의 소유자가 개인이 아닌 조직이다.
- 여러 명의 조직 관리자를 지정할 수 있다.
- 팀(Team)을 구성하여 저장소 접근 권한을 관리할 수 있다.
- 여러 프로젝트를 장기적으로 관리하기에 적합하다.

## 3. 방법 B: 개인 저장소 + Collaborator 초대

### 개념

개인 GitHub 계정에서 저장소를 만들고 다른 사용자를 Collaborator(공동 작업자)로 초대하는 방식이다.

저장소는 개인 계정이 소유하지만, 초대받은 팀원도 권한에 따라 코드 수정과 PR 작업에 참여할 수 있다.

### 생성 방법

1. GitHub 개인 계정에 로그인한다.
2. `New repository`를 선택하여 저장소를 생성한다.
3. 생성된 저장소의 `Settings`로 이동한다.
4. `Collaborators` 메뉴에서 `Add people`을 선택한다.
5. 팀원의 GitHub 계정을 검색하여 초대한다.
6. 팀원이 초대를 수락하면 공동 작업을 시작한다.

### 특징

- 저장소의 소유자는 개인 계정이다.
- 설정이 간단하여 소규모 프로젝트를 빠르게 시작할 수 있다.
- GitHub Free에서도 공개·비공개 저장소에 Collaborator를 초대할 수 있다.
- 조직의 팀 단위 권한 관리 기능은 제공되지 않는다.

## 4. 두 방식의 차이점

| 비교 항목 | Organization 저장소 | 개인 저장소 + Collaborator |
|---|---|---|
| 저장소 소유자 | 조직 계정 | 개인 계정 |
| 생성 및 초기 설정 | 상대적으로 단계가 많음 | 비교적 간단함 |
| 팀원 초대 | 조직 멤버 및 저장소 접근 권한 설정 | 저장소에 직접 초대 |
| 권한 관리 | 역할별·팀별 세부 관리 가능 | 상대적으로 단순한 권한 구조 |
| 여러 프로젝트 관리 | 유리함 | 프로젝트별 관리 필요 |
| 적합한 경우 | 지속적인 팀 프로젝트, 조직 협업 | 소규모 학습, 단기 협업 |

## 5. 공통점

두 방식 모두 다음과 같은 GitHub 협업 기능을 활용할 수 있다.

- 브랜치(Branch)를 생성하여 개별 작업 진행
- Issue를 등록하여 작업 내용 관리
- Pull Request(PR)를 통해 변경 사항 병합 요청
- 코드 리뷰를 통해 팀원 간 의견 교환
- 브랜치 보호 규칙을 통한 main 브랜치 관리(요금제 및 저장소 공개 여부에 따라 지원 범위 확인 필요)

따라서 **이번 미션에서 요구하는 GitHub Flow, Issue, PR, 코드 리뷰, 충돌 해결 실습은 두 방식 모두에서 진행할 수 있다.**

## 6. 학습 결과 및 정리

이번 학습을 통해 GitHub 팀 협업은 반드시 Organization을 만들어야만 가능한 것은 아니라는 점을 이해했다.

개인 저장소에서도 Collaborator 초대를 통해 여러 사람이 함께 개발할 수 있다.

다만 팀원 수가 많아지고 여러 저장소를 장기적으로 관리해야 한다면 Organization 방식이 권한 관리와 운영 측면에서 유리하다.

**정리하면, 간단한 소규모 협업은 개인 저장소 방식이 편리하고, 체계적인 팀 운영은 Organization 방식이 적합하다.**

## 7. 참고 자료

- [GitHub 공식 문서 - Organizations](https://docs.github.com/en/organizations)
- [GitHub 공식 문서 - 개인 저장소 Collaborator 초대](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/repository-access-and-collaboration/inviting-collaborators-to-a-personal-repository)
- [GitHub 공식 문서 - Organization 저장소 권한](https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization)