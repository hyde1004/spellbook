###### Reference
 - [Unity](http://unity.sourceforge.net/) 의 examples/example_2
 
이번 글에서는 이전 편과는 다른 순서로 진행한다. 이전 편에서는 함수를 만들고, Test Case를 구성하고, Test Runner 순으로 진행했으나, 이번 편에서는 반대순으로 진행해본다. 왜냐하면 Test Runner을 만드는 관점을 충분히 이해하지 못했기 때문이다.

``` c
/* all_test.c */
#include "unity_fixture.h"

static void RunAllTests(void)
{
    RUN_TEST_GROUP(add);
    RUN_TEST_GROUP(abstract);
}

int main(int argc, char * argv[])
{
    return UnityMain(argc, argv, RunAllTests);
}
```

all_test.c는 Unity를 실행해주는 main( )이다. RunAllTests( )에는 Test Group을 나열해 준다. Test Group은 동일한 모듈을 테스트할 Test Cases을 모아놓은 Container이다. 여기서는 add와 abstract을 Test한다.

``` c
/* TestAdd_Runner.c    */
#include "unity.h"
#include "unity_fixture.h"

TEST_GROUP_RUNNER(add)
{
    RUN_TEST_CASE(add, positive_add);
    RUN_TEST_CASE(add, negative_add);
}

TEST_GROUP_RUNNER(abstract)
{
    RUN_TEST_CASE(abstract, positive_abstract);
    RUN_TEST_CASE(abstract, negative_abstract);
}
```
TestAdd_Runner.c는 Test Runner이다. (원래는 add만 있었음으로 파일이름이 TestAdd_Runner.c였으나, 나중에 abstract을 추가함) 여기는 main( )에 있던 Test Group에 Test Case을 등록하는 것이다. 즉, Test Group에 따른 모든 Test Case를 적어두는 것이다. 이전의 example_1과 비교하면 Test Runner만드는 법이 매우 쉽다. 또한 ruby script를 쓸 필요도 없다. 다만, 만약 여기에 포함되지 않은 Test Case가 있다면, Test되지 않는다. 따라서, Test Case를 추가했다면, 반드시 TEST_GROUP_RUNNER에 추가해주어야 한다.

``` c
/* TestAdd.c */
#include "add.h"
#include "abstract.h"
#include "unity.h"
#include "unity_fixture.h"

TEST_GROUP(add);

TEST_SETUP(add)
{

}

TEST_TEAR_DOWN(add)
{

}

TEST(add, positive_add)
{
    TEST_ASSERT_EQUAL(3, add(1,2));
    TEST_ASSERT_EQUAL(7, add(3,4));
    TEST_ASSERT_EQUAL(43, add(10, 33));
}

TEST(add, negative_add)
{
    TEST_ASSERT_EQUAL(-2, add(-1,-1));
    TEST_ASSERT_EQUAL(-4, add(-3, -1));
    TEST_ASSERT_EQUAL(-12, add(-10,-2));
}

TEST_GROUP(abstract);

TEST_SETUP(abstract)
{

}

TEST_TEAR_DOWN(abstract)
{

}

TEST(abstract, positive_abstract)
{
    TEST_ASSERT_EQUAL(5, abstract(8,3));
    TEST_ASSERT_EQUAL(8, abstract(10,2));
    TEST_ASSERT_EQUAL(2, abstract(10,8));
}

TEST(abstract, negative_abstract)
{
    TEST_ASSERT_EQUAL(-3, abstract(5, 8));
    TEST_ASSERT_EQUAL(-10, abstract(10, 20));
    TEST_ASSERT_EQUAL(-7, abstract(10, 17));
}
```
TestAdd.c (처음에는 add Test Case만 있었으나, abstract을 추가)에는 Test Case를 서술한다. 예제에서는 add와 abstract을 별도 함수로 분리하였으나, 여기 예제처럼 하나의 파일로도 가능하다.
모든 Test Group에서는 TEST_SETUP( ), TEST_TEAR_DOWN( )은 반드시 있어야 하며 그렇지 않으면 컴파일 에러가 발생한다.

다음은 test를 위한 source이다.

``` c
/* add.c */
#include "add.h"

int add(int a, int b)
{
    return a + b;
}
```

``` c
/* abstract.c */
#include "abstract.h"

int abstract(int a, int b)
{
    return a - b;
}
```

``` c
/* add.h */
int add(int a, int b);
```

``` c
/* abstract.h */
int abstract(int a, int b);
```

컴파일하는 법은 다음과 같다. 실제 프로젝트에 이용할때는 Makefile에 src, Test, Unity src로 분리하여 구성하는 것이 좋겠다.

``` sh
gcc src/add.c                                 \
    src/abstract.char                        \
    -Isrc/include 

    -I../Unity-master/extras/fixture/src     \
    -I../Unity-master/src/                     \
    ../Unity-master/src/unity.c             \
    ../Unity-master/extras/fixture/src/unity_fixture.c     \ 

    test/TestAdd.c                             \    
    test/test_runners/TestAdd_Runner.c         \
    test/test_runners/all_tests.c
```
