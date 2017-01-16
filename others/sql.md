여기서는 SQL을 사용하기 위한 기본 문법을 서술한다.

###### Reference
 - [w3school.com의 SQL Tutorial](http://www.w3schools.com/sql/default.asp) : SQL 기본 명령과 웹상에서 SQL 명령을 실행해 볼 수 있다.
 - [SQLite C Interface - Functions](https://www.sqlite.org/c3ref/funclist.html)
 - [tutorialspoint - SQLite](https://www.tutorialspoint.com/sqlite/index.htm)

#### 문법
SQL은 기본적으로 column 위주인것 같다.
항상 column을 명시해야 한다.

`SELECT <컬럼> FROM <TABLE> WHERE <조건>`

``` sql
SELECT * FROM Customers;
SELECT CustomerName, Address FROM Customers;

SELECT * FROM Customers WHERE country='Mexico'
SELECT CustomerName, Address FROM Customers FROM Customers WHERE country='Mexico';
```

#### Android TV Provider를 이용한 연습
``` sql
.open tv.db -- tv.db 열기

.tables  -- db안의 테이블 출력
/*  출력화면
android_metadata  channels          programs          watched_programs
*/
.schema channels -- schema 보이기
/* output
CREATE TABLE channels (
  _id INTEGER PRIMARY KEY AUTOINCREMENT,
  package_name TEXT NOT NULL,
  input_id TEXT NOT NULL,
  type TEXT NOT NULL DEFAULT 'TYPE_OTHER',
  service_type TEXT NOT NULL DEFAULT 'SERVICE_TYPE_AUDIO_VIDEO',
  original_network_id INTEGER NOT NULL DEFAULT 0,
  transport_stream_id INTEGER NOT NULL DEFAULT 0,
  service_id INTEGER NOT NULL DEFAULT 0,
  display_number TEXT,
  display_name TEXT,
  network_affiliation TEXT,
  description TEXT,
  video_format TEXT,
  browsable INTEGER NOT NULL DEFAULT 0,
  searchable INTEGER NOT NULL DEFAULT 1,
  selectable INTEGER,
  locked INTEGER NOT NULL DEFAULT 0,
  app_link_icon_uri TEXT,
  app_link_poster_art_uri TEXT,
  app_link_text TEXT,
  app_link_color INTEGER,
  app_link_intent_uri TEXT,
  internal_provider_data BLOB,
  internal_provider_flag1 INTEGER,
  internal_provider_flag2 INTEGER,
  internal_provider_flag3 INTEGER,
  internal_provider_flag4 INTEGER,
  logo BLOB,
  version_number INTEGER,
  channel_genre TEXT,cam_channel INTEGER,
  UNIQUE(_id,package_name));
*/
```
tv.db의 schema를 살펴보자. `_id`는 primary key이면서 자동 증가하는 것으로 보인다. 필드에 `NOT NULL`이라고 되어 있는 부분은 필수적으로 값이 필요하며, `DEFAULT`는 기본값으로 보인다.

``` sql
.dump channels # dump channel table records
/*
PRAGMA foreign_keys=OFF;
BEGIN TRANSACTION;
CREATE TABLE channels (_id INTEGER PRIMARY KEY AUTOINCREMENT,package_name TEXT NOT NULL,input_id TEXT NOT NULL,type TEXT NOT NULL DEFAULT 'TYPE_OTHER',service_type TEXT NOT NULL DEFAULT 'SERVICE_TYPE_AUDIO_VIDEO',original_network_id INTEGER NOT NULL DEFAULT 0,transport_stream_id INTEGER NOT NULL DEFAULT 0,service_id INTEGER NOT NULL DEFAULT 0,display_number TEXT,display_name TEXT,network_affiliation TEXT,description TEXT,video_format TEXT,browsable INTEGER NOT NULL DEFAULT 0,searchable INTEGER NOT NULL DEFAULT 1,selectable INTEGER,locked INTEGER NOT NULL DEFAULT 0,app_link_icon_uri TEXT,app_link_poster_art_uri TEXT,app_link_text TEXT,app_link_color INTEGER,app_link_intent_uri TEXT,internal_provider_data BLOB,internal_provider_flag1 INTEGER,internal_provider_flag2 INTEGER,internal_provider_flag3 INTEGER,internal_provider_flag4 INTEGER,logo BLOB,version_number INTEGER,channel_genre TEXT,cam_channel INTEGER,UNIQUE(_id,package_name));
INSERT INTO "channels" VALUES(2290,'com.lge.android.tvinput','com.lge.android.tvinput/.dtv.DTvInputService','TYPE_OTHER','dvb://dtv&7&4&98&98&',172,11,13046,'98','Airtel SD Home',NULL,NULL,NULL,1,1,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2&14&17&',0);
INSERT INTO "channels" VALUES(2291,'com.lge.android.tvinput','com.lge.android.tvinput/.dtv.DTvInputService','TYPE_OTHER','dvb://dtv&7&0&99&99&',172,1,7999,'99','Airtel Offers 1',NULL,NULL,NULL,1,1,1,0,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,'2&14&17&',0);
이하 생략
*/
```
`dump`는 테이블에 입력된 모든 명령을 보여주는 것인가?

``` sql
SELECT transport_stream_id, service_id, display_number FROM channels;
/*
11|13046|98
1|7999|99
11|12112|100
11|12173|101
5|1101|102
10|10125|103
11|1102|104
10|11127|105
3|1103|106
*/
```

채널 이름을 확인하고자 display_name 컬럼도 추가로 표시하였다.
``` sql
SELECT transport_stream_id, service_id, display_number, display_name FROM channels;
/*
11|13046|98|Airtel SD Home
1|7999|99|Airtel Offers 1
11|12112|100|Airtel HD Home
11|12173|101|Airtel Offers 2
5|1101|102|Star Plus
10|10125|103|Star Plus HD
11|1102|104|Zee TV
10|11127|105|Zee TV HD
3|1103|106|Sony Ent
10|12013|107|Sony HD
*/
```
결과 화면의 정보를 구분하기 위해 헤더 정보를 출력한다.
``` sql
.headers ON
SELECT transport_stream_id, service_id, display_number, display_name FROM channels;
/* 출력 화면
transport_stream_id|service_id|display_number|display_name
11|13046|98|Airtel SD Home
1|7999|99|Airtel Offers 1
11|12112|100|Airtel HD Home
11|12173|101|Airtel Offers 2

이하 생략
*/
```

컬럼 정보를 좀 더 쉽게 구분하기 위해 `.mode`를 사용한다.
``` sql
.mode column                                                                        
SELECT transport_stream_id, service_id, display_name, display_number FROM channels;
/* 출력 화면
transport_stream_id  service_id  display_name    display_number                             
-------------------  ----------  --------------  --------------                             
11                   13046       Airtel SD Home  98                                         
1                    7999        Airtel Offers   99                                         
11                   12112       Airtel HD Home  100                                        
11                   12173       Airtel Offers   101                                        
5                    1101        Star Plus       102                                        
10                   10125       Star Plus HD    103                                        
11                   1102        Zee TV          104   

이하 생략
*/                                     
```

데이터가 너무 많으므로, 10개로 제한하여 출력하자.
``` sql
SELECT transport_stream_id, service_id, display_name, display_number FROM channels LIMIT 10;
/*  출력 화면
transport_  service_id            display_na  display_number
----------  --------------------  ----------  --------------
11          13046                 Airtel SD   98
1           7999                  Airtel Off  99
11          12112                 Airtel HD   100
11          12173                 Airtel Off  101
5           1101                  Star Plus   102
10          10125                 Star Plus   103
11          1102                  Zee TV      104
10          11127                 Zee TV HD   105
3           1103                  Sony Ent    106
10          12013                 Sony HD     107
*/
```

transport_stream_id 값으로 오름 차순 정렬하여 출력해보자.
``` sql
SELECT transport_stream_id, service_id, display_number, display_name FROM channels ORDER BY transport_stream_id ASC;
/*  출력 화면
transport_  service_id            display_nu  display_name
----------  --------------------  ----------  ---------------
1           7999                  99          Airtel Offers 1
1           2124                  114         HomeShop 18
1           12072                 115         Shop CJ
1           12212                 126         The EPIC Channe
1           12192                 128         Naaptol Blue
1           1107                  131         Enter 10
1           12207                 133         ID
1           12108                 138         DD India

이하 생략
*/
```

transport_stream_id 값만 출력해보자
``` sql
SELECT transport_stream_id FROM channels;
/*  출력화면
transport_stream_id
--------------------
11
1
11
11
5
10
11
10
3
10
2
8
11
10
11
6

이하 생략
*/
```

중복값이 제거된 transport_stream_id을 출력해보자.
``` sql
SELECT DISTINCT transport_stream_id FROM channels;
/* 출력 화면
transport_stream_id
--------------------
11
1
5
10
3
2
8
6
7
9
12
4
*/

SELECT DISTINCT transport_stream_id FROM channels ORDER BY transport_stream_id; -- 오름차순 정렬
/* 출력 화면
transport_stream_id
--------------------
1
2
3
4
5
6
7
8
9
10
11
12
*/

```

##### better idea
 - LCN기준이 아니라 triplet id로 하자
 - 기본적으로는 triplet id를 이용하여 channel identity를 구분하는게 맞으나 Airtel 경우는 같은 triplet id에도 2개의 채널이CAM/FTA) 존재할 수 있다. 따라서 Airtel 경우에는 triplet + CAM/FTA 로 구분해야 한다.
