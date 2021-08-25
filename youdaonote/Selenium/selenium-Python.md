文档：



参考地址：https://selenium-python-zh.readthedocs.io/en/latest/navigating.html

https://python-selenium-zh.readthedocs.io/zh_CN/latest/

https://www.selenium.dev/documentation/zh-cn/getting_started_with_webdriver/browsers/



安装

```javascript
pip install selenium

```



简单的case示例：

```javascript
import unittest
from selenium import webdriver
from selenium.webdriver.common.keys import Keys

class PythonOrgSearch(unittest.TestCase):

    def setUp(self):     //在每一个测试方法执行之前被执行
        self.driver = webdriver.Firefox()

    def test_search_in_python_org(self):     //测试方法始终以 test`开头
        driver = self.driver
        driver.get("http://www.python.org")
        self.assertIn("Python", driver.title)
        elem = driver.find_element_by_name("q")
        elem.clear()
        elem.send_keys("pycon")
        elem.send_keys(Keys.RETURN)      //16.17合成一条  elem.send_keys("pycon", Keys.RETURN)
        assert "No results found." not in driver.page_source


    def tearDown(self):      //在每一个测试方法执行之后被执行
        self.driver.close()

if __name__ == "__main__":     //入口函数
    unittest.main()

```





- input/textarea

```javascript
elem = driver.find_element_by_name("q")
elem.clear()
elem.send_keys("pycon")
elem.send_keys(Keys.RETURN)      //16.17合成一条  elem.send_keys("pycon", Keys.RETURN)

```



- select

```javascript
from selenium.webdriver.support.ui import Select
select = Select(driver.find_element_by_name('name'))
select.select_by_index(index)
select.select_by_visible_text("text")
select.select_by_value(value)
//取消已选择元素
select.deselect_by_index(index)
select.deselect_by_value(value)
select.deselect_by_visible_text(text)
select.deselect_all()  //取消所有

```



- option

```javascript
s1 = Select(driver.find_element_by_id('s1Id'))
for select in s1.options:  //返回这个select元素所有的options
	print select.text
 
 s1.all_selected_options .  //所有被选中的options
 s1.first_selected_options .  //第一个被选中的option

```



- submit

```javascript
element.submit()
//或者找到提交元素并点击
driver.find_element_by_id("submit").click()

```



- window/frame

```javascript
driver.switch_to_window("windowName")  //不同windows之间移动
driver.switch_to_frame("frameName")   //不同frames之间移动
driver.switch_to_default_content()   //返回父frame

```



- wait

```javascript
//显式等待
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(EC.element_to_be_clickable((By.ID,'someid')))

//隐式等待
from selenium import webdriver

driver = webdriver.Firefox()
driver.implicitly_wait(10) # seconds
driver.get("http://somedomain/url_that_delays_loading")
myDynamicElement = driver.find_element_by_id("myDynamicElement")

```



隐式等待和显式等待的区别：

参考地址：https://blog.csdn.net/weixin_39614657/article/details/110538807

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"textAlign":"left","verticalAlign":"middle","wrap":true,"value":"隐式等待 Implicit Wait","inlineStyles":{"bold":[{"from":0,"to":18,"value":true}],"color":[{"from":0,"to":18,"value":"#4f4f4f"}]}},{"textAlign":"left","verticalAlign":"middle","wrap":true,"value":"显示等待 Explicit Wait","inlineStyles":{"bold":[{"from":0,"to":18,"value":true}],"color":[{"from":0,"to":18,"value":"#4f4f4f"}]}},{"textAlign":"left","verticalAlign":"middle","wrap":true,"backColor":"rgb(247, 247, 247)","value":"隐式等待时间应用于脚本中的所有元素","inlineStyles":{"color":[{"from":0,"to":17,"value":"#4f4f4f"}]}},{"textAlign":"left","verticalAlign":"middle","wrap":true,"backColor":"rgb(247, 247, 247)","value":"显式等待时间只应用于指定等待的元素","inlineStyles":{"color":[{"from":0,"to":17,"value":"#4f4f4f"}]}},{"textAlign":"left","verticalAlign":"middle","wrap":true,"value":"我们不需要在要定位的元素上指定ExpectedConditions","inlineStyles":{"color":[{"from":0,"to":33,"value":"#4f4f4f"}]}},{"textAlign":"left","verticalAlign":"middle","wrap":true,"value":"我们需要在要定位的元素上指定ExpectedConditions","inlineStyles":{"color":[{"from":0,"to":32,"value":"#4f4f4f"}]}},{"textAlign":"left","verticalAlign":"middle","wrap":true,"backColor":"rgb(247, 247, 247)","value":"建议在元素的出现时间小于隐式等待中指定的时间范围时使用","inlineStyles":{"color":[{"from":0,"to":27,"value":"#4f4f4f"}]}},{"textAlign":"left","verticalAlign":"middle","wrap":true,"backColor":"rgb(247, 247, 247)","value":"建议在元素加载时间较长时使用，也可以用于验证元素的属性，如(visibilityofelementlocate, elementToBeClickable, elementtobesselected)","inlineStyles":{"color":[{"from":0,"to":100,"value":"#4f4f4f"}]}}],"widths":[481,481],"heights":[40,40,40,40]}
```







1.通过select 进行定位下拉框

![](https://i.loli.net/2021/08/25/kx3VX4lgSRbFQm6.png)

#通过index进行选择

Select(driver.find_element_by_id("cardType")).select_by_index(1)

#通过value进行选择

#Select(driver.find_element_by_id("cardType")).select_by_value(1)

#通过选项文字进行选择

#Select(driver.find_element_by_id("cardType")).select_by_visile_text("通用卡")



注：Select only works on <select> elements（Select只对<select>标签的下拉菜单有效）



2.定位非<select>标签的下拉菜单

两个步骤：先定位到下拉菜单，在对其中的选项进行定位

![](https://i.loli.net/2021/08/25/MXIScEUZWGfRaDh.png)







