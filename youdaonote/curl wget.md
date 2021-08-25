wget是个专职的下载利器，简单，专一，极致；

curl可以下载，但是长项不在于下载，而在于模拟提交web数据，POST/GET请求，调试网页，等等。



1. curl -o x.log "http://www.yyyy.com" --speed-time 5 --speed-limit 1

是说将url内容保存到x.log中, 如果传输速度小于1字节/秒的状态持续5秒,该连接就会终止.



2.curl -s -w "%{http_code}" 'url' -o /dev/null

仅获取相应码



/dev/null（或称空设备）在类Unix系统中是一个特殊的设备文件，它丢弃一切写入其中的数据（但报告写入操作成功），读取它则会立即得到一个EOF。 在程序员行话，尤其是Unix行话中， /dev/null 被称为比特桶或者黑洞.

![](https://i.loli.net/2021/08/25/3kUM8Qruo4gzhKq.png)



