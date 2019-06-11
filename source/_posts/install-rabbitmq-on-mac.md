---
title: "在 Mac 上安装 RabbitMQ"
layout: post
categories: RabbitMQ
description: 说是安装，实际是记录安装过程中遇到的问题，方便日后自己查阅。
date: 2018-06-03
updated: 2018-06-03
comments: false
---

# 环境
我的苹果电脑操作系统版本是 **macOS High Sierra Version 10.13.4**，说明版本号是在安装过程中遇到的问题与此有关。

# 安装过程
参考[RabbitMQ 官方文档](http://www.rabbitmq.com/install-homebrew.html)，利用 Homebrew 进行安装，主要步骤就两步。
> `brew update`
> `brew install rabbitmq`

在安装 RabbitMQ 之前，程序会优先安装一些依赖，可以在控制台看到需要的依赖有以下几种
> Installing dependencies for rabbitmq: openssl, jpeg, libpng, libtiff, wxmac, erlang

依赖安装完成之后，开始安装 RabbitMQ，但是在安装过程中出现了如下错误。

```
Error: The `brew link` step did not complete successfully
The formula built, but is not symlinked into /usr/local
Could not symlink sbin/cuttlefish
/usr/local/sbin is not writable.

You can try again using:
  `brew link rabbitmq`
```

尝试使用给出的解决方案，即 `brew link rabbitmq` 。执行完成之后，依然会有错误，错误信息是
```
Linking /usr/local/Cellar/rabbitmq/3.7.5...
Error: Could not symlink sbin/cuttlefish
/usr/local/sbin is not writable.
```

然后利用 Google 网上找到解决方案，结合网站 [brew link php71: Could not symlink sbin/php-fpm](https://stackoverflow.com/questions/46778133/brew-link-php71-could-not-symlink-sbin-php-fpm?noredirect=1) 与网站 [Can't chown /usr/local in High Sierra](https://github.com/Homebrew/brew/issues/3228) 执行以下几条命令。

> cd /usr/local/
> sudo mkdir sbin
> sudo chown -R $(whoami) $(brew --prefix)/*

**PS：如果 Mac 的操作系统不是 High Sierra，我们可以使用命令`sudo chown -R $(whoami) $(brew --prefix)` 。**

然后再执行命令 `brew link rabbitmq`， 控制台会告诉我们已经成功创建 `Linking /usr/local/Cellar/rabbitmq/3.7.5... 23 symlinks created`。

# 加入环境变量
开始建立的连接，主要是将 RabbitMQ sever scripts 安装在 `/usr/local/sbin` , 但是这个路径不会自动添加到自己的 path 中，所以需要我们手动添加。添加方法利用 vi 在文件 ~/.bashrc 中添加一行 `export PATH=$PATH:/usr/local/sbin` , 然后执行命令 `source ~/.bashrc` 。

# 启动 RabbitMQ
```
To have launchd start rabbitmq now and restart at login:
  `brew services start rabbitmq`
Or, if you don't want/need a background service you can just run:
  `rabbitmq-server`
```

执行完后，可以尝试访问 [http://localhost:15672](http://localhost:15672)。
