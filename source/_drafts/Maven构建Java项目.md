---
title: "使用Maven构建Java项目"
layout: post
categories: Maven
---

# 使用命令行工具构建一个Maven项目
创建一个工作目录，在工作目录下打开一个shell终端，输入命令
mvn archetype:generate
archetype是插件，项目原型，generate是目标，可以选择项目运行结构
第一次运行有点慢，会从网上下载项目原型
根据提示一步步操作

然后分析项目结构，简单介绍pom文件
src目录 java放源码，test放测试用例

运行命令 mvn package，打包成功，去项目看多了target目录
运行java文件
java -cp target/mystudy-1.0-snapshot.jar com.jikexueyuan.App

# 使用Eclipse构建一个Maven项目
最新版的Eclipse已经集成Maven，如果没有安装则在eclipse market中安装插件，搜索maven，找到m2e的图标

Maven配置，偏好设置 Maven Installation 找到Maven安装目录
User Settings
其他的一些设置，如源码与文档的下载

新建-》maven项目 project
根据想到来

jikexueyuan.com
mvnstudy

打包项目
run，run configuration Maven build 选择new，修改名字，选择项目，goals输入package，点击应用，点击run，

项目刷新，可以看到target项目，可以看到已经生成来jar文件

如何导入Maven项目，import
