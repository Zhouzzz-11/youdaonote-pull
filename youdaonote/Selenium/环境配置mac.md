### pytest+selenium+allure



示例代码：

```javascript
import allure
from selenium import webdriver
import pytest
import yaml
import time

@allure.testcase('http://www.github.com')
@allure.feature('百度搜索')
@pytest.mark.parametrize('data', "123")
def test_steps_demo(data):
    with allure.step("打开百度首页"):
        driver = webdriver.Chrome()
        driver.get("http://www.baidu.com")
        driver.maximize_window()

    with allure.step(f"输入关键词：{data}"):
        driver.find_element_by_id('kw').send_keys(data)
        time.sleep(2)
        driver.find_element_by_id('su').click()
        time.sleep(2)

    with allure.step("保存图片"):
        driver.save_screenshot("./screenshot/"+data+".png")
        allure.attach.file("./screenshot/"+data+".png")
        attachment_type = allure.attachment_type.PNG

    with allure.step("关闭浏览器"):
        driver.quit()

```



1. python3环境，使用pip3安装pytest、yaml、allure

```javascript
pip3 install -U pytest
pip3 install selenium 
brew install allure 
pip3 install pyyaml
pip3 install allure-pytest

```



2. 下载浏览器驱动文件

https://www.selenium.dev/documentation/zh-cn/getting_started_with_webdriver/third_party_drivers_and_plugins/

选择与浏览器版本适配的插件



3. 配置环境变量

chromedriver mac环境及环境变量配置

打开Finder，使用command+shift+G，

在弹出的目录中填写/usr/local/bin

将解压的Chromedrive.exe文件拖进去

最后

验证版本

```javascript
chromedriver --version 

```



Mac系统的环境变量，加载顺序为：

/etc/profile /etc/paths ~/.bash_profile ~/.bash_login ~/.profile ~/.bashrc



可以配置一下环境，但貌似没看到作用，不太清楚·····



打开终端，输入：

```javascript
vim ~/.bash_profile

```



在PATH路径最后加上

:/usr/local/bin/ChromeDriver

保存退出，执行

```javascript
 source ~/.bash_profile

```



最后可以在IDE运行一下示例代码，输入：

```javascript
pytest /Users/sghl-11/test-demo/UI-auto-demo/test_data.py

```

会自动打开浏览器，执行代码中的浏览器操纵



结束～

