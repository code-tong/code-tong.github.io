---
layout: post
title: "java基础知识小节之String类"
date: 2018-07-12 
description: "java基础知识 String类"
tag: Java基础知识 
---   

## 知识点十一： String类

-----

字符串广泛应用 在Java 编程中，在 Java 中字符串属于对象，Java 提供了 String 类来创建和操作字符串。 

------

## 创建字符串

创建字符串最简单的方式如下:

```java
String str = "hello world";
```

在代码中遇到字符串常量时，这里的值是 "**hello world**""，编译器会使用该值创建一个 String 对象。

和其它对象一样，可以使用关键字和构造方法来创建 String 对象。

String 类有 11 种构造方法，这些方法提供不同的参数来初始化字符串，比如提供一个字符数组参数:

## StringDemo.java 文件代码：

```java
public class StringDemo{   
    public static void main(String args[]){      
        char[] helloArray = { 'h', 'e', 'l', 'l', 'o'};      
        String helloString = new String(helloArray);        
        System.out.println( helloString );   
    }
}
```

以上实例编译运行结果如下：

```
hello
```

**注意:**字符串类是常量,他们的值在创建后不会改变。

如果需要对字符串做很多修改，那么应该选择使用 StringBuffer & StringBuilder 类。

------

## 字符串长度

用于获取有关对象的信息的方法称为访问器方法。

String 类的一个访问器方法是 length() 方法，它返回字符串对象包含的字符数。

下面的代码执行后，len变量等于11:

StringDemo.java 文件代码：

```java
public class StringDemo {    
    public static void main(String args[]) {        
        String site = "hello world";        
        int len = site.length();        
        System.out.println( "hello world的长度 : " + len );   
    }
}
```

以上实例编译运行结果如下：

```
全栈开发者社区长度 : 11
```

------

## 连接字符串

String 类提供了连接两个字符串的方法：

```java
string1.concat(string2);
```

返回 string2 连接 string1 的新字符串。也可以对字符串常量使用 concat() 方法，如：

```java
"hello ".concat("world");
```

更常用的是使用'+'操作符来连接字符串，如：

```java
"hello," + " world" + "!"
```

结果如下:

```java
"hello, world!"
```

下面是一个例子:

StringDemo.java 文件代码：

```java
public class StringDemo {    
    public static void main(String args[]) {            
        String string1 = "hello：";            
        System.out.println("1、" + string1 + "world");      
    }
}
```

以上实例编译运行结果如下：

```java
1、hello：world
```

------

## 创建格式化字符串

我们知道输出格式化数字可以使用 printf() 和 format() 方法。

String 类使用静态方法 format() 返回一个String 对象而不是 PrintStream 对象。

String 类的静态方法 format() 能用来创建可复用的格式化字符串，而不仅仅是用于一次打印输出。

如下所示：

```java
System.out.printf("浮点型变量的值为 " +  "%f, 整型变量的值为 " + " %d, 字符串变量的值为 " +  "is %s", floatVar, intVar, stringVar);
```

你也可以这样写

```java
String fs;
fs = String.format("浮点型变量的值为 " + "%f, 整型变量的值为 " + " %d, 字符串变量的值为 " + " %s", floatVar, intVar, stringVar);
```

------

## String方法

| 作用               | 方法名                                                   | 方法描述                                                     |
| :----------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| 构造方法           | public String()                                          | 空参数构造方法                                               |
|                    | public String(String original)                           | 就是字符串字面值，封装成对象                                 |
|                    | public String(byte[] bytes)                              | 把字节数组转换字符串                                         |
|                    | public String(byte[] bytes, int startIndex,  int length) | 把字节数组一部分元素 转换成字符串                            |
|                    | public String(char[] value)                              | 把字符数组 转换成字符串                                      |
|                    | public String(char[] value, int startIndex, int count)   | 把字符数组一部分元素 转换成字符串                            |
| 判断功能的方法     | boolean equals(Object obj)                               | 判断两个字符串中的内容是否相同                               |
|                    | boolean equalsIgnoreCase(String str)                     | 判断两个字符串中的内容是否相同, 忽略大小写                   |
|                    | boolean contains(String str)                             | 判断该字符串中 是否包含给定的字符串                          |
|                    | boolean startsWith(String str)                           | 判断该字符串 是否以给定的字符串开头                          |
|                    | boolean endsWith(String str)                             | 判断该字符串 是否以给定的字符串结尾                          |
|                    | boolean isEmpty()                                        | 判断该字符串的内容是否为空的字符串                           |
| 获取功能的方法     | int length()                                             | 获取该字符串的长度                                           |
|                    | char charAt(int index)                                   | 获取该字符串中指定位置上的字符                               |
|                    | String substring(int start)                              | 从指定位置开始，到末尾结束，截取该字符串，返回新字符串       |
|                    | String substring(int start,int end)                      | 从指定位置开始，到指定位置结束，截取该字符串，返回新字符串   |
|                    | int indexOf(int ch )                                     | 获取给定的字符，在该字符串中第一次出现的位置                 |
|                    | int indexOf(String str)                                  | 获取给定的字符串，在该字符串中第一次出现的位置               |
|                    | int indexOf(int ch,int fromIndex)                        | 从指定位置开始，获取给定的字符，在该字符串中第一次出现的位置 |
|                    | int indexOf(String str,int fromIndex)                    | 从指定位置开始，获取给定的字符串，在该字符串中第一次出现的位置 |
| 转换功能的方法     | byte[] getBytes()                                        | 把该字符串 转换成 字节数组                                   |
|                    | char[] toCharArray()                                     | 把该字符串 转换成 字符数组                                   |
|                    | String toLowerCase()                                     | 把该字符串转换成 小写字符串                                  |
|                    | String toUpperCase()                                     | 把该字符串转换成 大写字符串                                  |
|                    | String concat(String str)                                | 把该字符串与给定的字符串相连接，返回一个新的字符串           |
| 替换功能的方法     | String replace(char old,char new)                        | 在该字符串中，将给定的旧字符，用新字符替换                   |
|                    | String replace(String old,String new)                    | 在该字符串中， 将给定的旧字符串，用新字符串替换              |
| 去除字符串两端空格 | String trim()                                            | 去除字符串两端空格，中间的不会去除，返回一个新字符串         |

------

转载请注明原地址，宋德凌的博客：[http://CoderOfSong.github.io](http://CoderOfSong.github.io) 谢谢！