1.去掉某列重复数据

db.getCollection('表名‘).distinct('name')  ----去掉name重复的数据

2，查询age=22

db.getCollection('表名‘).find({"age":22})

3.age>22

db.getCollection('表名‘).find({age:{$gt:22}})

4.age<22

db.getCollection('表名‘).find({age:{$lt:22}})

5.age>=22

db.getCollection('表名‘).find({age:{$gte:22}})

6.age>=22 and <=30

db.getCollection('表名‘).find({age:{$gte:22,$lte:26}})

7.查询name中包含abc的数据

db.getCollection('表名‘).find({age:/abc/})

8.age>22,name=abc

db.getCollection('表名‘).find({age:{$gt:22}},{name:abc})

9.排序

db.getCollection('表名‘).sort({age:1})升序

db.getCollection('表名‘).sort({age:-1})降序

10.查询总数

db.getCollection('表名‘).find({age:/abc/}).count()



查看磁盘：

```javascript
Bertram:PRIMARY> use Bertram
Bertram:PRIMARY> db.stats();
{
	"db" : "Bertram",	//当前数据库名
	"collections" : 28,     //当前数据库多少表
	"views" : 0,	
	"objects" : 303342925,	//当前数据库所有表多少条数据
	"avgObjSize" : 912.4506189883941,	//每条数据的平均大小
	"dataSize" : 276785439682,	//所有数据的总大小
	"storageSize" : 41067261952,	//所有数据占的磁盘大小 
	"numExtents" : 0,
	"indexes" : 100,	//索引数量
	"indexSize" : 97699581952,	//索引大小 
	"ok" : 1
}


```



默认单位：字节byte

可以通过传参数，比如：

如果想要返回kb：db.stats(1024);

如果想要返回MB：db.stats(1048576);

如果想要返回GB：db.stats(1073741824);

同理，查看单表的数据占用大小： db.History.stats(1073741824)



mongodb状态查询：参考地址：

https://www.cnblogs.com/SZxiaochun/p/6902531.html



