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



