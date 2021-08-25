 有时候我们在定位一个页面元素的时候发现一直定位不了，反复检查自己写的定位器没有任 何问题，代码也没有任何问题。这时你就要看一下这个页面元素是否在一个iframe中，这可能就是找不到的原因之一。如果你在一个default content中查找一个在iframe中的元素，那肯定是找不到的。反之你在一个iframe中查找另一个iframe元素或default content中的元素，那必然也定位不到。

selenium webdriver中提供了进入一个iframe的方法：

WebDriver  org.openqa.selenium.WebDriver.TargetLocator.frame(String nameOrId)



也提供了一个返回default content的方法：

WebDriver org.openqa.selenium.WebDriver.TargetLocator.defaultContent()



这样使我们面对iframe时可以轻松应对。

以下面的html代码为例，我们看一下处现iframe。



main.html

 

<html>

    <head>

        <title>FrameTest</title>

    </head>

    <body>

    <divid ="id1">this is a div!</div>

        <iframeid ="frame" frameborder="0"scrolling="no"style="left:0;position:absolute;"src = "frame.html"></iframe>

    </body>

</html>

 

frame.html

 

<html>

    <head>

        <title>this is a frame!</title>

    </head>

    <body>

    <divid ="div1">this is a div，too!</div>

    <label>input:</label>

    <inputid ="input1"></input>

    </body>

</html> 





Java代码



import org.openqa.selenium.By;

import org.openqa.selenium.WebDriver;

import org.openqa.selenium.firefox.FirefoxDriver;

 

public class FameStudy {

 

     

    publicstaticvoid main(String[] args) {

        WebDriver dr = new FirefoxDriver();

        String url = "\\Your\\Path\\to\\main.html";

        dr.get(url);

 

        //在default content定位id="id1"的div

        dr.findElement(By.id("id1"));

         

        //此时，没有进入到id="frame"的frame中时，以下两句会报错

        dr.findElement(By.id("div1"));//报错

        dr.findElement(By.id("input1"));//报错

         

        //进入id="frame"的frame中，定位id="div1"的div和id="input1"的输入框。

        dr.switchTo().frame("frame");    

        dr.findElement(By.id("div1"));

        dr.findElement(By.id("input1"));

         

        //此时，没有跳出frame，如果定位default content中的元素也会报错。

        dr.findElement(By.id("id1"));//报错

         

        //跳出frame,进入default content;重新定位id="id1"的div

        dr.switchTo().defaultContent();

        dr.findElement(By.id("id1"));

    }

 

} 



switch_to方法会new1个TargetLocator对象，使用该对象的frame方法可以将当前识别的”主体”移动到需要定位的frame上去。









