---
layout:     post
title:      "ITMS-90809: Deprecated API Usage"
subtitle:   ""
date:       2020-05-22
author:     "newstrong"
header-img: "https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/bg_iphone_feature.png"
catalog: false
tags:
    - iOS
    - "Deprecated API Usage"
---

# 解决ITMS-90809: Deprecated API Usage UiWebView 审核不通过

> 苹果审核时提示ITMS-90809: Deprecated API Usage - Apple will stop accepting submissions of new apps that use UIWebView APIs starting from April 2020. See https://developer.apple.com/documentation/uikit/uiwebview for more information.

解决方案：查找代码中哪些代码或者二进制库使用了UiWebView，然后进行修改或者版本升级

## 方法一：

切换到项目根目录

~~~shell
grep -r UiWebView .
~~~

## 方法二：

切换到项目根目录

~~~shell
find . -type f | grep -e ".a" -e ".framework" | xargs grep -s UIWebView
~~~

### 方法二输出如下：

~~~shell
find . -type f | grep -e ".a" -e ".framework" | xargs grep -s UIWebView                                                        2 ↵
Binary file ./Pods/Crashlytics/iOS/Crashlytics.framework/Crashlytics matches
Binary file ./Pods/IronSourceVungleAdapter/ISVungleAdapter/ISVungleAdapter.framework/ISVungleAdapter matches
Binary file ./Pods/IronSourceAdColonyAdapter/ISAdColonyAdapter/ISAdColonyAdapter.framework/ISAdColonyAdapter matches
Binary file ./Pods/IronSourceTapjoyAdapter/ISTapjoyAdapter/ISTapjoyAdapter.framework/ISTapjoyAdapter matches
Binary file ./Pods/Fabric/upload-symbols matches
Binary file ./Pods/IronSourceSDK/IronSource/IronSource.framework/Versions/A/IronSource matches
~~~



## 理论上上述两种方法都能在代码中找到对应使用了UiWebView的库，但是第一种方法，以前可以使用，最近好像不好使了。在此记录下。

