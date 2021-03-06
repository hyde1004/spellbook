### sqlite3 module
###### Reference
 - [파이썬을 이용한 시스템 트레이딩 (기초편)](https://wikidocs.net/1307)
 - [Introduction to SQLite in Python](http://www.pythoncentral.io/introduction-to-sqlite-in-python/)
 - [SQLite Python Tutorial](https://www.tutorialspoint.com/sqlite/sqlite_python.htm)

Reference를 봐도 충분할것 같다.
아래는 SQL 명령과 Python과의 연결부분을 분리하여 정리한다.

#### SQL 명령
``` sql
INSERT INTO kospi(Name text, ClosingPrice int);

INSERT INTO kospi VALUES('LG전자', 74500);
INSERT INTO kospi VALUES('네이버', 774000);
INSERT INTO kospi VALUES('다음', 169100);

SELECT * FROM kospi;
```

#### sqlite3
``` python
import sqlite3

# DB 파일에 연결
con = sqlite3.connect("kospi.db")

# cursor 객체 생성
cursor = con.cursor()

# SQL 명령 수행
cursor.execute("....")

# 작업한 내용을 DB에 반영
con.commit()

# 데이터 읽기
cursor.execute("*SELECT * FROM kospi;")
for row in cursor:
	print(row)

cursor.execute("*SELECT * FROM kospi;")
cursor.fetchone() # 하나 읽기

mydata = cursor.fetchall() # 전체 읽기
# DB 닫기
con.close()
```
