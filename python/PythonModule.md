
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

url = 'http://astro.kasi.re.kr/Life/Knowledge/sunmoon_map/sunmoon_popup.php'
# query = urllib.parse.urlencode({'year':2014, 'month':9, 'location':'천안'})
query = urllib.parse.urlencode({'year':2014, 'month':9, 'location':'천안'.encode('euc-kr')})
# '천안'.encode('euc-kr')로 encode하지 않으면, 제대로 동작하지 않는다. 왜일까?

query = query.encode('euc-kr') 
# encode 하지 않으면, open할때 에러 발생. 
# TypeError: POST data should be bytes or an iterable of bytes. 
# It cannot be of type str.

req = urllib.request.Request(url, query)
f = urllib.request.urlopen(req)
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
