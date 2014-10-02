#### CppUTest

###### Reference
 - [Cpputest](http://cpputest.github.io/)

CppUTest는 unit test framework이다. C++로 만들어졌으나, C언어에도 쉽게 적용가능하다.

##### Compile
```sh
g++ <test file> -I$(CPPUTEST_HOME)/include -L$(CPPUTEST_HOME)/lib -lCppUTest -lCppUTestExt
```
참고로 `-I<include directory path>`, `-L<library directory path>`, 그리고 `-l<library file name>`이다. library는 항상 lib로 시작하고, 확장자는 .a 이므로 이러한 정보는 생략하여 표시한다. 즉, -lCppUTest는 실제로 libCppUtest.a와 링크하라는 의미이다. 

Mac에서는 brew를 이용하여 설차하였는데 설치된 경로는 `/usr/local/opt/cpputest`이었다. 이유는 알수 없으나 컴파일시에 `$(CPPUTEST)`의 괄호를 제거해주어야만 제대로 되었다.

```C
// AllTests.cpp

#include "CppUTest/CommandLineTestRunner.h"

int main(int ac, char** av)
{
	return RUN_ALL_TESTS(ac, av);
}
```

```C
// add_test.cpp

#include "CppUTest/TestHarness.h"

TEST_GROUP(Add)
{
};

TEST(Add, test)
{
	FAIL("FAIL ME!");
}


```
