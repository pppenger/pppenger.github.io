目录

[TOC]



### 封装

1.概念：将类的信息隐藏在类内部，不允许外部程序直接访问，而是通过该类提供的方法来实现对隐藏信息的操作和访问

2.好处：

a.只能通过规定的方法访问数据

b.隐藏类的实例细节，方便修改和实现



### 多态

#### 引用多态

父类的引用可以指向本类的对象
父类的引用可以指向子类的对象

#### 方法多态

创建本类对象时，调用的方法为本类方法
创建子类对象时，调用的方法为之类重写的方法或者继承的方法



### java访问修饰符

| 访问修饰符 | 本类 | 同包 | 子类 | 其他 |
| ---------- | ---- | ---- | ---- | ---- |
| private    | √    |      |      |      |
| 默认       | √    | √    |      |      |
| protected  | √    | √    | √    |      |
| public     | √    | √    | √    | √    |





### static

#### Java 中的 static 使用之静态变量

<font size=3>Java 中被 static 修饰的成员称为静态成员或类成员。它属于整个类所有，而不是某个对象所有，即被类的所有对象所共享。静态成员可以使用类名直接访问，也可以使用对象名进行访问。当然，鉴于他作用的特殊性更推荐用类名访问~~</font>

使用 static 可以修饰变量、方法和代码块。

例如，我们在类中定义了一个 静态变量 hobby ，操作代码如下所示：

[![img](http://img.mukewang.com/5392d47b0001571708530473.jpg)](http://img.mukewang.com/5392d47b0001571708530473.jpg)

运行结果：[![img](http://img.mukewang.com/5392d4a4000133c002950084.jpg)](http://img.mukewang.com/5392d4a4000133c002950084.jpg)

**注意：**静态成员属于整个类，当系统第一次使用该类时，就会为其分配内存空间直到该类被卸载才会进行资源回收！~~







#### Java 中的 static 使用之静态方法

与静态变量一样，我们也可以使用 static 修饰方法，称为静态方法或类方法。其实之前我们一直写的 main 方法就是静态方法。静态方法的使用如：

[![img](http://img.mukewang.com/539137150001c96c08220542.jpg)](http://img.mukewang.com/539137150001c96c08220542.jpg)

运行结果：[![img](http://img.mukewang.com/5391358100013f8502330076.jpg)](http://img.mukewang.com/5391358100013f8502330076.jpg)

需要注意：

1、 **静态方法中可以直接调用同类中的静态成员，但不能直接调用非静态成员。**如：

[![img](http://img.mukewang.com/5392d6eb0001283007020239.jpg)](http://img.mukewang.com/5392d6eb0001283007020239.jpg)

**如果希望在静态方法中调用非静态变量，可以通过创建类的对象，然后通过对象来访问非静态变量**。如：

[![img](http://img.mukewang.com/5392d7390001a10806150193.jpg)](http://img.mukewang.com/5392d7390001a10806150193.jpg)

2、 **在普通成员方法中，则可以直接访问同类的非静态变量和静态变量**，如下所示：

[![img](http://img.mukewang.com/5392d78e000155c305470193.jpg)](http://img.mukewang.com/5392d78e000155c305470193.jpg)

3、 **静态方法中不能直接调用非静态方法，需要通过对象来访问非静态方法。**如：

[![img](http://img.mukewang.com/53a3fb160001d04a04910345.jpg)](http://img.mukewang.com/53a3fb160001d04a04910345.jpg)









#### Java 中的 static 使用之静态初始化块

Java 中可以通过初始化块进行数据赋值。如：

[![img](http://img.mukewang.com/5392da9600010e5503680168.jpg)](http://img.mukewang.com/5392da9600010e5503680168.jpg)

在类的声明中，可以包含多个初始化块，当创建类的实例时，就会依次执行这些代码块。如果使用 static 修饰初始化块，就称为静态初始化块。

需要特别注意：**静态初始化块只在类加载时执行，且只会执行一次，同时静态初始化块只能给静态变量赋值，不能初始化普通的成员变量**。

我们来看一段代码：

[![img](http://img.mukewang.com/53941e320001fdd507670575.jpg)](http://img.mukewang.com/53941e320001fdd507670575.jpg)

运行结果：

[![img](http://img.mukewang.com/53941e880001cb8003530223.jpg)](http://img.mukewang.com/53941e880001cb8003530223.jpg)

通过输出结果，我们可以看到，程序运行时静态初始化块最先被执行，然后执行普通初始化块，最后才执行构造方法。由于静态初始化块只在类加载时执行一次，所以当再次创建对象 hello2 时并未执行静态初始化块。







### final关键字

final可以修饰类、方法、属性和变量

final修饰类，则该类不允许被继承

final修饰方法，则改方法不允许被覆盖(重写)

final修饰属性

​		则该类的属性不可修改且不会进行隐式自动初始化

​		或在构造方法中赋值（只能选其一）

final修饰变量，变量不可修改，只能赋值一次，即变为常量









### 什么是 Java 中的内部类

**问：什么是内部类呢？**

答：内部类（ Inner Class ）就是定义在另外一个类里面的类。与之对应，包含内部类的类被称为外部类。

**问：那为什么要将一个类定义在另一个类里面呢？清清爽爽的独立的一个类多好啊！！**

答：内部类的主要作用如下：

1. 内部类提供了更好的封装，可以把内部类隐藏在外部类之内，不允许同一个包中的其他类访问该类

2. 内部类的方法可以直接访问外部类的所有数据，包括私有的数据

3. 内部类所实现的功能使用外部类同样可以实现，只是有时使用内部类更方便

**问：内部类有几种呢？**

答：内部类可分为以下几种：

- 成员内部类
- 静态内部类
- 方法内部类
- 匿名内部类

#### Java 中的成员内部类

内部类中最常见的就是成员内部类，也称为普通内部类。我们来看如下代码：

[![img](http://img.mukewang.com/539e60d80001223908320512.jpg)](http://img.mukewang.com/539e60d80001223908320512.jpg)

运行结果为：[![img](http://img.mukewang.com/539e60f70001b89302170050.jpg)](http://img.mukewang.com/539e60f70001b89302170050.jpg)

从上面的代码中我们可以看到，**成员内部类的使用方法**：

1、 Inner 类定义在 Outer 类的内部，相当于 Outer 类的一个成员变量的位置，Inner 类可以使用任意访问控制符，如 public 、 protected 、 private 等

2、 Inner 类中定义的 test() 方法可以直接访问 Outer 类中的数据，而不受访问控制符的影响，如直接访问 Outer 类中的私有属性a

3、 定义了成员内部类后，必须使用外部类对象来创建内部类对象，而不能直接去 new 一个内部类对象，即：内部类 对象名 = 外部类对象.new 内部类( );

4、 编译上面的程序后，会发现产生了两个 .class 文件

[![img](http://img.mukewang.com/53a004590001164004560040.jpg)](http://img.mukewang.com/53a004590001164004560040.jpg)

其中，第二个是外部类的 .class 文件，第一个是内部类的 .class 文件，即成员内部类的 .class 文件总是这样：外部类名$内部类名.class

另外，**友情提示哦：**

1、 外部类是不能直接使用内部类的成员和方法滴

[![img](http://img.mukewang.com/54641b6300012da606460299.jpg)](http://img.mukewang.com/54641b6300012da606460299.jpg)

可先创建内部类的对象，然后通过内部类的对象来访问其成员变量和方法。

2、 如果外部类和内部类具有相同的成员变量或方法，内部类默认访问自己的成员变量或方法，如果要访问外部类的成员变量，可以使用 this 关键字。如：

[![img](http://img.mukewang.com/539e638b0001ab1208200295.jpg)](http://img.mukewang.com/539e638b0001ab1208200295.jpg)

运行结果：[![img](http://img.mukewang.com/539e63d400016cf101960050.jpg)](http://img.mukewang.com/539e63d400016cf101960050.jpg)



#### Java 中的静态内部类

静态内部类是 static 修饰的内部类，这种内部类的特点是：

1、 静态内部类不能直接访问外部类的非静态成员，但可以通过 **new 外部类().成员** 的方式访问 

2、 如果外部类的静态成员与内部类的成员名称相同，可通过“类名.静态成员”访问外部类的静态成员；如果外部类的静态成员与内部类的成员名称不相同，则可通过“成员名”直接调用外部类的静态成员

3、 创建静态内部类的对象时，不需要外部类的对象，可以直接创建 **内部类 对象名= new 内部类();**

[![img](http://img.mukewang.com/539e948a0001a71007630511.jpg)](http://img.mukewang.com/539e948a0001a71007630511.jpg)

运行结果 ： [![img](http://img.mukewang.com/539e94a500014f0101930052.jpg)](http://img.mukewang.com/539e94a500014f0101930052.jpg)



#### Java 中的方法内部类

方法内部类就是内部类定义在外部类的方法中，方法内部类只在该方法的内部可见，即只在该方法内可以使用。

[![img](http://img.mukewang.com/539ea96700013ca708200621.jpg)](http://img.mukewang.com/539ea96700013ca708200621.jpg)

**一定要注意哦：**由于方法内部类不能在外部类的方法以外的地方使用，因此方法内部类不能使用访问控制符和 static 修饰符。



### Object类

#### toString()方法

在Object类里面定义toString()方法的时候返回的对象在哈希code码(对象地址字符串)

可以通过重写toString()方法表示出对象的属性

#### equals和==的区别

==是一个比较运算符，基本数据类型比较的是值，引用数据类型比较的是地址值。

equals()是一个方法，只能比较引用数据类型。重写前比较的是地址值，重写后比一般是比较对象的属性。

**除了String和封装器，equals()和“==”没什么区别**
**但String和封装器重写了equals()，所以在这里面，equals()指比较字符串或封装对象对应的原始值是否相等，"=="是比较两个对象是否为同一个对象**





### 引用类型转换

1.向上类型转换（隐式/自动类型转换），是小类型到大类型的转换

2.向下类型转换（强制类型转换），是大类型到小类型

3.instanceof运算符（判断前面是否包含后面），来解决引用对象的类型，避免类型转换的安全性问题



### 接口interface

必选加sbstract关键字，默认有加

**接口可以多继承父类，但类只能单继承**
**一个类可以实现一个或多个接口**

常量：接口中的属性是常量，即使定义时不添加public static final修饰符，系统也会自动加上
方法：只能是抽象方法，不加public static修饰符，系统也会自动加上

#### 匿名内部类

没有名字的内部类，一般不关注类的名称只关注实现

语法：

`Interface i=new Interface(){`

`public void method(){...};`

`}`

`i.method`







### java中String new和直接赋值的区别

    对于字符串：其对象的引用都是存储在栈中的，如果是编译期已经创建好(直接用双引号定义的)的就存储在常量池中，如果是运行期（new出来的）才能确定的就存储在堆中。对于equals相等的字符串，在常量池中永远只有一份，在堆中有多份。

例如：

String str1="ABC"； 和String str2 = new String("ABC"); 

**String str1="ABC" 可能创建一个对象或者不创建对象**，如果"ABC"这个字符串在java String池里不存在，会在java String池创建这个一个String对象("ABC").如果已经存在，str1直接reference to 这个String池里的对象。

**String str2 = new String("ABC") 至少创建一个对象，也可能两个。**因为用到new 关键字，会在heap创建一个 str2 的String 对象，它的value 是 "ABC".同时，如果"ABC"这个字符串在java String池里不存在，会在java String池创建这个一个String对象("ABC").

String 有一个**intern()** 方法，native，用来检测在String pool是否已经有这个String存在。



考虑下面的问题：

String str1 = new String("ABC");
String str2 = new String("ABC");

str1 == str2 的值是True 还是False呢？ False.

String str3 = "ABC";
String str4 = "ABC";

String str5 = "A" + "BC";

str3 == str4 的值是True 还是False呢？ True.

str3 == str5 的值是True 还是False呢？ True.

String a = "ABC";
String b="AB";
String c=b+"C";
System.out.println(a==c); false
a和b都是字符串常量所以在编译期就被确定了！

而c中有个b是引用不是字符串常量所以不会在编译期确定。
而String是final的！所以在b+"c"的时候实际上是新创建了一个对象，然后在把新创建对象的引用传给c.



    public static void main(String[] args) throws Exception {  
        String a =  "b" ;   
        String b =  "b" ;   
        System.out.println( a == b);   
        String d = new String( "d" ).intern() ; //jdk6复制副本但还是指向堆内存，jdk6+复制了后把引用也指过去了
        String c = "d" ;  
        System.out.println( c == d);  //jdk6及以前为false，jdk6+为true
        System.out.println("------------------"); 
        String d1 = new String( "d" ) ; 
        String e1=d1.intern();
        String c1 = "d" ;   
        System.out.println( c1 == d1);  
        System.out.println( c1 == e1);  
        System.out.println( e1 == d1); 
        System.out.println("------------------"); 
        String s1=new String("kvill"); 
        String s2=s1.intern(); 
        System.out.println( s1==s2 ); //s1=s1.intern()
        System.out.println( s1+" "+s2 ); 
        System.out.println( s2==s1.intern() ); 
    }  

运行结果：
true
true
false
true
false
false
kvill kvill
true

s1==s1.intern()为false说明原来的“kvill”仍然存在； 

例子代码：


        String s1 = "china"; 
        String s2 = "china";
        String s3 = "china"; 
        String ss1 = new String("china"); 
        String ss2 = new String("china"); 
        String ss3 = new String("china");   
    
        这里解释一下，对于通过 new 产生一个字符串（假设为 ”china” ）时，会先去常量池中查找是否已经有了 ”china” 对象，如果没有则在常量池中创建一个此字符串对象，然后堆中再创建一个常量池中此 ”china” 对象的拷贝对象。

**也就是有道面试题： String s = new String(“xyz”); 产生几个对象？**

**一个或两个。如果常量池中原来没有 ”xyz”, 就是两个。如果原来的常量池中存在“xyz”时，就是一个。**

对于基础类型的变量和常量：变量和引用存储在栈中，常量存储在常量池中。

应用的情况：建议在平时的使用中，尽量使用String = “abcd”;这种方式来创建字符串，而不是String = new String(“abcd”);这种形式，因为使用new构造器创建字符串对象一定会开辟一个新的heap（堆）空间，而双引号则是采用了String interning(字符串驻留)进行了优化，效率比构造器高。







### String

**String 对象创建后则不能被修改**，是不可变的，所谓的修改其实是创建了新的对象，所指向的内存空间不同。

#### Java 中 String 类的常用方法 Ⅰ

String 类提供了许多用来处理字符串的方法，例如，获取字符串长度、对字符串进行截取、将字符串转换为大写或小写、字符串分割等，下面我们就来领略它的强大之处吧。

String 类的常用方法：

[![img](http://img.mukewang.com/53d9f7d200010bb007780366.jpg)](http://img.mukewang.com/53d9f7d200010bb007780366.jpg)

结合代码来熟悉一下方法的使用：

[![img](http://img.mukewang.com/53a8e7320001a8d807090391.jpg)](http://img.mukewang.com/53a8e7320001a8d807090391.jpg)

运行结果：

[![img](http://img.mukewang.com/53a8e74e00011f5703850166.jpg)](http://img.mukewang.com/53a8e74e00011f5703850166.jpg)

**友情提示：**

\1. 字符串 str 中字符的索引从0开始，范围为 0 到 str.length()-1

\2. 使用 indexOf 进行字符或字符串查找时，如果匹配返回位置索引；如果没有匹配结果，返回 -1

\3. 使用 substring(beginIndex , endIndex) 进行字符串截取时，包括 beginIndex 位置的字符，不包括 endIndex 位置的字符



#### Java 中的 String 类常用方法 Ⅱ

我们继续来看 String 类常用的方法，如下代码所示：

[![img](http://img.mukewang.com/53a9260b0001808e06540410.jpg)](http://img.mukewang.com/53a9260b0001808e06540410.jpg)

运行结果：

[![img](http://img.mukewang.com/53a9239300017e1c07910137.jpg)](http://img.mukewang.com/53a9239300017e1c07910137.jpg)

那么，“==” 和 equals() 有什么区别呢？
==: 判断两个字符串在内存中首地址是否相同，即判断是否是同一个字符串对象
equals(): 比较存储在两个字符串对象中的内容是否一致

PS：字节是计算机存储信息的基本单位，1 个字节等于 8 位， gbk 编码中 1 个汉字字符存储需要 2 个字节，1 个英文字符存储需要 1 个字节。所以我们看到上面的程序运行结果中，每个汉字对应两个字节值，如“学”对应 “-47 -89” ，而英文字母 “J” 对应 “74” 。同时，我们还发现汉字对应的字节值为负数，原因在于每个字节是 8 位，最大值不能超过 127，而汉字转换为字节后超过 127，如果超过就会溢出，以负数的形式显示。



####   java中字符串和字符数组的转换？

1、字符串是类，字符数组是数组。
2、字符数组是char类型的，字符串是String类型的
3、两者之间的相互转化：
String s="this is a string";
char[ ] c={'t','h','i','s','i','s','a','c','h','a','r'};
字符串转换为字符数组
char[ ] ch=s.toCharArray();
字符数组转化为字符串
String str=string.valueOf(c);  



###  StringBuilder 和StringBuffer

当频繁操作字符串时，就会额外产生很多临时变量。使用 StringBuilder 或 StringBuffer 就可以避免这个问题。至于 StringBuilder 和StringBuffer ，它们基本相似，不同之处，**StringBuffer 是线程安全的，而 StringBuilder 则没有实现线程安全功能**，所以性能略高。因此一般情况下，如果需要创建一个内容可变的字符串对象，应优先考虑使用 StringBuilder 类。

那么如何定义 StringBuilder 类的对象呢？ 我们来看下面的代码：

[![img](http://img.mukewang.com/53a7d1f70001be9d06340127.jpg)](http://img.mukewang.com/53a7d1f70001be9d06340127.jpg)

运行结果： **imooc**  





#### Java 中的 StringBuilder 类的常用方法

StringBuilder 类提供了很多方法来操作字符串：

[![img](http://img.mukewang.com/53a7d34300011c6005970125.jpg)](http://img.mukewang.com/53a7d34300011c6005970125.jpg)

例如：在下面的示例代码中，创建了 StringBuilder 对象，用来存储字符串，并对其做了追加和插入操作。这些操作修改了 str 对象的值，而没有创建新的对象，这就是 StringBuilder 和 String 最大的区别。

[![img](http://img.mukewang.com/53a7d36c0001e3cd06760242.jpg)](http://img.mukewang.com/53a7d36c0001e3cd06760242.jpg)

运行结果： [![img](http://img.mukewang.com/53a7d3ab0001ff3803060080.jpg)](http://img.mukewang.com/53a7d3ab0001ff3803060080.jpg)







### Java 中基本类型和字符串之间的转换

在程序开发中，我们经常需要在基本数据类型和字符串之间进行转换。

其中，基本类型转换为字符串有三种方法：

\1. 使用包装类的 toString() 方法

\2. 使用String类的 valueOf() 方法

\3. 用一个空字符串加上基本类型，得到的就是基本类型数据对应的字符串

[![img](http://img.mukewang.com/53abea61000151e105120118.jpg)](http://img.mukewang.com/53abea61000151e105120118.jpg)

再来看，将字符串转换成基本类型有两种方法：

\1. 调用包装类的 parseXxx 静态方法

\2. 调用包装类的 valueOf() 方法转换为基本类型的包装类，会自动拆箱

[![img](http://img.mukewang.com/53abeaad000109af04610098.jpg)](http://img.mukewang.com/53abeaad000109af04610098.jpg)







#### valueOf与parseInt方法

**首先从返回类型可以看出parseInt返回的是基本类型int，而valueOf返回的是对象（可自动拆装箱）。**

源码：

`public static Integer valueOf(String s) throws NumberFormatException {`
        `return Integer.valueOf(parseInt(s, 10));`
 `}`

 `public static Integer valueOf(int i) {`
    `assert IntegerCache.high >= 127;`
 `if (i >= IntegerCache.low && i <= IntegerCache.high)`
        `return IntegerCache.cache[i + (-IntegerCache.low)];`
    `return new Integer(i);`
 `}`

 `public static int parseInt(String s) throws NumberFormatException {`
    `return parseInt(s,10);`
 `}`

因为JDK5以后实现了自动拆装箱，因而两者的差别也不是特别大了，但是从效率上考虑，建议首先考虑parseInt方法。