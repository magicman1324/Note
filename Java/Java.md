

# Java的运行

jdk   Java Development Kit

它是一个用于开发小程序和Java应用程序的软件开发环境。JDK是物理存在的，它包含JRE+开发工具。

jre    Java Runtime Environment

它是一组为运行其他软件而设计的软件工具。它是JVM的一种实现，JRE提供了一个运行时环境。

jvm    Java Virtual Machine

JVM是一个将Java**字节码**转换为机器语言的抽象机器。它还能够运行程序员用其他语言编写的程序（编译为Java字节码）。JVM也被称为虚拟机，因为它在物理上并不存在。JVM本质上是JRE（Java运行环境）的一部分。

## 执行过程

编码-》编译成class文件（字节码文件）-》用jvm执行

![](F:\Photos\snipaste\Java\Java 最早\Test.png)

### javac 与java

javac：是编译命令，将java源文件编译成class字节码文件 

将文件保存成class文件

java：是运行字节码文件 由jvm对字节码进行解释与与运行 

将class文件放在内存中

# package

package com.microsoft.demo

. 代表文件夹

用来定位的 说明你的Main.java在哪里

![](F:\Photos\snipaste\Java\Java 最早\package.png)



# javadoc

![](F:\Photos\snipaste\Java\Java 最早\javadoc.png)

```shell
javadoc -encoding UTF-8 -docencoding UTF-8 -charset UTF-8 Main.java
```

参数含义：

- `-encoding UTF-8`：告诉 javadoc 去按 UTF‑8 解读你的 `.java` 源文件。
- `-docencoding UTF-8`：告诉它用 UTF‑8 编码输出生成的 HTML 文件。
- `-charset UTF-8`：指定 HTML 中声明的字符集。

# String

# 自动类型转换

![](F:\Photos\snipaste\Java\Java 最早\自动类型转换.png)

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

![](F:\Photos\snipaste\Java\Java 最早\空指针异常.png)

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

![](F:\Photos\snipaste\Java\Java 最早\toString 1.png)

特殊的单独写-------方法的重写

![](F:\Photos\snipaste\Java\Java 最早\toString 2.png)

# 构造方法

alt insert   constuctor 

![](F:\Photos\snipaste\Java\Java 最早\构造方法.png)

用来初始化对象（实例）



![](F:\Photos\snipaste\Java\Java 最早\构造方法的重载.png)

**构造方法可以重载**

*java 垃圾回收机制（自动）

```java
System.gc(); //手动回收
```

# 静态变量与静态方法

![](F:\Photos\snipaste\Java\Java 最早\静态变量.png)

`static` 关键字的主要作用是使成员属于**类**而不是类的实例，并提供对这些成员的类级别访问。

## private static

<img src="F:\Photos\snipaste\Java\Java 最早\private static.png"  />

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

![](F:\Photos\snipaste\Java\Java 最早\继承.png)

## 多层继承

爷父孙

灰太狼 

属性：吃不到羊

太太太太太太太太太太爷爷 ——》.......+》灰太狼

## 方法的重写

alt insert   @Override

![](F:\Photos\snipaste\Java\Java 最早\方法的重写.png)

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

![](F:\Photos\snipaste\Java\Java 最早\抽象类.png)

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





# 左移

```java
public class Main {
    public static void main(String[] args) {
        int i=-1;
        System.out.println("初始数据"+i);
        System.out.println("初始数据对应的二进制字符串"+Integer.toBinaryString(i));
        i<<=42;  //== i<<=10   等同于 左移十位
        System.out.println("左移42位后的数据"+i);
        System.out.println("左移42位后对应的二进制字符"+Integer.toBinaryString(i));
    }
}
```

# 异常

```java
public class Main {
    public static void main(String[] args) {
        try{
            test(1,0);
        }catch (Exception e){
            e.printStackTrace();
        }
}
    public static int test(int a,int b) throws Exception{
        if(b==0)throw new Exception("by zero precision");
        return a/b;
    }
}
```

# 数学类

```java
import java.sql.SQLOutput;
import java.util.Random;

public class Main{
    public static void main(String[] args) {
        System.out.println(Math.pow(5,3));

        System.out.println(Math.abs(-1));
        System.out.println(Math.max(91, 31));
        System.out.println(Math.min(2, 3));
        System.out.println(Math.sqrt(4));
        System.out.println(Math.sin(Math.PI / 2));
        System.out.println(Math.cos(Math.PI));
        System.out.println(Math.tan(Math.PI / 4));

        System.out.println(Math.asin(1));
        System.out.println(Math.acos(1));
        System.out.println(Math.atan(0));

        System.out.println(Math.sin(Math.PI));
        Math.log(Math.E);//e为底的对数函数ln
        Math.log10(100);

        double a=Math.log(4)/Math.log(2);
        System.out.println(a);

        System.out.println(Math.ceil(2.4)); //向上取整
        System.out.println(Math.floor(4.6)); //向下取整

        Random ran =new Random();
        for(int i=0;i<30;i++){
            System.out.print(ran.nextInt(100)+" ");  //nextInt 0-100之间的随机数
        }
    }

}
```

# 数组类

```java
import java.sql.SQLOutput;
import java.util.Arrays;
import java.util.Random;

public class Main{
    public static void main(String[] args) {
       int []a =new int[]{1,3,4,2,4,5,2,3,4,2,1};
       System.out.println(Arrays.toString(a));
       Arrays.sort(a);
       System.out.println(Arrays.toString(a));

       int []arr=new int[10];
       Arrays.fill(arr,66);
        System.out.println(Arrays.toString(arr));

        int []p=new int[]{1,2,3,4,5};
        int []target =Arrays.copyOf(p,5);
        System.out.println(Arrays.toString(target));
        System.out.println(p==target);

        int []target2 =Arrays.copyOfRange(p,3,5);
        System.out.println(Arrays.toString(target2));
        System.out.println(p==target2);

        int[] g=new int[]{2,3,4,5,6};
        int[] gt=new int[5];
        System.arraycopy(g,0,gt,0,5);
        System.out.println(Arrays.toString(gt));

        System.out.println(Arrays.binarySearch(g,5));

        int [][]d=new int[][]{{2,22,4,2},{24,4,1,5}};
        System.out.println(Arrays.deepToString(d));
        int [][]e=new int[][]{{2,22,4,2},{24,4,1,5}};
        System.out.println(Arrays.deepEquals(d,e));
    }

}
```

# 数据结构

```java
/**
 线性表抽象类
 @param <E> 存储的数据类型

 **/

public abstract class AbstractList<E> {
    /**
     * 获取表的长度
     * @return 长度
     */
    public abstract int size();

    /**
     * 指定位置添加元素
     * @param e  元素
     * @param index  索引，从0开始
     */
    public abstract void add(E e,int index);

    /**
     * 指定位置移除
     * @param index 位置，索引
     */
    public abstract void remove(int index);

    /**
     * 获取指定位置的元素
     * @param index  索引，位置
     * @return 元素
     */
    public abstract  E get(int index);
}

```

```java
/**
 * 队列抽象类
 * @param <E>
 */
public abstract class AbstractQueue <E>{
    /**
     * 进队操作
     * @param e
     */
    public abstract void offer(E e);

    /**
     * 出队操作
     * @return 元素
     */
    public  abstract E poll();
}

```

```java
/**
 * 栈抽象类
 * @param <E>
 */
public abstract class AbstractStack <E> {
    /**
     * 在尾部添加 元素
     * * @param e  元素
     */
    public abstract void push(E e);

    /**
     * 尾部删除元素
     * @return 元素
     */
    public  abstract  E pop();

}	

```

# 顺序表

Arraylist.java

```java
package com.test.collection;

public class ArrayList<E> {
    private int size = 0;
    private int capacity = 10;
    private  Object[] array=new Object[capacity];

    /***
     *  顺序表的插入操作
     * @param element 插入元素
     * @param index   插入位置
     */
    public void add(E element,int index){
        if(index<0||index>size){
            throw new IndexOutOfBoundsException("index不合法，index须在0~"+size);
        }
        if(size>=capacity){
            int newCapacity=capacity+(capacity>>1);
            Object[] newArray = new Object[newCapacity];
            System.arraycopy(array,0,newArray,0,size);
            array=newArray;
            capacity=newCapacity;
        }
        for(int i=size;i>index;i--){
            array[i]=array[i-1];

        }
        array[index]=element;
        size++;
    }

    /**
     * 打印顺序表的tostring重写方法
     * @return
     */
    @Override
    public String toString() {
        StringBuilder stringBuilder=new StringBuilder();
        for(int i=0;i<size;i++){
            stringBuilder.append(array[i]).append(" ");

        }return stringBuilder.toString();
    }

    /**
     * 顺序表的删除操作
     * @param index
     * @return   删除的元素
     */
    @SuppressWarnings("unchecked")
    public E remove(int index){
        E e=(E)array[index];
        for(int i=index;i<size;i++){
            array[i]=array[i+1];

        }
        size--;
        return e;
    }

    /**
     * 顺序表的查找操作
     * @param index
     * @return 查找的元素
     */
    @SuppressWarnings("unchecked")
    public E get(int index){
        if(index<0||index>size){
            throw new IndexOutOfBoundsException("查询位置不合法，范围是0~"+index);
        }
        return (E) array[index];
    }

    /**
     * 判断是否为空
     * @return
     */
    public boolean isEmpty(){
        return size==0;
    }
}

```

Main.java

```java
package com.test.collection;
import com.test.collection.ArrayList;
public class Main {
    public static void main(String[] args) {
        ArrayList<String> list =new ArrayList<>();
        list.add("AAA",0);
        list.add("BBB",1);
        list.add("CCC",2);
        System.out.println(list.get(2));
        System.out.println(list);
        list.remove(0);
        list.remove(0);
        list.remove(0);
        System.out.println(list.isEmpty());
    }
}

```

# 线性表

LinkedList.java

```java
package com.test.collection;

import javax.imageio.plugins.jpeg.JPEGImageReadParam;

/**
 * 线性表的类定义
 * @param <E>
 */
public class LinkedList<E> {
    //头节点不带元素，首元节点
    private  Node<E>head=new Node<>(null);
    private  int size;

    private static class Node<E>{
        E element;
        Node<E> next;

        public Node(E element){
            this.element=element;
        }

    }

    /**
     * 线性表的添加
     * @param element
     * @param index
     */
    public  void add(E element,int index){
        if(index<0||index>size){
            throw new IndexOutOfBoundsException("添加位置不合法，范围应在0~"+size);
        }
        Node<E>prev=head;
        for(int i=0;i<index;i++){
            prev= prev.next;
        }
        Node<E> node=new Node<>(element);
        node.next=prev.next;
        prev.next=node;
        size++;
    }

    /**
     * 线性表的打印 重写toString
     * @return
     */
    public String toString(){
        StringBuilder stringBuilder=new StringBuilder();
        Node<E> node=head.next;
        while(node!=null){
            stringBuilder.append(node.element).append("->");
            node=node.next;
        }
        stringBuilder.append("null");
        return stringBuilder.toString();
    }

    /**
     * 线性表的删除
     * @param index
     * @return
     */
    public E remove(int index){
        if(index<0||index>size){
            throw new IndexOutOfBoundsException("删除位置不合法，范围0~"+size);
        }

        Node<E>prev=head;
        while(index-->0){
            prev=prev.next;
        }
        Node<E>node;
        node=prev;
        prev=prev.next.next;
        node.next=prev;
        size--;
        return node.element;
    }

    /**
     * 线性表的查找
     * @param index
     * @return
     */
    public E get(int index){
        if(index<0||index>size){
            throw new IndexOutOfBoundsException("查找位置不合法，范围0~"+size);
        }
        Node<E>prev=head;
        //查找和删除不同，直接index遍历到该位置就行，不需要停在前一个位置
        while(index-->=0){
            prev=prev.next;
        }
        Node<E>node=new Node<>(prev.element);
        node=prev;
        return node.element;
    }

}
```

Main.java

```java
package com.test.collection;
import com.test.collection.ArrayList;
public class Main {
    public static void main(String[] args) {
        LinkedList<String> list =new LinkedList<>();
        list.add("AAA",0);
        list.add("BBB",1);
        list.add("CCC",2);
        System.out.println(list.get(2));
        System.out.println(list);
        list.remove(0);
        System.out.println(list);
//        System.out.println(list.isEmpty());
    }
}

```

