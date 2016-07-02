---
title: "安卓开发问题碎片汇总"
layout: post
comments: true
description: "工作或者学习过程中遇到的关于Android的问题整合"
---
在整合阿里百川时，遇到的两个问题，通过google找到了解决方案。
1.第一个问题
>Error:Execution failed for task ':app:dexDebug'.
>com.android.ide.common.process.ProcessException: org.gradle.process.internal.ExecException: Process 'command '/usr/java/jdk1.7.0_17/bin/java'' finished with non-zero exit value 2

 解决方法是：
 <code><pre>defaultConfig { multiDexEnabled true }</pre></code>

参考网址 [stackoverflow](http://stackoverflow.com/questions/28917696/errorexecution-failed-for-task-appdexdebug-com-android-ide-common-process)

2.第二个问题
> Error:Execution failed for task ':app:packageAllDebugClassesForMultiDex'.
> java.util.zip.ZipException: duplicate entry: com/ta/utdid2/device/UTDevice.class

**解决方法**：从提示就能看明白是有两个相同的类.经调查，我将其中一个删除了，暂时没有什么问题。
