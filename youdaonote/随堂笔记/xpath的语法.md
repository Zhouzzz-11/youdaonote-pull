xpath的语法

XPath 是XML的查询语言，和SQL的角色很类似。以下面XML为例，介绍XPath 的语法。

xpath 教程链接：http://www.w3school.com.cn/xpath/



<?xml version="1.0" encoding="ISO-8859-1"?>
<catalog>
   <cd country="USA">
      <title>Empire Burlesque</title>
      <artist>Bob Dylan</artist>
      <price>10.90</price>
   </cd>
   <cd country="UK">
      <title>Hide your heart</title>
      <artist>Bonnie Tyler</artist>
      <price>9.90</price>
   </cd>
   <cd country="USA">
      <title>Greatest Hits</title>
      <artist>Dolly Parton</artist>
      <price>9.90</price>
   </cd>
</catalog>

 

定位节点

　　XML是树状结构，类似档案系统内数据夹的结构，XPath也类似档案系统的路径命名方式。不过XPath 是一种模式(Pattern)，可以选出 XML档案中，路径符合某个模式的所有节点出来。例如要选catalog底下的cd中所有price元素可以用：

/catalog/cd/price   

如果XPath的开头是一个斜线（/）代表这是绝对路径。如果开头是两个斜线（//）表示文件中所有符合模式的元素都会被选出来，即使是处于树中不同的层级也会被选出来，即相对路径。以下的语法会选出文件中所有叫做cd的元素（在树中的任何层级都会被选出来）：

//cd

 

选择未知的元素

　　使用星号（Wildcards,＊）可以选择未知的元素。下面这个语法会选出/catalog/cd 的所有子元素：

/catalog/cd/*

以下的语法会选出所有catalog的子元素中，包含有price作为子元素的元素。

/catalog/*/price

以下的语法会选出有两层父节点，叫做price的所有元素。

/*/*/price

以下的语法会选择出文件中的所有元素。

//*

要注意的是，想要存取不分层级的元素，XPath语法必须以两个斜线开头(//)，想要存取未知元素才用星号(*)，星号只能代表未知名称的元素，不能代表未知层级的元素。

 

选择分支

　　使用中括号可以选择分支。以下的语法从catalog的子元素中取出第一个叫做cd的元素。XPath的定义中没有第0元素这种东西。

/catalog/cd[1]

以下语法选择catalog中的最后一个cd元素：（XPathj并没有定义 first() 这种函式喔，用上例的 [1]就可以取出第一个元素。

/catalog/cd[last()]

以下语法选出含有price子元素的所有/catalog/cd元素。

/catalog/cd[price]

以下语法选出price元素的值等于10.90的所有/catalog/cd元素

/catalog/cd[price=10.90]

以下语法选出price元素的值等于10.90的所有/catalog/cd元素 的price元素

/catalog/cd[price=10.90]/price

 

选择一个以上的路径

　　使用Or操作数(|)就可以选择一个以上的路径。例如：

/catalog/cd/title | catalog/cd/artist

选择所有title以及artist元素

//title | //artist

选择所有title以及artist以及price元素

//title | //artist | //price

 

选择属性

　　在XPath中，除了选择元素以外，也可以选择属性。属性都是以@开头。例如选择文件中所有叫做country的属性。

//@country

选择所有含有country这个属性的cd元素：

//cd[@country]

以下语法选择出含有属性的所有cd元素

//cd[@*]

以下语法选择出country属性值为UK的cd元

//cd[@country='UK']

选择多个属性

//cd[@country='UK'][@name='hyddd']

 

 

xpath定位中starts-with、contains和text()的用法

starts-with 顾名思义，匹配一个属性开始位置的关键字

contains 匹配一个属性值中包含的字符串

text（） 匹配的是显示文本信息，此处也可以用来做定位用

eg

//input[starts-with(@name,'name1')]     查找name属性中开始位置包含'name1'关键字的页面元素

//input[contains(@name,'na')]         查找name属性中包含na关键字的页面元素

<a href="http://www.baidu.com">百度搜索</a>

xpath写法为 //a[text()='百度搜索'] 

或者 //a[contains(text(),"百度搜索")]

