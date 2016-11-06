---
title: "使用Maven构建多模块项目"
layout: post
categories: Maven
---
# 多模块项目介绍
在Maven中，通常会将一个大型的项目切分成若干个子项目，这些子项目被称为module，也就说模块。
1. 解放大型模块的管理
2. 公用模块
3. 。。。

查看Struts2项目，导入Eclipse
dubbo项目 有58个模块

如何将helloweb项目构建成都模块项目
helloweb项目的组成
helloweb-parent:定义项目信息，插件，依赖等等
helloweb-entity：领域层
helloweb-core：持久层，业务层，也可以进一步细分
helloweb-web：交互控制成
然后这个模块完成了，一个登陆功能

# 创建helloweb项目的骨架结构
进入helloweb项目
然后建四个文件夹：helloweb-parent, helloweb-entity, helloweb-core, helloweb-web
将pom.xml文件与src文件复制粘贴到以上四个目录，然后将根目录的src文件删除

打开根目录pom.xml文件
介绍modelVersion
packaging:war(web应用程序) jar, ear, pom(当前项目是一个父项目)
将之前的东西全部删除，添加以下代码
<modules>
    <module>helloweb-parent</module>
    <module>helloweb-entity</module>
    <module>helloweb-core</module>
    <module>helloweb-web</module>
</modules>

每个module就是一个模块，helloweb-parent这些都是相对路径，如果业务足够复杂，可以进一步建目录放模块信息，这样就更加清晰

顺序无要求，maven自己构建的时候会自动排序

# 将helloweb项目导入Eclipse
还有很多工作要做，不用文本完成，而是用Eclipse来完成

导入完成，有一个需要勾选

打开helloweb-parent的pom文件，将打包类型修改成pom
打开helloweb-core的，打包类型改为jar
helloweb-entity,打包类型为jar
helloweb-entity,war

修改helloweb-core的pom文件
添加以下配置
<parent>
    <groupId>com.jikexueyuan</groupId>
    <artifactId>hellowweb.parent</artifactId>
    <version>1.0</version>
    <relativePath></relativePath>
</parent>

helloweb-entity,helloweb-web同样的操作，注意修改各自的artifactId

删除项目，重新导入一下，可能有个激活项目的东西要选workingset

删除各个项目的pom文件里的依赖
先parent core entity web

删除完成后，更新整个项目的依赖，再构建一下maven install

# 使用depencyManagement管理依赖
depencyManagement 作用：
Maven使用depencyManagement元素来提供一种管理依赖版本号的方式
<depencyManagement>
    <dependencies>
        <dependncy>
            <groupId></groupId>
            <artifactId></artifactId>
            <version></version>
            <scope></scope>
        <dependncy>
    <dependencies>
<depencyManagement>

添加了servlet-api,servlet.jsp,junit，mysql
构建项目，看能否正常下载

父项目添加好之后，子项目就不用指定版本号了
如entity添加了junit，不需要指定版本好了。

这样升级，更换版本号，只要父容器就行
如果子项目需要其它的版本好，只需要申明个xx
注意：depencyManagement只是申明依赖，不会实现引入
所以子项目需要进行申明，然后自动引入

# 使用pluginMangement管理插件
pluginMangement的作用：
Maven使用pluginMangement元素提供了一种管理插件的方式。
先看entity的pom文件的，effectiv-pom
parent的pom.xml文件添加一下内容
<build>
    <pluginMangement>
        <plugins>
            <plugin>
                <gourpId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</groupId>
                <version>2.3.2</version>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <!-- 资源文件插件 -->
            <plugin>
                <gourpId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</groupId>
                <version>2.6</version>
            </plugin>
            <!-- 打包文件插件 -->
            <plugin>
                <gourpId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</groupId>
                <version>2.4</version>
                <configuration>
                    <warName>${project.artifactId}</warName>
                </configuration>
            </plugin>
        </plugins>
    </pluginMangement>
</build>
这样就不用在子项目中显示指定java源码的版本号

Maven插件非常多，会进一步介绍
# 定义项目属性与配置信息
打开parent的pom文件
在<name>helloweb parent</name>下添加一个properties标签
可以定义一下常量
<properties>
    <jdk.version>1.7</jdk.version>
    <servlet.api.version>3.0.1</servlet.api.version>
    <jsp.api.version>2.1</jsp.api.version>
    <junit.version>4.11</junit.version>
    <mysql.version>5.1.21</mysql.version>
    <project.build.souceEncoding>UTF-8</project.build.souceEncoding>
</properties>

然后下面的引用就可以使用这些常量，形式为${jdk.version}
重新构建，看更改是否正确，使用maven install

定义项目信息
<name>helloweb parent</name>
<description>这是个练习项目</description>
<url>towerking.github.io</url>
<inceptionYear>2016</inceptionYear>
还可以定义组织与人员信息

# 完善helloweb-entity模块
创建mysql数据库
数据库名字：maven_db
create table tbl_user (
    id int(11) unsigned not null auto_increment,
    name varchar(50) not null,
    password varchar(50) not null,
    email varchar(50),
    primary key(id)) engine = InnoDB default charset=utf8;

创建完表，插入一条数据
新建实体类，com.jikexueyuan.entity
public class User {
    private long id;
    private string name;
    private string password;
    private string email;
    getter();setter();
    toString();
}


# 完善helloweb-core模块
创建一个属性文件，保存数据库连接字符串
main 新建 resources文件夹，然后build as resources,然后新建配置文件dbconfig.properties,添加数据库的配置信息
driver=com.mysql.jdbc.Driver
dburl=jdbc:mysql://localhost:3306/maven_db
user=root
password=

maven 的默认约定
新建数据库连接工厂类
package util
public class ConnectionFactory {
    private static String driver;
    private static String dburl;
    private static String user;
    private static String password;

    private static final ConnectionFactory factory = new ConnectionFactory();

    private Connection conn;
    static {
        Properties prop = new Properties();
        try {
            InputStream in = ConnectionFactory.class.getClassLoader().getResourceAsStream("dbconfig.properties");
            prop.load(in);
        } catch (Execption e) {
            System.out.println("配置文件读取错误：" + e.getMessage);
        }
        driver = prop.getProperty("driver");
        dburl = prop.getProperty("dburl");
        user = prop.getProperty("user");
        password = prop.getProperty("password");
    }
    private ConnectionFactory() {}

    public static ConnectionFactory getInstance() {
        return factory;
    }
    public Connection makeConnection() {
        try {
            Class.forName(driver);
            conn = DriverManager.getConnection(dburl, user, password);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return conn;
    }

    然后写main方法的测试

    运行会发现缺少mysql驱动类

    com.jikexueyuan.dao
    com.jikexueyuan.dao.impl
        UserDao.java

    com.jikexueyuan.service
        CheckUserService.java

需要添加entity依赖
<dependency>
    <groupId>com.jikexueyuan</groupId>
    <artifactId>helloweb-entity</artifactId>
    <version>1.0<version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
打包项目，看能不能通过

# 完善helloweb-web模块
action 用于调用登陆校验登陆信息
jsp 显示

com.jikexueyuan.action
CheckAction 继承HttpServlet
override doGet与doPost 可以用Eclipse操作
doPost方法中获取用户名密码信息
if (用户名密码空) {
    重定向
} else {
    检查用户名 密码是否正确
    if (true) {
        success.jsp
    } else {
        error.jsp
    }
}

配置tomcat插件，run configuration -> Maven Build -> 新建 -> tomcat:run

# 使用log4j打印日志
log4j的介绍
log4j的官网网站 logging.apache.org/log4j/2.x
我们不用下载，可以在maven中进行配置
parent的pom文件添加log4j的依赖，需要添加两个依赖，分别为log4j-api,log4j-core，构建maven install
然后配置entity的pom，的log4j构建 maven install

entity
 新建resources目录，添加一个配置文件log4j2.xml，配置文件内容


 编写个test测试一下


# 使用junit进行单元测试
介绍了junit 的作者
新建了一个计算器类，然后做单元测试
src新建test，新建java，然后as source
1. mvn目标执行，Maven Build 新建 目标 test
2. 也可以run as junit

# 使用guava美化代码
guava介绍
guava核心功能
[1](https://github.com/google/guava/)

maven如何使用
parent pom文件添加guava的申明
entity 使用guava修改User的toString方法
