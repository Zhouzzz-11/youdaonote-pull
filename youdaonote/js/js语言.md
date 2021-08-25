一、运算符



1.“?:”条件运算符是唯一的一个三元运算符;

       一个表达式的布尔结果?表达式1(任意类型的任意值)：表达式2(任意类型的任意值);

　　根据第一个运算数的布尔值结果，如果为true，则执行第二个运算数表达式，返回第二个运算数表达式的值;如果第一个运算数的布尔值结果是false，则执行第三个运算数表达式，返回第三个运算数表达式的值。



二/ 变量



1.局部变量：定义在函数内，作用域只针对函数内部

2.全局变量：定义在函数外，作用域为所有函数



note：即使命名一致，它们也是两个不同的变量。修改其中一个，不会影响另一个的值。

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"textAlign":"left","verticalAlign":"middle","wrap":true,"value":"","resource":"AC88206449164C9F90169DC0C91E2038"},{"textAlign":"left","verticalAlign":"middle","wrap":true,"value":"变量声明时如果不使用 var 关键字，那么它就是一个全局变量，即便它在函数内定义。","inlineStyles":{"bold":[{"from":11,"to":14,"value":true}],"underline":[{"from":0,"to":41,"value":true}]}}],"heights":[34],"widths":[35,710]}
```

严格模式下，不允许使用未声明的变量 ‘use strict’；



三/闭包



一个计数器：

var add = (function () {
    var counter = 0;
    return function () {return counter += 1;}
})();
 
add();//返回1

变量add指定了函数自我调用的返回值， 这个叫作 JavaScript 闭包。它使得函数拥有私有变量变成可能。

如果表达式后面紧跟 () ，则会自动调用。

