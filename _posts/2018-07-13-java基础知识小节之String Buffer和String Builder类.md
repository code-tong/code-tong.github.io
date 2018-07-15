---
layout: post
title: "java基础知识小节之String Buffer和String Builder"
date: 2018-07-13 
description: "java基础知识 String Buffer和String Builder"
tag: Java基础知识 
---   

## 知识点十二： String Buffer和String Builder

-----

## String Buffer和String Builder类

当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。

和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。

StringBuilder 类在 Java 5 中被提出，它和 StringBuffer 之间的最大不同在于 StringBuilder 的方法不是线程安全的（不能同步访问）。

### StringBuilder和String的差异图示

**String操作示意图**：

![String操作示意图](https://i.imgur.com/KVV81oh.png)

**StringBuilder操作示意图：**

![StringBuilder操作示意图](https://i.imgur.com/9R7jkKG.png)

由于 StringBuilder 相较于 StringBuffer 有速度优势，所以多数情况下建议使用 StringBuilder 类。然而在应用程序要求线程安全的情况下，则必须使用 StringBuffer 类。

Test.java 文件代码：

```java
public class Test{  
    public static void main(String args[]){    
        StringBuffer sBuffer = new StringBuffer("hello");    
        sBuffer.append("：");    
        sBuffer.append("world");    
        System.out.println(sBuffer);    
    }
}
```

以上实例编译运行结果如下：

```java
hello：world
```

------

## StringBuffer的方法

以下是 StringBuffer 类支持的主要方法： 

![主要方法](https://i.imgur.com/tGaytS4.png)

下面的列表里的方法和 String 类的方法类似： 

![相似方法](https://i.imgur.com/VGEzIf5.png)

------

转载请注明原地址，宋德凌的博客：[http://CoderOfSong.github.io](http://CoderOfSong.github.io) 谢谢！