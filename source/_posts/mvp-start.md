---
title: "MVP初识"
layout: post
date: 2016-01-08
updated: 2016-07-02
categories: Android
---

MVP已经学习两天，依然不知道如何下手去整一个MVP的Android APP，但是其思想是值得记住的。在后面写代码的时候时刻记住就好，就像脑子中时刻想这命名的重要性以及不要复制自己的原则，在写代码时会刻意的去取个自己容易理解的名字，抑或是看到两段差不多的代码，就想着把公共的部分提炼出来。代码最好也未必就变得特别容易阅读，至少自己在一两个月过后还是能够比较快一点的明白自己在表达是什么，不过也有无法想起的时候。

所以我记住MVP的一些基本原则，后面写代码时多想想，刻意训练下，代码应该会更容易懂点。现在说说自己对MVP学习这件事情之后的一些理解。

学习的是MVP，但思想并不是局限于MVP，他和其他的模式如MVC、MVVM之类的目的其实是一样的。都是要使得代码更加简洁优雅。无论是大家对哪种模式的反对与赞同，明白目的一样之后，就没必要为到底选哪一种模式而苦恼，甚至可以在同一个项目中使用多个模式。

那MVP，MVC或者MVVM主要思想是什么呢，主要体现在一下几点，由于参考的文章是英文，也不知道怎么翻译才足够准确，就原文复制下来。

* Independent of Frameworks.

* Testable.

* Independent of UI.

* Independent of Database.

* Independent of any external agency.

![MVP图解](/images/clean_architecture.png)

具体的请参考[这篇博文](http://fernandocejas.com/2014/09/03/architecting-android-the-clean-way/).

如图说明一样，各个模块彼此独立，而且里面的圈一定不要依赖外面的圈，只能外面的圈依赖里面的圈。现在还是不能很好的理解，得动手试试并多想想场景才能够很好的理解。总之，写代码的时候多想想用什么方式使得代码更简洁就好。
