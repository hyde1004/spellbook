#### static variable

함수에서외부 정적 변수를 return하면 어떻게 될까? (임베디드 C를 위한 TDD, p74)

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
