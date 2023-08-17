# 내가 팀프로젝트에서 사용한 Git

Table of Content

- Github Flow
- FAQ

## Github Flow

1. 다른 사람이 같은 이슈를 작업하고 있진 않는지 확인하기
2. 그렇지 않다면, 깃랩에서 이슈 생성 및 feature 브랜치를 생성하기
    1. 하루 단위로 작업할 수 있는 feature 브랜치를 만들어주세요 
    2. 이슈 생성시, label을 명확히 분간하여 달아주세요
3. 일 하기 
    
    ```
    $ git add . && git commit
    ```
    
4. 최신 업데이트 하기
    
    ```
    $ git pull --rebase origin develop
    ```
    
5. 깃랩에 푸시하기
    
    ```
    $ git push origin my-feature-sth
    ```

6. 깃랩에서 Pull Request 하기

    ```
    source: my-feature-sth 
    to    : develop
    ```

7. 깃랩의 issue 탭에서 동료가 코드 리뷰 후 Merge 하기 
    

## FAQ

Q. Error: Updates were rejected because the tip of your current branch is behind

- 깃랩에 있는 feature 브랜치를 삭제하고 다시 푸시하세요

```
$ git push -d origin feature-sth && git push origin feature-sth
```

Q. 작업하던 feature 브랜치를 업데이트 하는 방법은?

- develop 브랜치를 바탕으로 업데이트 합니다

```
$ git pull --rebase origin develop 
```

Q. 집 노트북으로 작업하던 것을 외부 노트북으로 연이어 작업하는 방법은?

- 내 로컬 feature 브랜치를 깃랩 feature 브랜치로 업데이트 합니다

```
$ git pull --rebase origin feature-sth
```

Q. merge 가 안됩니다

- merge는 오직 maintainers만 할 수 있습니다. maintainers 에게 말해주세요

Q. rebase 할때, conflict 났습니다. 

- 철회하고 maintainers 을 불러주세요

```
$ git rebase --abort
```

### Reference

[GitHub Flow](https://scottchacon.com/2011/08/31/github-flow.html)
