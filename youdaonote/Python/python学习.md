参考文档：https://www.jianshu.com/p/4edb3afaee00

*****表示新增内容



## 一、Python字符串

1.头下标:尾下标] 获取的子字符串包含头下标的字符，但不包含尾下标的字符。如：

例1：

>>> s = 'abcdef'
>>> s[1:5]
'bcde'

例2：

str = 'Hello World!'
 
print str           # 输出完整字符串
print str[0]        # 输出字符串中的第一个字符
print str[2:5]      # 输出字符串中第三个至第五个之间的字符串
print str[2:]       # 输出从第三个字符开始的字符串
print str * 2       # 输出字符串两次
print str + "TEST"  # 输出连接的字符串

print str[0:5:2]    #参数为截取的步长

Hello World!
H
llo
llo World!
Hello World!Hello World!
Hello World!TEST

Hlo

*****

输出带有单引号或双引号的字符？用转义符号\

例如，输出Let's go: 'Let\'s go'

输出带有反斜杠的字符？可以给每个反斜杠再加上转义字符（很麻烦），或者用r

例如，输出C:\data\env:r'C:\data\env'

note:用r的话 末尾不能再有\ 否则会报错 例如：C:\data\env\

*****



## 二、变量赋值

1。Python 中的变量赋值不需要类型声明。直接赋值：

counter = 100 # 赋值整型变量
miles = 1000.0 # 浮点型
name = "John" # 字符串

2。多变量赋值：

a = b = c = 1

或

a, b, c = 1, 2, "john"

****类型转换：int() float() str()

isinstance() type()获取类型信息:

eg.isinstance(12,int)>>true

   type(12)>>int

*****

## 三、列表list

列表中值的切割也可以用到变量 [头下标:尾下标] ，就可以截取相应的列表，从左到右索引默认 0 开始，从右到左索引默认 -1 开始，下标可以为空表示取到头或尾。

列表的数据项不需要具有相同的类型。

创建一个列表，只要把逗号分隔的不同的数据项使用方括号 [ ] 括起来即可。



list = [ 'runoob', 786 , 2.23, 'john', 70.2 ]
tinylist = [123, 'john']
 
print list               # 输出完整列表

...和字符串一致

*****

列表相加和字符串相加一致，而不是和数字列表那样把值做加法运算

list的加减乘除运算都是列表的扩张，而不是值的运算

*****

## 四、元组tuple（tup）

元组是另一个数据类型，类似于 List（列表）。

元组用 () 标识。内部元素用逗号隔开。但是元组不能二次赋值，相当于只读列表。元组与列表类似，不同之处在于元组的元素不能修改。

元组使用小括号 ( )，列表使用方括号。

tuple = ( 'runoob', 786 , 2.23, 'john', 70.2 )
tinytuple = (123, 'john')
 
print tuple               # 输出完整元组

*****

创建空元组：tuple()

创建只有一个元素的元组：tuple=(1,)或者 tuple=1, 必须要加，表示是元组，否则是int类型

更新和删除：通过切片来实现

eg.temp=(1,2,3,4)

temp=temp[:1]+("a")+temp[1:]

>>temp=(1,2,a,3,4)

*****

## 五、字典dictionary（dic）

列表是有序的对象集合，字典是无序的对象集合。

两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。

字典用"{ }"标识。字典由索引(key)和它对应的值value组成。

dict = {}
dict['one'] = "This is one"
dict[2] = "This is two"
 
tinydict = {'name': 'john','code':6734, 'dept': 'sales'}
 
 
print dict['one']          # 输出键为'one' 的值
print dict[2]              # 输出键为 2 的值
print tinydict             # 输出完整的字典
print tinydict.keys()      # 输出所有键
print tinydict.values()    # 输出所有值

This is one
This is two
{'dept': 'sales', 'code': 6734, 'name': 'john'}
['dept', 'code', 'name']
['sales', 6734, 'john']



## 六/条件控制语句

if 

else



## 七/循环语句

while循环

for循环



## 八/函数

函数代码块以 def 关键词开头，后接函数标识符名称和圆括号 ( )。

任何传入参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数。

函数的第一行语句可以选择性地使用文档字符串，用于存放函数说明。

函数内容以冒号起始，并且缩进。

return [表达式] 结束函数，选择性地返回一个值给调用方。不带表达式的 return 相当于返回 None。

def add(x):

    return x+1



## 九/模块（不同模块的函数调用）

模块是一个包含所有你定义的函数和变量的文件，其后缀名是.py。

模块可以被别的程序引入，以使用该模块中的函数等功能。这也是使用 python 标准库的方法。

示例代码如下：

编写文件 myfunction.py：

def add(x):
    return x + 10

引用该模块

import myfunction

print(myfunction.add(1)) # 11



## 十/类

class person:

      def __init__(self,name,age)

          self.name=name

__init__是构造函数，self相当于Java中的this



类中的私有变量怎么定义：不以下划线打头的变量是公有变量，任何代码都可以访问它们。

若要将age变成私有变量：

 self.__age=age

访问私有变量：

>>>p=person('hehe',30)

>>>p._person__age

对象名._类名__私有变量名



if __name__ = '__main__' :意思是当该文件被直接运行时，执行后续代码块，否则不执行

（参考地址：https://blog.csdn.net/yjk13703623757/article/details/77918633）



## 十一：函数

1.乘方：pow(4,3)

2.平方：

import numpy

numpy.square(4)

或者

pow(5,2)

 3.平方根：

import numpy

numpy.sqrt(16)

或者

pow(25, 0.5)



## 十二：特性

### 1.切片--取指定索引范围

>>> L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']

>>> L[0:3]
['Michael', 'Sarah', 'Tracy']

L[-1]取倒数第一个元素

字符串也同样可以使用

>>> 'ABCDEFG'[:3]
'ABC'



### 2.迭代--通过for循环来遍历这个list或tuple

dict类型：

>>> d = {'a': 1, 'b': 2, 'c': 3}
>>> for key in d:
...     print(key)
...
a
c
b



字符串类型：

for ch in 'ABC':
...     print(ch)
...
A
B
C



判断一个对象是否可迭代：

>>> from collections import Iterable
>>> isinstance('abc', Iterable) # str是否可迭代
True
>>> isinstance([1,2,3], Iterable) # list是否可迭代
True
>>> isinstance(123, Iterable) # 整数是否可迭代
False

note：整数不可迭代

Iterable 迭代器

generator 生成器

isinstance用法：判断类型返回布尔型true or false 。  isinstance(object,type)

>>> isinstance('abc', str) # 是否是str类型
True



### 3.列表生成式--for循环

比如计算平方数：

>>> L = []
>>> for x in range(1, 11):
...    L.append(x * x)
...
>>> L
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

利用列表生成式简化的形式:

>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]



### 4.生成器--generator

把列表生成式改变下形式：[] 变为（)

>>> g = (x * x for x in range(10))

g是一个generator

想要获取g的值？

1）通过next()函数获得generator的下一个返回值

>>> next(g)
0
>>> next(g)
1

2）for循环,生成器是可迭代对象

>>> g = (x * x for x in range(10))
>>> for n in g:
...     print(n)
... 
0
1
4
9
16
25
36
49
64
81

函数中包含yield关键字,那么该函数是一个generator

generator和函数的执行流程不一样。函数是顺序执行，遇到return语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。





### 5.迭代器

凡是可作用于for循环的对象都是Iterable类型；

凡是可作用于next()函数的对象都是Iterator类型，它们表示一个惰性计算的序列；

生成器都是Iterator对象，但list、dict、str虽然是Iterable，却不是Iterator，不过可以通过iter()函数获得一个Iterator对象。

>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter('abc'), Iterator)
True

note:

iter() 函数用来生成迭代器

>>>lst = [1, 2, 3]
>>> for i in iter(lst):
...     print(i)
... 
1
2
3

6.闭包

![](https://i.loli.net/2021/08/25/SlOyY3EpzC4ar9q.png)

FunY是一个闭包



![](https://i.loli.net/2021/08/25/o2eT1Rn3HKlSt5C.png)

nonlocal关键字：表示x不是全局变量

