# mysql-final-test

2019-2020 mysql final test

姓名：石力玮		

学号：17061725

说明1：考试为开卷，可以上网，自觉不要相互电话和QQ；

说明2：考试时间为：2020 年 4 月 10 日 8:10分-9:40分。

说明3：试题比较多，抓紧时间，超时提交的github commit不被接受。未避免完全超时提交，可以在做题过程中多 commit 几次。

说明4：结束后发邮件给 42225@hdu.edu.cn 标题为“MySQL期末考试,姓名+学号”，内容为github链接。


1 打印当前时间（例如 2020-04-07 13:41:42），写出SQL语句和结果
```
mysql> select curdate();
+------------+
| curdate()  |
+------------+
| 2020-04-10 |
+------------+
1 row in set (0.02 sec)
```

2 组合打印自己的姓名和学号
```
select concat('石力玮','17061725');
```

3 建立如下表1和表2，写出建表语句和插入语句。

表1：其中deptno为主键
```
deptno, dename, loc
(10, "ACCOUNTING", "NEW YORK"),
(20, "RESEARCH", "DALLAS"),
(30, "SALES", "CHICAGO"),
(40, "OPERATIONS", "BOSTON")
```

```
mysql> create table table1(deptno int,dename varchar(50),loc varchar(50));
Query OK, 0 rows affected (0.03 sec)
mysql> insert into table1(deptno, dename, loc) values(10, "ACCOUNTING", "NEW YORK"),(20, "RESEARCH", "DALLAS"),(30, "SALES", "CHICAGO"),(40, "OPERATIONS", "BOSTON");
```

表2：其中empno字段为主键
```
        empno, ename,    job,    MGR,   Hiredate,    sal,   comm, deptno
        (7369, "SMITH", "CLERK", 7902, "1981-03-12", 800.00, NULL, 20),
	(7499, "ALLEN", "SALESMAN", 7698, "1982-03-12", 1600, 300, 30),
	(7521, "WARD", "SALESMAN", 7698, "1838-03-12", 1250, 500, 30),
	(7566, "JONES", "MANAGER", 7839, "1981-03-12", 2975, NULL, 20),
	(7654, "MARTIN", "SALESMAN", 7698, "1981-01-12", 1250, 1400, 30),
	(7698, "BLAKE", "MANAGER", 7839, "1985-03-12", 2450, NULL, 10),
	(7788, "SCOTT", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
	(7839, "KING", "PRESIDENT", NULL, "1981-03-12", 5000, NULL, 10),
	(7844, "TURNER", "SALESMAN", 7689, "1981-03-12", 1500, 0, 30),
	(7878, "ADAMS", "CLERK", 7788, "1981-03-12", 1100, NULL,20),
	(7900, "JAMES", "CLERK", 7698,"1981-03-12",  950, NULL, 30),
	(7902, "FORD", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
	(7934, "MILLER", "CLERK", 7782, "1981-03-12", 1300, NULL, 10)
```
```
mysql> mysql> create table table2(
	'empno' INT NOT NULL,
	'ename' VARCHAR(100), 
	'job' VARCHAR(100), 
	'MGR' INT,
	'Hiredate' DATE, 
	'sal' FLOAT NULL,
	'comm' INT NULL, 
	'deptno' INT NOT NULL,
	PRIMARY KEY ( 'empno' )
	FOREINGN KEY('deptno')
);
INSERT INTO table2 (empno, ename,    job,    MGR,   Hiredate,    sal,   comm, deptno)
VALUES
(
    (7369, "SMITH", "CLERK", 7902, "1981-03-12", 800.00, NULL, 20),
	(7499, "ALLEN", "SALESMAN", 7698, "1982-03-12", 1600, 300, 30),
	(7521, "WARD", "SALESMAN", 7698, "1838-03-12", 1250, 500, 30),
	(7566, "JONES", "MANAGER", 7839, "1981-03-12", 2975, NULL, 20),
	(7654, "MARTIN", "SALESMAN", 7698, "1981-01-12", 1250, 1400, 30),
	(7698, "BLAKE", "MANAGER", 7839, "1985-03-12", 2450, NULL, 10),
	(7788, "SCOTT", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
	(7839, "KING", "PRESIDENT", NULL, "1981-03-12", 5000, NULL, 10),
	(7844, "TURNER", "SALESMAN", 7689, "1981-03-12", 1500, 0, 30),
	(7878, "ADAMS", "CLERK", 7788, "1981-03-12", 1100, NULL,20),
	(7900, "JAMES", "CLERK", 7698,"1981-03-12",  950, NULL, 30),
	(7902, "FORD", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
	(7934, "MILLER", "CLERK", 7782, "1981-03-12", 1300, NULL, 10)
)
```

3.1 表2 中再插入一条记录：
```

INSERT INTO table2 (empno, ename,    job,    MGR,   Hiredate,    sal,   comm, deptno)
VALUES
(17061725, shiliwei, "CLERK", 7782, "1999-01-15", NULL, NULL, 10)
```

3.2 表中入职时间（Hiredate字段）最短的人。
```
SELECT t2.ename
FROM table2 t2
WHERE t2.Hiredate >= all(SELECT Hiredate FROM t2)
```

3.3 有几种职位（job字段）？在关系代数中，本操作是什么运算？
6种

3.4 将 MILLER 的 comm 增加 100； 然后，找到 comm 比 MILLER 低的人；
```
UPDATE table2 comm = comm + 100
WHERE table2.ename = "MILLER"

SELECT t2.ename
FROM table2 t2
WHERE (t2.comm > (SELECT t2.comm FROM t2 WHERE t2.ename = "MILLER"));
```

3.5 计算每个人的收入(ename, sal + comm)；计算总共有多少人；计算所有人的平均收入。 提示：计算时 NULL 要当做 0 处理；
```
SELECT IFNULL("COMM",0) FROM table2

SELECT IFNULL("SAL",0) FROM table2

SELECT ename, count (t2.comm, t2.sal) as salary
FROM table2 t2

SELECT ename, AVG(t2.comm + t2.sal) as avgsalary
FROM table2 t2 
```

3.6 显示每个人的下属, 没有下属的显示 NULL。本操作使用关系代数中哪几种运算？
```
SELECT t2.ename, tt2.enmae as branch
FROM table2 t2 INNER JOIN table2 t22 ON t2.empno = tt2.MGR
```
使用了交运算

3.7 建立一个视图：每个人的empno, ename, job 和 loc。简述为什么要建立本视图。
```
CREATE view TEMP as
SELECT empno, ename, job, loc
FROM table2
```
更直观方便的找到需要的信息，排除不需要的内容

3.8 为表2增加一个约束：deptno字段需要在表1中存在；这称做什么完整性？
```
ALTER TABLE table2 ADD CONSTRAINT deptno FOREIGN KEY REFERENCES table1;
```
参照完整性

3.9 为表2增加一个索引：ename 字段。简述为什么要在 ename 字段建立索引
```
CREATE INDEX enameindex on table2(ename);
```
可以提高查询速度，和数据库性能

3.10 将表2的 sal 字段改名为 salary
```
ALTER TABLE table2 CHANGE sal salary
```

3.11 撰写一个函数 get_deptno_from_empno，输入 empno，输出对应的 deptno。 简述函数和存储过程有什么不同。
存储过程用户在数据库中完成特定操作或者任务（如插入，删除等），函数用于返回特定的数据。存储过程不需要返回类型，函数必须要返回类型。sql语句（DML或SELECT)中不可用调用存储过程，而函数可以。
```
CREATE FUNCTION get_deptno_from_empno() RETURN INTEGER;

BEGIN

​	DECLARE;
```

4 建立一个新用户，账号为自己的姓名拼音，密码为自己的学号；
```
mysql>  GRANT USAGE ON *.* TO 'shiliwei'@'localhost' IDENTIFIED BY '17061725' WITH GRANT OPTION;
Query OK, 0 rows affected, 1 warning (0.01 sec)
```

4.1 将表1的SELECT, INSERT, UPDATE(ename)权限赋给该账号。
```
grant select on t1 to shiliwei ;
```

4.2 显示该账号权限
```
mysql> show grants for 'shiliwei'@'host';
```

4.3 `with grant option` 是什么意思。
表示该用户可以将自己拥有的权限授权给别人。

5 表 1 和表 2 这样设计是否符合第一范式，是否符合第二范式，为什么？
不符合。数据库表中不存在非关键字段对任一候选关键字段的部度分函数依赖。

6 画出表 1 和表 2 所对应的 E-R 图

7 什么是外模式，什么是内模式。为什么要分成这几层？
外模式又称子模式，对应于用户级。它是某个或某几个用户所看到的数据库的数据视图，是与某一应用有关的数据的逻辑表示。外模式是从模式导出的一个子集，包含模式中允许特定用户使用的那部分数据。

内模式又称存储模式，对应于物理级，它是数据库中全体数据的内部表示或底层描述，是数据库最低一级的逻辑描述，它描述了数据在存储介质上的存储方式翱物理结构，对应着实际存储在外存储介质上的数据库。内模式由内模式描述语言来描述、定义，它是数据库的存储观。

8 什么是ACID？
ACID，是指在可靠数据库管理系统（DBMS）中，事务(transaction)所应该具有的四个特性：原子性 一致性 隔离性 持久性

8.1 编写一个事务，“将 MILLER 的 comm 增加 100，如果增加后的 comm 大于 1000 则回滚”；

8.2 如何查看 MySQL 当前的隔离级别？
通过命令 set session transaction isolation level 可以设置本次会话的事务隔离级别

8.3 如果隔离级别为 READ-UNCOMMITED, 完成 “MILLER 的 comm 增加 100” 事务操作完成后，可能读到的结果有哪些，原因是什么？

9 有哪些场景不适合用关系型数据库？为什么？
1.图片，文件，二进制数据
2.短生命期数据
3.日志文件
