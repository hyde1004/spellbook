#### Python Note

##### 정수 나눗셈
``` python
3 / 2 # 1.5
3 // 2 # 1
```

##### List Comprehension
아래에서 결국엔 `len(n)`으로 List가 채워진다.
``` python
len_cycles = [len(n) for n in cycles]
```

##### Directory operators
https://docs.python.org/3.4/library/pathlib.html#basic-use

##### zip function
여러 리스트를 김밥말듯 말아서, 자른다.
```python
a = [1, 2, 3, 4, 5]
b = ['a', 'e', 'i', 'o', 'u']
for x, y in zip(a, b):
	print(x, y)

1 a
2 e
3 i
4 o
5 u    
```

##### import 사용법
``` python
# import 파일명 형태
import module1
module1.hello()

# from 파일명 import 함수명 형태 (파일명 생략가능)
from module1 import hello() 
```

`if __name__ == '__main__'` 구문은 파일 단독으로 실행하는 경우만 동작하고, 다른 파일에서 재사용할때는 동작하지 않는 부분이다.

##### list slice
###### 출처 : http://codingbat.com/prob/p148661
다음의 결과는 서로 다르다.

``` python
def rotate_left3(nums):
	return nums[1:] + nums[0:1] # list + list
    return nums[1:] + nums[0] # 불가 : list + int
```

##### 진수 관련
10진수를 제외한 진수은 0을 붙이고 시작한다.
``` python
a = 10     # 10진수 10
b = 0b10   # 2진수 10, 10진수 2
c = 0o10   # 8진수 10, 10진수 8
d = 0x10   # 16진수 10, 10진수 16

```

10진수를 다른 진수로 변환하기
``` python
bin(10)    # '0b1010'
oct(10)    # '0o12'
hex(10)    # '0xa'
```

문자를 해당 진수로 해석하기
``` python
int("10")     # 10
int("10", 2)  # 2
int("10", 8)  # 8
int("10", 16) # 16
```

##### 객체 타입 확인하기
`isinstance(object, classinfo)`를 사용한다. unittest의 객체 생성후에 확인용도로도 적합할것 같다.

``` python
isinstance(1, int) # True
```

##### list의 마지막 원소
`a[len(a)-1]`은 `a[-1]`처럼 reverse index를 사용하면, 더 단순하다. 

##### print 사용시에 이어서 출력하기
``` python
print('0', end='')
print('1', end='')
print('2', end='')
```

##### 몫, 나머지 구하기
``` python

divmod(10,3) # (3,1) 

```

#### list의 `append`와 `extend`의 차이
`append`는 더하고, `extend`는 합친다.

``` python
x = [1, 2, 3]
x.append([4, 5])
print (x) 
# [1, 2, 3, [4, 5]] 

x = [1, 2, 3]
x.extend([4, 5])
print (x)
# [1, 2, 3, 4, 5]
```
