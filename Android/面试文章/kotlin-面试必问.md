---
theme: juejin
---
鸡血：面试是决定岗位、公司规模、薪资待遇和职业前景的关键环节，影响着你的职业发展和未来的美好。

# 一、文章概述

Kotlin作为Android开发官方语言，很多知识点还是需要理解透彻的。很多开发者也许碰到过，也用过。但是面试被问起来相关的原理，又一无所知或一知半解。根据市面上大部分面试情况，总结出kotlin相关的高频面试知识点，并吃透每个知识点，达到面面俱到，胸有成竹。
### Kotlin
Kotlin 是一门支持多范式、多平台的现代静态编程语言。Kotlin 支持面向对象、泛型与函数式等编程范式，它支持 JVM、Android、JavaScript 目标平台。而且 Kotlin 具有很多现代静态语言特性：如类型推断、多范式支持、可控性达、扩展函数、高阶函数、内联函数、模式匹配等，Compose跨平台UI框架，也是在Kotlin基础上创造出来的，且Google将Kotlin作为Android开发的原生语言，可见其重要和强大。这都2024年了，应该用上Kotlin了吧？

大家是否清楚Kotlin是如何编译的呢？明确这点也很重要，也关系我们研究代码时候，能够看到其本质。

相信大家都知道，早期Java作为Android开发语言，通过Java编译器会编译为`.class`文件。而在JVM（虚拟机）中`.class文件`通过类加载器将字节码加载到内存中，并创建对应的 `Class` 对象，从而使得程序可以调用这个类，最终在程序解释器和即时编译(JIT编译)的配合下最终被转换为机器码并在硬件上执行...JVM内容很多，此处大家了解编译流程便可。JVM单独拿出来便是很重要的考点，近两年来，`安卓逆向`、`字节码插桩`、`内存优化`...等都离不开JVM的基础知识。推荐大家阅读书籍【深入理解Java虚拟机】。

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e7dc1bfb6bc74fa8ad09fb15930fafc1~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1916&h=790&s=400716&e=png&b=edf2fb)

Java 生态系统极其强大且丰富，性能分析工具等，这些工具都是基于 Java 字节码的。在移动端，早期Java作为Android开发语言，悠久的历史长河中，为其留下来广袤丰富的物质遗产，Kotlin必须无缝地与现有的 Java产物代码丝滑互操作。种种的原因，Kotlin 最终编译为 Java 字节码，能够被JVM加载执行，也算站在巨人（虚拟机）的肩上默默贡献而被广为人知。所以我们需要明白，Kotlin在移动端最终会被编译为Java字节码，继而被JVM虚拟机加载。

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bf701c104fe949ae9f9f61838f0adef5~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1922&h=836&s=555282&e=png&b=eef3fc)

[基础知识请看官方文档](https://book.kotlincn.net/)
### 反射
曾经，面试官问过这样一个问题`"Kotlin有无反射操作，和Java反射有什么区别呢？"`。因为的确没了解过是空白，只凭猜想想回答了。当时大概说了一下理解，大概回答如下类似，这一块的确没了解过，Kotlin起初设计便做好了Java的兼容，Kotlin是可以无缝调用Java类和方法等的，且Kolin最终也会编译为Java字节码。Kotlin提供反射操作我不清楚，即便目前没提供Kotlin反射操作支持，使用Java反射相关操作应该完全可以的。

面试结束便恶补了一下Kotlin反射相关的知识。首先查看了[官方文档-反射](https://book.kotlincn.net/text/reflection.html)的确是有的。那究竟和Java反射有何区别呢？
#### 1、Java反射
Java 反射使用 `Class` 类和 `Method`、`Field`、`Constructor` 等类来表示类、方法、字段和构造函数的信息。

```kotlin
package com.example.kotlin_stuty;

public class Person {
    private String name;
    private int age;
    public Person(String name,int age){
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void printInfo(){
        System.out.println("my name is"+name+",i am "+age+"year old");
    }
}
```
#### 2、Kotlin反射



### 操作符

### 高阶函数
高阶函数（Higher-Order Function）是函数式编程中的一个概念，指的是可以接受一个或多个函数作为参数，并且/或者返回一个函数作为结果的函数。在高阶函数中，函数被视为一等公民（first-class citizen），可以像其他数据类型一样被传递、赋值、返回等操作。

如下：calculationByType函数有一个**函数类型**的参数【compute】，这个方法根据传递的函数不同可以进行加减乘除等运算。

```kotlin
    fun main() {
        //加法运算
        val plusResult = calculationByType(0,1, plus)
        println("plus=$plusResult")
        //减法运算
        val subTrtResult = calculationByType(0,1, subtract)
        println("subtract=$subTrtResult")
    }

    fun calculationByType(a: Int, b: Int, compute: (Int, Int) -> Int): Int {
        return compute.invoke(a, b)
    }

    //加法
    val plus = fun(a: Int, b: Int): Int{
        return a + b
    }

    //减法
    val subtract = fun (a: Int, b: Int): Int{
        return a - b
    }
```
在上述案例中，可以看到每个方法都需要像变量一样进行定义每个函数,类似匿名函数，这样让函数显得不够直观。我们熟悉的方法一般如下，方法声明、方法名、参数、返回值。如果不用定义函数变量是否有其他方式进行调用plus和subtract呢？当然了，Kotlin提供了`::`操作符。不清楚的可以了解[此文](https://juejin.cn/post/7052631881560850445#heading-5)。

```kotlin
    //加法
    fun plus(a: Int, b: Int): Int{
        return a + b
    }

    //减法
    fun subtract(a: Int, b: Int): Int{
        return a - b
    }
```

### 内联函数

### 非内联函数

### 外联函数

### Data class

### 泛型



### 密封类和密封接口



### 

，
https://zhuanlan.zhihu.com/p/224965169
https://juejin.cn/post/7244098228248182845?from=search-suggest#heading-7 