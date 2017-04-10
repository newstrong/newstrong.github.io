---
layout:     post
title:      "Android开发备忘"
subtitle:   ""
date:       2017-04-06
author:     "newstrong"
header-img: "img/in-post/post-android-note/post-android-note-bg.jpg"
tags:
    - 技术
    - Android
    - 开发
---



# Android开发备忘

### library依赖外部库报错:Multiple dex files define exception

​	不同模块特别是library中依赖了同名的库,分别是通过gradle依赖和jar包,android stuido 不能区分出他们是一个库,虽然包名相同.在打包阶段会同时编译进APK中,造成dex multi exception.解决方式很简单,尽量不出现分别用两种方式依赖库的形式,并且首选使用gradle compile project方式依赖.



### 同一个依赖库使用不同版本,报错

​	例如support:appcompat-v7库,在library中使用的版本和module中使用不同,会导致莫名crash错误.需要注意的是在编译的时候可能编译通过并能正常运行.





