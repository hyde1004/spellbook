###### Reference : http://www.joinc.co.kr/modules/moniwiki/wiki.php/Site/C/Documents/minzkn_make#s-7

makefile에서 target이 있는 경우에는 해당 명령이 실행되지 않는다. 
이 부분이 문제가 일으킬 수 있는데, 예를 들어 make clean 을 실행할때 
실제로 clean이라는 파일이 존재하는 경우이다. 
이 때문에 clean이라는 파일의 유무에 상관없이 make clean이 항상 실행되도록 할 필요가 있으며, 
명시적으로 .PHONY: 를 통해 해당 target은 존재유무에 상관없이 항상 만들도록 한다.

즉, 해당 target은 실제 파일이 아님을 명시적으로 알려주는 것이다.

``` 
/* filename : hello.c */
 
#include <stdio.h>
 
int main(void)
{
    printf("Hello, world!\n");
   
    return 0;
}
```

```
#filename : makefile
.PHONY: clean
 
all: hello
    gcc hello.c -o hello
 
clean:
    rm hello
```
