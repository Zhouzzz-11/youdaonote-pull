1.os模块，os 模块提供了一些基本的系统操作函数

var os = require("os")



2.path 模块提供了一些用于处理文件路径的小工具

var path = require("path")

e.g

path.join([path1][, path2][, ...])

用于连接路径。该方法的主要用途在于，会正确使用当前系统的路径分隔符，Unix系统是"/"，Windows系统是"\"。



path.resolve([from ...], to)

将 to 参数解析为绝对路径，给定的路径的序列是从右往左被处理的，后面每个 path 被依次解析，直到构造完成一个绝对路径。 例如，给定的路径片段的序列为：/foo、/bar、baz，则调用 path.resolve('/foo', '/bar', 'baz') 会返回 /bar/baz。



3.dotenv 貌似是用来读取.env文件的

const dotenv = require('dotenv')



4.moment模块，设置时间格式

const Moment = require('moment');

const myDate = Moment.utc().format('YYYYMMDD');

YYYY-如2014

MM-如09

DD-如31



5.const let var变量

var关键字定义的变量可以先使用后声明。

let关键字定义的变量需要先声明再使用。

const关键字定义的常量，声明时必须进行初始化，且初始化后不可再修改。

// 错误写法
const PI;
PI = 3.14159265359;

// 正确写法
const PI = 3.14159265359;



使用var声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象；

使用let声明的变量，其作用域为该语句所在的代码块内，不存在变量提升；

使用const声明的是常量，在后面出现的代码中不能再修改该常量的值。



简单来说是： let是修复了var的作用域的一些bug，变的更加好用。let是更好的var。var的作用于是函数作用域，而let是块级别（大括号括起来的内容）

const声明的变量只可以在声明时赋值，不可随意修改，这是最大的特点



6.箭头函数=>

![](https://i.loli.net/2021/08/25/Rsp3Jn9SfAyDMNl.png)



