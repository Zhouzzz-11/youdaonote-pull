## Java考试试题

### 1.选择题（10分）

1. 下列命令中，是Java编译命令的是：（	）

   A.	javac 			B.  java				C.  javadoc			D.  appleviewer

2. 执行下列赋值语句`a = Float.valueOf("12.34") ;`后，a的值为：（）

   A.	12 			B.  34				C.  0.34			D.  12.34

3. 软件需求分析一般应确定的是用户对软件的（  ）

   A.  功能需求		 			B.  非功能需求				

   C.  性能需求		  			D.  功能需求和非功能需求

4. 下列叙述中，正确的是：（  ）

   A.  Java语言的标识符是区分大小写的		 	B.  源文件名与public类名可以不相同				

   C.  源文件的扩展名为.jar	  				D.  声明变量可以不指定类型

5. 在Java中，负责对字节代码.class文件解释执行的是（  ）

   A.  垃圾回收器 			B.  虚拟机			C.  编译器			D.  多线程机制

6. 下列属性合法的Java标识符的是：（ ） 

   A.  hello_kitty 			B.  5books			C.  +static			D.  -3.1415

7. 已知： `int a[] = new int[100] ;` 在下列给出的数组元素中，非法的是：（  ）

   A.  a[0] 			B.  a[1]			C.  a[99]			D.  a[100]

8. int型成员变量MAX_LENGTH，该值保持为常数100，则定义这个变量的语句是：（  ）

   A.  `public int MAX_LENGTH=100`			 	B.  `final int MAX_LENGTH=100`			

   C.  `public const int MAX_LENGTH=100`	  	D.  ` final abstract int MAX_LENGTH=100`

9. 顺序执行下列程序语句后，b的结果为：（  ） 

```java
public class Test{
    public static void main(String args[]){
        String a = "Hello" ;
        String b = a.substring(0,2) ;
        System.out.println(b) ;
    }
}
```

​	A.  Hello 			B.  Hel			C.  He			D.  null

10. 多态的表现形式有：（ ）

    A.  重写 			B.  抽象			C.  继承			D.  封装

### 2.填空题（10分）

1. 在Java程序中定义的类有两种成员：_______________________ 、_______________________ 
2. 设x = 2 ,则表达式(x++)*3的值为：_______________________
3. 构造方法只能通过_______________________关键字调用，用户不能直接调用。
4. Java语言中如果要使用某个包中的类时，需要使用_______________________导入

### 3.程序分析题（25分）

1. 下面程序段的输出结果为：

```java
public class Test{
    int a,b ;
    public Test(){
        a = 100 ;
        b = 200 ;
    }
    public Test(int x,int y){
        a = x ;
        b = y ;
    }
    public static void main(String args[]){
        Test obj1 = new Test(12,45) ;
        System.out.println("a1="+obj1.a+",b1="+obj1.b) ;
        Test obj2 = new Test() ;
        System.out.println("a2="+obj2.a+",b2="+obj2.b) ;
    }
}
```

2. 执行下面程序段的输出结果为：

```java
public class TestArray{
    public static void main(String args[]){
        int arr[] = new int[5] ;
        System.out.println(arr[0]) ;
    }
}
```

3. 下列程序的输出结果是：

```java
public class TestArray{
    public static void main(String args[]){
        System.out.println("题目1：") ;
        int[] arr = new int[3] ;
        for(int i=0; i<arr.length; i++){
            arr[i] = i+2 ;
        }
        for(int result:arr){
            System.out.println(result) ;
        }
        System.out.println("题目2：") ;
        int array[] = new int[4] ;
        for(int i=array.length-1; i>=0; j--){
            array[i] = i ;
            System.out.print("hello"+array[i]) ;
        }
    }
}
```

4. 下面程序的执行结果是什么：

```java
public class AA{
    void show(){
        System.out.println("Java从入门到精通") ;
    }
}
public class BB extends AA{
    void show(){
        System.out.println("Java从入门到放弃") ;
    }
}
public class Test{
    public static void main(String args[]){
        AA a = new AA() ;
        a.show() ;
        BB b = new BB() ;
        b.show() ;
    }
}
```

5. 阅读以下程序，写出程序的运行结果

```java
public class Demo{
    static int x ;
}
public class Test{
    public static void main(String args[]){
        Demo a = new Demo() ;
        System.out.println("a.x="+a.x) ;
        a.x = 1 ;
        System.out.println("a.x="+a.x) ;
        Demo b = new Demo() ;
        b.x = 2 ;
        System.out.println("a.x="+a.x) ;
        System.out.println("b.x="+b.x) ;
    }
}
```

### 4.简答题（25分）

1. 面向对象的特点有哪些？



2. 数组有没有length()方法？String有没有length()方法？



3. 重载Overload和方法重写Override的区别，Overload的方法是否可以改变返回值类型？



4. 什么是抽象类，抽象类具备的特点有哪些？



5. 说明this和super关键的含义以及使用？



### 5.程序设计题（20分）

1. 设计一个类，通过构造方法获取身份证号，如果身份证号不足18位则提示报错，实现从身份号码中获取生日和性别

```java
public class Card{
    //请根据以下代码，补充Card类的内容
}
public class Use{
    public static void main(String args[]){
        Card p = new Card("430121201102132519") ;
        String birth = p.getBirth() ;
        String sex = p.getSex() ;
        System.out.println("该身份证所示的生日为："+birth+",性别为："+sex) ;
    } 
}
```

2. 第一题 （Map）利用Map，完成下面的功能： 

   从命令行读入一个字符串，表示一个年份，输出该年的世界杯冠军是哪支球队。如果该 年没有举办世界杯，则输出：没有举办世界杯。

   历届世界杯冠军 

|   届数   | 举办年份 | 举办地点 |  冠军  |
| :------: | :------: | :------: | :----: |
|  第一届  |  1930年  |  乌拉圭  | 乌拉圭 |
|  第二届  |  1934年  |  意大利  | 意大利 |
|  第三届  |  1938年  |   法国   | 意大利 |
|  第四届  |  1950年  |   巴西   | 乌拉圭 |
|  第五届  |  1954年  |   瑞士   |  西德  |
|  第六届  |  1958年  |   瑞典   |  巴西  |
|  第七届  |  1962年  |   智利   |  巴西  |
|  第八届  |  1966年  |  英格兰  | 英格兰 |
|  第九届  |  1970年  |  墨西哥  |  巴西  |
|  第十届  |  1974年  |  前西德  |  西德  |
| 第十一届 |  1978年  |  阿根廷  | 阿根廷 |
| 第十二届 |  1982年  |  西班牙  | 意大利 |
| 第十二届 |  1982年  |  西班牙  | 意大利 |
| 第十三届 |  1986年  |  墨西哥  | 阿根廷 |
| 第十四届 |  1990年  |  意大利  |  西德  |
| 第十五届 |  1994年  |   美国   |  巴西  |
| 第十六届 |  1998年  |   法国   |  法国  |
| 第十七届 |  2002年  |   韩日   |  巴西  |
| 第十八届 |  2006年  |   德国   | 意大利 |
| 第十九届 |  2010年  |   南非   | 西班牙 |
|第二十届|2014年|巴西|德国|

（Map）在原有世界杯Map 的基础上，增加如下功能： 读入一支球队的名字，输出该球队夺冠的年份列表。 例如，读入“**巴西**”，应当输出 **1958 1962 1970 1994 2002** 读入“**荷兰**”，应当输出 **没有获得过世界杯** 