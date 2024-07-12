# Java的运行

jdk   Java Development Kit

它是一个用于开发小程序和Java应用程序的软件开发环境。JDK是物理存在的，它包含JRE+开发工具。

jre    Java Runtime Environment

它是一组为运行其他软件而设计的软件工具。它是JVM的一种实现，JRE提供了一个运行时环境。

jvm    Java Virtual Machine

JVM是一个将Java**字节码**转换为机器语言的抽象机器。它还能够运行程序员用其他语言编写的程序（编译为Java字节码）。JVM也被称为虚拟机，因为它在物理上并不存在。JVM本质上是JRE（Java运行环境）的一部分。

## 执行过程

编码-》编译成class文件（字节码文件）-》用jvm执行

![](F:\Photos\snipaste\Java\Test.png)

### javac 与java

javac：是编译命令，将java源文件编译成class字节码文件 

将文件保存成class文件

java：是运行字节码文件 由jvm对字节码进行解释与与运行 

将class文件放在内存中

# package

package com.microsoft.demo

. 代表文件夹

用来定位的 说明你的Main.java在哪里

![](F:\Photos\snipaste\Java\package.png)

# String

# 自动类型转换

![](F:\Photos\snipaste\Java\自动类型转换.png)

# 方法的重载

 一是方法名相同，二是参数个数或参数类型不相同

# 变换思维

POP：面向过程

过程：

1.思考一些过程

2.思考第一步怎么做

3.思考第二步怎么做

4.接着怎么做

5.....

6.最后怎么做（return 0）

OOP：面向对象

1.该程序，要大众化

2.目标

3.不强调过程

## 规划目标站在更高层级看待事物

1.计划、规划-----设计它

2.当你执行完计划的时候----达到目标

3.OOP：站在更高层面看待事物

## 设计思维

 先考虑共性

## 代码例子

```java
package com.microsoft.bean;

public class Dogs {
    public String name;
    public String variety;
    public int age;
    public String food;

    void eat() {
        System.out.println("狗吃饭");
    }

    void sleep() {
        System.out.println("狗睡觉");
    }
}

package com.microsoft.bean;

public class ApplicationRun {
    public static void main(String[] args) {
        //对象 --实例
        //现实生活的一个东西，对抽象的东西进行表示出来的产物
        //实例：是一个活生生存在的事物，他是唯一的
        Dogs zhangDog = new Dogs();

        zhangDog.name = "Jerry";
        zhangDog.age = 2;
        zhangDog.variety = "拉布拉多";
        zhangDog.sleep();
        System.out.println("张大爷的狗叫啥名:"+zhangDog.name);
        Dogs wangDog = new Dogs();
        wangDog.name = "Tom";
        wangDog.age = 2;
        wangDog.variety = "藏獒";

        System.out.println("王阿姨的狗叫啥名:"+wangDog.name);
    }
}


```

# 成员变量行为类与this

```
//狗类 狗都有这些
// 类当中的变量和函数总称为：属性（共性、特性）
```

```
//成员变量：它们的组成构成了类，所以我们这样命名
//它们是类的组成部分
```

```
//一个动作，这些方法（函数）在类当中，我们有很好听的名字----行为
```

```
//this 指 调用对象
```

# 注销账户与空指针异常

```
//NullPointerException
```

![](F:\Photos\snipaste\Java\空指针异常.png)

# OOP封装

设置成private 

写Getter Setter 函数

```java
public void setAge(int age){
        if (age<0 ||age>30){
            System.out.println("输入数据不合法，已清零");
        }else{
            this.age = age ;
        }
    }
```

setAge();setName();面向对象的思想

# jar 导入和lombok

# toString 

alt insert 选中 toString  然后全选

![](F:\Photos\snipaste\Java\toString 1.png)

特殊的单独写-------方法的重写

![](F:\Photos\snipaste\Java\toString 2.png)

# 构造方法

alt insert   constuctor 

![](F:\Photos\snipaste\Java\构造方法.png)

用来初始化对象（实例）



![](F:\Photos\snipaste\Java\构造方法的重载.png)

**构造方法可以重载**

*java 垃圾回收机制（自动）

```java
System.gc(); //手动回收
```

# 静态变量与静态方法

![](F:\Photos\snipaste\Java\静态变量.png)

`static` 关键字的主要作用是使成员属于**类**而不是类的实例，并提供对这些成员的类级别访问。

## private static

<img src="F:\Photos\snipaste\Java\private static.png"  />

```java
private static String plot="xibei";
public static String getPlotInstance(){
    return plot;
}
```

## static 单例

```java
public class Earth {
    private static Earth earthInstance = new Earth();

    private Earth(){
    }

    public static Earth getEarthInstance(){
        return earthInstance;
    }
}
//使用静态变量来实现单例模式。单例模式是一种设计模式，其目的是确保一个类只有一个实例，并提供一个全局访问点。
```

# 继承

```java
public class Dogs extends Animal{
}
```

extends  子类继承父类

![](F:\Photos\snipaste\Java\继承.png)

## 多层继承

爷父孙

灰太狼 

属性：吃不到羊

太太太太太太太太太太爷爷 ——》.......+》灰太狼

## 方法的重写

alt insert   @Override

![](F:\Photos\snipaste\Java\方法的重写.png)

子类自己拥有的特性，不是来自父类的，他从父亲那里革新

子类自己认为，应该打破父亲的传统，进行革新，革新的内容就是**方法体**

## super

不想重写，就想用父类的

```java
super.                     //父类的
```

## final

设定final 修饰 ：没人能继承

final 的类 不能被继承

final 的方法不能被重写 只能用父类的



常量增加final

```java
public static final String name = "wang"
```

无法被修改

# 抽象类

抽象     具体

动物      狗

```java
public abstract class Animal {...};
```

![](F:\Photos\snipaste\Java\抽象类.png)

## 抽象类与抽象方法的使用

抽象类可以包含普通方法和抽象方法 

抽象方法不能有实际的意义 。

类的抽象方法必须被子类重写 ，以此来达到限制的作用，使得该方法能被具体的表现出来 （表现出实际的意义）

# 接口

接口中所有的方法都是抽象的 

```java
//Application.java
package com.microsoft.bean;

public class Application {
    public static void main(String[] args) {
        Chinese chinese = new Chinese();
        chinese.eat();
        chinese.run();

        Westerner westerner = new Westerner();
        westerner.eat();
        westerner.run();
    }
}

//Chinese.class
package com.microsoft.bean;
//implement 实现
//类中的方法称之为重写
//接口:实现
public class Chinese implements Human{
    @Override
    public void eat() {
        System.out.println("吃中餐");
    }

    @Override
    public void run() {
        System.out.println("小步跑");
    }
}

//Westerner.class
package com.microsoft.bean;

public class Westerner implements Human{
    @Override
    public void eat() {
        System.out.println("吃西餐");
    }

    @Override
    public void run() {
        System.out.println("大步跑");
    }
}

```

# class 与interface 的区别

Animal抽象类是对具体事物的抽象

Animal接口是对它行为的抽象

抽象类主要是用来抽象类别，接口主要是用来抽象方法功能。当你关注事物的本质的时候，请用抽象类；当你关注一种操作的时候，用接口。

# 多态

两个以上类 有继承关系

花木兰替父从军

吕子乔 吕小布

小吃摊  烧烤 炸串 一体

多种形态 多功能

```java
// HuaHu.class
package com.microsoft.bean;

public class HuaHu {
    public String name = "HuaHu";
    public int age = 45;

    public static void SayMe() {
        System.out.println("大家好！我叫HuaHu，今年45");
    }

    public void fight() {
        System.out.println("干架！");
    }

}

//HuaMuLan.class
package com.microsoft.bean;

public class HuaMuLan extends HuaHu{
    public String name = "HuaMuLan";
    public int age = 19;

    public static void Dressing() {
        System.out.println("化妆...");
    }
    public static void SayMe() {
        System.out.println("大家好！我叫HuaMuLan，今年19");
    }
}


//Application
package com.microsoft.bean;

public class Application {
    public static void main(String[] args) {
        //替父从军 向上转型
        HuaHu huahu = new HuaMuLan();
//        System.out.println(huahu.name);
//        System.out.println(huahu.age);
//        HuaHu.SayMe();

        // 打完仗了，遇到心爱的人，做回自己
        HuaMuLan huaMuLan = (HuaMuLan) huahu;
        System.out.println(huaMuLan.name);
        System.out.println(huaMuLan.age);
        HuaMuLan.SayMe();
        HuaMuLan.Dressing();


    }
}
```

# 匿名内部类

在代码中，已经创建了一个匿名内部类，并重写了 `eat` 和 `run` 方法。要同时调用这两个方法，可以在匿名内部类后面直接调用这两个方法。

```java
package com.microsoft.bean;

public class Application {
    public static void main(String[] args) {
        new Human() {
            @Override
            public void eat() {
                System.out.println("中国人吃中国菜");
            }

            @Override
            public void run() {
                System.out.println("中国人小步跑");
            }
        }.eat(); // 调用 eat 方法
        // 调用 run 方法
        new Human() {
            @Override
            public void eat() {
                System.out.println("中国人吃中国菜");
            }

            @Override
            public void run() {
                System.out.println("中国人小步跑");
            }
        }.run();
    }
}
```

上面的代码中，我在 `eat()` 方法后面直接调用了 `run()` 方法。这样就能同时调用 `eat` 和 `run` 方法。请注意，每次创建新的匿名内部类实例都会导致新的对象创建，因此 `eat()` 和 `run()` 方法的调用是独立的。如果希望在同一个对象上调用这两个方法，可能需要将匿名内部类的实例保存到一个变量中。
