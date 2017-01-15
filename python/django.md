#### Django

기본적 파일 구성은 다음과 같다.
 - admin.py : 관리자 페이지
 - settings.py : 디버그 모드, 앱추가, 데이터베이스 엔진 설정
 - manage.py : 실행파일
 - urls.py : 유저가 접근하는 url

manage.py의 관리 명령
 - startapp : 앱 생성
 - runserver : 서버 실행
 - createsuperuser : 관리자 생성
 - makemigrations app : app의 모델 변경 사항 체크
 - migrate : 변경 사항을 DB에 반영


간단한 예제
``` bash
pip install django

django-admin startproject tutorial # tutorial project 생성

cd tutorial

./manage.py startapp community # community 앱 생성

./manage.py migrate # 데이터베이스 생성 (db.sqlite3 생성)

./manage.py createsuperuser # admin 계정 생성

./manage.py runserver # 웹 서버 구동

# http://127.0.0.1/admin : admin page
```

``` python
# 앱 추가 : settings.py
INSTALLED_APPS = [
    'community',
]

# 모델 생성 : community/models.py
class Article(models.Model):
    name = models.CharField(max_length=50)
    title = models.CharField(max_length=50)
    contents = models.TextField()
    url = models.URLField()
    email = models.EmailField()
    cdate = models.DateTimeField(auto_now_add=True) # 자동으로 생성 날짜 추가

# 모델의 데이터베이스 생성.
./manage.py makemigrations community # community 앱의 변화 확인
./manage.py migrate # 실제 데이터베이스 생성

# 글쓰기 홈페이지 생성하기
# 유저가 접근하는 url 추가 : urls.py
urlpatterns = [
    url(r'^write/', write, name='write'), # url에 대응하는 write() 함수 추가
]
from community.views import * # write()는 views.py에 생성할 것임

# community/views.py : write() 함수 구현부. 사용자의 요청사항은 request 인자를 통해 전달된다.
def write(request):
    return render(request, 'write.html') # write.html로 보낸다.

# community/templates write.html을 저장할 디렉토리 생성함
# community/templates/write.html 생성함
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>write</title>
  </head>
  <body>
    hello django!
  </body>
</html>

# 실행결과를 확인하기 위해 서버를 실행
./manage.py runserver
http://127.0.0.1:8000/write/ 페이지 열기
hello django! 확인 할 수 있다.

# 사용자의 입력을 받는 Form 만들기
# community/forms.py를 생성
from django.forms import ModelForm
from community.models import *

class Form(ModelForm):
    class Meta:
        model = Article # Article 모델을 이용하여 form 만들기
        fields = ['name', 'title', 'contents', 'url', 'email'] # Model 중 사용할 field 나열

# form을 templates에 전달하기
# views.py
from community.forms import *

def write(request):
    form = Form() # community.forms.py에 있음
    return render(request, 'write.html', {'form':form}) # form을 전달하기 위해서, 변수명과 객체 전달

# write.html  <body>
  <body>
    <form action="" method="post">
      {{ form.as_p }} # p 태그로 form 사용
      <button type="submit" class="btn btn-primary">저장</button> # Submit 버튼
  </body>           

# 다시 http://127.0.0.1/write 실행하여 form 형태 확인

# 사용자가 입력한 내용을 데이터베이스에 저장
# community/views.html
def write(request):
    if request.method == 'POST':
        form = Form(request.POST)
        if form.is_valid():
            form.save()
    else:
        form = Form()

    return render(request, 'write.html', {'form':form})
```
