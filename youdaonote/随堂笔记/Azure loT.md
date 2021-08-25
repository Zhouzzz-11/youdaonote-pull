architecture and the implementation technology choices for how to build loT

warm storage （recent data)/ cold storage(historic data)---machine learning about telemetry data--user management

设备 ，云网关，存储器 ，可视化界面



Storage： Azure service to store：

1）warm storage：Azure Cosmos DB--the best for scenarios that do not require queries（recommend）

                                 Azure SQL DB--the best for datasets that require relational storage and query capabilities

2）cold storage：Azure Blob Storage--available in all Azure regions. It is highly scalable（recommend）

                               Azure Data Lake--big data analytics and/or unlimited storage are required.

3）warm storage VS cold storage：

- hot data requires the fastest and most expensive storage because it’s accessed more frequently, and cold (or cooler) data that is accessed less frequently can be stored on slower, and consequently, less expensive media.

- Hot storage is data that needs to be accessed right away

- Cold data is data that is accessed less frequently and also doesn’t require the fast access of warmer data. That includes data that is no longer in active use and might not be needed for months, years, decades, or maybe ever. 

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"mergeHeight":1,"mergeWidth":4,"verticalAlign":"middle","value":"Traditional Views of Cold and Hot Data Storage","inlineStyles":{"font-family":[{"from":0,"to":46,"value":"Verdana"}]}},{"mergePointDX":1,"mergePointDY":0,"value":""},{"mergePointDX":2,"mergePointDY":0,"value":""},{"mergePointDX":3,"mergePointDY":0,"value":""},{"verticalAlign":"top","wrap":true,"value":""},{"verticalAlign":"top","wrap":true,"value":""},{"verticalAlign":"top","wrap":true,"value":"Cold","inlineStyles":{"font-family":[{"from":0,"to":4,"value":"Verdana"}]}},{"verticalAlign":"top","wrap":true,"value":"Hot","inlineStyles":{"font-family":[{"from":0,"to":3,"value":"Verdana"}]}},{"verticalAlign":"middle","wrap":true,"value":""},{"verticalAlign":"middle","wrap":true,"value":""},{"verticalAlign":"middle","wrap":true,"value":"","resource":"CD05629F4D9945548BA4DE459FD00AAD"},{"verticalAlign":"middle","wrap":true,"value":"","resource":"349C45A931ED4CC7AC3BB863FC11E75D"},{"verticalAlign":"middle","value":""},{"textAlign":"left","verticalAlign":"middle","value":"Access Speed","inlineStyles":{"font-family":[{"from":0,"to":12,"value":"Verdana"}]}},{"verticalAlign":"middle","value":"Slow","inlineStyles":{"font-family":[{"from":0,"to":4,"value":"Verdana"}]}},{"verticalAlign":"middle","value":"Fast","inlineStyles":{"font-family":[{"from":0,"to":4,"value":"Verdana"}]}},{"verticalAlign":"middle","backColor":"rgb(248, 248, 248)","value":""},{"textAlign":"left","verticalAlign":"middle","backColor":"rgb(248, 248, 248)","value":"Access Frequency","inlineStyles":{"font-family":[{"from":0,"to":16,"value":"Verdana"}]}},{"verticalAlign":"middle","backColor":"rgb(248, 248, 248)","value":"Seldom or Never","inlineStyles":{"font-family":[{"from":0,"to":15,"value":"Verdana"}]}},{"verticalAlign":"middle","backColor":"rgb(248, 248, 248)","value":"Frequent","inlineStyles":{"font-family":[{"from":0,"to":8,"value":"Verdana"}]}},{"verticalAlign":"middle","value":""},{"textAlign":"left","verticalAlign":"middle","value":"Data Volume","inlineStyles":{"font-family":[{"from":0,"to":11,"value":"Verdana"}]}},{"verticalAlign":"middle","value":"Low","inlineStyles":{"font-family":[{"from":0,"to":3,"value":"Verdana"}]}},{"verticalAlign":"middle","value":"High","inlineStyles":{"font-family":[{"from":0,"to":4,"value":"Verdana"}]}},{"verticalAlign":"middle","backColor":"rgb(248, 248, 248)","value":""},{"textAlign":"left","verticalAlign":"middle","backColor":"rgb(248, 248, 248)","value":"Storage Media","inlineStyles":{"font-family":[{"from":0,"to":13,"value":"Verdana"}]}},{"verticalAlign":"middle","backColor":"rgb(248, 248, 248)","value":"Slower drives, LTO, offline","inlineStyles":{"font-family":[{"from":0,"to":27,"value":"Verdana"}]}},{"verticalAlign":"middle","backColor":"rgb(248, 248, 248)","value":"Faster drives, durable drives, SSDs","inlineStyles":{"font-family":[{"from":0,"to":35,"value":"Verdana"}]}},{"verticalAlign":"middle","value":""},{"textAlign":"left","verticalAlign":"middle","value":"Cost","inlineStyles":{"font-family":[{"from":0,"to":4,"value":"Verdana"}]}},{"verticalAlign":"middle","value":"Lower","inlineStyles":{"font-family":[{"from":0,"to":5,"value":"Verdana"}]}},{"verticalAlign":"middle","value":"Higher","inlineStyles":{"font-family":[{"from":0,"to":6,"value":"Verdana"}]}}],"heights":[50,40,40,50,50,50,50,50],"widths":[169,259,169,169]}
```







智能边缘设备 Azure loT Edge4 。  filed Gateway

物联网交叉应用

security5

日志监控logging and monitoring-operation management suite （OMS）

hyper-scale部署

灵活性

设备和数据模型：抽象式分离

数据记录和数据流：

       1）loT data stream术语：messages  events  telemetry遥测 。 alerts 。  ingestion 

       2）遥测记录telemetry会生成另一种类型的记录，称之为警报alerts

设备连接方式connect patterns：

       1）云网关

       2）现场网关，如蓝牙

       3）自定义云网关custom cloud gateway

       4）现场网关和自定义云网关，如VPN

Azure loT Hub is service enable communication from a variety of devices

客户端连接方式：

       1）通过代理连接agent

       2）通过客户端组件集成client component--use SDK

       3）直接连接connect directly



data flow----Lambda architecture

1）fast path：short- term critical information and actions, such as alarms.

2）slow path：multiple sources and over a longer period of time，such as reports, machine learning models, etc.



simple scenarios ： stateless processors and fairly static rules

one complex scenarios：stateful processors with dynamic analysis logic and reference data.



technology for loT visualization：

1）Azure App Service

2）Azure Time Series Insights (TSI)

3）Azure Notification Hubs

4）dashboards--Power BI

5）Azure Maps

6）Azure Active Directory (AAD)



monitoring and visualization solution：

1）Operations Management Suite (OMS)（recommend）

2）Elastic Stack

3）Splunk

