

[toc]

## 1.1 leaning-pytest



官方文档：https://docs.pytest.org/en/6.2.x/contents.html#toc

### mark标签：

在方法前加上：@pytest.mark.名称；运行时输入：$pytest -v 名称；则最后只会运行加了标志的方法

### test命名：

所有以test_开头的py文件都被当成了测试文件

所有测试文件中以test开头的方法被当成了测试用例执行

### 使用命令行选项

pytest --collect-only  搜集用例，只是搜集并不执行

pytest -k “表达式”  根据表达式内容匹配到包含该字段到用例

pytest -x  遇到断言失败就停止执行.有利于我们查找原因.

pytest -If If是last failed简称，可以直接过滤出最后一个失败的用例，每次解决问题之后，再次运行-If，省了再执行后面成功的用例

pytest -ff  ff是first failed简称，过滤出第一个失败的用例，每次解决问题后，还需要把前面已经成功的都要再跑一遍，与-If相反

pytest -v 在控制台输出更多的内容，最明显的区别是每个文件中的每个用例都各占一行（不用-v的则是每个文件占一行）

-q（--quiet）选项 与-v相反，会简化内容

pytest --tb=short 显示更详细的错误信息，具体到哪个文件哪个用例，哪个断言，哪个参数



### 执行指定函数

方法1      ::

pytest test1.py::test_func1

方法2      -k 模糊匹配

pytest -k func1 test1.py

方法3     给函数加标记

@pytest.mark.标记名

def test_func1():

      pass

pytest -m 标记名 test1.py

### 跳过指定函数

加标记@pytest.mark.skip(reason=‘选填备注‘）

### 预见错误

加标记@pytest.mark.xfail(reason=‘选填备注‘）

若实际通过，则结果xpass；若实际失败，则结果xfail

### 参数化

加标记@pytest.mark.parametrize(argnames,argvalues)

### fixture固件

加标记@pytest.fixture(scope=‘以下几种‘）

* function: 函数级，每个测试函数都会执行一次固件，默认；

* class: 类级别，每个测试类执行一次，所有方法都可以使用；

* module: 模块级，每个模块执行一次，模块内函数和方法都可使用；

* session: 会话级，一次测试只执行一次，所有被找到的函数和方法都可用。

fixture固件：也可以用来做数据的依次加载使用，在准备测试数据和初始化测试对象的阶段

在用于解析数据的方法前，@pytest.fixture

参数化fixture：给定一个params，@pytest.fixture(params=["smtp.gmail.com", "mail.python.org"])len(params)的值就是用例执行的次数

- 重命名：@pytest.fixture(name='NAME')，固件的名称默认为定义时的函数名，如果不想使用默认，可以通过 name 选项指定名称

### yield 

关键字之前的代码属于预处理，之后的属于后处理

### autouse 

自动执行 





## 1.2 Error 汇总

1. RecursionError: maximum recursion depth exceeded

自己调用自己







