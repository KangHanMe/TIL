## 오늘의 할일

- [v] CLI로 3-way 병합하기

## 3-way 병합 실습하기

- 내가 생각하는 3-way는 3개의 브랜치를 병합하는 방법이다.
- 일단 기능 개발을 위해 `[master]` 브랜치 기준으로 새로운 브랜치를 생성했고, 새로운 브랜치에서 기능을 개발하고 버그를 발견했다.
- 어차피 새로운 브랜치는 `[master]` 브랜치 기준으로 생성했기 때문에 같은 버그를 가지고 있다.
- 그래서 버그를 수정하기 위한 `[hotfix]` 브랜치 생성하고, 버그를 수정 및 테스트가 완료되었다면 `[master]` 브랜치와 새로운 기능 개발 브랜치 모두 병합되어야한다.

- `[master]` 브랜치에서 `[feature1]` 브랜치를 생성하고 `[feature1]` 브랜치로 이동하기 : `git checkout -b feature1`
- 파일 생성 및 수정한다 : 즉, 커밋한다.
- `[feature1]` 브랜치에서 커밋한 상태에서 버그를 찾았다.

- 버그를 수정하기 위해서 `[master]` 브랜치에서 `[hotfix]` 브랜치를 생성한다, : `git checkout -b hotfix master` (현재 브랜치는 `[feature1]`)
- `[hotfix]`브랜치에서 버그를 수정하고 커밋을 한다.
- 버그가 수정된 `[hotfix]` 브랜치를 `[master]` 브랜치에 병합한다 : `[master]` 브랜에서 `git merge hotfix`, 해당 병합은 `fast-merge`이다.
- `[feature1]`브랜치에도 반영을 해야한다.
- 그러나 `[master]` 브랜치와 `[feature1]` 브랜치는 서로 다른 분기라서 fast-merge를 할 수 없다. 그리고 이미 `[master]` 브랜치에서 버그가 있는 상태에서 `[hotfix]` 브랜치와 `[feature1]` 브랜치가 생성되었기 때문에 fast-merge가 된 `[master]`브랜치와 버그가 있는 `[feature1]` 브랜치는 충돌이 발생한다.
- `[feature1]` 브랜치에서 충돌을 해결하고 커밋을 하면 자동으로 병합이 된다. 물론, 머지를 취소할 수 있다(`git merge --abort`)
- `[feature1]` 브랜치에서 `[master]`브랜치를 병합한다. : `git merge master`
  ![git_merge_3_way](img/git_merge_3_way.png)
