#### static variable

함수에서외부 정적 변수를 return하면 어떻게 될까? (임베디드 C를 위한 TDD, p74 참조)
다른 파일에서도 외부 정적 변수 값을 읽을 수 있었다. 
아마도 정적 변수값을 call by value로 복사해서 주기 때문인것 같다.

``` c
/* reader.c */
void reader(void)
{
    printf("count : %d\n", getCount());
}
```

``` c
/* count.c */
static int count = 100;

int getCount(void)
{
    return count;
}
```
