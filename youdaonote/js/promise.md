

![](https://i.loli.net/2021/08/25/PK4j7HGYy2w8qTr.png)



![](https://i.loli.net/2021/08/25/EyR7IGg9U6l8VqJ.png)



![](https://i.loli.net/2021/08/25/lgEfq7KN6rsj5pM.png)



最后一个then方法，回调函数是console.log和console.error，用法上有一点重要的区别。console.log只显示step3的返回值，而console.error可以显示p1、step1、step2、step3之中任意一个发生的错误。举例来说，如果step1的状态变为rejected，那么step2和step3都不会执行了（因为它们是resolved的回调函数）。Promise 开始寻找，接下来第一个为rejected的回调函数，在上面代码中是console.error。这就是说，Promise 对象的报错具有传递性。

