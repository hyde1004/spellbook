#### volatile
##### References
 - [wikipedia : volatile 변수](http://ko.wikipedia.org/wiki/Volatile_%EB%B3%80%EC%88%98)
 - [naver 지식인](http://kin.naver.com/qna/detail.nhn?d1id=1&dirId=1040101&docId=68422258&qb=dm9sYXRpbGU=&enc=utf8&section=kin&rank=2&search_sort=0&spq=1&pid=R0SZYwpySEssssAlAiVssssssth-513952&sid=U0VDenJvLDUAAAfvHds)
 - [Volatile : 멀티쓰레드 프로그래밍 시 거의 쓸모 없는 그 것](http://blog.naver.com/the_sky_?Redirect=Log&logNo=150187339263)

volatile 키워드에 대해서 찾아보게 된 계기는 'Head First Design Patterns'의 싱글톤 패턴에서 volatile을 사용하고 있었기 때문이었다.

C언어 문법 중 완전히 이해되지 않은 부분이 volatile이었는데, 오늘에야 그 의미를 이해하게 되었다. volatile의 의미는 컴파일 최적화를 하지 않는다는 것이다. 그것은 컴파일러의 최적화 옵션과 관련이 있다.
 - 코드는 순서대로 실행되지 않는다.
 - 코드대로 기계어로 변환되지 않는다.

아래는 위키에서 가져온 코드이다.
```C
static volatile int foo;
 
void bar (void)
{
    foo = 0;
 
    while (foo != 255);
}
```

사실 위 코드는 foo값이 255가 될때까지 기다린다. 그러나 volatile 키워드가 없다면, 컴파일러는 아래와 같이 최적화한다.
```C
void bar_optimized(void)
{
    foo = 0;
 
    while (true);
}
```
사실 컴파일러 입장에서는 명백하다. foo는 0이고 변경되지 않기 때문에 항상 while은 참이 되므로, foo를 비교할 필요없다고 여기게 된다. 그러나, 실제로는 하드웨어 인터럽트등을 통해 값이 변경될 수 있다는 것이다.
'Head First Design Patterns'에서는 멀티스레딩에 대한 내용을 서술하면서, 위의 코드에서와 비슷한 상황을 설명하고 있다. 그러나 References의 마지막 링크에서는 조금 다른 이야기를 하고 있으므로 참조할 필요가 있다.