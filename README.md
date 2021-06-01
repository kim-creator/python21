mysql> use mysql
mysql> show  tables;
mysql> create  database acedb;
mysql> show  databases;

## root password 지정 

mysql> alter  user  'root'@'localhost' identified with mysql_native_password by 'jj';
mysql> flush privileges;

## mysql 계정(account) 만들기 

계정(account)
id : ace
pw : 1234
사용DB : acedb



mysql> create  user ace@'%' identified by '1234';
mysql> grant all privileges on acedb.*  to  ace@'%' with grant option;
mysql> flush  privileges;



▶ 다른 터미널 : putty 새로 열기 

j@j:~$ mysql  -u  ace  -p1234

mysql> select user();
mysql> show  databases;
mysql> use  acedb;
Database changed
mysql> use mysql     ## 에러나면 정상 
ERROR 1044 (42000): Access denied for user 'ace'@'%' to database 'mysql'
mysql>




*************************************

## linux 계정(account) 만들기 

$sudo useradd -m  -s /bin/bash -d /home/aii  aii
$sudo passwd  bii
$sudo userdel  aii
▶ 리눅스 처음 접속 후 터미널 실행 

$date
$cal
$whoami
$ping  -c  8.8.8.8


▶ 패키지 설치 
$sudo  apt  list  --installed | nl          ## 설치된 패키지 목록 
$sudo  apt  list  --installed | grep  mysql ## mysql 설치 확인 
$sudo  apt  list  --installed | grep  ssh   ## ssh 설치 확인 
$sudo  apt  -y  install  openssh-server     ## 설치 

$sudo ps -ef | grep mysql          ## 실행 확인 
$sudo systemctl start mysql        ## 실행 
$sudo systemctl restart mysql      ## 재실행 
$sudo ufw allow mysql              ## 방화벽 열기
$sudo systemctl enable mysql       ## 부팅시 자동으로 실행 

$sudo apt -y  install  apache2
$sudo apt -y install  python3-pip

$pip freeze
$pip  install  pandas 
$pip  install  numpy
$pip  install  matplotlib
$pip  install  seaborn
$pip  install  pymysql



## linux 계정(account) 만들기 

$sudo useradd -m  -s /bin/bash -d /home/blue  blue
$sudo passwd  blue

##  확인 
$tail  -3  /etc/passwd 
$ls  /home
$sudo userdel  blue  // 삭제 



## root password 지정 

$sudo  mysql

mysql> alter  user  'root'@'localhost' identified with mysql_native_password by 'jj';
mysql> flush privileges;

## mysql 계정(account) 만들기 

계정(account)
id : myblue
pw : 11
사용DB : bluedb


mysql> create  database  bluedb;
mysql> create  user myblue@'%' identified by '11';
mysql> grant all privileges on bluedb.*  to  myblue@'%' with grant option;
mysql> flush  privileges;

**** linux 접속 *******
blue로 로그인

$ mysql -u myblue -p


mysql> select user();
+------------------+
| user()           |
+------------------+
| myblue@localhost |
+------------------+
1 row in set (0.00 sec)

mysql> use mysql;           ## 에러 나는 게 정상 - 권한 없음 
ERROR 1044 (42000): Access denied for user 'myblue'@'%' to database 'mysql'
mysql> use bluedb;
Database changed

** 성공 ** 

mysql> create table lunch( menu  char(20), price  int);
Query OK, 0 rows affected (0.02 sec)

mysql> desc  lunch;
+-------+----------+------+-----+---------+-------+
| Field | Type     | Null | Key | Default | Extra |
+-------+----------+------+-----+---------+-------+
| menu  | char(20) | YES  |     | NULL    |       |
| price | int      | YES  |     | NULL    |       |
+-------+----------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql> insert into lunch values('짜장면', 6000);
Query OK, 1 row affected (0.01 sec)

mysql> insert into lunch values('비빔밤', 30000);
Query OK, 1 row affected (0.02 sec)

mysql> insert into lunch values('볶끔밥', 240000);
Query OK, 1 row affected (0.02 sec)

mysql> select * from lunch;
+-----------+--------+
| menu      | price  |
+-----------+--------+
| 짜장면    |   6000 |
| 비빔밤    |  30000 |
| 볶끔밥    | 240000 |
+-----------+--------+
3 rows in set (0.00 sec)

mysql> update  lunch  set  menu='볶음밥', price=7000
    -> where  menu='볶끔밥';
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from lunch;
+-----------+-------+
| menu      | price |
+-----------+-------+
| 짜장면    |  6000 |
| 비빔밤    | 30000 |
| 볶음밥    |  7000 |
+-----------+-------+
3 rows in set (0.00 sec)

mysql> delete from lunch
    -> where menu = '비빔밥';
Query OK, 0 rows affected (0.00 sec)

mysql> select * from lunch;
+-----------+-------+
| menu      | price |
+-----------+-------+
| 짜장면    |  6000 |
| 비빔밤    | 30000 |
| 볶음밥    |  7000 |
+-----------+-------+
3 rows in set (0.00 sec)

mysql> delete from lunch  where menu = '비빔밤';
Query OK, 1 row affected (0.00 sec)

mysql> select * from lunch;
+-----------+-------+
| menu      | price |
+-----------+-------+
| 짜장면    |  6000 |
| 볶음밥    |  7000 |
+-----------+-------+
2 rows in set (0.00 sec)

mysql> select menu as'메뉴', price as'가격' from lunch;
+-----------+--------+
| 메뉴      | 가격   |
+-----------+--------+
| 짜장면    |   6000 |
| 볶음밥    |   7000 |
+-----------+--------+
2 rows in set (0.00 sec)
import pymysql as my 

con = my.connect(host='127.0.0.1', user='myblue', password='11', db='bluedb')
c = con.cursor()

c.execute('insert into lunch values("짜장면", 5000)')
c.execute('insert into lunch values("비빔밥", 8000)')
c.execute('insert into lunch values("돈까스", 7000)')

c.execute('select * from lunch')

res = c.fetchall()

print(' 메뉴  가격 ')
print('************')

for i in res:
    print(i[0], i[1])    
print('************')

con.commit()
c.close()

con.close()
<!DOCTYPE html>

<html>

<head>
    <meta charset="utf-8"> 
 	<title>나의 타이틀</title>
</head>

<body bocolor=green  text=white>

  <h1>짱구네 집</h1>
  <p>단락. paragraph</p>

  <div>
  	<a href='http://func.kr'>우리카페</a>
  </div>

  <div>
    <a href='http://www.naver.com'>네이버</a>
  </div>

 <div>
    <a href='http://w3schools.com'>공부하러가자</a>
</div>

<table style='width:50%' border=1 align=center>
  <tr align=center>
    <th>이름</th>
    <th>소속</th> 
    <th>연봉</th>
  </tr>
  
  <tr align=center>
    <td>류현진</td>
    <td>토론토</td>
    <td>1500</td>
  </tr>
  
  <tr align=center>
    <td>김하성</td>
    <td>센디에이고</td>
    <td>700</td>
  </tr>
  
  <tr align=center>
    <td>양현종</td>
    <td>텍사스</td>
    <td>800</td>
  </tr>
  
</table>
    
  
  <div id='id1'>
  	   여기는 서울 
       <p> 단락 </p>
  </div>
  
</body>

</html>
from bs4 import BeautifulSoup
import urllib.request
with open('my.html') as f:
    s = BeautifulSoup(f, 'html.parser')
s
import requests
from bs4 import BeautifulSoup
 
data = requests.get('https://movie.naver.com/movie/sdb/rank/rmovie.nhn')
soup = BeautifulSoup(data.text, 'html.parser')

movies = soup.select('#old_content > table > tbody > tr')

for i in movies:   
    a = i.select_one('td.title > div > a')
    if a is not None:        
        print(a.text)
​import os
import re
import sys
import json
import pandas as pd
import urllib.request

client_id = "uCGC5YEDwKAVTk0ytAzE"
client_secret = "g_z3Va8Oy6"
query = urllib.parse.quote(input("검색어를 입력 하세요 : "))

cols = ['Title', 'Link', 'Description']
df = pd.DataFrame(columns=cols)

count = 0

for i in range(1, 100, 10):
url = "https://openapi.naver.com/v1/search/webkr?query=" + query \
+ '&display=' + str(10) + '&start=' + str(i)

request = urllib.request.Request(url)
request.add_header("X-Naver-Client-Id",client_id)
request.add_header("X-Naver-Client-Secret",client_secret)
response = urllib.request.urlopen(request)
rescode = response.getcode()

if(rescode==200):
response_body = response.read()
response_dict = json.loads(response_body.decode('utf-8'))

items = response_dict['items']

for j in range(0, len(items)):
p = re.compile('<.*?>')
title = re.sub(p, '', items[j]['title'])
link = items[j]['link']
description = re.sub(p, '', items[j]['description'])
df.loc[count] = [title, link, description]
print(count, end = ' ')
count += 1

else:
print("Error Code:" + rescode)
import os
import re
import sys
import json
import pandas as pd
import urllib.request

client_id = "uCGC5YEDwKAVTk0ytAzE"
client_secret = "g_z3Va8Oy6"
query = urllib.parse.quote(input("검색어를 입력 하세요 : "))

cols = ['Title', 'Link', 'Description', 'Blgger Name', 'Blogger Link']
blog_df = pd.DataFrame(columns=cols)

count = 0

for i in range(1, 100, 10):
url = "https://openapi.naver.com/v1/search/blog?query=" + query \
+ '&display=' + str(10) + '&start=' + str(i) + '&sort=' + 'sim'

request = urllib.request.Request(url)
request.add_header("X-Naver-Client-Id",client_id)
request.add_header("X-Naver-Client-Secret",client_secret)
response = urllib.request.urlopen(request)
rescode = response.getcode()

if(rescode==200):
response_body = response.read()
response_dict = json.loads(response_body.decode('utf-8'))

items = response_dict['items']

for j in range(0, len(items)):
p = re.compile('<.*?>')
title = re.sub(p, '', items[j]['title'])
link = items[j]['link']
description = re.sub(p, '', items[j]['description'])
blogger_name = items[j]['bloggername']
blogger_link = items[j]['bloggerlink']

blog_df.loc[count] = [title, link, description, blogger_name, blogger_link]
print(count, end = ' ')
count += 1

else:
print("Error Code:" + rescode)

blog_df
