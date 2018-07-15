---
layout: post
title: "java基础知识小节之Character类"
date: 2018-07-03 
description: "java基础知识 Character类"
tag: Java基础知识 
---   

## 知识点十： Character类

-----

## Character类

Character 类用于对单个字符进行操作。

Character 类在对象中包装一个基本类型 **char** 的值

**实例**

```java
char ch = 'a'; 
// Unicode 字符表示形式
char uniChar = '\u039A'; 
// 字符数组
char[] charArray ={ 'a', 'b', 'c', 'd', 'e' };
```

然而，在实际开发过程中，我们经常会遇到需要使用对象，而不是内置数据类型的情况。为了解决这个问题，Java语言为内置数据类型char提供了包装类Character类。

Character类提供了一系列方法来操纵字符。你可以使用Character的构造方法创建一个Character类对象，例如：

```java
Character ch = new Character('a');
```

在某些情况下，Java编译器会自动创建一个Character对象。

例如，将一个char类型的参数传递给需要一个Character类型参数的方法时，那么编译器会自动地将char类型参数转换为Character对象。 这种特征称为装箱，反过来称为拆箱。

**实例**

```java
// 原始字符 'a' 装箱到 Character 对象 ch 中
Character ch = 'a'; 
// 原始字符 'x' 用 test 方法装箱
// 返回拆箱的值到 'c'
char c = test('x');
```

------

## 转义序列

前面有反斜杠（\）的字符代表转义字符，它对编译器来说是有特殊含义的。

下面列表展示了Java的转义序列：

![转义序列](https://i.imgur.com/QCLIB9b.png)

**实例**

当打印语句遇到一个转义序列时，编译器可以正确地对其进行解释。

以下实例转义双引号并输出：

## Test.java 文件代码：

```java
public class Test {   
    public static void main(String args[]) {      
        System.out.println("今天天气\"好\"");   
    }
}
```

以上实例编译运行结果如下：

```
今天天气"好"
```

------

## Character方法

下面是Character类的方法： 

![Character类的方法](https://i.imgur.com/nsrNXqu.png)

------

转载请注明原地址，宋德凌的博客：[http://CoderOfSong.github.io](http://CoderOfSong.github.io) 谢谢！