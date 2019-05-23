### git 협업 흐름

> 참고 : 만들면서 배우는 git + github 입문
> 우아한 형제들 블로그 : 우린 Git-flow를 사용하고 있어요 http://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html

### 정리 이유

- 시스템 유지보수를 하는 집단에서 일하다보니 CI/CD에 대한 열망이 강렬해졌다.
- 현재 개발계 운영 TOOL들 : SVN + FTP + WAS 껐다 켰다 하면서 운영됨
- 그림으로 나타내면 이렇다. -..-

  ![image](https://user-images.githubusercontent.com/21155325/58182863-5235ea00-7ce9-11e9-95a5-f19f0467aca8.png)

- 마을 공동우물처럼 레포지토리 1개를 쓰니 전화로 서로 언제 커밋하냐고 물어보고 ,메신저로 내가 개발한 소스 목록들 공유하면서 겹치는 개발 없는지 확인하고 그런다.

- 브랜치를 못따니 개인적으로 답답한 마음에 로컬에서는 혼자 GIT을 썼다. 이왕 개발계 자체를 GIT으로 소스관리하고, 다들 GIT 공부좀 해서 CI/CD까지 같이 구축했으면 좋겠다는 생각을 했다.

- 그런데 여러명이 GIT으로 소스관리할때는 어떤 전략으로 운용을 해야하는지 감이 잡히질 않았다. 왜냐하면 GIT을 혼자만 써왔던지라, 브랜치 작명법이라던가, 머지 전략과 같은 것들에 대해 특별히 생각해볼 이유가 없었기 때문이다.

- 공부 좀 해서 정리해놓을 겸 문서로 정리해본다.

### git-flow?
- **GitFlow is a branching model for Git**, created by Vincent Driessen. It has attracted a lot of attention because it is very well suited to collaboration and scaling the development team.
  > `https://datasift.github.io/gitflow/IntroducingGitFlow.html`
- 말그대로 branch 운용 전략을 얘기하는 듯하다.
- branching에 대한 model이니 다른 flow들이 있을 것이다. git-hub flow, git-lab flow 이런것들이 있는듯.
- ### 브랜치 종류
    - 1. `develop`
        - 1개만 존재한다.
        - 모든 개발이 여기서 시작된다.
        - 절대로 develop 브랜치에 direct commit 하지 않는다.
        - `feature`, `release`, `hotfix`만이 merge 가능
        - 오직 merge 커밋만 할 수 있다. 

    - 2. `feature`
        - 여러개가 존재한다.
        - develop에서 따져서 나오는거임. 
        - 마음대로 막 만들어도 됨. 단 관계성을 가지려면 develop과 머지 되어야함.
        - 따지는 것도, 합치는 것도 모든 것은 develop 이랑만!

    - 3. `release` 
        - develop에서 따져서 배포 기다리는 브랜치
        - 여기서는 새로운 기능추가는 안된다. 즉 feature와 머지는 전혀없고,
        버그 수정만 가능! => 완성도를 높이는 작업만 한다. 
        - 버그가 수정되었다? -> develop에 무조건 머지 되어야함.

    - 4. `master`
        - release 중에서 bugfix 다 마치고, 실제 배포버전
        - release, hotfix 하고만 관계

    - 5. `hotfix`
        - 배포중인 코드, 즉 master에 버그가 있어서 급하게 수정해야할 때 쓴다.
        - 끝나면 master와 develop에 머지해놔야겠지.

#### 정리 
> 1. 요구사항이 온다.
> 2. develop 브랜치에서 feature 브랜치 하나딴다.
> 3. 개발 완료하면 develop으로 pull request 보내거나 merge 시킨다.
> 4. 배포일자가 다가오면 develop에서 release 하나 딴다.
> 5. release에서 버그들을 고쳐낸다. 고치고 나면 develop에 머지
> 6. 배포시에는 release에서 master따서 배포한다.
> 7. master에서 버그났다? -> hotfix 만들어서 고친다.
> 8. hotfix에서 버그 수정 끝나면 develop과 master에 반영한다.

#### 느낌
- too much 하다고 느낄수 있는 곳도 있을것 같다. 그래서 github-flow나 gitlab-flow처럼 더 단순화된 모델이 있다는데 공부해보고 다시 기록해보겠다. 
