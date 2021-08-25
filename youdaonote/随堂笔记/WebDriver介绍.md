

 

 

1.WebDriver介绍

Selenium 2.0最主要的新特性就是集成了WebDriver API。我们设计WebDriver的初衷是提供更加简单明了的接口来弥补Selenium-RC API的不足。在动态网页中，通常只会更新局部的html元素，WebDriver会很好的帮助用户快速定位这些元素。我们最终的目的是通过提供精心设计的面向对象API来解决现代高级网页中的测试难题。

2.WebDriver如何驱动浏览器？与Selenium-RC有什么区别？

不同类型的浏览器都会有原生的接口支持自动化操作，Selenium通过这些接口直接向浏览器发送指令。如何发送这些指令取决于你当前使用的浏览器类型，我们将在这一章节后面来详细介绍。

看上去WebDriver与之前Selenium-RC的实现方式类似，实际上两者之间存在着本质的区别。对于所有类型的浏览器Selenium-RC都是使用的同一种方法：当浏览器启动时，向其中注入javascript，从而使用这些js来驱动浏览器中的AUT（Application Under Test）。WebDriver并没有使用这种技术，它是通过调用浏览器原生的自动化API直接驱动浏览器。

3.WebDriver与Selenium Server

是否需要是用Selenium Server取决于你使用WebDriver的方式。以下两种情况不需要使用Selenium Server，WebDriver直接运行浏览器即可：1、testcases仅仅使用了Webdriver的API；2、浏览器和testcase在同一台PC上，而且testcases仅仅使用了Webdriver的API。

以下三种情况你需要结合Selenium Server来使用WebDriver：

1）使用Selenium-Grid管理集群环境（或者虚拟机）上的testcase；

2）需要调用非本机上的不同版本的浏览器；

3）未使用任何language binding(java/c#/python/ruby)，且有意向使用HtmlUnitDriver。

4.配置Selenium-WebDriver工程

安装Selenium是指在开发环境上配置一个工程，然后可以在这个工程中用Selenium编写程序。如何配置取决于你使用的开发语言和编程环境。

 

使用Maven是配置一个Selenium 2.0 java工程最简单的方式。Maven会下载所有java bingdings以及所有相关的库（the Selenium 2.0 java client library）。通过使用pom.xml(maven配置文件)来新建工程，你可以根据自己的喜好将Maven工程导入IntelliJ IDEA或者Eclipse。



首先，创建一个文件夹存放Maven工程文件。然后，创建pom.xml，你可以使用text editor来编辑。鉴于已经有很多关于“如何在Maven工程中使用pom.xml”优秀的参考文献，这里将不再过多的讨论相关细节。下面给出一个示例，为你的工程也创建一个类似的文件。

 

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                 xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <groupId>MySel20Proj</groupId>
        <artifactId>MySel20Proj</artifactId>
        <version>1.0</version>
        <dependencies>
            <dependency>
                <groupId>org.seleniumhq.selenium</groupId>
                <artifactId>selenium-java</artifactId>
                <version>2.38.0</version>
            </dependency>
            <dependency>
                <groupId>com.opera</groupId>
                <artifactId>operadriver</artifactId>
            </dependency>
        </dependencies>
        <dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>com.opera</groupId>
                    <artifactId>operadriver</artifactId>
                    <version>1.5</version>
                    <exclusions>
                        <exclusion>
                            <groupId>org.seleniumhq.selenium</groupId>
                            <artifactId>selenium-remote-driver</artifactId>
                        </exclusion>
                    </exclusions>
                </dependency>
            </dependencies>
        </dependencyManagement>
</project>

请确认你使用的WebDriver是最新的当前版本。在这篇文档撰写时，上述示例给出的是最新的版本。在Selenium2.0发布不久WebDriver就有过频繁的更新。请在这个链接Maven Download Page确认当前的版本，相应地修改你工程中的pon.xml。

现在，你可以通过dos界面使用CD命令进入工程所在文件夹，通过以下命令运行Maven。

 

mvn clean install

 

运行之后会自动下载Selenium及相关套件，并加载到你的工程中去。

最后，将你的工程导入到你偏好的IDE中。如果你对导入的过程不是很清楚，我们已经准备了操作指南。

Importing a maven project into IntelliJ IDEA.Importing a maven project into Eclipse

5.如何将自动化工程从Selenium1.0迁移到Selenium2.0

已经在Selenium1.0上构建测试工程的用户，我们为您提供了一份指导如何将已有的代码迁移到Selenium2.0。Selenium2.0的首席开发工程师Simon Stewart为此撰写了一片文章：Magrating From Selenium RC to Selenium WebDriver。

6.Selenium-WebDriver API简介

WebDriver可以用来实现Web应用程序的自动化测试，特别适合于验证实际结果是否符合预期结果的场景。WebDriver旨在提供比Selenium1.0更加易用、友好的API，便于用户的探索和理解，从而使测试用例变得容易阅读和维护。WebDriver没有使用任何第三方测试框架，所以它可以很好与单元测试工具或者最古老的main函数结合使用。本章节将介绍如何使用WebDriver的API，帮助你慢慢开始了解WebDriver。如果你还没有新建一个Selenium工程，请先完成这个操作，在这个章节的上面有详细的描述。

 

当你创建完Selenium工程后，你会发现WebDriver和普通的第三方库一样是完全独立的，在你使用之前不需要启动任何额外的进程或者安装程序，相反如果你使用Selenium-RC需要先启动代理服务器。

 

注意：当你使用如下WebDriver时需要额外的步骤：Chrome Driver,Opera Driver,Android Driver,IPhone Driver。

 

现在你肯定跃跃欲试要写一些代码了。我们以一个简单的例子来开始第一段旅程：在Google上搜索“Cheese”，并打印出搜索结果网页的标题。

 

package org.openqa.selenium.example;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.ExpectedCondition;
import org.openqa.selenium.support.ui.WebDriverWait;

public class Selenium2Example  {
    public static void main(String[] args) {
        // 创建一个FirefoxDriver实例
        // 这个类依赖于接口而不是接口的实现
        WebDriver driver = new FirefoxDriver();

        // 使用get方法访问Google
        driver.get("http://www.google.com");
        // 使用下面这个方法也能够达到访问Google的目的
        // driver.navigate().to("http://www.google.com");

        // 找到html输入框的name
        WebElement element = driver.findElement(By.name("q"));

        // 输入要查找的内容
        element.sendKeys("Cheese!");

        // 提交表单，WebDriver会自动找到我们需要提交的元素所在的表单
        element.submit();

        // 打印网页的标题
        System.out.println("Page title is: " + driver.getTitle());
        
        // Google的搜索网页会通过JS动态渲染
        // 等待页面加载完毕，超时时间为10秒
        (new WebDriverWait(driver, 10)).until(new ExpectedCondition<Boolean>() {
            public Boolean apply(WebDriver d) {
                return d.getTitle().toLowerCase().startsWith("cheese!");
            }
        });

        // 控制台上将打印如下信息: "cheese! - Google Search"
        System.out.println("Page title is: " + driver.getTitle());
        
        // 关闭浏览器
        driver.quit();
    }
}

在本章节的接下来篇幅，我们将学习如何使用WebDriver操作你的浏览器，如何使用框架和窗口来测试Web网站。当然，我们将提供更加翔实的论述和举例。

 

7.Selenium-WebDriver API详解

7.1获取Web页面

我们第一件要做的事是通过WebDriver取得Web页面的控制权，一般情况下使用get方法

driver.get("http://www.google.com");

在某些情况下，比如操作系统和浏览器的穿插组合，WebDriver有可能不会等待Web页面加载完成，这种情况下WebDriver会返回错误或者直接运行下一步操作。为了保证程序的健壮性，你需要等待页面中某个元素加载完成后再进行下一步操作，请参考Explicit and Implicit Waits。

 

7.2定位UI元素

我们可以通过WebDriver实例或者WebElement类来定位UI元素。我们为每种编程语言都提供了两种方法：“Find Element”和“Find Elements”。第一种方法返回的一个WebElement，找不到则抛出异常。第二个方法返回一个WebElement链表（List），在找不到任何DOM元素的情况下会返回空的链表。

Find方法会使用类似探测器的类，类名叫做By。下面列举By的一些常用方法：

 

By ID

当我们定位一个UI 元素，这个是最有效也是最好的方法。不过这个方法不是万能的，有的前端开发在设计UI元素时会遗漏ID或者使用动态ID，这两种情况下都要避免使用这个方法。这时候使用获取class名称方法比By ID更合适。

示例：如何使用该方法定位元素

<div id="coolestWidgetEvah">...</div>
WebElement element = driver.findElement(By.id("coolestWidgetEvah"));

 

By Class Name

在这种场景下，我们引用DOM元素的属性。实际情况是很多元素都有一样的Class Name，因此找到多个有相同Class Name的元素，比找到第一个拥有这个Class Name的元素来的更重要。

示例：如何使用该方法定位元素

 

<div class="cheese"><span>Cheddar</span></div><div class="cheese"><span>Gouda</span></div>
List<WebElement> cheeses = driver.findElements(By.className("cheese"));



By Tag Name

 

DOM元素Tag的名称。

示例：如何使用该方法定位元素

 

<iframe src="..."></iframe>
WebElement frame = driver.findElement(By.tagName("iframe"));



By Name

 

找到与Name属性相同的Input元素。

示例：如何使用该方法定位元素

 

<input name="cheese" type="text"/>
WebElement cheese = driver.findElement(By.name("cheese"));



By Link Text

 

找到与Text属性精确匹配的超链接。

示例：如何使用该方法定位元素

 

<a href="http://www.google.com/search?q=cheese">cheese</a>
WebElement cheese = driver.findElement(By.linkText("cheese"));



By Partial Link Text

 

找到与Text属性模糊匹配的超链接。

示例：如何使用该方法定位元素

<a href="http://www.google.com/search?q=cheese">search for cheese</a>
WebElement cheese = driver.findElement(By.partialLinkText("cheese"));



By CSS

这个方法名称意味着它是一个CSS探测器。前提是浏览器默认支持这种方法，建议根据W3C的标准文档构建CSS选择器。如果浏览器不支持CSS选择器，可以使用Sizzle。IE6,7和FireFox3.0就是使用Sizzle作为CSS查询引擎。

 

注意不是所有浏览器都使用同样的CSS选择器表达式，有些CSS可能只在某一个版本中生效。

示例：如何使用该方法定位元素

 

<div id="food"><span class="dairy">milk</span><span class="dairy aged">cheese</span></div>
WebElement cheese = driver.findElement(By.cssSelector("#food span.dairy.aged"));



By XPath

当有需要时，WebDriver还可以使用浏览器自带的XPATH。对于那些不支持XPATH的浏览器，我们提供了WebDriver特有的实现方式。请确保熟悉XPATH在不同的引擎中的区别，否则会导致一些不可预料的问题。

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"verticalAlign":"middle","wrap":true,"value":"Driver"},{"verticalAlign":"middle","wrap":true,"value":"大小写敏感"},{"verticalAlign":"middle","wrap":true,"value":"属性值是否可见"},{"verticalAlign":"middle","wrap":true,"value":"是否支持XAPTH"},{"verticalAlign":"middle","wrap":true,"value":"HtmlUnit Driver"},{"verticalAlign":"middle","wrap":true,"value":"仅识别小写"},{"verticalAlign":"middle","wrap":true,"value":"可见"},{"verticalAlign":"middle","wrap":true,"value":"是"},{"verticalAlign":"middle","wrap":true,"value":"IE Driver"},{"verticalAlign":"middle","wrap":true,"value":"仅识别小写"},{"verticalAlign":"middle","wrap":true,"value":"可见"},{"verticalAlign":"middle","wrap":true,"value":"否"},{"verticalAlign":"middle","wrap":true,"value":"FireFox Diver"},{"verticalAlign":"middle","wrap":true,"value":"大小写不敏感"},{"verticalAlign":"middle","wrap":true,"value":"可见"},{"verticalAlign":"middle","wrap":true,"value":"是"}],"widths":[125,125,125,125],"heights":[40,40,40,40]}
```

上面的表格有一些抽象，让我们来看个例子

 

<input type="text" name="example" />
<INPUT type="text" name="other" />

List<WebElement> inputs = driver.findElements(By.xpath("//input"));



匹配结果如下

 

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"verticalAlign":"middle","wrap":true,"value":"XPATH表达式"},{"verticalAlign":"middle","wrap":true,"value":"HtmlUnit Driver"},{"verticalAlign":"middle","wrap":true,"value":"FireFox Driver"},{"verticalAlign":"middle","wrap":true,"value":"IE Driver"},{"verticalAlign":"middle","wrap":true,"value":"//input"},{"verticalAlign":"middle","wrap":true,"value":"1"},{"verticalAlign":"middle","wrap":true,"value":"2"},{"verticalAlign":"middle","wrap":true,"value":"2"},{"verticalAlign":"middle","wrap":true,"value":"//INPUT"},{"verticalAlign":"middle","wrap":true,"value":"0"},{"verticalAlign":"middle","wrap":true,"value":"2"},{"verticalAlign":"middle","wrap":true,"value":"0"}],"widths":[100,100,100,100],"heights":[40,40,40]}
```

有些标签的属性有默认值，这种情况下不指定属性值则匹配默认值。比如，"input"标签"type"属性默认为"text"。使用XPATH的首要原则就是不要忽略这些隐藏的实现。

使用JavaScript

只要返回的是一个Web Element，你还可以使用任意的JS代码查找Web元素，根据查询结果会自动修改为一个WebElement对象。

一个简单的使用jQuery的例子：

 

WebElement element = (WebElement) ((JavascriptExecutor)driver).executeScript("return $('.cheese')[0]");



查找页面中每个label的所有Input元素：

 

 

List<WebElement> labels = driver.findElements(By.tagName("label"));
List<WebElement> inputs = (List<WebElement>) ((JavascriptExecutor)driver).executeScript(
    "var labels = arguments[0], inputs = []; for (var i=0; i < labels.length; i++){" +
    "inputs.push(document.getElementById(labels[i].getAttribute('for'))); } return inputs;", labels);

 

 

7.3模拟用户输入行为

我们已经演示了在文本框输入文本内容，其他Web元素应该如何操作呢？你可以触发CheckBox的某个选项，也可以选择Select的某个选项。WebDriver处理Select元素也很简单。

WebElement select = driver.findElement(By.tagName("select"));
List<WebElement> allOptions = select.findElements(By.tagName("option"));
for (WebElement option : allOptions) {
    System.out.println(String.format("Value is: %s", option.getAttribute("value")));
    option.click();
}



上面的例子，将选择Web页面中的第一个Select元素，并将循环打印出选项的取值并单击选项。或许你已经注意到，使用这个方法并不是最有效的。WebDriver提供一个“Select”类，这个类的方法更适合于处理上述这种场景。

Select select = new Select(driver.findElement(By.tagName("select")));
select.deselectAll();
select.selectByVisibleText("Edam");



上面的例子，首先去除选定第一个选项的焦点，然后选中取值为"Edam"的选项。

一旦你完成了所有表单字段的输入，下一步就是提交表单。一种方法就是找到Web页面中的Submit按钮并单击：

driver.findElement(By.id("submit")).click();



作为另一种选择，WebDriver的Element类有一个更加便利的方法"sublmit"。如果你对表单中的某个Element使用该方法，WebDriver将会走读其所在的DOM对象，直到找到其所属的表单，并提交。如果该Element并不在某个表单中，将会抛出异常NoSuchElementException。

element.submit();



7.4在windows和frames间切换

 

有些Web程序包含许多Frame和窗口，WebDriver提供"switch to"方法在这之间进行切换：

driver.switchTo().window("windowName");



所有传输给WebDriver的指定将被传输给切换后的窗口。如何直到窗口的名称呢？查看JS并打开该窗口就可以了：

<a href="somewhere.html" target="windowName">Click here to open a new window</a>



作为另一种选择，你可以使用一个“窗口句柄”传递给"switchTo().window()"方法。根据此方法，将会使用迭代器遍历所有打开的窗口：

for (String handle : driver.getWindowHandles()) {
    driver.switchTo().window(handle);
}



你也可以在Frame之间切换（或者进入Frame）：

driver.switchTo().frame("frameName");



你还可以根据路径使用Frame的子Frame，而且可以通过索引定位Frame。

driver.switchTo().frame("frameName.0.child");

以上方法将切换到名称为“frameName”的Frame的第一个子Frame，所有Frame都是Web页面的最顶端开始计数。

 

7.5弹出框

 

Selenium2.0 beta1版本，我们提供方法获取弹出框。在你触发弹出框的操作后，你可以用一下方法进入弹出框：

Alert alert = driver.switchTo().alert();



以上方法将会返回当前当前打开的alert对象，你可以对这个对象进行任何可操作：点击取消，点击确定，关闭窗口，获取alert的文本内容等。这个接口在alerts、confirms、prompts对象上都有很好的应用，具体请参见API文档。

 

 

7.6Navigation：浏览器本地历史记录

 

前文中，我们使用get方法来获取网页（driver.get("http://www.example.com")）。正如你看到的，WebDriver有不少轻量级的功能聚焦的接口，Navigation就是这样一个。正因为加载网页是一个再普通不过的需求，这个方法存在于Driver类下面，但是用法很简单：

 

driver.navigate().to("http://www.example.com");



重申一下，"navigate().to()"和"get()"做的是同样的事情，只不过其中一个更适合打印。

 

Navigate接口还提供方法可以在浏览器历史记录中前后翻页。

 

driver.navigate().forward();
driver.navigate().back();



请注意，以上功能完全取决于底层的浏览器。如果你习惯跨浏览器操作，当你使用这些接口时可能会出现意想不到的的异常。

 

 

7.7Cookies

 

在我们开始下一步的讲解之前，你可能对WebDriver如何操作本地Cookies很感兴趣。首先，你必须处于当前Cookie的作用域。如果你在打开一个网页之前尝试预置Cookie，而且你的主页大到需要很长一段时间来加载，这时候你需要找一个小点的网页来替代，比如HTTP 404网页（http://example.com/some404page）。

// 打开Cookie作用的网站
driver.get("http://www.example.com");

// 设置全局Cookie
Cookie cookie = new Cookie("key", "value");
driver.manage().addCookie(cookie);

// 输出当前网页所有可用的Cookie
Set<Cookie> allCookies = driver.manage().getCookies();
for (Cookie loadedCookie : allCookies) {
    System.out.println(String.format("%s -> %s", loadedCookie.getName(), loadedCookie.getValue()));
}

// 你又三种方法删除Cookie
// By name
driver.manage().deleteCookieNamed("CookieName");
// By Cookie
driver.manage().deleteCookie(loadedCookie);
// Or all of them
driver.manage().deleteAllCookies();



7.8 修改用户代理服务器

 

对于FireFox来说很简单：

FirefoxProfile profile = new FirefoxProfile();
profile.addAdditionalPreference("general.useragent.override", "some UA string");
WebDriver driver = new FirefoxDriver(profile);



7.9 拖拽Web元素

下面是一个拖拽Web页面元素的例子，前提是本地事件必须可用。

 

WebElement element = driver.findElement(By.name("source"));
WebElement target = driver.findElement(By.name("target"));

(new Actions(driver)).dragAndDrop(element, target).perform();

 



 

      



