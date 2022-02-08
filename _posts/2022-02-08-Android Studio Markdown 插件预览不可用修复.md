---
layout:     post
title:      "Android Studio Markdown 插件预览不可用修复"
subtitle:   ""
date:       2022-02-08
author:     "newstrong"
header-img: "img/20220208.jpg"
catalog: ture
tags:
    - 技术
    - Android
    - 开发
---
### 修复Idea高版本不能使用markdown预览的bug

-   -   [1\. 分析](#1-分析)
    -   -   [1.1 换编辑器](#11-换编辑器)
        -   [1.2 解决JavaFX问题](#12-解决javafx问题)
    -   [2\. 原因](#2-原因)

1\. 分析
------

idea从2020.4开始依赖jdk11, 目前基于国内现状, 可reset eval的版本最高到2021.2.3, 实际最方便的是2021.1.x版本, 但不管哪个版本, 依赖都是JDK11, 而JDK从8版本以后不再内置JavaFX, 需要单独下载引入, Idea的Markdown编辑器实际上就是依赖JavaFX实现的, 所以现在的解决方案有2个, 一个是换一个编辑器, 一个是解决JavaFX的问题.

### 1.1 换编辑器

```
直接在插件仓库搜索了一下, 找到了Markdown Editor编辑器, 下载量还比较高, 下载安装重启, 发现不会用, 暂时放弃, 以后再研究

```

### 1.2 解决JavaFX问题

解决JavaFX的问题还是有2种方案, 一种是单独去下载安装并集成到环境中, 考虑下载安装简单, 集成到Idea的启动环境可能还有坑, 所以暂时放弃, 以后再研究\
现在就说另一种解决方案, 也是目前采用的方案, 搞一个带集成JavaFX的JDK11+就好了

这个灵感是在查看设置>language & frameworks > markdown时, 发现右侧面板显示模块不可用, 以为是idea缓存问题, 刷新缓存重启后, 进入了之前就打开的md文件, 提示错误信息 Not Support JCEF: Your environment does not support JCEF, cannot use Markdown Editor , 所以对Idea来说, 实际上就是需要JCEF的JDK运行环境了.\
到idea官网找了一下, 找到2个网址\
[下载JCEF集成的启动环境自行安装](https://github.com/JetBrains/JetBrainsRuntime/releases)\
[在Idea中设置JCEF启动环境](https://intellij-support.jetbrains.com/hc/en-us/articles/206544879-Selecting-the-JDK-version-the-IDE-will-run-under)\
第二个连接进去之后, 大体意思是在idea中输入**CTRL+SHIFT+A**, 打开动作指令窗口, 或者双击Shift在最上方选择**Action**, 在输入框中输入**Choose Boot Java Runtime for the IDE**(其实输入个Choose Boot就出来了), 在弹出窗口中的select中选择一个 xxx JetBrains Runtime With JCEF, 点OK等待下载完成重启即可, 我这里试了试, 下载过程中总是失败, 就放弃了

进入第一个连接, 下载一个集成了JCEF的JetBrains Runtime, 最上面一栏是Idea默认的, 下面是各类环境的, 按需下载安装, 并回到刚才的ChooseBoot中, 在location栏目定位本地解压缩后的运行环境即可, 重启后问题解决.

2\. 原因
------

早期使用2020.3以前版本时不知道是出了什么bug, 当时找资料大体是让我用OpenJDK而不是JetBrains自带的, 就换了, 后来升级2021启动不起来, 才设置了IDeaHome专门使用JDK11, 这个OpenJDK11就不包含JavaFX, 所以出了问题

版权声明\
本文为[demontxy]所创，转载请带上原文链接，感谢\
https://blog.csdn.net/demontxy/article/details/121968403
