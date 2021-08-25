

1.写一个shell脚本

打开文本编辑器(可以使用 vi/vim 命令来创建文件)，新建一个文件 test.sh，扩展名为 sh（sh代表shell）

![](https://i.loli.net/2021/08/25/gZ87ElM9yYthXqw.png)

#! 是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种 Shell。

echo 命令用于向窗口输出文本。



2.运行一个shell脚本

1）作为可执行程序

![](https://i.loli.net/2021/08/25/aRAxDWHXvtp1duy.png)

2）作为解释器参数

![](https://i.loli.net/2021/08/25/sLYxXDio78jzPUR.png)

直接运行解释器，其参数就是 shell 脚本的文件名，这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。



3.变量

1）定义变量

命名规则：

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。

- 中间不能有空格，可以使用下划线（_）。

- 不能使用标点符号。

- 不能使用bash里的关键字（可用help命令查看保留关键字）。



2）使用变量

使用一个定义过的变量，只要在变量名前面加美元符号即可，变量名外面的花括号是可选的，加不加都行，推荐给所有变量加上花括号，这是个好的编程习惯。已定义的变量，可以被重新定义。

![](https://i.loli.net/2021/08/25/97XzimdWTRp1qBZ.png)



4.字符串

字符串可以用单引号，也可以用双引号，也可以不用引号

1）单引号

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；

- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

2）双引号

- 双引号里可以有变量

- 双引号里可以出现转义字符

![](https://i.loli.net/2021/08/25/5BJTfo1UnXgNI8p.png)



5.传递参数

格式：$n

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"参数处理"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"说明"},{"value":"$1","inlineStyles":{"font-family":[{"from":0,"to":2,"value":"Tahoma"}]}},{"value":"n为数字，代表执行的第n个参数"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"$#"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"传递到脚本的参数个数"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"$*"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"以一个单字符串显示所有向脚本传递的参数。\n如\"$*\"用「\"」括起来的情况、以\"$1 $2 … $n\"的形式输出所有参数。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"$$"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"脚本运行的当前进程ID号"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"$!"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"后台运行的最后一个进程的ID号"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"$@"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"与$*相同，但是使用时加引号，并在引号中返回每个参数。\n如\"$@\"用「\"」括起来的情况、以\"$1\" \"$2\" … \"$n\" 的形式输出所有参数。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"$-"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"显示Shell使用的当前选项，与set命令功能相同。","inlineStyles":{"underline":[{"from":16,"to":21,"value":true}],"font-size":[{"from":16,"to":21,"value":13}],"color":[{"from":16,"to":21,"value":"#006600"}],"href":[{"from":16,"to":21,"value":"https://www.runoob.com/linux/linux-comm-set.html"}]}},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"$?"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。"}],"heights":[40,40,40,40,40,40,40,40,40],"widths":[417,417]}
```

参考地址：https://www.runoob.com/linux/linux-shell-passing-arguments.html



6.数组



7.基本运算符

- 算术运算符

原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用。

![](https://i.loli.net/2021/08/25/BG2StgHQPNbzT6p.png)



![](https://i.loli.net/2021/08/25/xNh7JMPeTSYZH49.png)

- 关系运算符

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"运算符"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"说明"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"举例"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"-eq"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"检测两个数是否相等，相等返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"[ $a -eq $b ] 返回 false。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"-ne"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"检测两个数是否不相等，不相等返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"[ $a -ne $b ] 返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"-gt"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"检测左边的数是否大于右边的，如果是，则返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"[ $a -gt $b ] 返回 false。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"-lt"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"检测左边的数是否小于右边的，如果是，则返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"[ $a -lt $b ] 返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"-ge"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"检测左边的数是否大于等于右边的，如果是，则返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"[ $a -ge $b ] 返回 false。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"-le"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"检测左边的数是否小于等于右边的，如果是，则返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"[ $a -le $b ] 返回 true。"}],"heights":[40,40,40,40,40,40,40],"widths":[278,278,278]}
```

- 布尔运算符

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"运算符"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"说明"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"举例"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"!"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"非运算，表达式为 true 则返回 false，否则返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"[ ! false ] 返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"-o"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"或运算，有一个表达式为 true 则返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"[ $a -lt 20 -o $b -gt 100 ] 返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"-a"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"与运算，两个表达式都为 true 才返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"[ $a -lt 20 -a $b -gt 100 ] 返回 false。"}],"heights":[40,40,40,40],"widths":[278,278,278]}
```

- 字符串运算符

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"运算符"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"说明"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"举例"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"="},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"检测两个字符串是否相等，相等返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"[ $a = $b ] 返回 false。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"!="},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"检测两个字符串是否相等，不相等返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"[ $a != $b ] 返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"-z"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"检测字符串长度是否为0，为0返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"[ -z $a ] 返回 false。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"-n"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"检测字符串长度是否不为 0，不为 0 返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"[ -n \"$a\" ] 返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"$"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"检测字符串是否为空，不为空返回 true。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"[ $a ] 返回 true。"}],"heights":[40,40,40,40,40,40],"widths":[278,278,278]}
```



8.echo

显示结果至定向文件：echo "It is a test" > myfile



9.循环

![](https://i.loli.net/2021/08/25/PaJFHksOnMR2Nof.png)



![](https://i.loli.net/2021/08/25/haNp1iWRZmlLF7P.png)

无限循环for (( ; ; ))

![](https://i.loli.net/2021/08/25/YxyVlSMqK1zBuow.png)

case循环：

![](https://i.loli.net/2021/08/25/hrTm3xPXdSws7al.png)

每一模式必须以右括号结束。取值可以为变量或常数。匹配发现取值符合某一模式后，其间所有命令开始执行直至 ;;。如果无一匹配模式，使用星号 * 捕获该值，再执行后面的命令。

![](https://i.loli.net/2021/08/25/GMKEr4ZQ3fwCVDj.png)

跳出循环：break和continue



10.重定向

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"命令"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"#8db3e5","value":"说明"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"command > file"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"将输出重定向到 file。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"command < file"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"将输入重定向到 file。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"command >> file"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"将输出以追加的方式重定向到 file。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"n > file"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"将文件描述符为 n 的文件重定向到 file。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"n >> file"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"将文件描述符为 n 的文件以追加的方式重定向到 file。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"n >& m"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"将输出文件 m 和 n 合并。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"n <& m"},{"textAlign":"left","verticalAlign":"top","wrap":true,"value":"将输入文件 m 和 n 合并。"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"<< tag"},{"textAlign":"left","verticalAlign":"top","wrap":true,"backColor":"rgb(246, 244, 240)","value":"将开始标记 tag 和结束标记 tag 之间的内容作为输入。"}],"heights":[40,40,40,40,40,40,40,40,40],"widths":[277,557]}
```



11.文件包含

在test2.sh中使用test1.sh，在2文件中“使用 . 号来引用test1.sh 文件“       . ./test1.sh



12.注释

# 单行注释



:<<!
# 多行注释
！



13.Shell重定向 >、＆>file、2>&1、1>&2 、/dev/null

0代表标准输入，1代表标准输出，2代表标准错误

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"value":">","inlineStyles":{"font-family":[{"from":0,"to":1,"value":"Tahoma"}]}},{"value":"默认为标准输出重定向，与1>相同"},{"value":"＆>file"},{"value":"把标准输出和标准错误都重定向到文件file中"},{"value":"2>&1"},{"value":"把标准错误重定向到标准输出"},{"value":"/dev/null"},{"value":"是一个文件，所有传给他的东西他都会丢弃掉"}],"heights":[40,40,40,40],"widths":[103,517]}
```



