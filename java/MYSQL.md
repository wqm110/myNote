

# MYSQL

尚硅谷 周杨网盘课笔记

## 简介

## 初级

```sql
SELECT (min_salary+max_salary)/2 as salary from jobs ORDER BY salary LIMIT 1; -- 限制行数
 SELECT (min_salary+max_salary)/2 as salary from jobs ORDER BY salary LIMIT 1 OFFSET 5;--排名第五
```

```sql
SELECT * FROM jobs ORDER BY 3,4;  -- 按列位置排序
SELECT * FROM employees ORDER BY job_id,salary;--第一个相同第二个才排序
-- 默认升序
SELECT * FROM employees ORDER BY job_id DESC,salary DESC;
```

```sql
SELECT * FROM employees WHERE salary BETWEEN 3000 AND 5000 ORDER BY job_id DESC,salary DESC;
SELECT * FROM departments WHERE manager_id is NULL;
-- 优先处理 AND
-- IN 比 OR 效率高 ，in 可以包含子查询
-- '%' 不匹配 NULL
-- - 匹配单个
-- [^JM] 开头部位J/M 通配符尽量后放
```

```sql
/* 文本 */ 关键字不区分大小写
SELECT CONCAT(department_name,'-',department_id) AS d_bi  FROM departments ORDER BY department_id;
-- TRIM() LTRIM 
-- SUBTR() /SUBSTRING() LEFT("hello wrold",5)

-- UPPER() LOWER()
-- SOUNDEX()
SELECT department_id,department_name from departments where SOUNDEX(department_name)=SOUNDEX('菜务'); 
```

```sql
/*时间 */
-- DATEPART
SELECT DATE_FORMAT (hiredate,"yyyy") from employees;
 SELECT YEAR(hiredate) from employees;
```

```sql
/*数值*/
-- ABS()
--COS()
--EXP() 指数值
--PI()
--SQRT
--TAN()
```

```sql
/*聚集函数*/
-- AVG（列名） 单列
--COUNT()  count（*） 计算表中的所有行 null 空 非空 全部计算 
						--count（列） 不计算 NULL
--MAX（）可计算文本返回排序后的最后一行
--MIN()

 SELECT job_id,min_salary,(min_salary+max_salary)/2 as mx FROM jobs   GROUP BY  job_id ORDER BY mx DESC;
 
 SELECT job_id,min_salary,max_salary,(min_salary+max_salary)/2 as mx FROM jobs   GROUP BY  job_id ORDER BY mx DESC;
 -- group 列序
 SELECT job_id,min_salary,max_salary,(min_salary+max_salary)/2 as mx FROM jobs   GROUP BY  1 ORDER BY mx DESC;
 
 -- group by  + 条件==》 having 

```

```sql
SELECT j.job_title,COUNT(j.job_title) as members from employees  
			as e JOIN jobs as j ON e.job_id = j.job_id   
			GROUP BY j.job_title  ORDER BY members desc
;

```

 SA_REP	Sales Representative	30
ST_CLERK	Stock Clerk	20
SH_CLERK	Shipping Clerk	20
ST_MAN	Stock Manager	5

```sql
-- union  --去重
-- union all 显示全部匹配行
```

```sql
-- create table xx as select xxx;
select * into tablexx from custroms;
```

```sql
TRUNCATE TABLE tablename; 清空 不记录操作
```

```sql
create INDEX indx_tname_colname1_colname2 ON tablename (col1,col2)
```





## 高级



### 架构介绍

![image-20210102013802832](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8pttibt7j30jg0ask27.jpg)

### 

### 

![image-20210102021444432](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8qvy4ec5j30ey0b0dge.jpg)

![image-20210102021418469](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8qvhys16j30ub079tag.jpg)

```sql
-- CREATE TABLE tbl_dept (
-- id int not null auto_increment,
-- deptName VARCHAR( 30) DEFAULT null,
-- locAdd VARCHAR (40) DEFAULT NULL,
-- PRIMARY KEY (id) 
-- ) ENGINE=INNODB,auto_increment=1 DEFAULT CHARSET =UTF8;
-- 
-- CREATE TABLE tbl_emp(
-- id INT NOT NULL AUTO_INCREMENT,
-- name VARCHAR(40) DEFAULT NULL,
-- dept_id int(11) DEFAULT NULL,
-- PRIMARY KEY (id)
-- #KEY fk_dept_id(deptid)
-- )
-- ENGINE = INNODB AUTO_INCREMENT=1 ,DEFAULT CHARSET=UTF8;
-- 
-- INSERT INTO tbl_dept(deptName,locAdd)VALUES("RD",11);
-- INSERT INTO tbl_dept(deptName,locAdd)VALUES("HR",12);
-- INSERT INTO tbl_dept(deptName,locAdd)VALUES("MK",13);
-- INSERT INTO tbl_dept(deptName,locAdd)VALUES("MIS",14);
-- INSERT INTO tbl_dept(deptName,locAdd)VALUES("FD",15);

-- INSERT into tbl_emp(name,dept_id)VALUES("z3",1);
-- INSERT into tbl_emp(name,dept_id)VALUES("z4",1);
-- INSERT into tbl_emp(name,dept_id)VALUES("z5",1);
-- 
-- INSERT into tbl_emp(name,dept_id)VALUES("w5",2);
-- INSERT into tbl_emp(name,dept_id)VALUES("w6",2);

-- INSERT INTO tbl_emp(name,dept_id)VALUES("s7",3);
-- INSERT INTO tbl_emp(name,dept_id)VALUES("s8",4);
-- INSERT INTO tbl_emp(name,dept_id)VALUES("s9",51);
```



inner join

![image-20210102022002553](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8r1gq36kj308x09vabr.jpg)

```sql
SELECT * from tbl_dept as d INNER JOIN tbl_emp as e on  d.id = e.dept_id;

```



left join

![image-20210102022030874](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8r1yd67qj308k08egnf.jpg)

```sql
# LEFT JOIN
SELECT * FROM tbl_dept as d LEFT JOIN tbl_emp as e on d.id = e.dept_id;
```



Right join

![image-20210102022048280](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8r29937oj308f08mtai.jpg)

```sql
# RIGHT JOIN
SELECT * FROM tbl_dept as d RIGHT JOIN tbl_emp as e on d.id = e.dept_id;
```



left join  b is null

![image-20210102022250875](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8r4dpt5wj307w0970uq.jpg) 

```sql
#  RIGHT NULL
SELECT * FROM tbl_dept as d LEFT JOIN tbl_emp as e on d.id = e.dept_id WHERE e.dept_id is null;
```



right join a is null

![image-20210102022335602](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8r55s9txj307s08ywgg.jpg)

```sql
SELECT * FROM tbl_dept as d RIGHT JOIN tbl_emp as e on d.id = e.dept_id WHERE d.id is null;
```



outer join 圈里阿杰

![image-20210102022803730](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8r9tcqxxj30d4071go6.jpg)

Mysql 不支持full outer join

SELECT * from tbl_dept as d FULL JOIN tbl_emp as e on  d.id = e.dept_id;

```sql
# LEFT JOIN
SELECT * FROM tbl_dept as d LEFT JOIN tbl_emp as e on d.id = e.dept_id   
UNION 
SELECT * FROM tbl_dept as d RIGHT JOIN tbl_emp as e on d.id = e.dept_id;
```



![image-20210102022912835](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8rb0ji94j30ee06xjue.jpg)

```sql
SELECT * FROM tbl_dept as d RIGHT  JOIN tbl_emp as e on d.id = e.dept_id WHERE d.id is null  
UNION 
SELECT * FROM tbl_dept as d LEFT  JOIN tbl_emp as e on d.id = e.dept_id where e.dept_id is null;

```

#### 索引优化分析

![image-20210102055121992](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8x5cdk7ij3153032q4n.jpg)

![image-20210102055622312](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8xak47t9j30p501pgmc.jpg)

![image-20210102060206285](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8xgj5sy1j31am0iw14q.jpg)

![image-20210102061658379](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8xvznvm0j31dz04yae0.jpg)



##### 索引建立的场景



##### 优势

![image-20210102061936704](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8xyqc0upj30xo047408.jpg)

劣势

![image-20210102062813373](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8y7p4kykj31cb06bwjh.jpg)

![image-20210102063405598](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8ydt4912j313d0arq5x.jpg)

![image-20210102063707653](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8ygyiq1uj314w0bmjve.jpg)

![image-20210102063904174](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8yizfy4vj30jq07hgmn.jpg)



检索原理

![image-20210102064230435](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8ymkctohj31360gsgz5.jpg)

![image-20210102064546473](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8ypyh726j316o08e7ab.jpg)

![image-20210102064601744](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8yq8654zj31ar05wtes.jpg)

![image-20210102065056881](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8yvcdfurj31d60e9agd.jpg)

![image-20210102065332211](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8yy1cf5kj31fn07raez.jpg)

##### Mysql 优化器

![image-20210102070017831](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8z52cqkej309k01wdfv.jpg)

![image-20210102070100552](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8z5t89ovj31a70d4tnb.jpg)

![image-20210102070223502](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8z7962efj31ay04wwhs.jpg)

##### EXPLAIN

![image-20210102070333149](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8z8gqazyj30hu0a9gmv.jpg)



![image-20210102070356210](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8z8v4afxj31df05m0vl.jpg)

![image-20210102072851044](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8zysdvczj30p40dgju1.jpg)

```
EXPLAIN SELECT * from sswgvideo_

```

![image-20210102070829996](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8zdm3d1hj319803amxk.jpg)

![image-20210102071729066](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8zmy97ovj30eg02wq3f.jpg)



###### id

![image-20210102071526275](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8zktyfe8j310j06dq5a.jpg)

![image-20210102072423716](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8zu59s33j30w90bxad8.jpg)

![image-20210102072725494](https://tva1.sinaimg.cn/large/0081Kckwgy1gm8zxajobsj30zk0ewq72.jpg)

###### selecttype

![image-20210102073029716](https://tva1.sinaimg.cn/large/0081Kckwgy1gm900hj836j30jw0cijtp.jpg)

![image-20210102073526309](https://tva1.sinaimg.cn/large/0081Kckwgy1gm905n72pkj319g0i4tep.jpg)

###### table

###### type

![image-20210102074100571](https://tva1.sinaimg.cn/large/0081Kckwgy1gm90bfid58j30xr08jjty.jpg)

![image-20210102074253288](https://tva1.sinaimg.cn/large/0081Kckwgy1gm90de72ocj31a50e278p.jpg)

![image-20210102074352370](https://tva1.sinaimg.cn/large/0081Kckwgy1gm90ef2b9bj31cv0g8aiw.jpg)

![image-20210102074927468](https://tva1.sinaimg.cn/large/0081Kckwgy1gm90k7y1wjj30l807kwfi.jpg)

![image-20210102075003220](https://tva1.sinaimg.cn/large/0081Kckwgy1gm90kuc8gej311901t74z.jpg)

range 范围查找



###### ref

![image-20210102075326274](https://tva1.sinaimg.cn/large/0081Kckwgy1gm90ok67pfj30zu07ajsm.jpg)

![image-20210102075249409](https://tva1.sinaimg.cn/large/0081Kckwgy1gm90nq7fkwj310202djs5.jpg)

###### Ref 

使用了test 库的 t1 表的 id 索引

###### rows

一共查询了 多少行

![image-20210102080440576](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91026tivj30yp0duwhv.jpg)

###### extra

![image-20210102080638068](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91236f2fj30gp01kq35.jpg)

![image-20210102080815299](https://tva1.sinaimg.cn/large/0081Kckwgy1gm913s498ij31ey04rmz2.jpg)

1.useing filesort 全文扫描

![image-20210102081816657](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91e7rqclj30nh0kbad0.jpg)

2.useing temporay  ![image-20210102082001627](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91g12wwvj31fj02hdh2.jpg)

![image-20210102082432755](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91kq9zxqj30qd0k6mzy.jpg)

2.using index

![image-20210102082741102](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91nzqxz0j3161050417.jpg)

 ![image-20210102082938472](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91q1am8vj30x40imn23.jpg)

3.覆盖索引

查的和和建立的索引一致

![image-20210102083147277](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91s9ra0ej31aa0a9qbg.jpg)

![image-20210102083200188](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91shknodj30up052jtm.jpg)

4 using where

5.using joinbuffer

6 。impossible where  where 条件 但终不能满足

![image-20210102083403326](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91umebrqj314u04mgnf.jpg)

8 。 distinct 找到第一个就收工

![image-20210102083841519](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91zg5xanj30ys0b8gnv.jpg)

![image-20210102083911176](https://tva1.sinaimg.cn/large/0081Kckwgy1gm91zyv33uj31aa0arwot.jpg)

索引优化

```sql
create table if not EXISTS article(
id int(10) UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
author_id int(10) UNSIGNED NOT NULL,
category_id int(10) UNSIGNED NOT NULL,
views int(10) UNSIGNED NOT NULL,
comments int(10) UNSIGNED NOT NULL,
title VARBINARY(255) NOT NULL,
content TINYTEXT NOT NULL
)
ENGINE=INNODB ;

INSERT INTO article (author_id,category_id,views,comments,title,content)values
(1,1,1,1,"1","1"),
(2,2,2,2,"2","2"),
(1,1,3,3,"3","3");
```

```sql
SELECT id,author_id from article where comments >1 ORDER BY views DESC LIMIT 1
```

```sql
EXPLAIN SELECT id,author_id from article where comments >1 ORDER BY views DESC LIMIT 1;
```

![image-20210102090019828](https://tva1.sinaimg.cn/large/0081Kckwgy1gm92lyj75qj31dw03sgm3.jpg)

![image-20210102090242868](https://tva1.sinaimg.cn/large/0081Kckwgy1gm92og8idzj316504l0w4.jpg)

![image-20210102090300683](https://tva1.sinaimg.cn/large/0081Kckwgy1gm92or7aoyj316w0c8aeg.jpg)

范围导致索引失效

![image-20210102091338301](https://tva1.sinaimg.cn/large/0081Kckwgy1gm92zteeutj316g0g37dv.jpg)

![image-20210102091456721](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9315zit2j30rt07kacl.jpg)

左连接 加右表

```sql
create table if not EXISTS class(
id int(10) UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
card int(10) UNSIGNED NOT NULL
)
create TABLE IF NOT EXISTS book(
bookid int(10) UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
card int(10) UNSIGNED NOT NULL
)
create TABLE IF NOT EXISTS phone(
phoneid int(10) UNSIGNED NOT NULL PRIMARY KEY AUTO_INCREMENT,
card int(10) UNSIGNED NOT NULL
)

INSERT INTO phone(card)VALUES(FLOOR(1+RAND()*20));

INSERT INTO class(card)VALUES(FLOOR(1+RAND()*20));
 
INSERT INTO book(card)VALUES(FLOOR(1+RAND()*20));

SELECT * from class LEFT JOIN book on book.card = class.card WHERE book.card = class.card;
EXPLAIN SELECT * from class LEFT JOIN book on book.card = class.card WHERE book.card = class.card;

show INDEX from book;

create INDEX ind_book on book(card);
EXPLAIN SELECT * from class RIGHT JOIN book on book.card = class.card WHERE book.card = class.card;
```

![image-20210102095212883](https://tva1.sinaimg.cn/large/0081Kckwgy1gm943y56svj30wt09kwfa.jpg)

![image-20210102095235791](https://tva1.sinaimg.cn/large/0081Kckwgy1gm944cmdbrj30ns028t8q.jpg)

 ![image-20210102095448756](https://tva1.sinaimg.cn/large/0081Kckwgy1gm946nl093j30qb089js7.jpg)



##### 索引失效

![image-20210102095938319](https://tva1.sinaimg.cn/large/0081Kckwgy1gm94cos559j30yc0cswgi.jpg)

###### 最佳左前缀法则

name age pox   

![image-20210102100748491](https://tva1.sinaimg.cn/large/0081Kckwgy1gm94k61hyij30oj00z74c.jpg)

![image-20210102102618797](https://tva1.sinaimg.cn/large/0081Kckwgy1gm953fdwafj30x60f6q4e.jpg)



![image-20210102102751835](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9551jglgj30s10b6js9.jpg)

![image-20210102103018118](https://tva1.sinaimg.cn/large/0081Kckwgy1gm957kuaiyj30oj08dgm2.jpg)

 

![image-20210102103301150](https://tva1.sinaimg.cn/large/0081Kckwgy1gm95aehdi6j30x00fgmz5.jpg)





![image-20210102112408199](https://tva1.sinaimg.cn/large/0081Kckwgy1gm96rlc8caj30mk076wf4.jpg)

### 查询截取分析



![image-20210102113356174](https://tva1.sinaimg.cn/large/0081Kckwgy1gm971shqgaj30ns0dlwfy.jpg)



![image-20210102114221794](https://tva1.sinaimg.cn/large/0081Kckwgy1gm97ak2cfwj30mc0eygp9.jpg)



![image-20210102114454128](https://tva1.sinaimg.cn/large/0081Kckwgy1gm97d775gaj31a50avn1l.jpg)

![image-20210102120732504](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9825b01aj31a10iaq94.jpg)



![image-20210102121404528](https://tva1.sinaimg.cn/large/0081Kckwgy1gm987k1igwj30oa0hx7em.jpg)

日志

![image-20210102121701562](https://tva1.sinaimg.cn/large/0081Kckwgy1gm98amn4k3j31c50hk479.jpg)

![image-20210102121713254](https://tva1.sinaimg.cn/large/0081Kckwgy1gm98attsagj31bz069n11.jpg)

![image-20210102121746011](https://tva1.sinaimg.cn/large/0081Kckwgy1gm98begr02j31970jfdk9.jpg)

```sql
SHOW VARIABLES like "%slow%"
```

![image-20210102122002568](https://tva1.sinaimg.cn/large/0081Kckwgy1gm98dro06hj30me084t9g.jpg)



![image-20210102121920713](https://tva1.sinaimg.cn/large/0081Kckwgy1gm98d4qc3oj30za0lewjm.jpg)

![image-20210102122300567](https://tva1.sinaimg.cn/large/0081Kckwgy1gm98gusk5rj31390kqgsp.jpg)

```
admin@MacBook-Pro:~|master⚡ ⇒  mysqldumpslow  --help
Usage: mysqldumpslow [ OPTS... ] [ LOGS... ]

Parse and summarize the MySQL slow query log. Options are

  --verbose    verbose
  --debug      debug
  --help       write this text to standard output

  -v           verbose
  -d           debug
  -s ORDER     what to sort by (al, at, ar, c, l, r, t), 'at' is default
                al: average lock time
                ar: average rows sent
                at: average query time
                 c: count
                 l: lock time
                 r: rows sent
                 t: query time
  -r           reverse the sort order (largest last instead of first)
  -t NUM       just show the top n queries
  -a           don't abstract all numbers to N and strings to 'S'
  -n NUM       abstract numbers with at least n digits within names
  -g PATTERN   grep: only consider stmts that include this string
  -h HOSTNAME  hostname of db server for *-slow.log filename (can be wildcard),
               default is '*', i.e. match all
  -i NAME      name of server instance (if using mysql.server startup script)
  -l           don't subtract lock time from total time

```

![image-20210102123453987](https://tva1.sinaimg.cn/large/0081Kckwgy1gm98t8827tj30q40ildik.jpg)



创建函数

```sql
show VARIABLES like '%log_bin%'
set GLOBAL log_bin_trust_function_creators=ON
```

```sql
CREATE DEFINER=`java`@`%` FUNCTION `getRandomStr`(n int) RETURNS varchar(255) CHARSET utf8
BEGIN
# 产生随机字符串
   DECLARE chars_str VARCHAR(100) DEFAULT 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
	 DECLARE return_str VARCHAR(255) DEFAULT '';
	 DECLARE i INT DEFAULT 0;
	 WHILE i<n DO
			  set return_str= CONCAT(return_str,SUBSTRING(chars_str,FLOOR(1+RAND()*52),1));
				set i=i+1; 
END WHILE 
	return return_str; 
END
```



```sql
CREATE DEFINER=`java`@`%` FUNCTION `getRandomInt`() RETURNS int
BEGIN
  # 随机产生部门编号
	DECLARE i INT DEFAULT 0;
	set i = FLOOR(RAND()*10+100); 
RETURN i;
END
```

```
 show profiles;
show profile  cpu,block io for QUERY 52
```



![image-20210102135427586](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9b3zy7vwj30ym0gc76o.jpg)

![image-20210102135358691](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9b3ia9p2j30x00digp6.jpg)

全局日志

![image-20210102140053376](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9bapd7kgj313f0jvq7d.jpg)

### 缓存

my.cnf加入以下配置，重启Mysql开启查询缓存

```sql
query_cache_type=1  
query_cache_size=600000
```

Mysql执行以下命令也可以开启查询缓存

```sql
set global  query_cache_type=1;  
set global  query_cache_size=600000;
```

如上，**开启查询缓存后在同样的查询条件以及数据情况下，会直接在缓存中返回结果**。这里的查询条件包括查询本身、当前要查询的数据库、客户端协议版本号等一些可能影响结果的信息。因此任何两个查询在任何字符上的不同都会导致缓存不命中。此外，如果查询中包含任何用户自定义函数、存储函数、用户变量、临时表、Mysql库中的系统表，其查询结果也不会被缓存。

缓存建立之后，Mysql的查询缓存系统会跟踪查询中涉及的每张表，如果这些表（数据或结构）发生变化，那么和这张表相关的所有缓存数据都将失效。

**缓存虽然能够提升数据库的查询性能，但是缓存同时也带来了额外的开销，每次查询后都要做一次缓存操作，失效后还要销毁。** 因此，开启缓存查询要谨慎，尤其对于写密集的应用来说更是如此。如果开启，要注意合理控制缓存空间大小，一般来说其大小设置为几十MB比较合适。此外，**还可以通过sql_cache和sql_no_cache来控制某个查询语句是否需要缓存：**

```bash
select sql_no_cache count(*) from usr;
```

### 锁机制

- **InnoDB存储引擎的锁的算法有三种：**
- Record lock：单个行记录上的锁
- Gap lock：间隙锁，锁定一个范围，不包括记录本身
- Next-key lock：record+gap 锁定一个范围，包含记录本身

![image-20210102140805137](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9bi6jcgwj31fu03wgo1.jpg)

![image-20210102141004911](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9bk99htoj30jy0azabm.jpg)

表锁



![image-20210102141029984](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9bkp5gpkj319n02y75g.jpg)

```sql
Show open  tables;  查看表情况
```

```sql
lock table mylock read,book write; 手动上锁
unlock tables;
```

![image-20210102142722858](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9c29g03lj313q0kkjvt.jpg)

![image-20210102142811008](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9c33ndmmj316b07h40y.jpg)

![image-20210102142818234](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9c37rnkcj316m085wg9.jpg)

![image-20210102142835085](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9c3imin9j31470bmwh8.jpg)

![image-20210102142844337](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9c3o56prj314r062t9v.jpg)

![image-20210102143546628](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9cb1f2ndj31br0ktqd2.jpg)

![image-20210102143623383](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9cbmt10tj30u401d750.jpg)

##### 事务

![image-20210102144253986](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9ciexwc5j315q0dqael.jpg)

![image-20210102144309693](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9ciomzwkj31cf0dudn4.jpg)

![image-20210102144339826](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9cj798yaj31b80b3jyd.jpg)

![image-20210102144419164](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9cjw3ixnj31bv085djt.jpg)



![image-20210102144620830](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9cm09bylj31b40jmn8y.jpg)

![image-20210102184741619](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9jlcusz7j30x20juah5.jpg)



```
show VARIABLES like "%"
show STATUS;
show STATUS like "LOCK row"
desc tbl_emp;
begin：
 SELECT name WHERE id = 12 FROM tbl_emp for UPDATE;
 SELECT SLEEP(15);
 COMMIT;
```



### 主从复制



Mysql 版本一致

#### 修改主机my.ini配置文件

server id=1

![image-20210102191324592](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9kbw5gfnj31290lvgum.jpg)

启用二进制文件

![image-20210102191402538](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9kcj2ehuj31550k3n4b.jpg)

### 

![image-20210102191521057](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9kdw9wm0j30tl0d5wg1.jpg)

 ![image-20210102191738547](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9kgmdhetj30mk03pjrj.jpg)

 

![image-20210102191813023](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9kgvekvmj30lr02yt8t.jpg)

![image-20210102191836984](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9khabg92j30ra0cutad.jpg)

![image-20210102191914036](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9xgxp9ypj30oy0783z5.jpg)

从机

![image-20210102201629229](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9m5idc0vj30m104vwfl.jpg)

![image-20210102202301818](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9mcbo7kcj30dm055q3q.jpg)

![image-20210102202452160](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9me82zq5j30jn04y757.jpg)

![image-20210102204240076](https://tva1.sinaimg.cn/large/0081Kckwgy1gm9mwxxnukj30vx01xjs9.jpg)































### mysql 练习

-- 1 查询工资最低的员工信息: last_name, salary

```sql
DESC employees; 
SELECT 	salary  FROM 	employees; 
SHOW INDEX  FROM 	employees;
SELECT 	last_name, 	salary  FROM 	employees  ORDER BY salary  LIMIT 1, 1;
```

1	SIMPLE	employees		ALL					107	100.00	Using filesort



--2 /*-- 2 查询平均工资最低的部门信息*/

```sql
DESC jobs;
SELECT 	job_id, 	job_title, 	min_salary, 	max_salary  FROM 	jobs;  
 
( SELECT job_id,job_title,min_salary,	max_salary , AVG( min_salary + max_salary ) AS avg_sal FROM jobs GROUP BY job_id ) AS sals;

/*查出部门平均工资*/
SELECT  	job_id, 	avg_sal , 		min_salary, 	max_salary 
FROM
	( SELECT job_id,job_title,min_salary,max_salary, AVG( min_salary + max_salary )/2 AS avg_sal FROM jobs GROUP BY jobs.job_id ) AS sals 
ORDER BY avg_sal LIMIT 1,1;
```

1	PRIMARY	<derived2>		ALL					19	100.00	Using filesort
2	DERIVED	jobs		index	PRIMARY	PRIMARY	22		19	100.00	

-- 3.查询平均工资最低的部门信息和该部门的平均工资

```sql
explain SELECT 
	job_id,
	job_title ,
		min_salary,
	max_salary ,
	avg_sal
FROM
	( SELECT job_id,job_title,min_salary,max_salary, AVG( min_salary + max_salary )/2 AS avg_sal FROM jobs GROUP BY jobs.job_id ) AS sals 
ORDER BY avg_sal LIMIT 1,1;
```

1	PRIMARY	<derived2>		ALL					19	100.00	Using filesort
2	DERIVED	jobs		index	PRIMARY	PRIMARY	22		19	100.00	

-- 4.查询平均工资最高的 job 信息

```sql
-- 4 查询平均工资最高的 job 信息
SELECT 
	job_id,
	job_title ,
		min_salary,
	max_salary ,
	avg_sal
FROM
(SELECT job_id,job_title,min_salary,max_salary, AVG( min_salary + max_salary )/2 AS avg_sal FROM jobs GROUP BY jobs.job_id ) AS sals

ORDER BY avg_sal desc LIMIT 1,1;
```

1	PRIMARY	<derived2>		ALL					19	100.00	Using filesort
2	DERIVED	jobs		index	PRIMARY	PRIMARY	22		19	100.00	

-- 5.查询平均工资高于公司平均工资的部门有哪些?

```sql
-- 公司平均工资 
SELECT   (AVG(min_salary)+avg(max_salary))/2  FROM   (SELECT job_id ,min_salary,max_salary from jobs GROUP BY job_id) as t1;

EXPLAIN SELECT 
	job_id,
	job_title ,
		min_salary,
	max_salary ,
	avg_sal
FROM
(SELECT job_id,job_title,min_salary,max_salary, AVG( min_salary + max_salary )/2 AS avg_sal FROM jobs GROUP BY jobs.job_id ) AS sals
WHERE avg_sal > (SELECT   (AVG(min_salary)+avg(max_salary))/2  FROM   (SELECT job_id ,min_salary,max_salary from jobs GROUP BY job_id) as t1);
```

1	PRIMARY	<derived2>		ALL					19	33.33	Using where
3	SUBQUERY	<derived4>		ALL					19	100.00	
4	DERIVED	jobs		ALL	PRIMARY				19	100.00	
2	DERIVED	jobs		index	PRIMARY	PRIMARY	22		19	100.00	

--6 查询出公司中所有 manager 的详细信息

```sql
SELECT
e.employee_id,
e.first_name,
e.last_name,
e.email,
e.phone_number,
e.job_id,
e.salary,
e.commission_pct,
e.manager_id,
e.department_id,
e.hiredate
FROM employees as e  JOIN  
( SELECT job_id, job_title from jobs  where job_title LIKE '%Manager') as t 
on e.job_id = t.job_id;
```

-- 7. 各个部门中 最高工资中最低的那个部门的 最低工资是多少

```sql
EXPLAIN 
SELECT job_id,min_salary ,max_salary FROM jobs  ORDER BY max_salary LIMIT 1,1; 
```

 

-- 8. 查询平均工资最高的部门的 manager 的详细信息: last_name, department_id, email,  salary

```sql
-- 各部门的平均工资
SELECT job_id ,job_title,(min_salary+max_salary)/2 as avg_sal FROM jobs ORDER BY avg_sal DESC limit 1,1;
-- 员工的manager
SELECT last_name, department_id, email,  salary from employees;
-- boss id
SELECT DISTINCT(e.manager_id) FROM employees as e , 
		(SELECT job_id ,job_title,(min_salary+max_salary)/2 as avg_sal FROM jobs ORDER BY avg_sal DESC limit 1,1) as t
where e.job_id = t.job_id;
-- 完整版
SELECT last_name, department_id, email,  salary from employees WHERE employee_id = (
SELECT DISTINCT(e.manager_id) FROM employees as e , 
		(SELECT job_id ,job_title,(min_salary+max_salary)/2 as avg_sal FROM jobs ORDER BY avg_sal DESC limit 1,1) as t
where e.job_id = t.job_id
);

```





