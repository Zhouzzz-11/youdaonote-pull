使用python处理selenium中的css_selector定位元素的模糊匹配问题

# 匹配id，先指定一个html标签，然后加上“#”符号，再加上id的属性值

self.driver.find_element_by_css_selector('div#ID').click()

# 匹配class，先指定一个html标签，然后加上“.”符号，再加上class的属性值

self.driver.find_element_by_css_selector('div.CLASS').click()

# 匹配其他属性

self.driver.find_element_by_css_selector('div[name=NAME]').click()

# 组合匹配

self.driver.find_element_by_css_selector('div[name=NAME][type=TYPE]').click()

# 匹配头部

self.driver.find_element_by_css_selector('div[style^="sp.gif"]').click()

# 匹配尾部

self.driver.find_element_by_css_selector('div[style$="sp.gif"]').click()

# 匹配中间

self.driver.find_element_by_css_selector('div[style*="sp.gif"]').click()

