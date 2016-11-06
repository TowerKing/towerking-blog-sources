---
title: "Maven构建Web项目"
layout: post
categories: Maven
---
# 创建一个Web项目
生成一个简单的项目
mvn archetype:generate
选择项目原型输入字符串web过滤一下，然后随便找一个，选择版本
输入groupId:com.jikexueyang等等
进入目录看项目结构，看各个文件

进入hello world目录mvn package
构建成功，target的war包，放入Tomcat对应的目录，启动tomcat

# 使用Tomcat插件运行Web项目
使用maven tomcat插件，一个命令解决问题
进入网页tomcat.apache.org/maven-plugin.html
配置tomcat的插件文件，打开pom文件
<plugin>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat6-maven-plugin</artifactId>
    <version>2.2</version>
</plugin>
这是6的插件，可以复制下，改成7就是7的文件
mvn tomcat:run
然后可以看到tomcat已经启动了，然后输入地址
mvn tomcat7:run

# 使用Jetty插件运行Web项目
maven的jetty插件更加小巧丰富
wiki.eclipse.org/Jetty/Feature/Jetty_Maven_Plugin
配置插件，打开pom文件
<plugin>
    <groupId>org.mortbay.jetty</groupId>
    <artifactId>jetty-maven-plugin</artifactId>
</plugin>
mvn jetty:run
jetty是把项目直接放在根目录下了

# 添加J2EE依赖
为了添加Servlet需要添加相关的jar文件
javaee-web-api
javax.servlet-api
scope provided
jsp依赖
jstl依赖

# 创建JSP和Servlet
webapp新建一个jsp文件，可以使用touch命令
进入java目录，新建一个Servlet文件HelloServlet.java文件
WEB-INF 新建web.xml文件，编写Servlet name和Servlet-mapping文件
mvn clean package
启动mvn jetty:run
# 在Eclipse中使用Maven构建Web项目
过滤web
配置maven build
选择项目路径
goals可以选择 jetty:run
