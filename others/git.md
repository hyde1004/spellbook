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
 - `git log <tag name>..HEAD` : 특정 tag name 이후의 commit 표시

##### 응용
repo 명령과 결합하여, commit hash, committer, date, subject을 출력하기
 - commit에 색상을 넣기 위해 `%C`를 사용
 - commit date를 `YYYY-MM-DD`로 표시하기 위해 `%cd`와 `--date=short` 사용
 - repo와 결합 사용시 project별로 new line을 위해 `tformat` 사용
 - committer와 subject를 구분하기 위해 `%x09`를 사용하여 tab 띄우기 

```
git log --pretty=tformat:'%C(yellow)%h %C(green) %cn %x09 %C(white)%cd %s' --date=short

project android/
d5225e6  yt8.kim         2016-11-24 [Airtel][][18p][Cannonball r157][]

project android/device/lge/
9444424  jihyun.lee1     2016-11-22 [Airtel][][WIFI][ change default value of def_wifi_scan_always_available to 1 (to support scan always ]

project android/frameworks/
3a5dd0b  Jeong jin Ko    2016-11-24 [][None][SQLITE][][roll-back ContentProviderNative.java because of CTS failure]

project android/vendor/airtel/
d1ec868  yt8.kim         2016-11-23 [Airtel][][App][Airtel TV app ver.0.25.2][]

project android/vendor/broadcom/
70972d9  taeil10.kim     2016-11-24 [Airtel][][HDMI][HDCP control when power on/off][]
120375b  taeil10.kim     2016-11-24 [Airtel][][HDMI][disable hdcp hotplug][]

project android/vendor/lge/
3c75411  junggu.lee      2016-11-25 [Airtel][][CM][Dtv Rev. 3471][]
594411a  Jeong jin Ko    2016-11-25 Merge branch 'feature/netflix' of ssh://mod.lge.com:2222/airtel/android_vendor_lge into feature/netflix
0a15c7c  Jeong jin Ko    2016-11-25 [][None][TVInput][][added Logcat log for debugging]
5da3f90  taeil10.kim     2016-11-24 [Airtel][][HDMI][add hdcp control][]
955ccc3  keith.kim       2016-11-24 Merge branch 'feature/netflix' of ssh://mod.lge.com:2222/airtel/android_vendor_lge into test2
29f252e  keith.kim       2016-11-24 [Airtel][][PVR][to avoid null point exception, TATA-1028][]
9300fd1  yt8.kim         2016-11-23 [Airtel][][UI][bootanimation : TATA-1025][]

```
