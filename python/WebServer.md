#### (작성 중)Python을 이용한 간략 Web Server
Python을 이용하여 간단한 Web Server를 구성하려 한다. 내부 결과를 Web Browser를 통해 볼 수 있도록 하며, 이를 통해 Python의 Web Server 구현과 Http에 대한 이해를 높일 것이다.
###### Reference
 - [http.server — HTTP servers](https://docs.python.org/3/library/http.server.html?highlight=http.server#module-http.server)
 - [[python] BaseHTTPServer 웹 서버의 구현](http://carpedm20.blogspot.kr/2013/05/python-basehttpserver.html)
 - [웹페이지를 통해 내 PC의 프로그램 상태 모니터하기](https://wiki.changwoo.pe.kr/project:downloadmonitor)
 - [국민내비 김기사와 Python](https://drive.google.com/file/d/0B2PzpeLe8OqBMHJmWk4zZ0MwTk0/edit?usp=sharing)

##### Web Server 구동하기
Python3에서는 다음과 같이 간단히 확인할 수 있다. 아래를 실행하고 `http://localhost:8000/`, 내 컴퓨터의 파일들을(DOS에서는 'C:\Users\heuser' ) 보여준다. 

``` shell 
python --help
-m mod : run library module as a script (terminates option list)

python -m http.server 8000

```

##### Web Server 변경하기
아래코드는  [[python] BaseHTTPServer 웹 서버의 구현](http://carpedm20.blogspot.kr/2013/05/python-basehttpserver.html)에서 가져온 코드의 에러를 수정한 것이다. 기본적으로 HTTP Request를 어떻게 처리할것인가에 대한 Handler를 정의하면 된다.

``` python
import http.server

class MyHandler(http.server.BaseHTTPRequestHandler):
	def do_GET(self):
		self.send_response(200)
		self.send_header('Content-type', 'text/html')
		self.end_headers()
		self.wfile.write(bytes('<html><body>Hello, world!</body></html>', 'UTF-8'))

print("Listening on port 8000")
server = http.server.HTTPServer(('', 8000), MyHandler)
server.serve_forever()
```

Request Handler로서 다음 3가지 class가 있다.
 - http.server.BaseHTTPRequestHandler : HTTP Request 처리
 - http.server.SimpleHTTPRequestHandler : This class serves files from the current directory and below, directly mapping the directory structure to HTTP requests.
 - http.server.CGIHTTPRequestHandler : This class is used to serve either files or output of CGI scripts from the current directory and below.


