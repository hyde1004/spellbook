#### du (disk usage)
 - s (summary) : 디렉토리 전체 용량
 - h (human-readable) : 용량을 K, M, G 단위로 표시

```bash
du -sh /work  # work 디렉토리 전체 용량
du -sh /home/*  # /home의 사용자별 용량
```

#### return code
`$?`는 마지막 명령의 return code이다. 일반적으로 `0`이면 성공이다.

```bash
OUT=$?
if [ $OUT -eq 0];then
 echo "User account found!"
eles
 echo "User account does not exists!"
fi
```
```bash
if [ "$?" -ne "0" ]; then
  echo "Sorry, cannot find user ${1} in /etc/passwd"
  exit 1
fi
```
