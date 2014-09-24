#### GDB 사용법

다음 예제는 introduction to GDB a tutorial - Harvard CS50 (http://www.youtube.com/watch?v=sCtY--xRUyI)에서 가져왔다. 프로그램은 factorial을 구하는 것으로 버그를 가지고 있어서 제대로 동작하지 않는다.

```c
/* filename : factorial.c */
#include <stdio.h>

int main(void)
{
        int num;
        int factorial;
        int i;

        do
        {
                printf("Enter a positive integer: ");
                scanf("%d",&num);
        }
        while(num<0);

        for(i=0; i<=num;i++)
                factorial = factorial * i;

        printf("%d! = %d\n", num, factorial);

        return 0;
}
```

##### Compile하는 법
Compile option으로 `-g`을 넣는다. 
``` bash
gcc -g factorial.c`)
```

##### gdb 실행법
``` bash
gdb ./factorial
```

##### gdb 종료법
``` bash
quit
```

##### break point 걸기
``` bash
break main
```

##### line별로 실행하기
```bash
next # go to next line
run
```

##### 기타
```bash
list
```