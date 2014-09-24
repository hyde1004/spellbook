#### Unity를 이용한 TDD

##### Reference
 - [Unity](http://unity.sourceforge.net) 의 examples/example_1

Unity는 C언어를 이용한 TDD framework이다. Embedded에 적용할 수 있도록 header file 2개와 c파일 하나로 구성되어 있다.
다만, Test Runner하는 부분이 성가신데, 이는 ruby script를 이용하여 해결할 수 있다.

다음과 같이 단순한 예제를 구성하였다.
```c
/* add.h */
#include <stdint.h>
int32_t add(int32_t a, int32_t b); 
```

```c
/* add.c */
#include <stdint.h>

int32_t add(int32_t a, int32_t b)
{
    return (a+b);
}
```

```c
/* test_add.c */
#include "add.h"
#include "unity.h"

void setUp(void)
{
    /* 생략시 에러 발생 */
}

void tearDown(void)
{
    /* 생략시 에러 발생 */
}

void test_add(void)
{
    TEST_ASSERT_EQUAL(7, add(3,4));
}
```

파일은 Unity중 필수적으로 필요한 것만 복사하여 구성하였다.
```bash
.
├── add.c
├── add.h
├── test_add.c
└── unity
    ├── generate_test_runner.rb
    ├── unity.c
    ├── unity.h
    └── unity_internals.h

1 directory, 7 files

```


컴파일 및 실행하는 방법은 다음과 같다.

```bash
ruby unity/generate_test_runner.rb test_add.c
gcc -Iunity unity/unity.c add.c test_add_Runner.c
./a.out

test_add.c:11:test_add:PASS
-----------------------
1 Tests 0 Failures 0 Ignored
OK

```

이러한 방법은 실제로 사용하기에는 다소 불편하다.
 - Test Runner를 만드는 방법이 복잡하다. ruby script를 이용하면 되지만, 번거롭고 ruby가 설치되어 있어야 한다.
 - Test Case가 변경되면, Test Runner도 같이 변경해주어야 한다.
 - shell command에서 명령을 내리기에는 손이 많이 간다.

Unity example에 포함된 makefile을 다음과 같이 수정하였다.
```bash
/* makefile */
# ==========================================
#   Unity Project - A Test Framework for C
#   Copyright (c) 2007 Mike Karlesky, Mark VanderVoord, Greg Williams
#   [Released under MIT License. Please refer to license.txt for details]
# ==========================================

UNITY_ROOT=./unity
C_COMPILER=gcc
TARGET=testAdd
SRC_FILES=$(UNITY_ROOT)/unity.c add.c test_add.c test_add_Runner.c
INC_DIRS=-I$(UNITY_ROOT)

CLEANUP = rm -f *.o ; rm -f $(TARGET)

all: clean default

default:
        ruby $(UNITY_ROOT)/generate_test_runner.rb test_add.c
        $(C_COMPILER) $(INC_DIRS) $(SRC_FILES) -o $(TARGET)
        ./$(TARGET)

clean:
        $(CLEANUP)
```

디렉토리 구조나 makefile을 좀 더 적절하게 변경하는 것은 추후에 추가할 예정이다.

그런데 example_1을 따라해보니, 실제로 매우 불편했다.
 - 나 스스로는 Test Runner를 만들지 못하겠다. script를 써야만 했다.
 - Test Group하나만 가능하다. 즉 Test Case 모음은 하나의 파일에만 존재해야 했다. Test Runner를 만들기 위해서 ruby scriptt로 2개의 Test Case 파일을 시도하면 에러가 발생했다. ( main( ) 함수가 2개 생기기 때문이다. )

이러한 문제는 example_2에서 해결되었다.