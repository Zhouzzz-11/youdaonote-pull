

[toc]





### 一、什么是RestFul架构：

　　（1）每一个URI代表一种资源；

　　（2）客户端和服务器之间，传递这种资源的某种表现层；

　　（3）客户端通过四个HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"。



### 二、RESTful架构有一些典型的设计误区：

- URI包含动词。因为"资源"表示一种实体，所以应该是名词，URI不应该有动词，动词应该放在HTTP协议中。（放做参数）

- 在URI中加入版本号，因为不同的版本，可以理解成同一种资源的不同表现形式，所以应该采用同一个URI。版本号可以在HTTP请求头信息的Accept字段中进行区分



### 三、RestFul API规范细节：



1. URI，资源，资源一般对应服务器端领域模型中的实体类

1. 小写，中杠

1. URI中的名词表示资源集合，使用复数形式

1. 资源集合：

```javascript
/zoos //所有动物园
/zoos/1/animals //id为1的动物园中的所有动物

```

            单个资源：

```javascript
/zoos/1 //id为1的动物园
/zoos/1;2;3 //id为1，2，3的动物园

```



1. 避免层级过深，尽量使用查询参数代替

1. 错误处理：

常用的http状态码及使用场景：

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"backColor":"#dce6f3","value":"状态码"},{"backColor":"#dce6f3","value":"使用场景"},{"value":"400 bad request"},{"value":"常用在参数校验"},{"value":"401 unauthorized"},{"value":"未经验证的用户，常见于未登录。如果经过验证后依然没权限，应该 403（即 authentication 和 authorization 的区别）"},{"value":"403 forbidden"},{"value":"无权限"},{"value":"404 not found"},{"value":"资源不存在"},{"value":"500 internal server error"},{"value":"非业务类异常"},{"value":"503 service unavaliable"},{"value":"由容器抛出，自己的代码不要抛这个异常"}],"heights":[40,40,40,40,40,40,40],"widths":[310,310]}
```



1. 状态码（Status Codes）

```javascript
200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。
201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。
202 Accepted - [*]：表示一个请求已经进入后台排队（异步任务）
204 NO CONTENT - [DELETE]：用户删除数据成功。
400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。
401 Unauthorized - [*]：表示用户没有权限（令牌、用户名、密码错误）。
403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的。
404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。
406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。
410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。
422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。
500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。

```



