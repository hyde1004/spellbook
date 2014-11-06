#### Compile

##### g++의 c파일 컴파일 warning 없애기
MacOS 환경에서 g++로 .c 파일 컴파일하면 warning이 발생한다. warning을 제거하려면 `-Wno-deprecated` 옵션을 추가한다.

##### Makefile

$*는 목표 이름에서 확장자를 제거한 이름이다.
``` bash
tcp.o	: tcp.c tcp.h 
  gcc -c tcp.c 
```
수정하면 다음과 같다.
``` bash
tcp.o	: tcp.c tcp.h 
    gcc -c $*.c
```
