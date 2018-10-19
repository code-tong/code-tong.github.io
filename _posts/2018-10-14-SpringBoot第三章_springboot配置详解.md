---
layout: post
title: "SpringBoot | 第三章_springboot配置详解"
date: 2018-10-14 
description: "SpringBoot "
tag: SpringBoot 
---   

##  第三章：springboot配置详解

-----

基于springboot的`约定优于配置`的原则，在多数情况下，启动一个应用时，基本上无需做太多的配置，应用就能正常启动。但在大部分开发环境下，添加额外配置是无所避免的，比如自定义应用端口号(比较在机器比较少的情况下，一台机器还是需要部署多个应用的，当然利用`docker`的话，是可避免的，这是后话了)、mq的服务地址、缓存服务的服务地址、数据库的配置等，都或多或少的需要一些外部的配置项。 

--------------

## 一、配置文件格式简要说明

springboot默认的全局配置文件名为`application.properties`或者`application.yml`(spring官方推荐使用的格式是`.yml`格式，目前官网都是实例都是使用yml格式进行配置讲解的),应用启动时会自动加载此文件，无需手动引入。除此之外还有一个`bootstrap`的全局文件，它的加载顺序在`application`配置文件之前，主要是用于在**应用程序上下文的引导阶段**，在后期讲解`springCloudConfig`时，主要是利用此特性，进行配置文件的动态修改，在此不表，在通常情况下，此两个配置文件是没有差别的，所以一般上都只需要配置`application`即可。 

-----------

## 二、自定义属性值

`application.properties`配置文件支持自定义属性的支持，比如

```xml
user.name=song
user.age=24
```

然后可通过`@Value("${user.name}")`的形式获取属性值。

```java
@RestController
public class DemoController {

    @Value("${user.name}")
    String name;

    @Value("${user.age}")
    String age;

    @RequestMapping("/")
    public String demo() {
        return name;
    }
}
```

> 这里提醒下，在填写一些默认的比 如，数据库属性时，可使用`alt+/`的方式，IDE会自动显示提示，避免了手动嵌入属性值或者忘记属性的尴尬。

[![img](http://qiniu.xds123.cn/18-7-14/95060000.jpg)](http://qiniu.xds123.cn/18-7-14/95060000.jpg)

**关于自定义属性时，特别是一些公用包，会使用到属性值时，建议在创建additional-spring-configuration-metadata.json属性元文件，这样在使用上述快捷方式时，会进行提示，包括属性名和属性说明，这样也方便调用者询问属性名是啥。**

[![img](http://qiniu.xds123.cn/18-7-14/32633042.jpg)](http://qiniu.xds123.cn/18-7-14/32633042.jpg)

[![img](http://qiniu.xds123.cn/18-7-14/64663506.jpg)](http://qiniu.xds123.cn/18-7-14/64663506.jpg)

相关`configuration-metadata`说明可查看：<https://docs.spring.io/spring-boot/docs/current/reference/html/configuration-metadata.html>

--------------

## 三、属性引用

在配置文件中，各个属性参数可进行引用的，比如：

```
user.name=song
user.age=24
user.desc=${user.name},${user.age}
```

最后`user.desc`的值即可：`song,24`。利用此特性，并可实现一些特殊的功能。比如后期讲解`spring cloud`时，注册`eurka`注册中心的实例名时，并会使用类似如下配置，使得实例名一眼就知道哪台服务地址：

```
eureka.instance.instance-id=${spring.cloud.client.ipAddress}:${server.port}
```

**这里需要注意，由于springboot在读取properties文件时，使用的是PropertiesPropertySourceLoader类进行读取，默认读取的编码是ISO 8859-1，故在默认的配置文件中使用中文时，会出现乱码，此时可以将中文转成Unicode编码或者使用yml配置格式(默认就支持utf-8),再不济可以将作为配置写入到一个自定义配置文件，利用@PropertySource注解的encoding属性指定编码**

--------------

## 四、随机数

Spring Boot的属性配置文件中可以通过`${random}`来产生int值、long值或者string字符串，来支持属性的随机值。

```
# 随机字符串
.rdm.value=${random.value}
# 随机int
.rdm.number=${random.int}
# 随机long
.rdm.bignumber=${random.long}
# 10以内的随机数
.rdm.test1=${random.int(10)}
# 1-20的随机数
.rdm.test2=${random.int[1,20]}
```

-----------------

## 五、自定义配置文件

在多数情况下，配置信息基本上都是放入`application.properties`文件中，但在一些场景下，比如某个配置项比较多时，为了分开存放，也可自定义配置文件，如`my.properties`。由于自定义的文件，系统不会自动加载，这个时候就需要手动引入了。
利用`@PropertySource`注解既可以引入配置文件，需要引入多个时，可使用`@PropertySources`设置数组，引入多个文件。

```java
@SpringBootApplication
@PropertySource(value="classpath:my.properties",encoding="utf-8")
public class Day3Application {
    public static void main(String[] args) {
        SpringApplication.run(Day3Application.class, args);
    }
}
```

---------------------

## 六、配置绑定对象

虽然使用`@Value()`方式，能方便的引入自定义的属性值，但在多某个配置项属于某一配置时，希望对应到一个实体配置类中，springboot也提供了支持。利用`@ConfigurationProperties`属性，即可完成
my.properties配置文件：

```
config.code=code
config.name=song
config.hobby[0]=看电影
config.hobby[1]=旅游
```

实体类：

```java
@Component
//@EnableConfigurationProperties(value= {Config.class})
@ConfigurationProperties(prefix="config")
@Data
public class Config {

    String code;

    String name;

    List<String> hobby;
}
```

**这里可直接加入@Component使其在启动时被自动扫描到，或者使用@EnableConfigurationProperties注解注册此实体bean.其次，在引入@ConfigurationProperties时，IDE会提示你引入spring-boot-configuration-processor依赖，前面提到，在自定义属性时，创建additional-spring-configuration-metadata.json可进行属性提示，而此依赖功能类似，会编译时自动生成spring-configuration-metadata.json文件，此文件主要给IDE使用，用于提示使用。添加后在配置文件点击属性时，会自动跳转到对应绑定的实体类中**

-------------------

- 转载请注明原地址https://blog.lqdev.cn/categories/springboot/

- 请关注宋德凌的博客：[http://CoderOfSong.github.io](http://CoderOfSong.github.io) 谢谢！