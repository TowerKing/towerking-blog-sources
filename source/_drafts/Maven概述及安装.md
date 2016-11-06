---
title: "Maven概述及安装"
layout: post
categories: Maven
---

一般情况下认为是构建工具
Maven是项目管理工具

Maven的定义是什么呢？ 从定义中可以看出Maven其实是一个项目管理工具，项目构建只是其一种功能而已。

Maven除了构建项目，还可以生成项目报告，项目站点，代码静态检查等等。

# Maven的功能

1.  构建项目 （Builds）
Maven可以管理项目的整个生命周期：代码验证、代码生成、编译、测试、打包、集成测试、安装、部署以及项目网站的创建等等。
2.  依赖管理（Dependencies）
3.  配置管理（SCMs）
4.  发布管理（Releases）
5.  文档编制（Documentation）
6.  报告（Reporting）

# Maven的特点
1.  微内核
Maven采用的是微内核设计，它通过插件来实现大部分功能，其核心功能与项目构建没有多大关系。其主要功能是XML文档解析，管理生命周期，管理插件。除此之外它什么活都不干，都委派给插件来做。
这些插件可以影响Maven的生命周期，提供对目标访问等等。绝大多数动作也是发生于Maven的插件，比如编译源码，打包二进制代码，发布站点等等。
第一次下载的代码其实是不知道如何做这些的，都是通过插件来完成，而这些插件都是通过Maven仓库中下载获得的。当我们第一次运行mvn install ，会从中央仓库中下载大部分核心插件，这样的好处就是mvn的压缩包足够小，不足就是要确保是联网状态。
2.  约定优于配置
Java文件
Resource文件
test文件
target文件

3.  项目模型
版本号等等

# Maven的安装

Mac电脑下载安装
打开浏览器 maven.apache.org,下载
下载完成之后拷贝到指定的文件夹下，解压，查看maven的目录结构并解释
.bash_profile export M2_HOME=安装目录，然后在PATH文件下，加上maven bin路径，接着使用source命令

使用mvn -version查看是否配置成功

2，还可以使用brew安装
