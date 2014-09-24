
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
 - urlparse()
 - urlunparse()

``` python
import urllib.parse
url = 'http://astro.kasi.re.kr/Life/Knowledge/sunmoon_map/sunmoon_popup.php?year=2014&month=9&location=%C3%B5%BE%C8'
urllib.parse.urlparse(url)

# ParseResult(scheme='http', netloc='astro.kasi.re.kr', path='/Life/Knowledge/sunmoon_map/sunmoon_popup.php', params='', query='year=2014&month=9&location=%C3%B5%BE%C8', fragment='')

url = 'http://search.naver.com/search.naver?where=nexearch&query=apple&sm=top_hty&fbm=1&ie=utf8'
urllib.parse.urlparse(url)
ParseResult(scheme='http', netloc='search.naver.com', path='/search.naver', params='', query='where=nexearch&query=apple&sm=top_hty&fbm=1&ie=utf8', fragment='')

```

#### BeautifulSoup4
###### Reference
 - [BeautifulSoup4 번역문서](http://coreapython.hosting.paran.com/etc/beautifulsoup4.html)
 - [How to find tags with only certain attributes - BeautifulSoup](http://stackoverflow.com/questions/8933863/how-to-find-tags-with-only-certain-attributes-beautifulsoup)

기본 사용방법은 html문서를 BeautfilSoup에 넣어주면 된다.

``` python
import bs4

soup = bs4.BeautifulSoup(html_doc)

print(soup.prettify())  # 보기 좋게 출력

soup.title		# title tag에 접근
soup.body		# body tag에 접근

for talk in soup.find_all('div', {'class':'talk'}):  # div tag의 속성으로 검색
	print(talk.span.text)
# <div class=\'talk\'><span>Mom: How was school today, Sam?</span></div>

```

`find_all()`의 결과는 ResultSet인데, 각 결과를 담고 있는 list이다. 따라서 list의 원소에 대해 다시 `find_all()`을 사용가능하다. 일출 시간을 가져오는 예제이다. (https://github.com/hyde1004/sunrise_info)

``` python
url = 'http://astro.kasi.re.kr/Life/Knowledge/sunmoon_map/sunmoon_popup.php?year=2014&month=9&location=%C3%B5%BE%C8'

soup = bs4.BeautifulSoup(html)

day_info = soup.tbody.find_all('tr')
for info in day_info:
	sunrise_info = info.find_all('td')
	print(sunrise_info[2].text)
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
