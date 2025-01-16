## Merge

![image](https://github.com/user-attachments/assets/00e756fa-3f30-4b0c-a57d-83f5cd64f070)
![image](https://github.com/user-attachments/assets/23b79710-b2d7-4da6-bc76-331eb0e6e569)

- Join two or more development histories together
- 다른 브랜치를 현재 checkout된 브랜치에 merge하는 명령
- 브랜치를 병합한 후 **새로운 병합 커밋(Merge Commit)** 을 생성하여 병합 이력을 기록
- 그림 : `feature` 브랜치에 두 브랜치의 기록을 연결하는 **새로운 “병합 커밋”이 만들어짐**

```bash
git checkout main  # main 브랜치로 이동
git merge feature  # feature 브랜치를 main 브랜치에 병합
```

### 특징

1. **병합 커밋 생성**
    - merge는 각 브랜치의 커밋 이력을 유지하면서 병합 커밋을 생성
    - 이력을 보존하며, 작업의 흐름을 명확하게 추적할 수 있음
2. **Conflict 처리**
    - 같은 파일의 같은 부분을 두 브랜치에서 수정한 경우 충돌 발생
    - 사용자가 직접 충돌을 해결한 뒤 병합 커밋을 생성해야함
3. **사용 상황**
    - 협업 시 두 브랜치의 이력을 명확히 보존하고 싶을 때 사용
    - 작업의 진행 흐름이 중요한 프로젝트에서 적합

## Rebase

![image](https://github.com/user-attachments/assets/a4a90f46-2e5d-472e-8079-cc7ae5baae27)
![image](https://github.com/user-attachments/assets/27428844-eab2-4d9b-8c6f-9d40c169ddc4)


- Reapply commits on top of another base tip
- 한 브랜치의 변경 사항을 다른 브랜치의 최상단으로 재배치하는 명령어
- merge와 같이 한 브랜치에서 다른 브랜치로 합치는 방법
- 기존 커밋 이력을 수정해 깔끔한 커밋 히스토리 유지
- 그림 : `main` 브랜치의 끝에서 시작하도록 전체 `feature` 브랜치를 이동하여 `main`에서 모든 새 커밋을 통합. 병합 커밋을 사용하는 대신 rebase는 **원본 브랜치에서 각 커밋에 대해 새로운 커밋**을 만들어 **프로젝트 기록을 다시 작성**

```bash
git checkout feature  # feature 브랜치로 이동
git rebase main       # main 브랜치의 최상단으로 feature 브랜치를 재배치
```

### 특징

1. 병합 커밋 없음
    - 커밋 히스토리를 재배치하기 때문에 merge와 달리 병합 커밋을 생성하지 않음
    - 기존 커밋 이력을 깔끔하게 유지 가능
2. 커밋 재작성
    - rebase는 기존 커밋을 새로운 부모 커밋 위에 복사하여 이력을 재작성
    - 이로 인해 커밋 해시가 변경됨
3. Conflict 처리
    - 재배치 과정에서 충돌이 발생하면 사용자가 충돌을 해결해야 함
    - 충돌 해결한 후 `git rebase --continue` 명령으로 재배치를 계속 진행
4. 사용 상황
    - 개인 작업 브랜치에서 커밋 이력을 정리하거나 깔끔한 히스토리를 유지하고 싶을 때 사용
    - rebase는 커밋 해시를 변경하므로 공유된 브랜치에는 사용하지 않는 것이 좋음. 협업 시 주의!

## **Merge vs Rebase**

| **특징** | **Merge** | **Rebase** |
| --- | --- | --- |
| **병합 커밋 생성 여부** | 병합 커밋 생성 | 병합 커밋 생성하지 않음 |
| **커밋 이력** | 각 브랜치의 이력을 보존하며 병합 | 기존 커밋 이력을 재배치하여 깔끔하게 유지 |
| **Conflict 처리** | 병합 과정에서 발생, 해결 후 병합 커밋 생성 | 재배치 중 발생, 해결 후 재배치 계속 진행 |
| **사용 목적** | 협업 시 이력 보존 및 작업 흐름을 명확히 추적 | 개인 작업 시 커밋 이력을 깔끔히 유지 |
| **장점** | 이력 보존, 작업의 흐름 명확 | 간결하고 깔끔한 커밋 히스토리 |
| **단점** | 병합 커밋이 많아지면 히스토리가 복잡해질 수 있음 | 커밋 해시 변경으로 협업 시 충돌 가능성 |

## **사용 시 주의사항**

### **Merge**

- 팀 작업에서는 이력 보존과 충돌 방지 측면에서 일반적으로 merge를 선호
- 특히 장기간 병합되지 않은 브랜치를 병합할 때 유용

### **Rebase**

- 로컬 브랜치에서만 사용하거나 **Push 전**에 커밋을 정리할 때 활용
- 이미 공유된 브랜치(예: 원격 브랜치)에서 rebase를 사용하면 협업에 문제가 발생할 수 있음

## 참고

https://git-scm.com/book/ko/v2

https://www.atlassian.com/ko/git/tutorials/merging-vs-rebasing
