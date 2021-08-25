Linux常用命令的使用：

--与DOS存在部分命令相同，例如：dir    cd    mkdir   rmdir

linux操作的注意事项：

1.所有的Linux操作都区分大小写，并且Linux命令全部都是小写的

2.从操作的角度，我们都是：    命令   -[参数]   [操作对象]    中间有空格，而且一定要注意空格

3.在学习Linux过程中，一定要结合英文单词

目录操作命令：

列表显示文件夹内容：ls   -->   list

常见的参数：

-a   显示所有文件，包含隐藏文件。     all

-l    显示文件，并且包含详细信息，以长格式显示。		long

-t    按照时间反序显示文件     time

我们最常见的一组操作是：    ls  -alt

有时候，我们想不改变路径，直接查看某个目录下的文件。   ls    /usr

我们想查看目录是否存在某个文件，比如查看是否存在windows的文件。    ls  win*

在Linux的使用中，最常见的一个操作是：ls  -l 因为要长格式显示，该操作可以简化为：   ll

在Linux中，查看IP地址的命令为：  ifconfig

查看某个命令是的位置：   whereis  命令名称

环境变量：给系统设置一个搜索范围，我执行某个命令如果这个命令不在当前目录下，就需要去那个所谓的搜索范围下去查看，看是否存在这个命令，如果存在则执行。

export   PATH = $PATH:\sbin

Linux操作的清除屏幕的命令：  clear

远程操作Linux：

1.远程就是操作别人的电脑，让别人的电脑执行我们的操作。我们的Linux系统是作为服务器而出现的，那么我们就需要远程连接和操作Linux服务器。

2.远程操作的工具，常见的有：   SecureCRT和Xshell

3.远程连接，必须要知道Linux的IP、用户名，密码

更换IP地址：如果IP地址有问题，处理方案如下：

1.在虚拟机-->设置-->网络适配器中，将网络连接方式进行修改。

2.在Linux终端里，设置为root账号登录：    su  root

3.输入  service  network  restart   来重启网络服务

cd 切换工作路径，切换目录：

1. 切换到根目录，  cd   /

2.切换到上一级目录     cd   ..

3.切换到上一次操作的目录     cd  -

4.切换到用户的home目录       cd   ~

要切换路径，就必须先知道自己所在的路径是哪里。   pwd    =   present  working  directory

小操作练习：

1.查看当前工作路径在哪里

2.然后再切换到根目录

3.然后再切换到/etc/sysconfig/network-scripts

4.查看这个目录是否存在ifcfg-eth0文件

创建文件夹：   mkdir		删除目录：  rmdir 

小练习：

1.切换到你的用户home目录       		cd  ~

2.创建一个叫做administrator的目录	mkdir  administrator

3.进入到这个administrator的目录		cd ad[tab]

4.在里面创建一个ssd目录

5.将这个ssd目录删除掉

6.附加练习：一次性创建  hunan/changsha 

7.将changsha目录拷贝到上一层目录下		cp  -r  changsha  ..

文件操作系列：

创建文件：  touch		该命令看起来与创建文件并没有关系，所以记不住。

操作为：  touch  文件名，但是一定要注意文件名是有后缀的（扩展名）

也有拷贝文件，操作为   cp

有剪切，在Linux中叫做移动： mv   操作与cp相似

另外mv有重命名操作，就是移动到当前位置并改名。

删除文件：rm 其操作为：  rm   -[参数]  操作对象

-i   删除会给到用户提示，是否删除。默认也是这个

-f   强制删除，不会提示。  force

-r   递归操作，将这个文件夹下所有的文件和文件夹全部删除。

rmdir只能删除空目录，但是rm  -rf  目录名  可以删除非空目录。 

rm  -rf  / 		有种你试试

练习：

1.在administrator目录下，创建一个叫做Person.java文件

2.将这个Person.java文件复制到hunan/changsha目录下

3.为减少麻烦，将Person.java文件重命名为person.java

4.发现person.java不应该在hunan/changsha目录下，而应该在另外那个changsha目录下，应移动至changsha目录下。

5.为减少不必要的麻烦，将hunan目录删除掉。

查找文件：find

在电脑中查找文件，或者是说在文件夹中进行查找文件。

find  位置  -name 文件名  -type f

-name  是按文件名进行查找

-type 是按文件类型进行查找，f是普通文件，d是文件夹

小练习：

在Linux中查找 stdio.h的文件，并进入到这个文件所在的路径。

显示文件的内容：cat命令

想不想知道stdio.h这个文件里面的内容？

其操作  cat   文件名称

-n  是显示行号  number

统计行数： wc		word  count 

操作为：  wc  文件名称

会显示三个数据：   行数   单词数   字符数

权限提升：

1.切换一个具有更高权限的账号，  su   root 

2.sudo，让这个操作在管理员身份下运行

我想知道这个stdio.h文件有多少行内容？

只查看文件的前面若干行：head

操作为：   head   -行数   文件名称

有显示文件的前面若干行，就有显示文件的后面若干行：  tail 

操作为：  tail  -行数  文件名称

在工作中，可能会出现这样的情况：我执行了一个操作，系统要把操作的结果保存到文件中，我要查看文件的内容，这个操作是：   tail   -f   文件名称      叫做监控日志信息

有显示文件前面，有显示后面，理论上有显示中间若干行。

head  -100  文件名称  |  tail  -50

1.查看文件stdio.h的前50行，并显示行号   		cat  -n  stdio.h | head  -50

2.查看stdio.h的50~100行，并显示行号			cat -n stdio.h|head -100 |tail -50

在文件中查找内容，如果找到了相关的内容，就将整行内容进行显示。

grep  -->   grep  要查找的内容   文件

-n  显示行号

例如我们要在stdio.h中查找包含include的行信息，而且我还想知道查询出来的这些内容分别是属于哪一行的。

在stdio.h中查询包含数字的行，我们需要使用到正则表达式。正则表达式，需要使用-E的作为参数。

正则表达式的使用：

内容表示：[内容]，如果是单个内容，则用逗号分隔，例如：[1,2]。如果是连续内容，则用减号连接，例如：[1-9]

然后，我想查找包含4位数字的内容[0-9]，在这里次数用大括号表示{4}表示4次

前面是4个数字，后面也有4个数字，中间是任意内容的 . 表示任意内容， * 表示任意次数

只以#$%开头的行，显示出来。^[#$%] 。如果是结尾，则用[0-9]$

不以#开头的行，对内容取非。^[^#]

文件编辑： vi		这个相当于windows中的记事本

在vi中有三大操作： 插入操作   文件操作   编辑操作

新建打开：vi  文件名

直接vi是打开一个无标题的文本编辑器。

vi 不存在的文件，是创建并打开一个文件。

vi 存在的文件，是通过文本编辑器打开一个文件

保存和退出：

在文本编辑器里面，按esc键后再输入:wq!  w=write写入（保存） q=quit（退出） !表示强制

插入模式：

要能够输入内容，则需要进入insert模式，输入 i 再进行操作即可。其实输入I也可以，还有输入A或者a也可以进入输入模式，但它们有区别。

百度：linux  mac地址与预期不符的解决方案。

vi的编辑操作：需要在esc模式下进行操作

1.复制操作，如果我要将整行内容进行复制    yy

2.粘贴操作，会在光标的后面粘贴复制的内容。 paste  取p

3.撤销操作：其操作为u 英文是  undo

4.删除操作：其英文为delete，所以操作为dd，如果是删除1个单词则用dw

5.剪切操作：我所知道的是剪切1个字符，用x

6.查找，这个是在vi中查找内容，其操作为：    /内容

7.查找下一个为：   next --> 取n   如果是查找上一个？用shift+n

8.上面6的查找是从上往下查找，如果要从下往上查找，则用 ?内容

9.转到多少行，输入   行数G    可能会出现文件第XX行出错了。

在vi中可以显示行号，操作为     :set nu  如果我不想显示行号了，怎么处理？

Linux在测试工作中的作用：

1.测试结果可能会保存在日志中，需要查看日志。

4种方式：全部查看，内容在日志前面，内容在日志后面，查找特定关键字的内容

2.有时候会在Linux中埋数据（vi）

3.要进行测试，必须要有系统，所以我们需要搭建系统。

more和less：

都是分页查看文件的内容。其操作为：  more  文件名称

文件权限RWX：

[qianli@localhost ~]$ ll

总用量 12

drwxr-xr-x  2 qianli qianli 4096  4月 23 18:41 Desktop

drwxrwxr-x  2 qianli qianli 4096  4月 23 19:20 ssd

-rw-------  1 qianli qianli   54  4月 24 02:16 wd.txt

-rw-------  1 qianli qianli    0  4月 23 19:32 windows.doc

在结果第2位开始到第10位有三段rwx的内容，表示文件的权限。

rwx：分别表示read,write,execute

有三段rwx：第一段表示当前user的权限，第二段表示所属组group的权限，第三段表示其他用户other的所有权限

修改文件拥有者：chown  -->  change  owner

其操作为：  chown   用户名   文件名

修改文件的权限：chmod   -->   change  modify

其操作为：  chmod   +权限   文件名

具体只加部分权限：u   g   o		所以就会产生：  ugo+rwx  root.txt

权限也可以使用数字来表示：

rwx		111		4+2+1

1		1

10		2

100		4

常见的数字权限有：  777	755		751		644

练习：

1.用root账号创建一个叫做root.txt的文件，查看其权限

touch  root.txt

2.设置这个root.txt文件的权限为-rw-r--r--

ll

3.切换至普通用户，进行追加内容。  whoami  >> root.txt

su qiusuo

whoami  >> root.txt			查看当前登录用户

4.以上会报错权限不够，我们通过修改文件所有者设置root.txt的所有者为普通用户

su - root

chown  qiusuo  root.txt

5.再一次使用普通用户登录，进行追加内容，执行：   whoami  >>  root.txt

whoami  >>  root.txt		这一次会成功

6.最后使用root账号，将root.txt文件的权限设置为-rwxrwxrwx

su root

chmod  +rwx  root.txt

在Linux下搭建测试环境：

在Linux系统中，没有exe可执行文件，它的可执行文件有：   rpm   bin

bin文件是一种二进制文件，通过   ./xxx.bin

.rpm的安装：rpm  -ivh  xxx.rpm	-i  -->  install   -v  -->  view

卸载：  rpm  -e  应用程序名

查询要卸载的应用程序名称：		rpm  -qa  程序名称的一部分

升级软件：	rpm  -Uvh  xx.rpm

软件不仅有可执行文件，还有绿色软件（压缩软件），就会涉及到压缩与解压缩操作：

我们在Linux下常见的压缩文件有：zip,gz,tar

.zip  ：  我们可以将一个文件或文件夹压缩成.zip文件，

其操作为：  zip  压缩后的文件命名   要压缩的文件

解压缩.zip文件，操作为：   unzip   要解压缩的文件名称

gzip：压缩文件    gzip  要压缩的文件名称		-->会产生一个.gz文件

如果要解压缩gz文件，其操作为：   gunzip  stdio.h.gz

将多文件打包成一个文件，命令为：  tar

其操作为：tar  -cvf 打包后的文件名称.tar   要打包的文件

-c  -->  create		创建，新建（new），建立（build）

-v  -->  view   可视模式下

-f   -->  format	文件格式，需要手工输入打包后的文件名称

如果要解压缩，则使用-x作为参数

其操作为：  tar  -xvf  要解压缩的文件名称

一般打包之后还会进行压缩操作，所以我们希望能够一步完成。

参数 -z  是解决gz文件的

其操作为：  tar  -zcvf  xx.tar.gz   要打包的文件名称

对于压缩文件而言，最多的操作是：将xx.tar.gz文件进行解压缩

解压缩操作为：  tar  -zxvf  xx.tar.gz

小练习：

1.在系统中，查找stdio.h文件，并将这个文件拷贝到/home/qiusuo/下

find  /  -type f  -name stdio.h

cd 

cp stdio.h  /home/qiusuo

2.切换到/home/qiusuo/下，将stdio.h文件压缩为stdio.zip文件

cd  /home/qiusuo/

zip  stdio.zip   stdio.h

3.移动stdio.zip到一个新的目录下，将其解压缩。

mv  stdio.zip   /home/hunan

unzip  stdio.zip	//	zip  -d  stdio.zip

4.将stdio.h文件压缩为stdio.h.gz文件，比较gz压缩与zip压缩的压缩比

gzip  stdio.h

5.解压缩stdio.h.gz文件

gunzip  stdio.h.gz

6.复制stdio.h的第50~100行的内容到stdio.cp文件中

head -100  stdio.h | tail -50  > stdio.cp

7.将stdio.h和stdio.cp文件一起进行压缩为gz文件

tar  -cvf  stdio.tar  stdio.h  stdio.cp

解压缩之后的文件，我们还需要进行安装：

1.配置，因为要将源程序与Linux系统结合起来   ./configure

2.源程序需要经过编译，编译操作为：   make

3.经过了编译，才真正意义上安装：   make  install 

安装成功之后，可能需要启动程序：

启动程序：其实就是运行程序		./程序名称

通过应用程序名称：   ./应用程序名称   start|stop|restart

我们启动的程序，可以在任务管理器被查看到。

ps  -ef			ps  -aux

查看进程一般我们会筛选并显示我们所关心的那些进程

ps  -ef | grep  "进程名"

我现在要关闭一个应用程序，所做的操作是：  ./应用程序名称   stop

我们需要验证这个应用程序是否成功关闭，这个操作：ps -ef | grep "keyword"

强制杀死进程：  kill  -9   进程编号 | 进程名称

网络命令：

查看Linux的IP地址：	ifconfig  	有一个-a的参数，all

设置ip地址的命令为：   netconfig

激活网络设备的命令：   service  network  start|stop|restart

查看网络连通性：ping  192.168.3.112  -c 5

查看端口：	netstat  -ano|grep "80"	我们查看哪个应用程序占用了80端口

export这是将环境变量启动的命令。设置环境变量的操作是：export  PATH=$PATH:/sbin

测试环境搭建：

我们在企业中比较常见的环境是：WEB系统（B/S系统）

动态网页：我们同一个URL，在不同的操作中，会产生不同的结果。

服务器端的配置：

1.网页的源代码	-->		phpwind(htdocs)

2.数据库以及基础数据		-->	Mysql，导入数据的操作

3.源代码没有办法通过浏览器直接打开，需要有一个容器去运行它，这个容器叫做WEB服务器，常见的有：Apache、Tomcat、Nginx、IIS、Weblogic

4.因为网页的源代码根据编程语言的不同而不同，常见的编程语言有：php、jsp、asp。所以要识别其中的内容需要有对应的编程语言的编译器，例如：php解析器、jsp-->jdk、.net framework

























