参考文档：https://segmentfault.com/a/1190000007535316#comment-area



async函数返回的是一个promise对象

![](https://i.loli.net/2021/08/25/hg7196fMR8vGjVc.png)



![](https://i.loli.net/2021/08/25/Qw5RncgFGr3KibL.png)



async/await的优势在于处理then链，因为async函数返回的是一个promise对象，而promise对象需要用then链来处理，await的优势就是比then处理看起来结构简明，层次清晰

