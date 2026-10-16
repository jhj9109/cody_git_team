# 팀 과제 요구사항 및 마무리 작업

사용자가 제공한 [과제 원문](assignment-original.txt)을 기준으로 정리한다. 작업 규칙은 [AGENTS.md](../AGENTS.md)를 따른다.

## 팀의 선택
- 결과물: 팀원별 Markdown 학습 정리 노트(C). `src/`에 노트를 두고 README에 목차를 제공한다.
- 저장소 구성: 개인 저장소 생성 후 Collaborator 초대(B).
- 핵심 목적: 복잡한 프로그램 구현보다 GitHub Flow, Issue, PR, 리뷰, 충돌 해결과 복구 과정의 학습 및 증빙.
- 과제 개발 환경: Python 3.10 이상, Git, GitHub. 현재 결과물은 Markdown이며 앱 실행·패키지 설치는 필요하지 않다.

## 필수 요구사항
| 구분 | 충족 기준 | 기록 위치 |
|---|---|---|
| 팀 및 저장소 | 3~5인, 전원 Git 작업 참여, 저장소 URL | README, SUBMISSION |
| main 보호 | 직접 push 금지, PR 병합 필수, 최소 1명 approve | GitHub 설정 증빙을 SUBMISSION에 연결 |
| 브랜치 전략 | GitHub Flow, main 안정 유지, feature/*, 네이밍 규칙 | CONTRIBUTING |
| 선택 이유 | GitHub Flow 선택 이유 3줄 이내 | README 또는 CONTRIBUTING |
| Issue 추적 | 작업별 Issue, PR 본문 Closes # 또는 Fixes # | 팀원별 Issue/PR을 SUBMISSION에 연결 |
| 커밋 규칙 | 구체적인 대상·변경을 담은 메시지, 의미 없는 메시지 금지 | CONTRIBUTING |
| 개인 PR | 각 팀원 생성·병합 PR 2개 이상 | SUBMISSION |
| 개인 리뷰 | 각 팀원 타인 PR 리뷰 2개 이상, 본인 PR 제외 | 리뷰 댓글 직접 링크 |
| 피드백 반영 | 각 팀원 본인 PR에서 1회 이상, 커밋·수정·답글 증빙 | SUBMISSION |
| PR 품질 | What/Why/How, 실질 코멘트 1개 이상, 작성자·리뷰어 상호작용 1회 이상 | 각 PR 및 증빙 링크 |
| 충돌 해결 | 팀 전체 2건 이상, 그중 비자명 충돌 1건 이상 | conflict-resolution.md |
| 복구 실습 | amend, reset --soft HEAD~1, 원격 push된 커밋 revert, stash/pop 모두 | troubleshooting-log.md |
| 복구 참여 | 전원 최소 1개 시나리오 기록 작성 참여, 이름·역할 명시 | troubleshooting-log.md |
| 학습 노트 | 전원 노트 1개 이상 및 기여 커밋 1개 이상 | src/, README 목차, SUBMISSION |
| 히스토리 | git log --oneline --graph --all 텍스트 또는 스크린샷 | SUBMISSION에서 증빙 연결 |

비자명 충돌은 같은 파일의 같은 hunk를 서로 다르게 수정한 경우 또는 이동·이름 변경·삭제와 내용 수정이 얽힌 경우다. 실습 기록에는 참여자, 상황, 재현 절차, 실제 명령, 결과, 주의점 및 선택 이유를 남긴다. 충돌 기록에는 충돌 마커, 해결 전략, PR/커밋, 배운 점도 포함한다.

공유 브랜치의 무리한 이력 재작성과 팀 합의 없는 강제 push/rebase는 금지한다. Codex의 rebase는 사용자 지시에 따라 `codex`에만 적용한다.

## 선택 과제
- 개인 feature 브랜치의 `git rebase -i` squash/reword 및 전후 비교.
- `.github/CODEOWNERS`를 통한 리뷰 책임 지정.
- 선택 과제를 하지 않았다는 이유로 필수 과제 미완료로 판정하지 않는다.

## 현재 브랜치에서 확인한 현황

점검 기준: `bb8ad7146aa5ba6524b2247fd156b3d0f4d9847c`에서 시작한 `codex`. 아래는 문서와 조상 이력의 확인 결과이며 GitHub의 실시간 설정·리뷰 조회 결과가 아니다.

| 항목 | 확인 결과 | 다음 작업 및 위치 |
|---|---|---|
| 학습 노트 | src/에 6개 문서 존재 | 새 노트는 src/에 추가하고 README 목차와 SUBMISSION 기여 연결 갱신 |
| 팀원 | wp230, jhj9109, Patrick-sangwook, roiker7로 표기. reset 참여자의 계정은 사용자 확인으로 roiker7 확정 | 개인별 증빙 및 Collaborator 참여 확인 |
| 협업 규칙 | 필수 규칙이 CONTRIBUTING에 기재됨 | 실제 GitHub main 보호 설정 증빙 추가 |
| 충돌 기록 | 사례 1·2가 빈 양식. 이력에 ad20a65 충돌 해결 메시지 존재 | 메시지만으로 2회·비자명 여부를 확정하지 말고 실제 내용을 conflict-resolution.md에 작성 |
| amend | 참여자·전후 해시 기록 존재 | PR 및 피드백 증빙 연결. 학습 노트에는 결과 작성 안내 문구가 남아 있어 최종 내용 점검 |
| reset | 제목은 HEAD~1, 명령은 HEAD~2. 커밋 메시지 1/2와 전후 설명 asdf도 불일치 | 실제 실행 증빙과 문장을 대조하고 과제의 HEAD~1 수행 증빙 보완. 기존 실습을 임의로 고쳐 쓰지 않음 |
| revert | 실제 커밋·로그가 있지만 이름, #XX, [SHA] 자리표시자 남음 | troubleshooting-log.md에 실제 참여자·Issue·PR·커밋·결과·선택 이유 보완 |
| stash | 참여자·실행 로그·Issue/PR 링크 존재 | SUBMISSION에 연결하고 실제 리뷰 링크 및 피드백 반영 증빙 확보 |
| 개인 기여 | 학습 노트 커밋 및 관련 병합 이력 존재 | PR 작성자·리뷰어·승인·상호작용은 별도 증빙 필요 |
| 히스토리 | 최종 제출용 전체 이력 파일 없음 | 팀이 최종 병합 후 아래 위치에 생성 |

## 추가 자료 위치
- 학습 노트: `src/<작성자>-<주제>.md` → README 목차 및 SUBMISSION 연결.
- 충돌 2건: `docs/conflict-resolution.md`의 사례 1·2.
- 복구 4종: `docs/troubleshooting-log.md`의 해당 시나리오.
- 스크린샷: 기존 `screenshot/` 아래에 의미 있는 이름으로 추가하고 해당 기록과 SUBMISSION에서 연결.
- 최종 히스토리: `docs/evidence/git-history.txt` 권장. 파일 생성 전에는 제출 링크를 완료로 표시하지 않는다.
- 팀원별 Issue·PR·리뷰·피드백 링크 및 보호 설정 증빙: `SUBMISSION.md`.

현재 작업은 codex 자료만을 근거로 하므로 다른 브랜치를 모아 전체 이력을 확정하지 않는다. 최종 제출 담당자가 필요한 참조를 갖춘 환경에서 다음 명령으로 과제 요구 증빙을 만들고, 캡처 시점과 범위를 기록한다.

```bash
mkdir -p docs/evidence
git log --oneline --graph --all > docs/evidence/git-history.txt
```

## 제출 전 확인 방법
1. 팀원 전원의 최소 기준을 증빙 링크별로 대조한다.
2. 문서에 남은 작성 예정, 확인 필요, #XX, [SHA] 등을 실제 자료로 보완한다.
3. README의 모든 노트와 SUBMISSION의 문서·증빙 링크가 열리는지 확인한다.
4. 필수 항목이 충족된 경우에만 SUBMISSION 체크박스를 완료 표시한다.
