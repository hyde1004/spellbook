#### pytest

###### Reference
 - [pytest Installation and Getting Started](http://doc.pytest.org/en/latest/getting-started.html)

##### 사용법
pytest는 `assert`구문의 예외를 검사하는 방식으로 구현된다. test case는 'test_xxx()' 형태로 만든다.

```
def func(x):
    return x + 1

def test_answer():
    assert func(3) == 4

```
