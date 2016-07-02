---
title: "SwipeRefreshLayout程序自动触发"
layout: post
date: 2016-01-15
updated: 2016-07-02
categories: Android
comments: true
---

关于SwipeRefreshLayout程序自动触发是之前就已经解决的问题，只是当时没有记录的习惯，所以没有记录。今天工作主要是针对之前的项目一些修改，并没有新的知识点获得，就拿这个已经获得的东西来滥竽充数。

SwipeRefreshLayout是google自己推出的下拉刷新控件，易用，我在项目中一般都会使用该控件。下面开始说说它的几个常用方法以及相关代码片段。

- setColorSchemeResources设置用于进度条动画的颜色

```
// 这样设置后，在请求数据的过程中就有四种颜色可以交替变换
swipeRefreshLayout.setColorSchemeResources(android.R.color.holo_blue_light,
        android.R.color.holo_red_light, android.R.color.holo_orange_light,
        android.R.color.holo_green_light);
```

- setOnRefreshListener 为下拉刷新添加一个监听事件

```
swipeRefreshLayout.setOnRefreshListener(new SwipeRefreshLayout.OnRefreshListener() {
    @Override
    public void onRefresh() {
        // do something in background
    }
});
```

- setRefreshing 通知组件刷新状态已经修改，从而显示或者隐藏进度条，下拉刷新时不能调用此方法

```
// 一般在自己获取数据完成后调用
swipeRefreshLayout.setRefreshing(false);
```

- post(Runnable action) 用于执行后台程序，如果想自动触发下拉刷新，就需要调用此方法

```
swipeRefreshLayout.post(new Runnable() {
    @Override
    public void run() {
    	// 显示设置进度条可见
        swipeRefreshLayout.setRefreshing(true);
        // do something in background
    }
});
```
