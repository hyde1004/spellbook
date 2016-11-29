#### logging

###### Reference
 - [Python Logging 파이썬 로깅 모듈](http://ourcstory.tistory.com/97)
 - [파이썬 로깅모듈에 대해서](http://gyus.me/?p=418)

##### 로그 레벨
로그 레벨은 다음과 같이 정의되어 있으며, 기본 로그 레벨은 WARNING으로 설정되어 있다. 로그 레벨을 변경하기 위해서 `logging.basicConfig(level=logging.DEBUG)`을 사용한다.
 - DEBUG
 - INFO
 - WARNING
 - ERROR
 - CRITICAL

##### 예제
```
import logging

logging.basicConfig(level=logging.DEBUG)

logging.debug("debug")
logging.info("info")
logging.warning("warning")
logging.error("error")
logging.critical("critical")
```

##### 기타
로그를 파일로 저장, 날짜 정보, 파일 정보 등도 출력가능하다.
