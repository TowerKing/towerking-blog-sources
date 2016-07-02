---
title: "Butter Knife简介"
layout: post
comments: true
description: "初次使用Butter Knife，感觉挺好使，推荐之"
---

最初写Android项目的时候，也不知道可以用什么开源项目，就跟着《第一行代码》里面写的一些东西开始第一个界面。大量的XML文件，Activity中调用控件的时候，用的是下面的代码。

```
View view = findViewById(R.id.item);
// 如果是其他控件，还得自己手动转，如TextView，则需要这样写
TextView textView = (TextView) findViewById(R.id.text);
```

起初也没有感觉这么写有什么不好，虽然有点繁琐，但是将这些初始化的组件，在代码起初申明好变量，然后将所有获取控件的代码放在一个统一的方法中，也就无须管事。后来陆续看别人分享的代码或者开源项目的时候，大多数都使用了Butter Knife这个开源库，它是用注解的方式来完成我们之前的工作，形式如下。

```
@Bind(R.id.text) TextView textView;
```

就一行也许没有看出什么特别优势，但是如果写的控件比较多，这样写的优势还是很明显的，代码量至少节约点，也比较容易读，好像TextView是@Bind(R.id.text)类型一样(这样理解是不是有点问题)。声明完这些控件之后，不要忘记在Activity中的onCreated方法中调用一行代码，否则会出现空指针异常，找不到控件之类的。

```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    // 一定要加上这行代码
    ButterKnife.bind(this);
    // do more things
}
```

如果不是在Activity中使用这个，在其他地方使用，如继承RecyclerView.ViewHolder的ViewHolder中，绑定方式有些许区别。

```
 public static class ViewHolder extends RecyclerView.ViewHolder {
     @Bind(R.id.text) TextView mTextView;
     public ViewHolder(View view) {
         super(view);
         // 注意这句，绑定方式和之前的是不是有点不一样
         ButterKnife.bind(this, view);
     }
 }
```

如何在自己的项目中使用ButterKnife开源库，只需要在gradle中配置一行引用依赖

```
compile 'com.jakewharton:butterknife:7.0.1'
```
这个开源库学习起来还是比较简单的，基本上将其官网的东西从头到尾看一遍就好了，如果忘记就再查一下。我这里只是简单的说明了一下Butter Knife的使用方式，关于它的更多信息，可以参考其[官网](http://jakewharton.github.io/butterknife/)。

============
2016.01.18补记
今天在用ButterKnife的时候遇到一个错误exception java.lang.RuntimeException: Unable to bind views for Fragment on ButterKnife.bind(this, view)。经过查阅发现是控件绑定错误，本来是```ImageView```控件，在使用ButterKnife进行绑定的时候使用了```Button```。参考[Stackoverflow网站](http://stackoverflow.com/questions/31906268/butter-knife-unable-to-bind-views-for-fragment)
