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
