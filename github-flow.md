# github-flow
> 참고 : 만들면서 배우는 git + github 입문

## 등장 배경
- git-flow 단점 보완 
- git-flow 단점? = 빠른 개발과 배포에 맞지 않음.

## branch
> 딱 2개만 등장!!
- **master** : 언제나 배포 가능한 상태
- **feature** : master에서 갈라져나옴. 모든 코드 수정 담당.

## 작업 흐름
1. `master`에서 `feature`딴다.
2. `feature`에서 기능개발
3. 개발끝나면 `master`에 pull request 보내기
4. `feature`의 pr을 가지고 코드리뷰진행
5. 코드리뷰 반영해 `feature`에서 다시 수정개발 진행
6. 3~5를 계속 반복
7. 통과되면 `feature`를 `master`에 머지 후 배포완료

### gitlab-flow는 github-flow에 uat개념 (pre-production) 단계를 두는듯.