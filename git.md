# git

- fork 한 브랜치에서 작업 후, merge 하기 전에
    > 내 브랜치에서 내가 작업을 하는 동안, 다른 작업자가 다른 브랜치에서 작업을 마친 후, upstream/master 로 그 작업내역을 이미 push 한 경우 branch 작업의 흐름을 보기좋게 정리하기 위해서 다음과 같은 절차를 거침.

    1. upstream 에 최신 변경사항을 현재 내 브랜치로 가져옴
      ```
      // 작업한 브랜치에서
      $ git fetch upstream
      ```

    2. 내가 작업한 브랜치를 upstream/master 를 기준으로 rebase 한다.
      ```
      // 작업한 브랜치에서
      $ git rebase upstream/master
      ```
    
    3. 변경된 내 브랜치를 push 한다.
      ```
      // 작업한 브랜치에서
      $ git push --force origin "작업한 브랜치"
      ```
      
      * force 명령어를 사용해야 올바르게 push 할 수 있음.
      
       
