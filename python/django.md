#### Django

기본적 파일 구성은 다음과 같다.
 - admin.py : 관리자 페이지
 - settings.py : 디버그 모드, 앱추가, 데이터베이스 엔진 설정
 - manage.py : 실행파일

manage.py의 관리 명령
 - startapp : 앱 생성
 - runserver : 서버 실행
 - createsuperuser : 관리자 생성
 - makemigrations app : app의 모델 변경 사항 체크
 - migrate : 변경 사항을 DB에 반영


간단한 예제
``` python3
django-admin startproject tutorial
manage.py startapp community
```
