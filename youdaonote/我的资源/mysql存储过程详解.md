mysql存储过程详解

1.      存储过程简介

 

我们常用的操作数据库语言SQL语句在执行的时候需要要先编译，然后执行，而存储过程（Stored Procedure）是一组为了完成特定功能的SQL语句集，经编译后存储在数据库中，用户通过指定存储过程的名字并给定参数（如果该存储过程带有参数）来调用执行它。

一个存储过程是一个可编程的函数，它在数据库中创建并保存。它可以有SQL语句和一些特殊的控制结构组成。当希望在不同的应用程序或平台上执行相同的函数，或者封装特定功能时，存储过程是非常有用的。数据库中的存储过程可以看做是对编程中面向对象方法的模拟。它允许控制数据的访问方式。

存储过程通常有以下优点：

(1).存储过程增强了SQL语言的功能和灵活性。存储过程可以用流控制语句编写，有很强的灵活性，可以完成复杂的判断和较复杂的运算。

(2).存储过程允许标准组件是编程。存储过程被创建后，可以在程序中被多次调用，而不必重新编写该存储过程的SQL语句。而且数据库专业人员可以随时对存储过程进行修改，对应用程序源代码毫无影响。

(3).存储过程能实现较快的执行速度。如果某一操作包含大量的Transaction-SQL代码或分别被多次执行，那么存储过程要比批处理的执行速度快很多。因为存储过程是预编译的。在首次运行一个存储过程时查询，优化器对其进行分析优化，并且给出最终被存储在系统表中的执行计划。而批处理的Transaction-SQL语句在每次运行时都要进行编译和优化，速度相对要慢一些。

(4).存储过程能够减少网络流量。针对同一个数据库对象的操作（如查询、修改），如果这一操作所涉及的Transaction-SQL语句被组织程存储过程，那么当在客户计算机上调用该存储过程时，网络中传送的只是该调用语句，从而大大增加了网络流量并降低了网络负载。

(5).存储过程可被作为一种安全机制来充分利用。系统管理员通过执行某一存储过程的权限进行限制，能够实现对相应的数据的访问权限的限制，避免了非授权用户对数据的访问，保证了数据的安全。

 

2.      关于MySQL的存储过程

存储过程是数据库存储的一个重要的功能，但是MySQL在5.0以前并不支持存储过程，这使得MySQL在应用上大打折扣。好在MySQL 5.0终于开始已经支持存储过程，这样即可以大大提高数据库的处理速度，同时也可以提高数据库编程的灵活性。

3.      MySQL存储过程的创建

 

(1). 格式

MySQL存储过程创建的格式：CREATE PROCEDURE 过程名 ([过程参数[,...]])

[特性 ...] 过程体

这里先举个例子：

   

1. mysql> DELIMITER //  

1. mysql> CREATE PROCEDURE proc1(OUT s int)  

1.     -> BEGIN 

1.     -> SELECT COUNT(*) INTO s FROM user;  

1.     -> END 

1.     -> //  

1. mysql> DELIMITER ; 

 

注：

（1）这里需要注意的是DELIMITER //和DELIMITER ;两句，DELIMITER是分割符的意思，因为MySQL默认以";"为分隔符，如果我们没有声明分割符，那么编译器会把存储过程当成SQL语句进行处理，则存储过程的编译过程会报错，所以要事先用DELIMITER关键字申明当前段分隔符，这样MySQL才会将";"当做存储过程中的代码，不会执行这些代码，用完了之后要把分隔符还原。

（2）存储过程根据需要可能会有输入、输出、输入输出参数，这里有一个输出参数s，类型是int型，如果有多个参数用","分割开。

（3）过程体的开始与结束使用BEGIN与END进行标识。

这样，我们的一个MySQL存储过程就完成了，是不是很容易呢?看不懂也没关系，接下来，我们详细的讲解。

 

(2). 声明分割符

 

其实，关于声明分割符，上面的注解已经写得很清楚，不需要多说，只是稍微要注意一点的是：如果是用MySQL的Administrator管理工具时，可以直接创建，不再需要声明。

 

(3). 参数

MySQL存储过程的参数用在存储过程的定义，共有三种参数类型,IN,OUT,INOUT,形式如：

CREATE PROCEDURE([[IN |OUT |INOUT ] 参数名 数据类形...])

IN 输入参数:表示该参数的值必须在调用存储过程时指定，在存储过程中修改该参数的值不能被返回，为默认值

OUT 输出参数:该值可在存储过程内部被改变，并可返回

INOUT 输入输出参数:调用时指定，并且可被改变和返回

Ⅰ. IN参数例子

创建:

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE demo_in_parameter(IN p_in int)  

1. -> BEGIN   

1. -> SELECT p_in;   

1. -> SET p_in=2;   

1. -> SELECT p_in;   

1. -> END;   

1. -> //  

1. mysql > DELIMITER ; 



执行结果:

1. mysql > SET @p_in=1;  

1. mysql > CALL demo_in_parameter(@p_in);  

1. +------+  

1. | p_in |  

1. +------+  

1. |   1  |   

1. +------+  

1.  

1. +------+  

1. | p_in |  

1. +------+  

1. |   2  |   

1. +------+  

1.  

1. mysql> SELECT @p_in;  

1. +-------+  

1. | @p_in |  

1. +-------+  

1. |  1    |  

1. +-------+  



以上可以看出，p_in虽然在存储过程中被修改，但并不影响@p_in的值

 

Ⅱ.OUT参数例子

创建:

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE demo_out_parameter(OUT p_out int)  

1. -> BEGIN 

1. -> SELECT p_out;  

1. -> SET p_out=2;  

1. -> SELECT p_out;  

1. -> END;  

1. -> //  

1. mysql > DELIMITER ; 



执行结果:

1. mysql > SET @p_out=1;  

1. mysql > CALL sp_demo_out_parameter(@p_out);  

1. +-------+  

1. | p_out |   

1. +-------+  

1. | NULL  |   

1. +-------+  

1.  

1. +-------+  

1. | p_out |  

1. +-------+  

1. |   2   |   

1. +-------+  

1.  

1. mysql> SELECT @p_out;  

1. +-------+  

1. | p_out |  

1. +-------+  

1. |   2   |  

1. +-------+  



Ⅲ. INOUT参数例子

创建:

1. mysql > DELIMITER //   

1. mysql > CREATE PROCEDURE demo_inout_parameter(INOUT p_inout int)   

1. -> BEGIN 

1. -> SELECT p_inout;  

1. -> SET p_inout=2;  

1. -> SELECT p_inout;   

1. -> END;  

1. -> //   

1. mysql > DELIMITER ; 

 

 

执行结果:

1. mysql > SET @p_inout=1;  

1. mysql > CALL demo_inout_parameter(@p_inout) ;  

1. +---------+  

1. | p_inout |  

1. +---------+  

1. |    1    |  

1. +---------+  

1.  

1. +---------+  

1. | p_inout |   

1. +---------+  

1. |    2    |  

1. +---------+  

1.  

1. mysql > SELECT @p_inout;  

1. +----------+  

1. | @p_inout |   

1. +----------+  

1. |    2     |  

1. +----------+ 



(4). 变量

Ⅰ. 变量定义

DECLARE variable_name [,variable_name...] datatype [DEFAULT value];

其中，datatype为MySQL的数据类型，如:int, float, date, varchar(length)

例如:

1. DECLARE l_int int unsigned default 4000000;  

1. DECLARE l_numeric number(8,2) DEFAULT 9.95;  

1. DECLARE l_date date DEFAULT '1999-12-31';  

1. DECLARE l_datetime datetime DEFAULT '1999-12-31 23:59:59';  

1. DECLARE l_varchar varchar(255) DEFAULT 'This will not be padded';   

 

 

Ⅱ. 变量赋值

 SET 变量名 = 表达式值 [,variable_name = expression ...]

 

Ⅲ. 用户变量

 

ⅰ. 在MySQL客户端使用用户变量

1. mysql > SELECT 'Hello World' into @x;  

1. mysql > SELECT @x;  

1. +-------------+  

1. |   @x        |  

1. +-------------+  

1. | Hello World |  

1. +-------------+  

1. mysql > SET @y='Goodbye Cruel World';  

1. mysql > SELECT @y;  

1. +---------------------+  

1. |     @y              |  

1. +---------------------+  

1. | Goodbye Cruel World |  

1. +---------------------+  

1.  

1. mysql > SET @z=1+2+3;  

1. mysql > SELECT @z;  

1. +------+  

1. | @z   |  

1. +------+  

1. |  6   |  

1. +------+  

ⅱ. 在存储过程中使用用户变量

1. mysql > CREATE PROCEDURE GreetWorld( ) SELECT CONCAT(@greeting,' World');  

1. mysql > SET @greeting='Hello';  

1. mysql > CALL GreetWorld( );  

1. +----------------------------+  

1. | CONCAT(@greeting,' World') |  

1. +----------------------------+  

1. |  Hello World               |  

1. +----------------------------+  

 

ⅲ. 在存储过程间传递全局范围的用户变量

1. mysql> CREATE PROCEDURE p1()   SET @last_procedure='p1';  

1. mysql> CREATE PROCEDURE p2() SELECT CONCAT('Last procedure was ',@last_proc);  

1. mysql> CALL p1( );  

1. mysql> CALL p2( );  

1. +-----------------------------------------------+  

1. | CONCAT('Last procedure was ',@last_proc  |  

1. +-----------------------------------------------+  

1. | Last procedure was p1                         |  

1. +-----------------------------------------------+  

 

 

注意:

①用户变量名一般以@开头

②滥用用户变量会导致程序难以理解及管理

 

(5). 注释

 

MySQL存储过程可使用两种风格的注释

双模杠：--

该风格一般用于单行注释

c风格： 一般用于多行注释

例如：

 

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE proc1 --name存储过程名  

1. -> (IN parameter1 INTEGER)   

1. -> BEGIN   

1. -> DECLARE variable1 CHAR(10);   

1. -> IF parameter1 = 17 THEN   

1. -> SET variable1 = 'birds';   

1. -> ELSE 

1. -> SET variable1 = 'beasts';   

1. -> END IF;   

1. -> INSERT INTO table1 VALUES (variable1);  

1. -> END   

1. -> //  

1. mysql > DELIMITER ;  

 

4.      MySQL存储过程的调用

用call和你过程名以及一个括号，括号里面根据需要，加入参数，参数包括输入参数、输出参数、输入输出参数。具体的调用方法可以参看上面的例子。

5.      MySQL存储过程的查询

我们像知道一个数据库下面有那些表，我们一般采用show tables;进行查看。那么我们要查看某个数据库下面的存储过程，是否也可以采用呢？答案是，我们可以查看某个数据库下面的存储过程，但是是令一钟方式。

我们可以用

select name from mysql.proc where db=’数据库名’;

或者

select routine_name from information_schema.routines where routine_schema='数据库名';

或者

show procedure status where db='数据库名';

进行查询。

如果我们想知道，某个存储过程的详细，那我们又该怎么做呢？是不是也可以像操作表一样用describe 表名进行查看呢？

答案是：我们可以查看存储过程的详细，但是需要用另一种方法：

SHOW CREATE PROCEDURE 数据库.存储过程名;

就可以查看当前存储过程的详细。

 

6.      MySQL存储过程的修改

ALTER PROCEDURE

更改用CREATE PROCEDURE 建立的预先指定的存储过程，其不会影响相关存储过程或存储功能。

 

7.      MySQL存储过程的删除

删除一个存储过程比较简单，和删除表一样：

DROP PROCEDURE

从MySQL的表格中删除一个或多个存储过程。

 

8.      MySQL存储过程的控制语句

(1). 变量作用域

内部的变量在其作用域范围内享有更高的优先权，当执行到end。变量时，内部变量消失，此时已经在其作用域外，变量不再可见了，应为在存储

过程外再也不能找到这个申明的变量，但是你可以通过out参数或者将其值指派

给会话变量来保存其值。

 

 

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE proc3()  

1.      -> begin 

1.      -> declare x1 varchar(5) default 'outer';  

1.      -> begin 

1.      -> declare x1 varchar(5) default 'inner';  

1.      -> select x1;  

1.      -> end;  

1.      -> select x1;  

1.      -> end;  

1.      -> //  

1. mysql > DELIMITER ;  

 

 (2). 条件语句

Ⅰ. if-then -else语句

 

 

 

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE proc2(IN parameter int)  

1.      -> begin 

1.      -> declare var int;  

1.      -> set var=parameter+1;  

1.      -> if var=0 then 

1.      -> insert into t values(17);  

1.      -> end if;  

1.      -> if parameter=0 then 

1.      -> update t set s1=s1+1;  

1.      -> else 

1.      -> update t set s1=s1+2;  

1.      -> end if;  

1.      -> end;  

1.      -> //  

1. mysql > DELIMITER ;  



Ⅱ. case语句： 

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE proc3 (in parameter int)  

1.      -> begin 

1.      -> declare var int;  

1.      -> set var=parameter+1;  

1.      -> case var  

1.      -> when 0 then   

1.      -> insert into t values(17);  

1.      -> when 1 then   

1.      -> insert into t values(18);  

1.      -> else   

1.      -> insert into t values(19);  

1.      -> end case;  

1.      -> end;  

1.      -> //  

1. mysql > DELIMITER ; 

 

(3). 循环语句

Ⅰ. while ···· end while：

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE proc4()  

1.      -> begin 

1.      -> declare var int;  

1.      -> set var=0;  

1.      -> while var<6 do  

1.      -> insert into t values(var);  

1.      -> set var=var+1;  

1.      -> end while;  

1.      -> end;  

1.      -> //  

1. mysql > DELIMITER ; 

 

 

Ⅱ. repeat···· end repeat：

它在执行操作后检查结果，而while则是执行前进行检查。

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE proc5 ()  

1.      -> begin   

1.      -> declare v int;  

1.      -> set v=0;  

1.      -> repeat  

1.      -> insert into t values(v);  

1.      -> set v=v+1;  

1.      -> until v>=5  

1.      -> end repeat;  

1.      -> end;  

1.      -> //  

1. mysql > DELIMITER ;  

 



Ⅲ. loop ·····end loop:

loop循环不需要初始条件，这点和while 循环相似，同时和repeat循环一样不需要结束条件, leave语句的意义是离开循环。

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE proc6 ()  

1.      -> begin 

1.      -> declare v int;  

1.      -> set v=0;  

1.      -> LOOP_LABLE:loop  

1.      -> insert into t values(v);  

1.      -> set v=v+1;  

1.      -> if v >=5 then 

1.      -> leave LOOP_LABLE;  

1.      -> end if;  

1.      -> end loop;  

1.      -> end;  

1.      -> //  

1. mysql > DELIMITER ;  

 

 

Ⅳ. LABLES 标号：

标号可以用在begin repeat while 或者loop 语句前，语句标号只能在合法的语句前面使用。可以跳出循环，使运行指令达到复合语句的最后一步。

 

(4). ITERATE迭代

Ⅰ. ITERATE:

通过引用复合语句的标号,来从新开始复合语句

1. mysql > DELIMITER //  

1. mysql > CREATE PROCEDURE proc10 ()  

1.      -> begin 

1.      -> declare v int;  

1.      -> set v=0;  

1.      -> LOOP_LABLE:loop  

1.      -> if v=3 then   

1.      -> set v=v+1;  

1.      -> ITERATE LOOP_LABLE;  

1.      -> end if;  

1.      -> insert into t values(v);  

1.      -> set v=v+1;  

1.      -> if v>=5 then 

1.      -> leave LOOP_LABLE;  

1.      -> end if;  

1.      -> end loop;  

1.      -> end;  

1.      -> //  

1. mysql > DELIMITER ; 

 

 

9.      MySQL存储过程的基本函数

 

(1).字符串类

CHARSET(str) //返回字串字符集

CONCAT (string2 [,... ]) //连接字串

INSTR (string ,substring ) //返回substring首次在string中出现的位置,不存在返回0

LCASE (string2 ) //转换成小写

LEFT (string2 ,length ) //从string2中的左边起取length个字符

LENGTH (string ) //string长度

LOAD_FILE (file_name ) //从文件读取内容

LOCATE (substring , string [,start_position ] ) 同INSTR,但可指定开始位置

LPAD (string2 ,length ,pad ) //重复用pad加在string开头,直到字串长度为length

LTRIM (string2 ) //去除前端空格

REPEAT (string2 ,count ) //重复count次

REPLACE (str ,search_str ,replace_str ) //在str中用replace_str替换search_str

RPAD (string2 ,length ,pad) //在str后用pad补充,直到长度为length

RTRIM (string2 ) //去除后端空格

STRCMP (string1 ,string2 ) //逐字符比较两字串大小,

SUBSTRING (str , position [,length ]) //从str的position开始,取length个字符,

注：mysql中处理字符串时，默认第一个字符下标为1，即参数position必须大于等于1 

 

1. mysql> select substring('abcd',0,2);  

1. +-----------------------+  

1. | substring('abcd',0,2) |  

1. +-----------------------+  

1. |                       |  

1. +-----------------------+  

1. 1 row in set (0.00 sec)  

1.  

1. mysql> select substring('abcd',1,2);  

1. +-----------------------+  

1. | substring('abcd',1,2) |  

1. +-----------------------+  

1. |     ab                |  

1. +-----------------------+  

1. 1 row in set (0.02 sec)  

TRIM([[BOTH|LEADING|TRAILING] [padding] FROM]string2) //去除指定位置的指定字符

UCASE (string2 ) //转换成大写

RIGHT(string2,length) //取string2最后length个字符

SPACE(count) //生成count个空格

(2).数学类

ABS (number2 ) //绝对值

BIN (decimal_number ) //十进制转二进制

CEILING (number2 ) //向上取整

CONV(number2,from_base,to_base) //进制转换

FLOOR (number2 ) //向下取整

FORMAT (number,decimal_places ) //保留小数位数

HEX (DecimalNumber ) //转十六进制

注：HEX()中可传入字符串，则返回其ASC-11码，如HEX('DEF')返回4142143

也可以传入十进制整数，返回其十六进制编码，如HEX(25)返回19

LEAST (number , number2 [,..]) //求最小值

MOD (numerator ,denominator ) //求余

POWER (number ,power ) //求指数

RAND([seed]) //随机数

ROUND (number [,decimals ]) //四舍五入,decimals为小数位数]

注：返回类型并非均为整数，如：

(1)默认变为整形值

1. mysql> select round(1.23);  

1. +-------------+  

1. | round(1.23) |  

1. +-------------+  

1. |           1 |  

1. +-------------+  

1. 1 row in set (0.00 sec)  

1.  

1. mysql> select round(1.56);  

1. +-------------+  

1. | round(1.56) |  

1. +-------------+  

1. |           2 |  

1. +-------------+  

1. 1 row in set (0.00 sec) 





(2)可以设定小数位数，返回浮点型数据

1. mysql> select round(1.567,2);  

1. +----------------+  

1. | round(1.567,2) |  

1. +----------------+  

1. |           1.57 |  

1. +----------------+  

1. 1 row in set (0.00 sec) 

SIGN (number2 ) //

 

(3).日期时间类

ADDTIME (date2 ,time_interval ) //将time_interval加到date2

CONVERT_TZ (datetime2 ,fromTZ ,toTZ ) //转换时区

CURRENT_DATE ( ) //当前日期

CURRENT_TIME ( ) //当前时间

CURRENT_TIMESTAMP ( ) //当前时间戳

DATE (datetime ) //返回datetime的日期部分

DATE_ADD (date2 , INTERVAL d_value d_type ) //在date2中加上日期或时间

DATE_FORMAT (datetime ,FormatCodes ) //使用formatcodes格式显示datetime

DATE_SUB (date2 , INTERVAL d_value d_type ) //在date2上减去一个时间

DATEDIFF (date1 ,date2 ) //两个日期差

DAY (date ) //返回日期的天

DAYNAME (date ) //英文星期

DAYOFWEEK (date ) //星期(1-7) ,1为星期天

DAYOFYEAR (date ) //一年中的第几天

EXTRACT (interval_name FROM date ) //从date中提取日期的指定部分

MAKEDATE (year ,day ) //给出年及年中的第几天,生成日期串

MAKETIME (hour ,minute ,second ) //生成时间串

MONTHNAME (date ) //英文月份名

NOW ( ) //当前时间

SEC_TO_TIME (seconds ) //秒数转成时间

STR_TO_DATE (string ,format ) //字串转成时间,以format格式显示

TIMEDIFF (datetime1 ,datetime2 ) //两个时间差

TIME_TO_SEC (time ) //时间转秒数]

WEEK (date_time [,start_of_week ]) //第几周

YEAR (datetime ) //年份

DAYOFMONTH(datetime) //月的第几天

HOUR(datetime) //小时

LAST_DAY(date) //date的月的最后日期

MICROSECOND(datetime) //微秒

MONTH(datetime) //月

MINUTE(datetime) //分返回符号,正负或0

SQRT(number2) //开平方

