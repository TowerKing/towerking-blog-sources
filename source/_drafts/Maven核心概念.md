---
title: "初识maven核心概念"
layout: post
categories: Maven
---

# POM概述
构建了项目，运行了项目，maven是如何管理的呢，如何运行的呢？

POM是Project Object Model的缩写。项目的属性、依赖、构建配置这些信息都被抽象到项目对象模型里边。

完整的项目构成，有一张图

POM组成：
项目基本信息：
包括项目名称、项目官方网站、发起组织、开发者、贡献者列表、许可证证书等等，通过这些信息，我们对项目有一个基本对了解。

构建环境：
包含不同使用环境中，激活的profile，比如所在开发环境，需要将其部署到开发环境上，用的是开发数据库，缓存系统等等；等部署到生产环境则部署到生产系统中的数据库，缓存系统等等。构建环境为特定的环境定制了特定的设置，可以将不同的环境分开管理，非常的方便。

POM关系：
当前项目依赖的其他项目，涉及的父项目或者子项目，也可以设置自身的项目坐标等等。

构建设置：
可以改变项目的一些行为，比如源码、测试代码的位置，添加新的插件或者把插件的目标绑定到项目的生命周期上，另外还可以自定义站点生产参数等等。

项目信息都保存到pom.xml文件中

然后看mavenstudy的pom文件
maven坐标gourpId:artifactiId:packaging:version

多个项目的组成，父项目、子项目以及super pom文件

查看有效mvn格式 mvn help:effectiv

# 插件与目标
之前生成项目骨架的命令 mvn archetype:generate
archetype是插件，generate是目标
语法 pluginId:gloalId
一个目标是工作单元，而插件则是一个或者多个目标的集合
maven本质上是一个插件的框架，其核心其实不做任何构建任务，这些构建任务其实都是交给插件完成

调用插件目标的两种方式：
1. 将插件目标与生命周期绑定，执行生命周期
2. 直接执行插件目标

Maven常用插件
1. maven-archetype-plugins 通过这个插件生成一个项目骨架
2. maven-dependency-plugin 分析项目依赖，一个list的目标，一个ale
3. maven-help-plugin 帮助打印有效的pom，有效sitings，网上找找有哪些目标
4. maven-resources-plugin 资源文件过滤，管理Java文件
5. maven-surefire-plugin 单元测试，可以配置
6. jetty-maven-plugin 内置jetty容器，一个命令，可以运行web文件
7. maven-enforcer-plugin 设置规则，如设置Java版本，maven版本，可以扩展插件

Maven插件列表
[1](http://maven.apache.org/plugins/index.html)
[2](http://mojo.codehaus.org/plugins.html)
# 项目的生命周期阶段
mvn package 就是Maven的一个生命周期阶段
maven中项目的生命周期是指项目的构建过程，它包含了一系列的有序的阶段，而一个阶段就是构建过程中的一个步骤。

简化的Maven生命周期示例，有张图

插件目标可以绑定到生命周期阶段上。一个生命周期阶段可以绑定多个插件目标

mvn package查看输出日志 标准的生命周期，以及绑定的插件。

# Maven依赖管理
依赖的第三方jar文件，也可以说是构建

Maven通过坐标来管理依赖
打开maven study项目，打开pom.xml文件
Maven传递性依赖：
一个复杂的项目将会包含很多依赖，也有可能包含依赖于其它构建的依赖。你不必找出所有这些依赖然后把他们写到POM文件里，你只需要加上你直接依赖的那些库，Maven会隐式的把这些库间依赖的库也加入到你的项目中。

一个项目依赖一个库，而一个库依赖其它的库，你项目中不必把所有相关的依赖文件都加入pom文件，你只要加入直接的依赖库就OK

依赖范围：
maven 的pom文件中有一个scope，这个scope包含以下几个范围
compile (编译范围)
provided (已提供范围)
runtime (运行时范围)
test (测试范围)
system (系统范围) 不常用

# Maven仓库
Maven仓库就是一个存放来所有依赖的仓库，这个仓库通过依赖的坐标对其进行管理。

本地仓库

远程仓库

构建项目依赖本地仓库，如果本地仓库没有，则从远程仓库下载到本地仓库，如果本地仓库和远程仓库都没有，则会报错。

本地仓库的位置 .m2 ，修改本地仓库位置
mvn install 将文件下载都本地仓库

maven本省自带一个远程仓库，是maven的中央仓库，这个是继承来的
pom配置远程仓库，配置开源中国
# 项目站点报告
生成一个静态站点
生成各种报告信息，只要配置相关插件就好来，比如说testfire插件，是一个检查java程序样式的工具，它可以帮助我们检查代码是否遵循了代码规范，适合小组开发是代码样式规范和统一，通过插件生成bug，查看代码违规记录笔记，非常方便

为mvn study项目生成一个项目站点 mvn site,在target目录下有个site文件加，可以看到项目的基本样子，然后打开pom文件，进行相关的配置，添加相关信息，进行查看
mvn clean site
