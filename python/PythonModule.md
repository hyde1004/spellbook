
#### urllib
###### python3에서 urllib2는 urllib에 흡수되었다.

urllib는 다음 모듈을 모아 놓은 패키지이다.

- urllib.request for opening and reading URLs
- urllib.error containing the exceptions raised by urllib.request
- urllib.parse for parsing URLs
- urllib.robotparser for parsing robots.txt files

urllib는 url처리 모듈이다.
다음은 가장 간단한 사용방법이다.

``` python
# code from https://docs.python.org/3/howto/urllib2.html
import urllib.request
url = 'http://dna.daum.net'

response = urllib.request.urlopen(url) # file open과 유사
html = response.read()
response.close()
```
`urlopen()`은 url 또는 `Request`객체를 인자로 받는다. `Request` 객체를 사용하면, POST mehtod를 사용하거나, header를 추가할 수 있다. `urlopen()`에 data를 넘기면 POST method로 수행된다.

``` python
import urllib.request
url = 'http://dna.daum.net'
data = urllib.parse.urlencode({'spam':1, 'eggs':2})
data = data.encode('utf-8')
req1 = urllib.request.Request(url)
response = urllib.request.urlopen(url, data)
```
#### urllib.request
###### 출처 : https://docs.python.org/3/library/urllib.request.html#module-urllib.request

urllib.request는 URL관련한 열기, 인증, 쿠키 등에 대한 클래스와 함수를 정의한다.

``` python
# Class
urllib.request.Request(url, data=None, headers={}, origin_req_host=None, unverifiable=False, method=None)

# Function
urllib.request.urlopen(url, data=None, [timeout, ]*, cafile=None, capath=None, cadefault=False)
```
기본 사용형태는 다음과 같다
``` python
import urllib.request

url = "http://www.naver.com"

req = urllib.request.Request(url)
response = urllib.request.urlopen(req)

result = response.read().decode('utf-8')
```


#### urllib.parse
urllib.parse는 url을 분해하거나 결합하는 모듈이다.
 - urlparse(), urlunparse()
 - urlsplit(), urlunsplit() : params는 split하지 않는다.
 - urlencode() : percent encoded

``` python
import urllib.parse

url = 'http://astro.kasi.re.kr/Life/Knowledge/sunmoon_map/sunmoon_popup.php?year=2014&month=9&location=%C3%B5%BE%C8'

out = urllib.parse.urlparse(url)

print(out)
# ParseResult(scheme='http', netloc='astro.kasi.re.kr', path='/Life/Knowledge/sunmoon_map/sunmoon_popup.php', params='', query='year=2014&month=9&location=%C3%B5%BE%C8', fragment='')

print(out.scheme)
# http

print(out.netloc)
# astro.kasi.re.kr

print(out.query)
# year=2014&month=9&location=%C3%B5%BE%C8

urllib.parse.urlunparse(out)
# 'http://astro.kasi.re.kr/Life/Knowledge/sunmoon_map/sunmoon_popup.php?
# year=2014&month=9&location=%C3%B5%BE%C8'

```

``` python
import urllib.parse
import urllib.request


# try 1 : 원하는 encode 결과가 나오지 않는다.
url = 'http://astro.kasi.re.kr/Life/Knowledge/sunmoon_map/sunmoon_popup.php'
query = urllib.parse.urlencode({'year':2014, 'month':9, 'location':'천안'})
query = query.encode('euc-kr') 

# try 2 : 원하는 encode 결과가 나온다.
url = 'http://astro.kasi.re.kr/Life/Knowledge/sunmoon_map/sunmoon_popup.php'
query = urllib.parse.urlencode({'year':2014, 'month':9, 'location':'천안'.encode('euc-kr')})
query = query.encode('euc-kr') 

# try 3 : 원하는 encode 결과가 나온다.
url = 'http://astro.kasi.re.kr/Life/Knowledge/sunmoon_map/sunmoon_popup.php'
query = urllib.parse.urlencode({'year':2014, 'month':9, 'location':'천안'}, encoding='euc-kr')
query = query.encode('euc-kr') 


# try 2, 3 처럼 urlencode()에 encoding을 명시하지 않으면,
# encoding='utf-8'로 선처리되어, 원하는 결과가 나오지 않는다.

query = query.encode('euc-kr') 
# encode 하지 않으면, open할때 에러 발생. 
# TypeError: POST data should be bytes or an iterable of bytes. 
# It cannot be of type str.
# urllib.request.Request()의 인자로 사용하기 위해서는
# 반드시 bytes 형태로 변환해주어야 하는것 같다.

# 그런데, urllib.request.urlopen()에 넣는 방법은 str형태도 허용한다.
# POST 데이터를 보낼게 아니라면, 
# 위의 방법보다 try 2가 더 단순하고, 적절해 보인다.

# try 1
req = urllib.request.Request(url, query)
f = urllib.request.urlopen(req)
f.read()

# try 2
query = urllib.parse.urlencode({'year':2014, 'month':9, 'location':'천안'}, encoding='euc-kr')
f = urllib.request.urlopen("%s?%s" % (url, query))
f.read()
```

#### unittest

##### Skipping tests
`@unittest.skip( )`을 사용하면, 해당 test를 skip할 수 있다. 이외에 여러 조건을 지정할 수 있다.
``` python
class MyTestCase(unittest.TestCase):
	@unittest.skip("demonstrating skipping")
    def test_nothing(self):
    	self.fail("shouldn't happen")
```

##### 반복 구문
`setUp()`과 `tearDown()`을 사용하면 된다. 대소문자에 주의하자.
``` python
class MyTestCase(unittest.TestCase):
	def setUp(self):
		pass
	def tearDown(self):
		pass
```
##### floating tests
소수부는 상황에 따라서 조금씩 다른 값을 가진다. (예 1.0 <-> 0.9999999 )
비슷한 값을 비교할때 쓸 수 있는 조건이다.
``` python
assertAlmostEqual(a, b)
```

#### datetime
datetime모듈에는 datetime 클래스이외에 date, time 클래스가 있다.

```python
import datetime

today = datetime.date(2014, 9, 24)
print(today.year)
print(today.month)
print(today.day)

now = datetime.time(17, 40, 24)
print(now.hour)
print(now.minute)
print(now.second)
```

#### math
실수의 정수부와 소수부를 분리하는 함수이다.
``` python
import math
math.modf(1.4)
# (0.3999999999999999, 1.0)
```

#### random
``` python
import random
random.randint(1, 3) # 1~3 범위. 1과 3을 포함.
```
