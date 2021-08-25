配置文件语言：YAML

参考文档：http://www.ruanyifeng.com/blog/2016/07/yaml.html



一、语法规则

- 大小写敏感

- 使用缩进表示层级关系

- 缩进时不允许使用Tab键，只允许使用空格。

- 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可



二、数据结构

- 对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）

- 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）

- 纯量（scalars）：单个的、不可再分的值



1.对象

![](https://i.loli.net/2021/08/25/EcQ5GhrBuAyPtSw.png)

2.数组

![](https://i.loli.net/2021/08/25/yhtOKN2XfR8mbnr.png)



![](https://i.loli.net/2021/08/25/d8Dxybo24NSa6Bv.png)

3.复合结构

![](https://i.loli.net/2021/08/25/vExn3wPXSLGU2kQ.png)

4.纯量

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"value":"整数/浮点数"},{"value":"number: 12.30","inlineStyles":{"font-family":[{"from":0,"to":13,"value":"monospace"}],"font-size":[{"from":0,"to":13,"value":12}],"color":[{"from":6,"to":7,"value":"#999999"},{"from":8,"to":13,"value":"#990055"}],"back-color":[{"from":0,"to":13,"value":"#f5f2f0"}]}},{"value":"布尔值"},{"value":"isSet: true","inlineStyles":{"font-family":[{"from":0,"to":11,"value":"monospace"}],"font-size":[{"from":0,"to":11,"value":12}],"color":[{"from":5,"to":6,"value":"#999999"},{"from":7,"to":11,"value":"#990055"}],"back-color":[{"from":0,"to":11,"value":"#f5f2f0"}]}},{"value":"null"},{"value":"parent: ~ ","inlineStyles":{"font-family":[{"from":0,"to":10,"value":"monospace"}],"font-size":[{"from":0,"to":10,"value":12}],"color":[{"from":6,"to":7,"value":"#999999"},{"from":8,"to":9,"value":"#a67f59"}],"back-color":[{"from":0,"to":8,"value":"#f5f2f0"},{"from":8,"to":9,"value":"#ffffff"},{"from":9,"to":10,"value":"#f5f2f0"}]}},{"value":"时间"},{"value":"iso8601: 2001-12-14t21:59:43.10-05:00\n采用 ISO8601 格式","inlineStyles":{"font-family":[{"from":0,"to":37,"value":"monospace"},{"from":38,"to":51,"value":"monospace"}],"font-size":[{"from":0,"to":37,"value":12},{"from":38,"to":51,"value":12}],"color":[{"from":7,"to":8,"value":"#999999"},{"from":9,"to":13,"value":"#990055"},{"from":13,"to":14,"value":"#a67f59"},{"from":14,"to":16,"value":"#990055"},{"from":16,"to":17,"value":"#a67f59"},{"from":22,"to":23,"value":"#999999"},{"from":23,"to":25,"value":"#990055"},{"from":25,"to":26,"value":"#999999"},{"from":26,"to":31,"value":"#990055"},{"from":31,"to":32,"value":"#a67f59"},{"from":32,"to":34,"value":"#990055"},{"from":34,"to":35,"value":"#999999"},{"from":35,"to":37,"value":"#990055"},{"from":38,"to":51,"value":"#111111"}],"back-color":[{"from":0,"to":13,"value":"#f5f2f0"},{"from":13,"to":14,"value":"#ffffff"},{"from":14,"to":16,"value":"#f5f2f0"},{"from":16,"to":17,"value":"#ffffff"},{"from":17,"to":31,"value":"#f5f2f0"},{"from":31,"to":32,"value":"#ffffff"},{"from":32,"to":37,"value":"#f5f2f0"},{"from":38,"to":51,"value":"#f5f5d5"}]}},{"value":"日期"},{"value":"date: 1976-07-31\n采用复合 iso8601 格式的年、月、日表示","inlineStyles":{"font-family":[{"from":0,"to":16,"value":"monospace"},{"from":17,"to":40,"value":"monospace"}],"font-size":[{"from":0,"to":16,"value":12},{"from":17,"to":40,"value":12}],"color":[{"from":4,"to":5,"value":"#999999"},{"from":6,"to":10,"value":"#990055"},{"from":10,"to":11,"value":"#a67f59"},{"from":11,"to":13,"value":"#990055"},{"from":13,"to":14,"value":"#a67f59"},{"from":14,"to":16,"value":"#990055"},{"from":17,"to":40,"value":"#111111"}],"back-color":[{"from":0,"to":10,"value":"#f5f2f0"},{"from":10,"to":11,"value":"#ffffff"},{"from":11,"to":13,"value":"#f5f2f0"},{"from":13,"to":14,"value":"#ffffff"},{"from":14,"to":16,"value":"#f5f2f0"},{"from":17,"to":40,"value":"#f5f5d5"}]}},{"value":"字符串"},{"value":"str: 这是一行字符串","inlineStyles":{"font-family":[{"from":0,"to":12,"value":"monospace"}],"font-size":[{"from":0,"to":12,"value":12}],"color":[{"from":3,"to":4,"value":"#999999"}],"back-color":[{"from":0,"to":12,"value":"#f5f2f0"}]}}],"heights":[40,40,40,40,40,40],"widths":[150,318]}
```



