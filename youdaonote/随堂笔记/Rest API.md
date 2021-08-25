1.定义：

          Rest API本质是利用http提供操作（get post put patch delete)等来实现某URL所代表资源的状态转移

2.设计原则和规范：

- 资源：文本可以用TXT，也可以用HTML或者XML、图片可以用JPG格式或者PNG格式，JSON是现在最常用的资源表现形式。

- 动作（Verbs）：get post put patch delete  

  GET（SELECT）：从服务器获取一个指定资源或一个资源集合；

  POST（CREATE）：在服务器上创建一个资源；

  PUT（UPDATE）：更新服务器上的一个资源，需要提供整个资源；

  PATCH（UPDATE）：更新服务器上的一个资源，只提供资源中改变的那部分属性；

  DELETE（DELETE）：移除服务器上的一个资源；

- 版本号：将API的版本号放入URL。如GET:http://www.xxx.com/v1/friend/123

- 端点：URL中用于标识一个特定资源或资源集合的那部分URL片段。如https://api.example.com/v1/zoos中的/zoos

- 过滤器：

如果记录数量很多，服务器不可能都将它们返回给用户。API应该提供参数，过滤返回结果。limit=10：指定返回记录的数量；page=2&per_page=100：指定第几页，以及每页的记录数。

- 状态码：

1XX  提示信息 - 表示请求已被成功接收，继续处理

2XX  成功 - 表示请求已被成功接收，理解，接受   常见的有：200

3XX  重定向 - 要完成请求必须进行更进一步的处理   302

4XX  客户端错误 -  请求有语法错误或请求无法实现   404

5XX  服务器端错误 -   服务器未能实现合法的请求    500

- 返回值文档

- HTTP包解析

- 幂等（Idempotent）：多次重复操作得到的结果一样；









