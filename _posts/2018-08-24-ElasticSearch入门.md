---
layout: post
title: "ElasticSearch入门"
date: 2018-08-24 
description: "ElasticSearch入门"
tag: ElasticSearch 
---   

# ElasticSearch入门学习

-----

## 一、ElasticSearch简介

### 1.什么是ElasticSearch

Elaticsearch，简称为es， es是一个开源的高扩展的分布式全文检索引擎，它可以近乎实时的存储、检索数据；本身扩展性很好，可以扩展到上百台服务器，处理PB级别的数据。

es也使用Java开发并使用Lucene作为其核心来实现所有索引和搜索的功能，但是它的目的是通过简单的`RESTful API`来隐藏Lucene的复杂性，从而让全文搜索变得简单。

### 2.ElasticSearch和Solr的对比

- Solr 利用 Zookeeper 进行分布式管理，而 Elasticsearch 自身带有分布式协调管理功能;
- Solr 支持更多格式的数据，而 Elasticsearch 仅支持json文件格式；
- Solr 官方提供的功能更多，而 Elasticsearch 本身更注重于核心功能，高级功能多有第三方插件提供；
- Solr 在传统的搜索应用中表现好于 Elasticsearch，**但在处理实时搜索应用时效率明显低于 Elasticsearch**

-----

## 二、ElasticSearch安装与启动

### 1.下载ElasticSearch压缩包

ElasticSearch分为Linux和Window版本,这里使用Windows版本的

ElasticSearch的官方地址：[https://www.elastic.co/products/elasticsearch](https://www.elastic.co/products/elasticsearch) 

### 2.安装ElasticSearch服务

安装Windows版ElasticSearch解压即安装,解压后的ElasticSearch的目录结构如下：

![ElasticSearch目录结构](https://i.imgur.com/RUmiKLY.png)

**注:**修改elasticsearch配置文件：config/elasticsearch.yml，增加以下两句命令：

```yml
http.cors.enabled: true
http.cors.allow-origin: "*"
```

此步为允许elasticsearch跨越访问，如果不安装后面的elasticsearch-head是可以不修改，直接启动。

### 3.启动ElasticSearch服务

点击ElasticSearch下bin目录中的elasticsearch.bat启动，如果控制台显示的日志信息如下：

![找不到jdk错误](https://i.imgur.com/3ga7VeJ.png)

则是没有正确的配置好JDK环境变量，导致启动ElasticSearch失败。要保证JDK版本在8及8以上并配置好环境变量，若还无法正确启动，在elasticsearch.bat文件中添加

```
SET JAVA_HOME="java的安装目录"
```

如图

![配置文件](https://i.imgur.com/n8HiAHI.png)

配置好即可正常启动

![启动ElasticSearch](https://i.imgur.com/bWLXsyQ.png)

注意：9300是tcp通讯端口，集群间和TCPClient都执行该端口，9200是http协议的RESTful接口 。

通过浏览器访问ElasticSearch服务器，看到如下返回的json信息，代表服务启动成功：

![ElasticSearch启动界面](https://i.imgur.com/Cmu6kat.png)

 ### 4.安装ElasticSearch的图形化界面插件

ElasticSearch不同于Solr自带图形化界面，我们可以通过安装ElasticSearch的head插件，完成图形化界面的效果，完成索引数据的查看。安装插件的方式有两种，在线安装和本地安装。本文档采用本地安装方式进行head插件的安装。elasticsearch-5-*以上版本安装head需要安装node和grunt

1. 下载head插件：[https://github.com/mobz/elasticsearch-head](https://github.com/mobz/elasticsearch-head) 

2. 将elasticsearch-head-master压缩包解压到任意目录，但是要和elasticsearch的安装目录区别开

3. 下载nodejs：[https://nodejs.org/en/download/](https://nodejs.org/en/download/) 

   安装nodejs

4. 将grunt安装为全局命令 ，Grunt是基于Node.js的项目构建工具

   到elasticsearch-head-master目录下,打开cmd执行下面命令：

   ```
   npm install -g grunt-cli
   ```

   得到以下结果：

   ![安装grunt-cli](https://i.imgur.com/T87OkW8.png)

5. 接着输入以下命令：

   ```
   npm install
   ```

   *如果有出现**PhantomJs not found on PATH**然后报错，则应该是网速太慢到时连接超时*

   *如图*

   ![PhantomJs not found on PATH错误](https://i.imgur.com/LVPnch9.png)

   正确结果如下图

   ![安装npm](https://i.imgur.com/b4rzbO0.png)

6. 启动grunt，输入下面命令

   ```
   grunt server
   ```

   如图

   ![启动grunt](https://i.imgur.com/1kYZEm2.png)

7. 打开浏览器，输入 http://localhost:9100，看到如下页面：

   ![打开9100端口](https://i.imgur.com/lItgQwC.png)

   如果不能成功连接到es服务，需要修改ElasticSearch的config目录下的配置文件：config/elasticsearch.yml，增加以下两句命令：

   ```
   http.cors.enabled: true
   http.cors.allow-origin: "*"
   ```

   然后重新启动ElasticSearch服务。

-----

## 三、ElasticSearch相关概念

### 1.概述



-----

## 四、ElasticSearch的客户端操作



-----

## 五、IK分词器和ElasticSearch集成使用



-----

## 六、ElasticSearch集群



-----

## 七、ElasticSearch编程操作



-----

## 八、Spring Data ElasticSearch使用



------

转载请注明原地址，宋德凌的博客：[http://CoderOfSong.github.io](http://CoderOfSong.github.io) 谢谢！