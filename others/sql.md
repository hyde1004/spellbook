여기서는 SQL을 사용하기 위한 기본 문법을 서술한다.

###### Reference
 - [w3school.com의 SQL Tutorial](http://www.w3schools.com/sql/default.asp) : SQL 기본 명령과 웹상에서 SQL 명령을 실행해 볼 수 있다.
 - [SQLite C Interface - Functions](https://www.sqlite.org/c3ref/funclist.html)

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
``` bash
sqlite3 tv.db # open
```
``` sql
.schema channels # schema 보이기
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

##### better idea
 - LCN기준이 아니라 triplet id로 하자
 - 기본적으로는 triplet id를 이용하여 channel identity를 구분하는게 맞으나 Airtel 경우는 같은 triplet id에도 2개의 채널이CAM/FTA) 존재할 수 있다. 따라서 Airtel 경우에는 triplet + CAM/FTA 로 구분해야 한다.
