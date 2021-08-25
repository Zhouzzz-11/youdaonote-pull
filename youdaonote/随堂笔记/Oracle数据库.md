Oracle的用户名：scott	密码：tiger

Oracle的管理员账户：  system  	sys		Mysql的管理员账户：  root

用户名：sys		密码：admin123		connect  as:	sysdba	

在数据库中，用户的权限有三种： sysdba数据库管理员，sysoper数据库操作员，normal普通用户员

Oracle的客户端连接工具：plsql  developer		Mysql常用的是：sqlyog、navicat

他们自带有一个客户端工具，都是通过命令行使用的：

Mysql：	mysql  -u root -p

Oracle:	sqlplus	sys/admin123 as sysdba

Oracle自带有一个测试库，并且有一个用来测试的账号：scott，但是要先启用这个账号。

解锁账号：	alter user scott account unlock;

锁定账号：	alter user scott account lock;

解锁了账号之后，就需要设置密码：

alter  user  scott  identified by  tiger ;

使用scott账号进行登录，因为我们已经登录过其他账号，这时候用新账号去重新连接一下就可以了：		connect	scott/tiger

查看系统有哪些数据库：

在Mysql中：  show  databases;

在Oracle中，没有数据库的概念，只有tablespace表空间的概念，而且要求在连接的时候只连接一个数据库，我们登录的时候：sqlplus  用户名/密码@表空间  as 用户身份

如果密码省略，则需要我们去输入密码。如果表空间（数据库）省略则默认连接到上一次连接的那个表空间，as用户身份如果省略则以这个用户的身份登录，而如果这个用户有多重身份必须加入他的身份信息。

查看数据库中有哪些表：

在Mysql中：	show  tables;

在Oracle中：	select  *  from  tab;		并且可以加入WHERE条件。

查询EMP表的信息：在Oracle中表中的内容是区分大小写的

SELECT  *  FROM  tab  WHERE  tname = 'EMP' ;

查看表结构：

Mysql：		desc  表名称	

Oracle：	与Mysql相同

EMP表中的字段有：

empno:员工编号		ename:员工姓名		job：员工的工作

mgr：员工的领导编号	hiredate：入职日期		sal：工资（月薪）

comm：奖金			deptno：部门编号

DEPT部门表：

deptno：部门编号		dname：部门名称		dloc：部门位置

salgrade工资等级表：

grade：等级		losal：这个等级的最低工资	hisal：这个等级的最高工资

查看表中的全部内容：

SELECT  * FROM  emp ;

关于数据库部分需要掌握的知识重点：

查询：单表查询、分组查询、多表查询、子查询

增、删、改：

不带条件的单表查询：

在Oracle中的查询一定有SELECT和FROM 两个关键形成的子句。在Mysql中可以没有FROM，比如Mysql的：select  now()但是在Oracle中，对应的语句是：select sysdate from dual ;

1.全表查询，查询全部内容：

SELECT  *  FROM  表名称

2.查询部分字段：

SELECT  字段1,字段2,字段3  FROM 表名称

3.查询时，加字段的别名

SELECT  字段1 别名称,字段2 别名称  FROM 表名称

SELECT  字段1  AS  别名称,字段2  AS  别名称  FROM 表名称

4.查询时，不仅字段可以加别名，表也可以加别名

SELECT  字段1,字段2  FROM  表名称  别名称

SELECT * FROM emp e ;

5.从完整的查询语句来说，查询的字段应该完整标识为：表名称.字段名称

SELECT emp.empno,emp.ename  FROM emp;

SELECT  e.empno,e.ename   FROM  emp e ;

6.去除重复：DISTINCT，它是对所有字段进行去重复

SELECT DISTINCT 字段1,字段2 FROM  表名称

7.排序ORDER BY

SELECT * FROM 表名称  ODER BY 字段  ASC|DESC

1.ODER BY一定跟的是排序字段，后面跟如何排序

2.ASC小值在上面，大值在下面。DESC相反

3.如果涉及到多个排序项，则ODER BY 字段1 排序关键字,字段2 排序关键字

8.常量与变量

SELECT empno,ename,'你好'  FROM emp;

题目：查询emp表中的员工编号，姓名，工资和奖金，如果没有奖金则显示'加油'

SELECT empno,ename,sal,comm  FROM emp  WHERE comm is not null

UNION

SELECT empno,ename,sal,'加油'  FROM emp WHERE comm is null

带条件的查询：

1.查询语句中的比较符：

在Mysql中：=  >  >=  <  <=  !=   <>  <=>(=null)

在Oracle中：没有<=>，其他都有

2.逻辑关系AND  OR   NOT

3.模糊查询LIKE关键字，还有NOT  LIKE

SELECT  * FROM  EMP WHERE ename LIKE 'A%' ;

%匹配任意个数字符，_ 匹配仅1个字符

4.在某个范围之内，BETWEEN……AND……

1.BETWEEN…AND…只能针对数字有效

2.小的数值在AND前面，大的数值在AND后面。

问题：查询工资是1000到2000的员工信息 

5.在某个集合范围中，IN还有NOT  IN

SELECT  *  FROM 表名称  WHERE 字段  IN (1,2,3) ;

SELECT * FROM emp WHERE (job,deptno)  IN (('CLERK',20),('SALSMAN',30)) ;

6.为空查询：IS NULL

查询奖金为0和为空的员工信息

SELECT  *   FROM emp  WHERE comm  is NULL or  comm = 0 ;

7.结果集的相加UNION和UNION ALL

SELECT *  FROM emp  WHERE comm is null

UNION

SELECT *  FROM emp  WHERE comm = 0 ;

8.字段值为空的处理：

Mysql： select *  from emp where ifnull(comm,0) = 0 ;

Oracle：select * from emp where NVL(comm,0) = 0 ;

题目：

显示员工的姓名，工资和奖金+100元

分组查询：

1.查询emp表中每一个工作都有多少人

2.查询每个部门中最高工资和最低工资是多少

3.按工作和部门分组，求其最低工资

SQL数据库的函数：

与分组相关的函数：

聚合函数：COUNT()，MAX()，MIN()，AVG()，SUM()

其他函数：长度length()，当前日期（sysdate），to_date()

查询每个员工服务时间，即工作了多长时间

SELECT ename,hiredate,sysdate-hiredate 工作时长 FROM  emp;

查询80年前入职的员工信息

SELECT  *  FROM  emp  WHERE  hiredate < to_date('1980-1-1','yyyy-mm-dd') ;

分组表达式：

分组一定有分组项，GROUP BY 后面接的是分组项，如果有多个分组项则用逗号分隔

SELECT后面只能接分组项和聚合函数，其他的都不可以。但是Mysql中的SELECT可以包含非分组项和聚合函数，但是不建议这么做。

聚合函数中是统计什么项，就拿什么项列入聚合函数中

对部分数据进行分组，则使用WHERE条件对数据进行筛选。

比如查询10部门每个工作的最低工资

SELECT job,min(sal)  FROM  emp  WHERE  deptno=10  GROUP BY job

如果要对分组之后的结果进行筛选，这个时候就不能够使用WHERE关键字了而要使用HAVING关键字，HAVING关键字是对聚合函数做处理。

查询每个工作各有多少人，只显示人数超过2人的那些信息。

SELECT  job,count(empno)

FROM  emp

GROUP BY job

HAVING count(empno)>2 ;

多表查询：

1.有SELECT中包含包.字段名 FROM 表名称为多张表，一般会设置别名

2.多表查询一定有连接条件，一般为表的公共字段。

EMP表中有：deptno（部门编号），DEPT表中也有deptno（部门编号）

等值连接：

我们可以通过EMP表和DEPT表获取员工的姓名，部门编号，部门名称

员工姓名：emp.ename，部门编号（emp.deptno），部门名称（dept.dname）

SELECT  e.ename,e.deptno,d.dname

FROM emp e,dept d

WHERE e.deptno=d.deptno

不等值连接：用BETWEEN…AND…做连接

emp表中有sal工资，在salgrade表中有工资等级，我想知道每个员的工资和工资等级是多少。

SELECT  e.ename,e.sal,s.grade,s.losal,s.hisal

FROM  emp e,salgrade s

WHERE  e.sal  BETWEEN  s.losal  AND s.hisal AND e.sal>1000;

自身表连接：

要把这张表看成是两份表，并且给两个表分别设置别名。

在emp表中，有员工的编号，姓名和这个员工领导的编号。要显示员工的编号，员工的姓名和领导的领导和领导姓名。

SELECT e.empno,e.ename,e.mgr,l.empno,l.ename

FROM emp e , emp l

WHERE e.mgr=l.empno

左连接和右连接：

emp表中有员工编号，员工姓名和部门编号，dept表有部门编号，部门名称。其中有1个部门没有员工，现在要求显示员工编号，员工姓名，部门编号以及部门名称，要求没有员工部门也显示出来。

Oracle的独门技巧：

SELECT e.empno,e.ename,e.deptno,d.deptno,d.dname

FROM emp e,dept d

WHERE  e.deptno(+)  =  d.deptno

多表查询与分组查询联合使用：

分组查询之后结果也可以认为一张表，把它设置为a表即可。

例如：查询每个部门工资最高的那个员工姓名，部门编号和工资

SELECT e.empno,e.ename,e.deptno,e.sal

FROM emp e,(

select  deptno,max(sal)  ms from emp  group by deptno)  a

WHERE e.deptno = a.deptno AND e.sal = a.ms

查询每个工作的最低工资的员工姓名，工作和工资

查询每个工作的最高工资的员工姓名，工作和工资以及他所在的部门编号及部门名称

子查询：

就是查询中套查询，叫做子查询。首先前面多表查询与分组查询就包含了子查询，我们将子查询的结果看作是一张表作为FROM子句而存在。

子查询还有一种常用的体现是在WHERE条件中使用子查询。

子查询的结果如果为单列单行，则用=

查询emp表中工资最低那个员工的姓名，工作和工资

SELECT ename,job,sal  FROM  emp  WHERE sal = (select  min(sal)  from emp) ;

查询工资大于平均工资的员工姓名，工作和工资

子查询的结果为单列多行数据，则用IN

题目：查询部门名称包含S，这些部门的员工信息

1.SELECT  deptno FROM dept WHERE dname like '%S%' 

2.SELECT  *  FROM emp  WHERE deptno IN (SELECT  deptno FROM dept WHERE dname like '%S%' ) ;

子查询的结果为多列多行数据，也有IN来完成

例如：查询每个工作的最低工资的员工信息

1.SELECT  job,min(sal)  FROM emp  GROUP BY job

2.SELECT *  FROM emp  WHERE (job,sal) IN (SELECT  job,min(sal)  FROM emp  GROUP BY job) ;

综合练习：

1.查询没有奖金员工，都属于哪些部门

2.查询奖金最高的那个员工的基本信息

3.查询员工编号是奇数员工信息

SELECT * FROM emp WHERE mod(empno,2)=1 ;

4.查询每个部门分别要发多少年薪

Oracle中查询前面若干行：ROWNUM，在Mysql中是LIMIT

ROWNUM不是表中的列，但是每一个表中都有ROWNUM，是一个虚列。

查询emp表中的前5行信息：

Oracle的实现：select  * from emp where rownum <= 5 ;

Mysql的实现：select  *  from emp LIMIT 0,5

ROWNUM如果我要显示第5行以后的信息，如何处理？

Mysql：SELECT  *  FROM emp  LIMIT 5,99999

Oracle:  SELECT  * FROM emp WHERE rownum > 5 ;

Oracle中ROWNUM只支持<和<=，不支持=和>处理

1.我将查询结果显示出来结果结合rownum（要设别名）作为一张子表

2.再从这个子表进行查询，选择rownum大于某个值即可。

select * from (select  rownum rn,emp.* from emp) a where a.rn>5 ;

查询emp表中后面那一半数据

法一： select * from (select  rownum rn,emp.* from emp) a where a.rn>(select avg(rownum) from emp);

法二：select * from (select  rownum rn,emp.* from emp) a where a.rn>(select count(*)/2) from emp);

增、删、改，建表：

建表：与mysql相同，但是有两个不同：

1.数据类型：在Mysql中字符数据类型是char()和varchar()，在Oracle中，是varchar2()

2.关于自增长，在Mysql 中用的自增长是AUTO_INCREMENT，在Oracle中用的是序列

我们可以把查询的结果，保存一张新表中：

CREATE  TABLE  表名称  AS 子查询 ;

这个语句也可以创建一个空表，只复制别的表的表结构不复制数据。

CREATE TABLE 表名称  AS  子查询 WHERE 1=2

增加数据：

在Mysql中，支持INSERT  [INTO] 表名称  VALUE() ;也可以使用INSERT  INTO 表名称 VALUES(),();

在Oracle中，要使用VALUES而且只能一次性增加1个数据。

增加数据来源于其他表：

INSERT  INTO  bonus   select ename,job,sal,comm from emp where comm is not null;

修改数据：

UPDATE  表名称  SET  字段=值  WHERE 字段=值

一定要注意WHERE条件，如果没有WHERE条件将会产生全表更新。

删除数据：

DELETE  FROM 表 WHERE 条件		将会产生删除。

DELETE  FROM 表 	不加WHERE条件将会产生全表删除。

TRUNCATE TABLE 表名称	清空表，它与DELETE是有区别的。

大家找一下它们的区别，并且有一个面试题：

如果一张表里面有100万数据，现在要全表清空，有DELETE和TRUNCATE两种删除方式，请问分别有什么区别，你会使用哪种进行删除？

两种方式均可，truncate 效率高 delete 安全（可回滚，而truncate不可回滚）







