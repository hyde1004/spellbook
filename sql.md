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
