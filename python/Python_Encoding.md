#### Python 3와 Encoding
###### Reference

Python을 공부하면서 Web Page를 Scrap하는 코드를 만들어보았다.
웹에 대한 지식이 없는지라, 여러가지 시행 착오를 겪었는데 특히 encoding에 애를 먹었다.

우리에게 익숙한 진수로 먼저 예를 들어보자.
화면에 보이는 10진수 10은 2진수로는 '0b1010', 8진수로는 '0o12', 16진수는 '0xA'로 표현할(encode) 수 있다. 
이와 반대로 '10' 이라는 숫자는 2진수로 해석하면 10진수 2, 8진수로 해석하면 10진수 8, 16진수로 해석하면 10진수 16이 될것이다.

이제 우리가 눈에 보이는 문자열(str)을 기준으로 시작해보자.
문자열은 화면에 보이는 문자들의 모임이다. 내부적으로는 어떤 식으로 되어 있던 간에(UTF건, ASCII건, CP949건) 적절하게 처리하여 사용자에게 보여준다. 그런데 이 문자열을 외부로 (web, local file 등) 전송하기 위해서는bytes형태로 전송되고, 그 bytes를 상대방이 이해할 수 있게 알려주어야 한다.  
위에서 예를 들었던 '10'을 다시 생각해보자. 내가 Web page에서 byte 10을 읽어 왔는데, 이를 2진수, 8진수, 10진수에 따라 의미를 달리 해석하는것처럼 UTF-8, CP949에 따라 다른 결과가 나올것이다.

내 환경은 다음과 같다.
 - Python 3.4
 - Windows 7, OS X
 - Sublime Text 2

실제로 내가 겪었던 문제는 특정 Web page의 parsing 결과를 출력할때 에러가 발생하였다. 그런데 OS X와 Windows 결과가 다르고, 더 나아가 OS별 Sublime Text별로도 다르게 나와서 소위 멘붕에 빠졌다. (어쨌건 처음엔 다 안되었다). IDLE(Python GUI IDE)도 헷갈리고 하였고.

좀 더 확인해보니 문제가 발생하는 최초 문자는 '-' (EM DASH)인데, 이는 확장 ASCII table의 151에 해당한다 (http://www.ascii-code.com/). 따라서 이 문자를 기준으로 문제를 살펴보았다.

``` python
a = '—' # EM DASH     # <class 'str'>
b = a.encode('utf-8') # b'\xe2\x80\x94'  <class 'bytes'>
c = b.decode('utf-8') # '—' <class 'str'>
print(b)              # b'\xe2\x80\x94'
print(c)              # UnicodeEncodeError: 'cp949' codec can't encode character '\u2014' in position 0: illegal multibyte sequence
```

python 기준으로 정리해보자.
Python 문자는 내부적으로 어떤 bytes의 모임이다. 이를 PC에게 출력해달라고 bytes를 보내면, PC는 이 bytes를 적절하게 해석을 하고 해당 문자를 찾아서 보여주게 된다. 따라서 해당 bytes에 해당하는 문자를 찾지 못하면 에러가 발생하는 것이다. 

다음을 이해하는 것이 중요하다.
문자는 숫자(bytes)로 코드화할(encode) 수 있고, 숫자(bytes)는 그것을 문자로 해석할(decode) 수 있다.
```
str  -- encode( ) --> bytes -- decode( ) --> str
```
Web page를 열어서 값을 읽어 오는 경우를 정리하면,
해당 값은 bytes 모임이고, 내 PC 내부적으로 처리하는 해석방법과 동일하다면 다행이지만, 그렇지 않다면 적절하게 바꿔줘야 할것이다.

근본 문제는 UTF-8로 encode된 bytes가 들어왔는데, 출력단에서는 이를 해석했고, CP949의 문자들로 출력하려 한것으로 보인다. 그런데 bytes 중에 EM DASH가 있는데, 이는 CP949에는 없는 문자인 듯하다. (일반적인 문자라서 그럴리는 없을텐데...) 따라서 최종단을 UTF-8로 변경하기로 한다.

##### Mac OS X
 - shell : 참고로 Mac OS X는 UTF-8로 처리되고, Web Page 내용도 UTF-8 형식이라 그냥 잘 되었다. (-_-) Sublime Text 2에서 에러가 발생했고 이리저리 코드를 손 댄 덕분에 처음에 잘 안되었던 것이다. 
 - Sublime Text 2 : 실행하면 이상하게도 DOS형식의 'CP949' 관련 에러가 발생한다. 이는 출력단으로 'CP949'로 내보내는 것이라고 판단되었고, Sublime Text 2의 Python Build 옵션을 수정했더니 잘 되었다. ([Sublime Text 2 encoding error with python3 build](https://stackoverflow.com/questions/15166076/sublime-text-2-encoding-error-with-python3-build/15174760#15174760) )
 
##### Windows
 - cmd : Windows에서는 CP949를 사용한다. 위의 Python code를 실행하면 error가 발생하는데, cmd 창을 UTF-8로 바꿔줌으로써 정상적으로 실행되었다. ([cmd(도스 명령창/실행창)에서 UTF-8 , 한글적용하기](http://ciwhiz.tistory.com/252)) 그런데 항상 적용되는 게 아니라, 매번 창을 열고 설정을 변경해줘야 한다.
 - Sublime Text 2 : DOS가 기본적으로 CP949라 Python Build 옵션의 encoding 변경으로도 안되었다. cmd 변경하는 방법이 있을것 같은데 아직 찾지 못함.

이 방법 말고도 encode()의 옵션에서 해당 문자를 무시(ignore)하거나 대체(replace)하는 방법도 사용할 수 있다.