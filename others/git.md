#### git
###### Reference
 - [버전관리를 들어본적 없는 사람들을 위한 DVCS - Git](http://www.slideshare.net/ibare/dvcs-git)
 - [Lean Git Branching](http://pcottle.github.io/learnGitBranching/)
 - [Code School - Try git](https://try.github.io/)
 - [Atlassian git tutorial](https://www.atlassian.com/git/tutorials/)

'수정'의 단계는 '의미'를 기준으로 commit한다. `pull`은 remote에서 local 저장소로, `push`는 local에서 remote로 보내는 작업이다.

##### 명령어
 - `git log`
 - `git log -1` : 마지막 commit log
 - `git log -2` : 마지막 2개의 commit log
 - `git log --oneline` : 각 commit을 한줄로 표시
 - `git branch -r` : remote의 전체 branch 표시
 - `git log <tag name>..HEAD` : <tag name> 이후의 commit 표시
