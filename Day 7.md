# Day 7

## My SQL

### 数据库设计

> 按照规范设计的方法，考虑数据库及其应用系统开发全过程，将数据库设计分为以下6个阶段
>
> 1.需求分析
>
> 2.概念结构设计
>
> 3.逻辑结构设计
>
> 4.物理结构设计
>
> 5.数据库实施
>
> 6.数据库的运行和维护

1.需求分析阶段（常用自顶向下）

      进行数据库设计首先必须准确了解和分析用户需求（包括数据与处理）。需求分析是整个设计过程的基础，也是最困难，最耗时的一步。需求分析是否做得充分和准确，决定了在其上构建数据库大厦的速度与质量。需求分析做的不好，会导致整个数据库设计返工重做。
2.概念结构设计阶段（常用自底向上）

​    概念结构设计是整个数据库设计的关键，它通过对用户需求进行综合，归纳与抽象，形成了一个独立于具体DBMS的概念模型。

   **设计概念结构通常有四类方法：**

*自顶向下*。即首先定义全局概念结构的框架，再逐步细化。
*自底向上*。即首先定义各局部应用的概念结构，然后再将他们集成起来，得到全局概念结构。
*逐步扩张*。首先定义最重要的核心概念结构，然后向外扩张，以滚雪球的方式逐步生成其他的概念结构，直至总体概念结构。
*混合策略*。即自顶向下和自底向上相结合。

3.逻辑结构设计阶段（E-R图）

      逻辑结构设计是将概念结构转换为某个DBMS所支持的数据模型，并将进行优化。
    
       在这阶段，E-R图显得异常重要。大家要学会各个实体定义的属性来画出总体的E-R图。
    
       各分E-R图之间的冲突主要有三类：属性冲突，命名冲突，和结构冲突。
    
       E-R图向关系模型的转换，要解决的问题是如何将实体性和实体间的联系转换为关系模式，如何确定这些关系模式的属性和码。
4.物理设计阶段

       物理设计是为逻辑数据结构模型选取一个最适合应用环境的物理结构（包括存储结构和存取方法）。
    
       首先要对运行的事务详细分析，获得选择物理数据库设计所需要的参数，其次，要充分了解所用的RDBMS的内部特征，特别是系统提供的存取方法和存储结构。
    
        常用的存取方法有三类：1.索引方法，目前主要是B+树索引方法。2.聚簇方法（Clustering）方法。3.是HASH方法。

5.数据库实施阶段

      数据库实施阶段，设计人员运营DBMS提供的数据库语言（如sql）及其宿主语言，根据逻辑设计和物理设计的结果建立数据库，编制和调试应用程序，组织数据入库，并进行试运行。

 



6.数据库运行和维护阶段

       数据库应用系统经过试运行后，即可投入正式运行，在数据库系统运行过程中必须不断地对其进行评价，调整，修改。


### DCL

> **DCL**(Data Control Language)语句：数据控制语句，用于控制不同数据段直接的许可和访问级别的语句。这些语句定义了数据库、表、字段、用户的访问权限和安全级别。

**关键字**

+ Grant
+ Revoke

**查看用户权限**

当成功创建用户账户后，还不能执行任何操作，需要为该用户分配适当的访问权限。可以使用`SHOW GRANTS FOR` 语句来查询用户的权限。例如：

```mysql
mysql> SHOW GRANTS FOR test;
+-------------------------------------------+
| Grants for test@%                         |
+-------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO 'test'@'%' |
+-------------------------------------------+
1 row in set (0.00 sec)
```

**管理用户**

```mysql
1. 添加用户：
    * 语法：CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
    * 主机名可以用%表示该用户可以从任意地址访问数据库
2. 删除用户：
    * 语法：DROP USER '用户名'@'主机名';
3. 修改用户密码：
    UPDATE USER SET PASSWORD = PASSWORD('新密码') WHERE USER = '用户名';
    UPDATE USER SET PASSWORD = PASSWORD('abc') WHERE USER = 'lisi';

    SET PASSWORD FOR '用户名'@'主机名' = PASSWORD('新密码');
    SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123');

    * mysql中忘记了root用户的密码？
        1. cmd -- > net stop mysql 停止mysql服务
            * 需要管理员运行该cmd
        2. 使用无验证方式启动mysql服务： mysqld --skip-grant-tables
        3. 打开新的cmd窗口,直接输入mysql命令，敲回车。就可以登录成功
        4. use mysql;
        5. update user set password = password('你的新密码') where user = 'root';
        6. 关闭两个窗口
        7. 打开任务管理器，手动结束mysqld.exe 的进程
        8. 启动mysql服务
        9. 使用新密码登录。
4. 查询用户：
    -- 1. 切换到mysql数据库
    USE myql;
    -- 2. 查询user表
    SELECT * FROM USER;

注：通配符： % 表示可以在任意主机使用用户登录数据库
```

**权限管理**

```mysql
1. 查询权限：
    -- 查询权限
    SHOW GRANTS FOR '用户名'@'主机名';
    SHOW GRANTS FOR 'lisi'@'%';

2. 授予权限：
    -- 授予权限
    grant 权限列表 on 数据库名.表名 to '用户名'@'主机名';
    -- 给张三用户授予所有权限，在任意数据库任意表上
    GRANT ALL ON *.* TO 'zhangsan'@'localhost';
3. 撤销权限：
    -- 撤销权限：
    revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';
    REVOKE UPDATE ON db3.`account` FROM 'lisi'@'%';

```



### DQL

(获取表中数据)

**select配合内置函数使用**

```mysql
-- 查看当前时间
mysql> select now();
+---------------------+
| now()               |
+---------------------+
| 2020-06-13 19:16:47 |
+---------------------+
1 row in set (0.00 sec)

-- 查看当前所使用的数据库
mysql> use mysql
Database changed
mysql> select database();
+------------+
| database() |
+------------+
| mysql      |
+------------+
1 row in set (0.00 sec)

-- 打印字符串
mysql> select concat('hello world');
+-----------------------+
| concat('hello world') |
+-----------------------+
| hello world           |
+-----------------------+
1 row in set (0.00 sec)

-- 格式化输出
mysql> select concat(user,'@',host) from user;
+-------------------------+
| concat(user,'@',host)   |
+-------------------------+
| app@192.168.159.%       |
| awei@192.168.159.%      |
| mysql.session@localhost |
| mysql.sys@localhost     |
| root@localhost          |
+-------------------------+
5 rows in set (0.00 sec)

-- 查看当前数据库版本
mysql> select version();
+-----------+
| version() |
+-----------+
| 5.7.20    |
+-----------+
1 row in set (0.00 sec)

-- 查看当前登录用户
mysql> select user();
+----------------+
| user()         |
+----------------+
| root@localhost |
+----------------+
1 row in set (0.00 sec)

```

**计算**

```mysql
mysql> select 10*100;
+--------+
| 10*100 |
+--------+
|   1000 |
+--------+
1 row in set (0.01 sec)
```

**查询数据库参数**

```mysql
mysql> select @@port;
+--------+
| @@port |
+--------+
|   3306 |
+--------+
1 row in set (0.00 sec)

mysql> select @@datadir;
+-------------+
| @@datadir   |
+-------------+
| /data/3306/ |
+-------------+
1 row in set (0.00 sec)

mysql> select @@socket;
+-----------------+
| @@socket        |
+-----------------+
| /tmp/mysql.sock |
+-----------------+
1 row in set (0.00 sec)

-- 显示全部参数
mysql> show variables;

mysql> show variables like '%trx%';
+--------------------------------+-------+
| Variable_name                  | Value |
+--------------------------------+-------+
| innodb_api_trx_level           | 0     |
| innodb_flush_log_at_trx_commit | 1     |
+--------------------------------+-------+
2 rows in set (0.01 sec)
```



### DDL

> DDL(Data Definition Language)，数据定义语言，用来定义数据库对象：数据库，表，列等，例如创建、删除、修改：数据库、表结构等。本文主要讲的是mysql数据库中DDL语言的使用，当然这与sql标准的DDL是一脉相承的，只是特定数据库的数据类型有差异。

1.操作数据库的DDL，包括数据库查看、切换、创建和删除等

首先是客户端的用户登录，比如windows的dos状态下，mysql  -uxxx  -pyyy，xxx和yyy分别是用户名和密码。当然，登录之前要保证mysql的服务已经启动。

```
查看用户所有的数据库，show  databases;
```

注意执行sql的命令要加分号，否则有些命令会被认为是换行操作。

安装mysql之后，系统会自动创建一些数据库，有4个，分别为information_schema、mysql、performance_schema、test，上面有5个，其中mydb1是我新建的。

需要注意的是，不到对这些系统创建的数据库进行修改或者其他操作，否则可能会造成mysql使用异常，严重的灰造成数据库不能使用。
创建数据库的命令为： create  database  数据库名;
删除数据库的命令为：drop  database  数据库名;  

最后说的是数据库的切换，命令为：use  数据库名;



2.DDL操作表，主要包括表的创建、修改和删除等。其中表的的修改有包括增减列、修改列、修改表名等。

首先讲一讲需要使用道德查询数据库的所有表的操作，命令为：show  tables;



3.表的创建，创建语句如下：

create  table  表名(

列名1   列类型1,

列名2   列类型2,

​     ..........

列名n   列类型n

);

另外，需要说说查看表结构的命令，为：desc    表名;

值得一提的是，这里没有定义key，以及说明字段是否为空和默认值等



4.修改表之增减列

首先需要说的是修改表的命令结构为：

alter   table   表名

xxxxxxxxxx;

第一行都是相同的，第二行的写法不同。

增加列的命令：

alter   table   表名

add  新列名  新列类型;
注意mysql中的sql语句书写规范，命令行以分号结尾，语句可以多行书写

删除列的命令为：

alter  table  表名

drop  列名;



5.修改表之修改列

包括修改列类型和修改列名（同时伴随咧类型的修改）

修改列类型的命令为：

alter  table  表名

modify  列名  列新类型;

修改列名的命令为：

alter  table  表名

change   列名   新列名   新列类型;



6.修改表名称

修改表名称的命令为：

alter  table  表名

rename  to  新表名;



7.删除表

删除表的命令为：

drop  表名;



### DML

> DML（Data Manipulation Language）语句：数据操纵语句。
>
> 用途：用于添加、修改、删除和查询**数据库记录**，并检查数据完整性。
>
> 常用关键字：insert、update、delete、select等。
>
> DML 操作的对象是**库表的数据（记录）**。
>
> 主要包括插入（insert）、更新（update）、删除（delete）和查询（select）。
>
> DML 语句是开发人员使用最频繁的操作。

1.插入记录

**指定字段**

```mysql
INSERT INTO emp(ename, hiredate, sal, deptno) VALUES('zzx1', '2000-01-01', '2000', 1);
```

**不指定字段**

```mysql
INSERT INTO emp VALUES('zzx1', '2000-01-01', '2000', 1);
```

values后面的顺序应该和字段的排列顺序一致

2.更新记录

**单表更新**

```mysql
/*ename   hiredate    sal     deptno  
------  ----------  ------  --------
zzx1    2000-01-01  200.00         1*/
UPDATE emp SET sal=400 WHERE ename='zzx1';
```

**多表更新**

```mysql
UPDATE emp a, dept b
SET a.sal=a.sal*b.deptno, b.deptname=a.ename
WHERE a.deptno = b.deptno;
```

3.删除记录

```mysql
DELETE FROM emp WHERE ename='zzx1';
```

4.查询记录

**查询**

```mysql
#普通查询
select * from emp;
#带条件查询
SELECT * FROM emp WHERE ename='zzx1';
```

**查询指定字段**

```mysql
SELECT ename, sal FROM emp WHERE ename='zzx1';
```

**去重查询**

```mysql
#查询deptno字段并去除重复
SELECT DISTINCT deptno FROM emp;
```

**查询排序**

```mysql
#查询并将以sal排序
SELECT * FROM emp ORDER BY sal;
```

**多字段排序**

```mysql
#对于deptno相同按sal排序
SELECT * FROM emp ORDER BY deptno, sal DESC;
```

**查询数量限制**

```mysql
#从查询结果中取第1条返回
SELECT * FROM emp LIMIT 1;
```

**指定返回结果的开始和结束索引（从0开始）**

```mysql
#从查询结果跳过第1条，取2条
SELECT * FROM emp ORDER BY sal LIMIT 1,2;
```

**聚合**

+ 统计总数

  ```mysql
  SELECT COUNT(*) FROM emp;
  ```

  

+ 统计各部门的总数

  ```mysql
  SELECT deptno, COUNT(1) FROM emp GROUP BY deptno;
  ```

  

+ 统计各部门的总数和全部总数

  ```mysql
  SELECT deptno, COUNT(1) FROM emp GROUP BY deptno WITH ROLLUP;
  ```

  

+ 统计人数大于1人的部门

  ```mysql
  select deptno, count(1) from emp group by deptno having count(1) > 1;
  ```

  

+ 统计所有员工的薪水总额、最高和最低薪水

  ```mysql
  SELECT SUM(sal), MAX(sal), MIN(sal) FROM emp;
  ```

  

**表连接**

- 内连接：仅选出两张表中互相匹配的记录

  ```mysql
  SELECT ename, deptname FROM emp, dept WHERE emp.deptno=dept.deptno;
  ```

  

- 外连接：仅选出两张表中互相匹配的记录，还会包含不匹配的数据

  + 左连接

  ```mysql
  SELECT ename, deptname FROM emp LEFT JOIN dept ON emp.deptno=dept.deptno;
  ```

  + 右连接

    ```mysql
    SELECT ename, deptname FROM dept RIGHT JOIN emp ON dept.deptno=emp.deptno;
    ```

    - 左连接：包含所有的左边表中的记录甚至是右边表中没有和它匹配的记录
    - 右连接：包含所有的右边表中的记录甚至是左边表中没有和它匹配的记录



**子查询**

当进入查询的时候，需要的条件是另外一个SELECT语句的结果时候（关键字：in、not in、=、!=、exists、not exists等）

```mysql
SELECT * FROM emp WHERE deptno IN(SELECT deptno FROM dept);
#如果查询记录为一可以使用=代替in
SELECT * FROM emp WHERE deptno = (SELECT deptno FROM dept);
```

- MySQL4.1以前不支持子查询，需要用表连接来实现子查询的功能
- 表连接在很多情况下用于优化子查询



**联合**

> 将两个表的数据按照一定的查询条件查询出来后，将结果全并到一起显示出来

- UNION ALL：是把结果集直接合并在一起

  ```mysql
  SELECT deptno FROM emp
  UNION ALL
  SELECT deptno FROM dept;
  ```

  

- UNION：是将UNION ALL的结果进行一次DISTINCT，去除重复的结果

  ```mysql
  SELECT deptno FROM emp
  UNION
  SELECT deptno FROM dept;
  ```

  

### 事务

> 事务：一个最小的不可再分的工作单元；通常一个事务对应一个完整的业务(例如银行账户转账业务，该业务就是一个最小的工作单元)
> 一个完整的业务需要批量的DML(insert、update、delete)语句共同联合完成
> 事务只和DML语句有关，或者说DML语句才有事务。这个和业务逻辑有关，业务逻辑不同，DML语句的个数不同

**事务四大特征**

- 原子性(A)：事务是最小单位，不可再分
- 一致性©：事务要求所有的DML语句操作的时候，必须保证同时成功或者同时失败
- 隔离性(I)：事务A和事务B之间具有隔离性
- 持久性(D)：是事务的保证，事务终结的标志(内存的数据持久到硬盘文件中)

**开启标志**

任何一条DML语句(insert、update、delete)执行，标志事务的开启

**结束标志**(提交或回滚)

-  提交：成功的结束，将所有的DML语句操作历史记录和底层硬盘数据来一次同步
-  回滚：失败的结束，将所有的DML语句操作历史记录全部清空

**提交操作**(事务成功)

- start transaction
- DML语句
- commit

```mysql
  mysql> start transaction;#手动开启事务
  mysql> insert into t_user(name) values('pp');
  mysql> commit;#commit之后即可改变底层数据库数据
  mysql> select * from t_user;
  +----+------+
  | id | name |
  +----+------+
  |  1 | jay  |
  |  2 | man  |
  |  3 | pp   |
  +----+------+
  3 rows in set (0.00 sec)
```

**回滚操作**(事务失败)

- start transaction
- DML语句
- rollback

```mysql
  mysql> start transaction;
  mysql> insert into t_user(name) values('yy');
  mysql> rollback;
  mysql> select * from t_user;
  +----+------+
  | id | name |
  +----+------+
  |  1 | jay  |
  |  2 | man  |
  |  3 | pp   |
  +----+------+
  3 rows in set (0.00 sec)
```



### 索引

**索引是什么**

> 官方介绍索引是帮助MySQL高效获取数据的数据结构。更通俗的说，数据库索引好比是一本书前面的目录，能加快数据库的查询速度。
>
> 一般来说索引本身也很大，不可能全部存储在内存中，因此索引往往是存储在磁盘上的文件中的（可能存储在单独的索引文件中，也可能和数据一起存储在数据文件中）。
>
> 我们通常所说的索引，包括聚集索引、覆盖索引、组合索引、前缀索引、唯一索引等，没有特别说明，默认都是使用B+树结构组织（多路搜索树，并不一定是二叉的）的索引。



**索引类型**
主键索引
索引列中的值必须是唯一的，不允许有空值。

普通索引
MySQL中基本索引类型，没有什么限制，允许在定义索引的列中插入重复值和空值。

唯一索引
索引列中的值必须是唯一的，但是允许为空值。

全文索引
只能在文本类型CHAR,VARCHAR,TEXT类型字段上创建全文索引。字段长度比较大时，如果创建普通索引，在进行like模糊查询时效率比较低，这时可以创建全文索引。 MyISAM和InnoDB中都可以使用全文索引。

空间索引
MySQL在5.7之后的版本支持了空间索引，而且支持OpenGIS几何数据模型。MySQL在空间索引这方面遵循OpenGIS几何数据模型规则。

前缀索引
在文本类型如CHAR,VARCHAR,TEXT类列上创建索引时，可以指定索引列的长度，但是数值类型不能指定。

其他（按照索引列数量分类）
单列索引

组合索引

组合索引的使用，需要遵循最左前缀匹配原则（最左匹配原则）。一般情况下在条件允许的情况下使用组合索引替代多个单列索引使用。



**My SQL的索引实现**

*MyIsam索引*

以一个简单的user表为例。user表存在两个索引，id列为主键索引，age列为普通索引

```mysql
CREATE TABLE `user`
(
  `id`       int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(20) DEFAULT NULL,
  `age`      int(11)     DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE,
  KEY `idx_age` (`age`) USING BTREE
) ENGINE = MyISAM
  AUTO_INCREMENT = 1
  DEFAULT CHARSET = utf8;
```



*InnoDB索引*

*主键索引*

表user的索引存储在索引文件`user.MYI`中，数据文件存储在数据文件 `user.MYD`中。

简单分析下查询时的磁盘IO情况：

```mysql
select * from user where id = 28;
```

