---

title: CS61B-Java
date: 2021-09-04 12:48:15
tags:
- Java
- CS61
- CS61B
categories:
- CS61
cover: /myimage/cs61/cs61b_java_cover.png
---

## CS61B Java

#### 目录

>Java基础
>
>* Hello world
>* 类与实例
>* 方法与域
>* 静态static
>* 作用范围
>* 内存里的数据表示
>
>* 流程控制
>* 构造方法与方法重载
>
>Java高级语法
>
>* 继承与多态
>* 抽象类与接口
>* Java核心类
>
>Java链表
>
>* List（IntList 最直白的链表）
>* SLList（单向链表  哨兵节点）
>* DLList（循环链表 双哨兵节点）
>* Arrays（数组）
>* AList（数组链表）
>

在61B课程的第一部分，讲解了Java语言的基础用法，主要从面向对象的角度全面讲解Java语法特性。



### Java基础



#### HelloWorld

学任何一门语言都要从如何运行开始，关于如何配置Java环境在这就不赘述了，首先我们来看一个简单的Java程序

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
```

我们在Python语言中学过面向对象的编程方式，在Python中，面向对象只是编程的一种方式，而相比于python语言，java的所有代码都运行在一个类中，执行 Java 程序有两个步骤，一是对java程序进行编译，二是运行编译后的java程序，具体我们使用以下代码运行。

```java
$ javac HelloWorld.java
$ java HelloWorld
Hello World! 
```

这样我们就运行了一段java代码。



#### 类与实例

我们在CS61A当中学过，类只有被实例化之后才能作为一个独立的对象进行操作，在java中，对象的实例化使用new进行创建

```java
/**
 * 可以用来自动创建文档的注释
 */
public class Hello {
    
    private String name;
    private int age;
    private static num;
    
    {
    public Hello(String name,int age){
        this.name = name;
        this.age = age;
        num++;
    }
    
    public static void main(String[] args) {
        // 向屏幕输出文本:
        System.out.println("Hello, world!");}
        /* 多行注释开始
        注释内容
        注释结束 */
    }
    
    {
    public int getAge(){
        return this.age;
    }
        
    public String getName(){
        return this.name;
    }
        
    public static int getNum(){
        return num;
    }
    
    
} // class
```

不带返回参数类型的方法在Java类中用作构造方法，构造方法的名称必须和类名相同，这里的`public Hello`方法就是`Hello`类的构造方法，而后我们采用new创建Hello类的实例nh。

```java
>>> Hello nh = new Hello("David",15);
>>> nh.getName()
David
```

Java调用方法的方式与Python相同。



#### 方法与域

一个Java类中有方法和域，例如有一个类Student

``` java
public class Student {
    public String name;
    public int age;
    public int grade;
    
    public Student(String name,int age,int grade){
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
    
    public int getAge(){
        return this.age;
    }
        
    public String getName(){
        return this.name;
    }
    
    public int getGrade(){
        return this.grade;
    }
   
    
}
```

我们看到在这个类当中有`name`，`age`，`grade`三个域和`getName`，`getAge`和`getGrade`三个方法。

域是对象的属性，方法是对象的操作手段。

比如Student这个类就有名称，年龄和年级三个属性，实例化的每个对象都有自己不同的属性值，而他们都可以调用`getName`，`getAge`等方法。



#### 静态static

如果我们想给所有的学生增加school这个域，并且令所有学生的School域都为“MingHai”，那么我们该怎么办呢？

最常规的做法是增加一个域。并且在创建的时候给域赋值。

```java
    public String name;
    public int age;
    public int grade;
    public String school    

    public Student(String name,int age,int grade，String school){
        this.name = name;
        this.age = age;
        this.grade = grade;
        this.school = school;
    }
```

于是我们在创建每个对象的时候引入school域的值。

```java
Student David = new Student("David",15,3,"MingHai");
Student Lee = new Student("Lee",15,3,"MingHai");
Student Jane = new Student("Jane",15,3,"MingHai");
Student Bob = new Student("Bob",15,3,"MingHai");
```

我们会发现这样定义真的很麻烦....

于是我们就有了另一种方式，那就是利用static创建一个静态域。

```java
public String name;
    public int age;
    public int grade;
    public static String school="MingHai";    

    public Student(String name,int age,int grade){
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
```

我们将被static修饰的域称作静态域，没有static修饰的称作实例域，静态域在所有实例化的对象中都具有相同值，当在其中一个实例中修改静态域后，所有实例中的静态域都会发生改变，我们常常利用这个特性来进行计数。

```java
public String name;
    public int age;
    public int grade;
    public static String school="MingHai";    
    private static int num=0;

    public Student(String name,int age,int grade){
        this.name = name;
        this.age = age;
        this.grade = grade;
        num++;
    }
```

static静态除了可以用来修饰域，还可以用来修饰方法，被static修饰的方法只能由类进行调用，实例不可调用静态方法。

我们给Student增加一个可以获取`num`域的静态方法。

```java
public static int getNum() {
    return num;
}
```

这样我们就可以通过类来调用getNum方法了

```java
>>> Student.getNum();
xx
```

此外，static还可以修饰类，被static所修饰的类称为静态类，如果一个类要声明为静态类，只有一种情况，那就是静态内部类，如果在外部声明为静态类，无法通过编译。

静态内部类的相关知识，有看到再补充。



#### 作用范围

Java的作用范围主要有public，private和protected三种，延伸的还有pakage等，暂且不介绍。

作用范围修饰可以用于域，方法和类。

> public所修饰的域，方法可以在类外被调用。
>
> private所修饰的域，方法只能在类内部被调用。
>
> protected所修饰的域，方法只能在继承类被调用。
>

##### 关于域

为了确保安全，我们一般将关键域设置为private，然后利用JavaBean的方式创建getXX和setXX进行设置和访问，基于这个思想我们对Student类进行修改。

```java
public class Student {
    private String name;
    private int age;
    private int grade;
    
    public Student(String name,int age,int grade){
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
    
    public int getAge(){
        return this.age;
    }
        
    public String getName(){
        return this.name;
    }
    
    public int getGrade(){
        return this.grade;
    }
    
    public void setAge(int aAge){
        if(age>15)
        {
           return;
        }
        this.age = aAge;
    }
   
}
```

我们可以看到利用JavaBean的方式，可以在设置的时候对用户输入进行过滤，防止用户输入恶意代码对数据进行篡改。

protected一般用作修饰被继承类的域，这样就可以继承类中调用被继承类的域。



##### 关于方法

private修饰的方法一般是方法中的方法，该方法不能被外部调用篡改，只能在内部使用，比如

```java
private String InitOut = "Hello";

public String getName()
{
    return InitName("Hi,") + name;
}

private String InitName(String a)
{
    InitOut = a;
    return InitName;
}
```

我们需要得到用户的名字，并输出`Hello，xx`，如果将InitName设置为public，那么用户就可以修改InitName,造成安全隐患。



#### 数据在内存中表示

Java的数据类型分为基本类型和引用类型两种。

基本数据类型是CPU可以直接进行运算的类型。Java定义了以下几种基本数据类型：

> 整数类型：byte，short，int，long
>
> 浮点数类型：float，double
>
> 字符类型：char
>
> 布尔类型：boolean

对于基本类型，计算机会直接开辟相应的区域供基本类型存储。

```java
int x;
double y;
```

其在 内存中的表示如图所示：

![image-20210919153239683](https://i.loli.net/2021/09/19/ukH3RUtGZOBLNb7.png)

而对于引用类型，计算机会开辟一块区域来存储首地址，什么意思呢。我们以一个类为例，来看一看引用类型在内存中的存储。

当我们使用new（如狗、海象、行星）对对象进行实例化时，Java 首先为该类的每个实例变量分配一个框，并用默认值填充它们。然后，构造器通常用其他值填充每个框。

假设我们有一个Walrus类

```java
public static class Walrus {
    public int weight;
    public double tuskSize;

    public Walrus(int w, double ts) {
          weight = w;
          tuskSize = ts;
    }
}
```

我们实例化一个对象

```
new Walrus(1000, 8.3);
```

我们来看看这个实例化后的对象在内存中是什么样的。

![image-20210919154637430](https://i.loli.net/2021/09/19/X6tWORdAGxfCsj7.png)

我们发现，实例化后的对象占据了内存中的一块区域，那么我们该怎么确定对象在内存中的位置呢？

当我们声明任何参考类型的变量（海象、狗、行星、阵列等）时，Java 会分配一个 64 位的框，无论对象类型如何。乍一看，这似乎会导致悖论，因为仅仅weight这一个数据就占据了64位的区域，然而有一种办法可以解决这个问题，那就是将实例对象存放的首地址赋给变量。

```java
Walrus wl = new Walrus(100,8.3);
```

具体表示如下

![image-20210919155302354](https://i.loli.net/2021/09/19/FOpgal2w3i6MhNQ.png)

![image-20210919155229244](https://i.loli.net/2021/09/19/TuXL1AKhSRvkjVm.png)

我们将walrus实例在内存中的首地址赋给引用类型的变量wl，这样就可以通过首地址来查找到实例的位置。

我们用箭头简化表示这个过程

![image-20210919155602729](https://i.loli.net/2021/09/19/dQtsVjSJzpAflOK.png)

接下来我们通过一个例子来巩固一下这个概念。

```java
Walrus a = new Walrus(1000, 8.3);
Walrus b;
b = a;
```

执行第一行后，我们有：

![image-20210919155843381](https://i.loli.net/2021/09/19/2ZtFUu83IJHySiQ.png)

执行第二行后，我们有：

![image-20210919155857043](https://i.loli.net/2021/09/19/DdIbyVSieUYLAl2.png)

请注意，上面 b 是未定义的，不是空的。

最后a行只需将盒子中的位复制到b框中。或者就我们的视觉隐喻而言，这意味着 b 将完全复制箭头，现在显示指向同一对象的箭头。

![image-20210919155945022](https://i.loli.net/2021/09/19/z517cWYAl3OQM6a.png)

这就是对象引用的方法。

 ##### 参数传递

引用类型和基本类型在内存中的这种表示，影响最大的就是参数的传递，在Java中，所有的参数传递都是复制位，而非引用地址，我们把这种传参方式称作按值引用。

例如，请考虑以下功能：

```java
public static double average(double a, double b) {
    return (a + b) / 2;
}
```

假设我们调用此函数（如下图所示）

```java
public static void main(String[] args) {
    double x = 5.5;
    double y = 10.5;
    double avg = average(x, y);
}
```

执行此功能的前两行后，主要方法将具有两个标记为x和y的框，其中包含以下值：

![image-20210919160930033](https://i.loli.net/2021/09/19/CjOWkQte3hKn64F.png)

调用该函数时，average函数具有自己的范围，其中两个新框标记为a和b并且位只是复制。当我们说"按值传递"时，我们指的是这些位的复制。

![image-20210919160943966](https://i.loli.net/2021/09/19/MTF9gI8XYAyJ2ah.png)

如果average函数要更改a，x将会保持不变。

那么。如果将传入的参数改为引用类型呢？

```java
public class PassByValueFigure {
    public static void main(String[] args) {
           Walrus walrus = new Walrus(3500, 10.5);
           int x = 9;

           doStuff(walrus, x);
           System.out.println(walrus);
           System.out.println(x);
    }

    public static void doStuff(Walrus W, int x) {
           W.weight = W.weight - 100;
           x = x - 5;
    }
}
```

我们会发现，调用doStuff方法，weight被更改了，而x却没有变化，因为我们传入引用类型的参数，是将首地址复制给另一个引用类型的变量W，无论是walrus.weight还是W.weight指向的都是同一块内存区域。



#### 流程控制

Java的流程控制和Python没什么区别，if，else，for，while，for each.

唯一有些变化的就是for each循环

for循环经常用来遍历数组，因为通过计数器可以根据索引来访问数组的每个元素：

```java
int[] ns = { 1, 4, 9, 16, 25 };
for (int i=0; i<ns.length; i++) {
    System.out.println(ns[i]);
}
```

但是，很多时候，我们实际上真正想要访问的是数组每个元素的值。Java还提供了另一种for each循环，它可以更简单地遍历数组：

```java
public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 4, 9, 16, 25 };
        for (int n : ns) {
            System.out.println(n);
        }
    }
}
```

和for循环相比，for each循环的变量n不再是计数器，而是直接对应到数组的每个元素。for each循环的写法也更简洁。但是，for each循环无法指定遍历顺序，也无法获取数组的索引。

除了数组外，for each循环能够遍历所有“可迭代”的数据类型，包括后面会介绍的List、Map等。



#### 构造方法与方法重载

创建实例的时候，我们经常需要同时初始化这个实例的字段，例如：

```java
Person ming = new Person();
ming.setName("小明");
ming.setAge(12);
```

初始化对象实例需要3行代码，而且，如果忘了调用setName()或者setAge()，这个实例内部的状态就是不正确的。

能否在创建对象实例时就把内部字段全部初始化为合适的值？

完全可以。

这时，我们就需要构造方法。

创建实例的时候，实际上是通过构造方法来初始化实例的。我们先来定义一个构造方法，能在创建Person实例的时候，一次性传入name和age，完成初始化：

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
       this.name = name;
       this.age = age;
   }

   public String getName() {
       return this.name;
   }

    public int getAge() {
       return this.age;
   }

}
由于构造方法是如此特殊，所以构造方法的名称就是类名。构造方法的参数没有限制，在方法内部，也可以编写任意语句。但是，和普通方法相比，构造方法没有返回值（也没有void），调用构造方法，必须用new操作符。
```



##### 默认构造方法

是不是任何class都有构造方法？是的。

那前面我们并没有为Person类编写构造方法，为什么可以调用new Person()？

原因是如果一个类没有定义构造方法，编译器会自动为我们生成一个默认构造方法，它没有参数，也没有执行语句，类似这样：

```java
class Person {
    public Person() {
    }
}
```

要特别注意的是，如果我们自定义了一个构造方法，那么，编译器就不再自动创建默认构造方法：

如果既要能使用带参数的构造方法，又想保留不带参数的构造方法，那么只能把两个构造方法都定义出来：

```java
class Person {
    private String name;
    private int age;

   public Person() {

   }

   public Person(String name, int age) {
       this.name = name;
       this.age = age;
   }

   public String getName() {
      return this.name;
   }

   public int getAge() {
       return this.age;
   }

}
```

在Java中，创建对象实例的时候，按照如下顺序进行初始化：

先初始化字段，例如，int age = 10;表示字段初始化为10，double salary;表示字段默认初始化为0，String name;表示引用类型字段默认初始化为null；

执行构造方法的代码进行初始化。

因此，构造方法的代码由于后运行，所以，new Person("Xiao Ming", 12)的字段值最终由构造方法的代码确定。



##### 多构造方法

可以定义多个构造方法，在通过new操作符调用的时候，编译器通过构造方法的参数数量、位置和类型自动区分：

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
       this.name = name;
       this.age = age;
    }

    public Person(String name) {
          this.name = name;
          this.age = 12;
    }

    public Person() {
    }

}
```

> 如果调用new Person("Xiao Ming", 20);，会自动匹配到构造方法public Person(String, int)。
>
> 如果调用new Person("Xiao Ming");，会自动匹配到构造方法public Person(String)。
>
> 如果调用new Person();，会自动匹配到构造方法public Person()。

一个构造方法可以调用其他构造方法，这样做的目的是便于代码复用。调用其他构造方法的语法是this(…)：

```java
class Person {
    private String name;
    private int age;

  public Person(String name, int age) {
      this.name = name;
      this.age = age;
}

  public Person(String name) {
      this(name, 18); // 调用另一个构造方法Person(String, int)
}

  public Person() {
      this("Unnamed"); // 调用另一个构造方法Person(String)
}


```

##### 方法重载

上文我们说到，可以通过定义不同的构造方法来实现不同传入参数的对象构造，那么普通方法是否也可以传入不同参数呢？

当然可以，这就是方法重载。

在一个类中，我们可以定义多个方法。如果有一系列方法，它们的功能都是类似的，只有参数有所不同，那么，可以把这一组方法名做成同名方法。例如，在Hello类中，定义多个hello()方法：

```java
class Hello {
    public void hello() {
        System.out.println("Hello, world!");
    }

    public void hello(String name) {
        System.out.println("Hello, " + name + "!");
    }

    public void hello(String name, int age) {
        if (age < 18) {
            System.out.println("Hi, " + name + "!");
        } else {
            System.out.println("Hello, " + name + "!");
        }
    }
}
```

这种方法名相同，但各自的参数不同，称为方法重载（Overload）。

注意：方法重载的返回值类型通常都是相同的。



### Java高级语法



#### 继承与多态

在之前我们已经定义了Student类，现在我们想要定义一个HighStudent来表示大学生，添加其所选择的课程，我们可以选择这样定义

```java
public class HighStudent {
    private String name;
    private int age;
    private int grade;
    private String[] subject;
    
    public Student(String name,int age,int grade){
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
    
    public int getAge(){
        return this.age;
    }
        
    public String getName(){
        return this.name;
    }
    
    public int getGrade(){
        return this.grade;
    }
    
    public void setAge(int aAge){
        if(age>15)
        {
           return;
        }
        this.age = aAge;
    }
}   
```

我们发现Student类和HighStudent类几乎完全一样，除了增加了一个新域，于是我们考虑简化代码。

我们使用继承语法来简化代码，简化后的代码如下：


```java
public class HighStudent extends Student {
    public String[] subject={};
    
    public HighStudent {
        super(String name,int age,int grade);
    }
}
```

在Java中，我们使用extends表示继承，继承的类会继承父类的所有方法，并且通过super语法可以继承父类的构造方法。

在OOP的术语中，我们把Student称为超类（super class），父类（parent class），基类（base class），把HighStudent称为子类（subclass），扩展类（extended class）。

##### protected

继承有个特点，就是子类无法访问父类的private字段或者private方法。例如，Student类就无法访问Person类的name和age字段，因此我们要在父类中把private修饰的域改为protected修饰。

```java
protected String name;
protected int age;
protected int grade;
```

##### super

我们通过super来引用父类的方法和域，刚才我们在讲解继承的时候已经使用super引用 了父类的构造方法，正常来说，子类会自动继承父类的所有方法，但是有一个例外，子类可能对父类的方法进行重写

```
public int getAge(){
        return this.age + 1;
    }
```

如果我们在HighStudent中改写了getAge方法，而我们需要调用父类原有的方法，就需要使用super

```
HighStudent hs = new HighStudent("David",18,2);
hs.super.getAge();
```

这个功能更多运用在子类方法重写。

##### 阻止与限制继承

在Java中，我们使用permit限制继承，如果我们要限制一个类的继承

```java
public sealed class Student permits HighStudent,PrimStudent {
    ...
}
```

这样我们就限制了只有两个类能够继承Student类

如果我们要阻止该类的所有继承，我们使用final修饰该类

```java
public final class Student {
    ...
}
```

##### 转型

如果一个引用变量的类型是HighStudent，那么它可以指向一个HighStudent类型的实例：

```java
HighStudent s = new HighStudent();
```

如果一个引用类型的变量是Student，那么它可以指向一个Student类型的实例：

```java
Student p = new Student();
```

现在问题来了：如果HighStudent是从Student继承下来的，那么，一个引用类型为Student的变量，能否指向HighStudent类型的实例？

```java
Student p = new HighStudent(); 测试一下就可以发现，这种指向是允许的。
```

这是因为HighStudent继承自Student，因此，它拥有Student的全部功能。Student类型的变量，如果指向HighStudent类型的实例，对它进行操作，是没有问题的！

这种把一个子类类型安全地变为父类类型的赋值，被称为向上转型（upcasting）。

向上转型实际上是把一个子类型安全地变为更加抽象的父类型。
