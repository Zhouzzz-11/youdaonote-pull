1、网页前进、后退

 back（）  

  forward（）

2、刷新网页

refresh（）

3、窗口最大化

maximize_window()

4、获取当前窗口位置

get_window_position()

set_window_position()

5、获取当前窗口大小

get_window_size（）

set_window_size（）

6、获取title

title

用断言assertEqual判断是否是打开正确的页面

7、获取当前页面URL

current_url

8、获取打开窗口句柄，且可以互相切换

当前窗口句柄：current_window_handle

所有窗口句柄：window_handles

上述是以列表的方式存储的，要访问的话通过driver.window_handles[-1]获取当前打开窗口句柄

9、清空输入框内容

clear（）

10、双击

导包 ：from selenium.webdriver import ActionChains   双击、悬浮、拖拽

action_chains = ActionChains(self.driver)

action_chain.double_click(元素).perform()







