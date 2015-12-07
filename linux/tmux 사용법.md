#### tmux 사용법
##### reference
 - Node.js Q&A (http://nodeqa.com/sitemap# 에서 tmux로 검색)
 - http://awhan.wordpress.com/2010/06/20/copy-paste-in-tmux/
 - http://zanshin.net/2013/09/05/my-tmux-configuration/ (설정)
 
tmux는 좀 더 개선된 screen이라 생각하면 된다.

##### 용어
 - session : tmux 실행시 생성
 - window : 하나의 session에 여러개의 window 생성 가능
 - pane : 하나의 window안에 여러개의 pane으로 분할 가능

##### 사용법
다음은 실행과 종료 방법이다.
```bash
$ tmux
$ exit  # 종료  또는 ctrl + d
```

session 명령
```bash
$ tumx new -s 세션이름 # 세션이름으로 생성 

ctrl + b + d  # 셔션을 유지한채로 나오기

$ tmus ls  # 세션 목록 보이기
$ tmux attach -t 세션명 # 세션으로 다시 들어가기
```

window 명령
```bash
ctrl + b + c # 새 window 생성
ctrl + b + & # window 삭제
ctrl + b + , # window 이름 변경
ctrl + b + window 번호 # window 이동
ctrl + b + n # window 이동, next
ctrl + b + p # window 이동, previous
ctrl + b + l # window 이동, last
```

pane 명령
```bash
ctrl + b + % # 가로 나누기
ctrl + b + " # 세로 나누기
```
```bash
ctrl + b + q # 특정 pane 이동

ctrl + b + o # pane 이동
ctrl + b + 방향기 # pane 이동

$ exit # 삭제 또는 ctrl + d
ctrl + b + x # pane 삭제

ctrl + b + [Alt] + 방향키 # 크기 조절
```

copy mode
처음 실행시에 copy mode의 키가 제대로 동작하지 않았다. 기본으로 emacs style로 되어 있어서 그런것이었다. vi style로 변경하면 잘 된다.
vi style을 적용하면, copy mode에서 이동하는 방향키도 i,j,k,l, ctrl-f, ctrl-b 를 사용할 수 있다.
```bash
# ~/.tmux.conf
# set-window-option -g mode-keys vi

ctrl + b + [ # copy mode 진입
space # copy 시작
Enter # copy 완료
ctrl + b + ] # paste
```

tmux configuration
```bash
# .tmux.conf

# set scrollback history to 10000 (10k)
set -g history-limit 10000

# 상태바 수정하기 http://blog.outsider.ne.kr/699
# Set status bar
set -g status-bg black
set -g status-fg white
set -g status-left '#[fg=green]#H'

# Highlight active window
set-window-option -g window-status-current-bg red
```
