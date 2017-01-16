#### 코루틴

###### Reference
 - [Improve Your Python: 'yield' and Generators Explained](https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/)
 - [많은 함수를 동시에 실행하려면 코루틴을 고려](http://brownbears.tistory.com/237)
 - [파이썬의 제너레이터와 이더레이터](http://haerakai.tistory.com/34)
 - [Iterator와 Generator](http://pythonstudy.xyz/python/article/23-Iterator%EC%99%80-Generator)
 - [파이썬 이터레이터](http://www.flowdas.com/blog/iterators-in-python/)
 - [파이썬 제너레이터](http://www.flowdas.com/blog/generators-in-python/)

##### 사전 학습이 필요한 사항
 - Iterator
 - Iterable : Iteration이 가능한지. `iter()`을 통해 Iterator를 생성할수 있다.
 - Iteration : 각 요소를 가져오는 행위

for문은 컨테이너의 각 요소를 가져오는데, 이 때 next()가 호출된다. iterable한 컨테이너인 경우에는 내부적으로 `iter()`를 호출하여 iterator 객체를 만들고 `next()`를 통해 각 요소에 접근한다. 이는 `StopInteratorException`이 발생될때까지 계속된다.
코루틴은 기본적으로는 함수와 유사하다. 다만 함수가 return을 만나면 값을 리턴하고 종료된다는 것에 반해, 코루틴은 yield를 만나면 값을 리턴하고 실행을 잠시 중지한다.

코루틴을 통한 값 입력은 다음과 같은 방식이다.
``` python
    input_num = yield
```

코루틴은 다음 경우에 사용된다
 - 배열의 처리 : 원소가 매우 많거나, 하나의 값 처리에 시간이 많이 걸리는 경우
 - 무한 값에 대한 처리
 - 하나의 값에 대해 파이프라인 처리하기
 - 여러개의 함수를 실행하기 (쓰레드 효과)

 코루틴과 제너레이터의 차이점은?

 이터레이터는 내장함수 `next()`를 통해 원소를 탐색할 수 있는 객체를 의미한다. 만약 사용자가 정의한 클래스가 이터레이터를 지원하려면 다음의 메쏘드를 정의해야 한다. 예를 들어 `[]`는 이터레이터가 아니지만, 이터러블하다. 이는 `iter()`을 통해 이터레이터 객체를 리턴하고 이 객체에 `next()`를 이용하여 각 원소에 접근가능하다.
  - `__iter__()` : `iter()`에 의해 호출되며, 이터레이터 객체를 리턴해주는 메쏘드
  - `__next__()` : `next()`에 의해 호출되며, 다음 원소를 탐색하는 메쏘드

제너레이터를 이용하면 쉽게 이터레이터를 만들수 있다.

 ##### 좋은 구문
 리스트나 Set과 같은 컬렉션에 대한 iterator는 해당 컬렉션이 이미 모든 값을 가지고 있는 경우이나, Generator는 모든 데이타를 갖지 않은 상태에서 yield에 의해 하나씩만 데이타를 만들어 가져온다는 차이점이 있다. (http://pythonstudy.xyz/python/article/23-Iterator%EC%99%80-Generator)
