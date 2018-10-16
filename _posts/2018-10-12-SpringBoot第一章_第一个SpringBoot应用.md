---
layout: post
title: "SpringBoot | 第一章_第一个SpringBoot应用"
date: 2018-10-12 
description: "SpringBoot 第一个SpringBoot应用"
tag: SpringBoot 
---   

##  第一章：第一个SpringBoot应用

-----

## 一、SpringBoot的简单介绍

### 1.概述

随着动态语言的流行（Ruby、Groovy、Scala、Node.js），Java的开发显得格外的笨重：繁多的配置、低下的开发效率、复杂的部署流程以及第三方技术集成难度大。 在上述环境下，`Springboot`应运而生。它使用”习惯优于配置”（项目中存在大量的配置，此外还内置一个习惯性的配置，让你无须手动进行配置）的理念让你的项目快速运行起来。使用springboot很容易创建一个独立运行（运行jar，内嵌servlet容器）、准生产级别的基于Spring框架的项目，使用`springboot`你可以不用或者只需要很少的Spring配置。 

### 2.SpringBoot和传统maven-archetype-webapp区别

- **打包方式不同：**
  - 传统web maven项目使用的是maven-archetype-webapp骨架，打包方式是使用的war包
  - Spring Boot的打包方式是使用的jar包
- **pom.xml中引入的依赖不同：**
  - 传统web项目是引入多个单独的依赖
  - Spring Boot是引入的spring-boot-starter, 在spring boot中大部分依赖不需要指定version，因为版本号已经在spring-boot-starter-parent中定义过了
- **项目目录结构不同：**
  - 传统的web项目中src/main/java下是没有类的，Spring Boot项目中有一个启动类(Project名称+Application), 而且在src/test/java中也有一个测试类(Project名称+ApplicationTest)
  - 传统的web项目有src/main/webapp/WEB-INF/web.xml, Spring Boot中没有web.xml
  - 传统的web项目resources的目录是空的，Spring Boot项目中resources中有static、templates目录和一个配置文件application.properties
- **项目运行方式不同：**
  - 传统web项目是启动tomcat
  - Spring Boot项目是直接运行main方法或者直接运行jar(java -jar <project>.jar)

### 3.SpringBoot的核心功能

- **独立运行的Spring项目**

  > Spring Boot可以以jar包的形式独立运行，运行一个Spring Boot项目只需要通过java -jar xx.jar。

- **内置Servlet容器**

  > Spring Boot可选择内嵌Tomcat、Jetty或者Undertow，这样无须以war包形式部署。

- **提供starter简化maven配置**

  > Spring提供了一系列的starter pom来简化maven依赖加载，例如：当你使用了spring-boot-starter-web时，会自动加入相关依赖，无需你手动一个一个的添加坐标依赖。

- **自动配置Spring**

  > Spring Boot会根据在类路径中的jar包、类，为jar包里的类自动配置Bean，这样会极大地减少我们要使用的配置。当然，Spring Boot只是考虑了大多数的开发场景，并不是所有场景，若在实际开发中，我们需要自动配置bean，而Spring Boot没有提供支持，则可以自定义自动配置。

- **无代码生成和xml配置**

  > Spring Boot的神奇的不是借助于代码生成来实现的，而是通过条件注解来实现的，这是Spring 4.x提供的新特性，Spring 4.x提倡使用java配置和注解配置相结合，而Spring Boot不需要任何xml配置即可实现Sping Boot的所有配置。

### 4.SpringBoot的优缺点

- **优点**
  1. 集成框架非常简单，例如集成SpringMVC，只需引入spring-boot-starter-web这一个依赖，也不需要做任何配置，这样集成起来非常快速方便。Spring Boot支持很多常用的框架集成, 如 log、test、mybatis、nosql、mq、模板技术(thymeleaf、freemark)、jpa、aop、actuator 等， 具体请查看[Starter POMs](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-starters)、 [Starter POMs](https://blog.csdn.net/whatlookingfor/article/details/51393398)
  2. 引入的依赖的数量很少，例如要引入测试依赖JUnit、Hamcrest、Mockito只需要引入spring-boot-starter-test这一个依赖就行了
  3. 自动化配置，使用默认配置，再也不需要applicationContext.xml等配置文件了
  4. 支持自定义配置，可以配置在application.yml或者Config类中，如果自定义了就使用自定义的值，没有自定义的则使用默认的值
  5. 运行更加简单，直接使用java -jar 命令，或者直接在IDE中运行main方法
  6. 监控简单：提供了`actuator`包，可以使用它来对你的应用进行监控。
- **缺点**
  1. 缺少监控集成方案、安全管理方案：只提供基础监控，要实现生产级别的监控，监控方案需要自己动手解决；
  2. 高度封装，出现问题不易排查，适合有开发惊讶的攻城狮，不适合初学者，初学者上手容易，一旦出现问题就很难排查。
  3. 将现有或传统的Spring Framework项目转换为Spring Boot应用程序是一个非常困难和耗时的过程。它仅适用于全新Spring项目。
  4. Spring Boot 正在快速发展，可能版本变动比较大

----------------------

## 二、工程搭建

> 使用的工具为：`Spring Tool Suite(3.9.3.RELEASE)`
>
> SpringBoot：1.5.14.RELEASE

**[Spring Tool Suite 点击下载](https://spring.io/tools/sts/all)**

### 1.创建SpringBoot工程

> 利用**Spring Initializr**进行快速创建项目

- **选择Dashboard–>CREATE SPRING STARTER PROJECT进行创建项目，或者可以选择file–>new–>Spring Starter Project，打开创建面板**

  **第一种方式：**
  [![img](http://qiniu.xds123.cn/18-7-11/73137443.jpg)](http://qiniu.xds123.cn/18-7-11/73137443.jpg)

  **第二种方式：**
  [![img](http://qiniu.xds123.cn/18-7-11/72277454.jpg)](http://qiniu.xds123.cn/18-7-11/72277454.jpg)

- **出现创建面板，填写项目信息**

  > 这里url建议直接填写:`https://start.spring.io`(默认是http方式)

  [![img](http://qiniu.xds123.cn/18-7-11/71296322.jpg)](http://qiniu.xds123.cn/18-7-11/71296322.jpg)

  **maven相关命名说明**

  1. **Group**：一般为逆向域名格式，如本博客域名为`coderofsong.github.io`，则group一般以`io.github.coderofsong`开头
  2. **Artifact**：唯一标识，一般为项目名称。
     *具体maven相关信息，可自行搜索,这里只简单阐述*

- **选择依赖包和版本**

  ![创建.png](https://i.imgur.com/K1AEPu8.png)

  **除此下载包时，可能会比较慢，建议替换成阿里云的maven镜像**

### 2.项目结构

```
- src
    -main
        -java
            -cn.lqdev.learning.springboot.chapter1
                #主函数，启动类，运行它如果运行了 Tomcat、Jetty、Undertow 等容器
                -Chapter1Application	
        -resouces
            #存放静态资源 js/css/images 等
            - statics
            #存放 html 模板文件
            - templates
            #主要的配置文件，SpringBoot启动时候会自动加载application.properties/bootstrap.properties	
            - application.properties
    #测试文件存放目录		
    -test
 # pom.xml 文件是Maven构建的基础，里面包含了我们所依赖JAR和Plugin的信息
- pom
```

![目录结构.png](https://i.imgur.com/PjioQbF.png)

### 3.pom依赖

> 由于使用了`Spring Initializr`直接创建项目，相关依赖自动添加好了。 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
 
	<groupId>cn.lqdev.learning</groupId>
	<artifactId>springboot-chapter1</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>chapter-1</name>
	<description>Spring Boot | 第一章：第一个Springboot应用</description>

    <!-- Springboot的版本，大家选择时，应该选择 RELEASE 版本 -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.14.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
	    <!-- 内嵌了tomcat服务器，开发简单的web应用，此依赖即可  -->
 		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
        <!-- 测试包 -->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
</project>
```

### 4.主入口

```java
package com.sdl.springboot.day01;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
/**
 * 启动类
 * @author:    		songdeling
 * @classname: 		Day01Application
 * @description: 	TODO
 * @date:			2018年10月16日
 */
@SpringBootApplication
public class Day01Application {

	public static void main(String[] args) {
		SpringApplication.run(Day01Application.class, args);
	}
}
```

### 5.编写controller

```java
package com.sdl.springboot.day01.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;
/**
 * @author:    		songdeling
 * @classname: 		SayHelloController
 * @description: 	TODO
 * @date:			2018年10月16日
 */
//@RestController = @Controller + @ResponseBody 默认直接返回json
@RestController
public class SayHelloController {

	@RequestMapping(value = "/sayHello", method = RequestMethod.GET)
	public String sayHello() {
		return "Hello World";
	}
}
```

### 6.启动

> 直接`Chapter1Application`,右键 `run as` –> `Spring Boot App` 即可。 

看见以下提示，说明启动成功： 

![启动1.png](https://i.imgur.com/E8hjrjc.png)

**简单说明**

1. springboot 默认的端口号为：8080，此时浏览器访问：`127.0.0.1:8080/sayHello`即可查看。
2. 需要修改默认端口号时及上下文路径时，只需要在`application.properties`设置以下属性：

```
# 端口号
server.port=8888
# 应用上下文路径
server.context-path=/day01
```

访问：http://localhost:8080/sayHello

![启动2.png](https://i.imgur.com/EanIYE5.png)

**自此，一个简单的SpringBoot就开发完成了。比起原来的springmvc时的开发效率，简直是一个质的飞跃，无需再烦扰烦人的xml配置文件了。终于可以快乐的撸代码了~**

-------------------

- 转载请注明原地址https://blog.lqdev.cn/categories/springboot/

- 请关注宋德凌的博客：[http://CoderOfSong.github.io](http://CoderOfSong.github.io) 谢谢！