#### 코루틴

###### Reference
 - [Improve Your Python: 'yield' and Generators Explained](https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/)
 - [많은 함수를 동시에 실행하려면 코루틴을 고려](http://brownbears.tistory.com/237)

코루틴은 기본적으로는 함수와 유사하다. 다만 함수가 return을 만나면 값을 리턴하고 종료된다는 것에 반해, 코루틴은 yield를 만나면 값을 리턴하고 실행을 잠시 중지한다.

코루틴은 다음 경우에 사용된다
 - 배열의 처리 : 원소가 매우 많거나, 하나의 값 처리에 시간이 많이 걸리는 경우
 - 무한 값에 대한 처리
 - 하나의 값에 대해 파이프라인 처리하기
 - 여러개의 함수를 실행하기 (쓰레드 효과)
