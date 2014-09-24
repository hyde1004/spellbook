#### extern "C"의 사용

###### Reference
 - [Why do we need extern “C”{ #include <foo.h> } in C++?](http://stackoverflow.com/questions/67894/why-do-we-need-extern-c-include-foo-h-in-c)

##### 기본 code

```c
/* add.h */
int add(int a, int b);
```

```c
/* add.c */
int add(int a, int b)
{
	return a + b;
}
```

```c
/* hello.cpp */
#include <stdio.h>

#include "add.h"

int main(void)
{
	printf("hello world\n");
	add(3,5);

	return 0;
}
```

hello.cpp의 add 심볼을 보면, c++ 형태로 되어 있다.
```sh
Jungguui-MacBook-Pro:sand_project hyde1004$ g++ -c hello.cpp 
Jungguui-MacBook-Pro:sand_project hyde1004$ nm hello.o
0000000000000070 s EH_frame0
000000000000003f s L_.str
                 U __Z3addii
0000000000000000 T _main
0000000000000088 S _main.eh
                 U _printf
```

add.c의 add 심볼 역시, c++ 형태이다.
```sh
Jungguui-MacBook-Pro:sand_project hyde1004$ g++ -c add.c 
clang: warning: treating 'c' input as 'c++' when in C++ mode, this behavior is deprecated
Jungguui-MacBook-Pro:sand_project hyde1004$ nm add.o
0000000000000038 s EH_frame0
0000000000000000 T __Z3addii
0000000000000050 S __Z3addii.eh
```

add.c를 다음과 같이 수정하고, 심볼을 살펴보면 c형태로 되어 있음을 확인할 수 있다.
```c
/* add.c */
#ifdef __cplusplus
extern "C" {
#endif

int add(int a, int b)
{
	return a + b;
}

#ifdef __cplusplus
}
#endif
```

```sh
Jungguui-MacBook-Pro:sand_project hyde1004$ g++ -c add.c 
clang: warning: treating 'c' input as 'c++' when in C++ mode, this behavior is deprecated
Jungguui-MacBook-Pro:sand_project hyde1004$ nm add.o
0000000000000038 s EH_frame0
0000000000000000 T _add
0000000000000050 S _add.eh
```

현재 상태에서 링크를 시도하면, hello.o와 add.o의 심볼이 달라서 에러가 발생한다. hello.o의 add()는 c++형태이고, add.o는 c형태이다.
```sh
Jungguui-MacBook-Pro:sand_project hyde1004$ g++ hello.o add.o 
Undefined symbols for architecture x86_64:
  "add(int, int)", referenced from:
      _main in hello.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

다음과 같이 hello.cpp를 수정하고 다시 링크를 해보자. 정상적으로 링크가 완료된다. hello.cpp의 `extern "C"`를 add.h로 옮기는 것도 괜찮을 것 같다.
```sh
/* hello.cpp */
#include <stdio.h>

#ifdef __cplusplus
extern "C" {
#endif

#include "add.h"

#ifdef __cplusplus
}
#endif

int main(void)
{
	printf("hello world\n");
	add(3,5);

	return 0;
}
```

```sh
Jungguui-MacBook-Pro:sand_project hyde1004$ g++ -c hello.cpp 
Jungguui-MacBook-Pro:sand_project hyde1004$ nm hello.o
0000000000000070 s EH_frame0
000000000000003f s L_.str
                 U _add
0000000000000000 T _main
0000000000000088 S _main.eh
                 U _printf
```

```sh
Jungguui-MacBook-Pro:sand_project hyde1004$ g++ add.o hello.o
```