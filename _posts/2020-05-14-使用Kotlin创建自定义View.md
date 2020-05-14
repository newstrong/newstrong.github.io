---
layout:     post
title:      "使用Kotlin创建自定义View"
subtitle:   ""
date:       2020-05-14
author:     "newstrong"
header-img: "img/in-post/bg-kotlin-logo.jpg"
tags:
    - Android
    - Kotlin
    - 自定义View
---

# 使用Kotlin创建自定义View

通过Android Studio点击 New-Kotlin Class/Files 创建的一个类，指定它实现一个View，例如：FrameLayout。此时IDE会提示你需要实现它的构造方法，Alert+Enter 即可，完成后如下：



~~~kotlin
class CustomViewTest(context: Context) : FrameLayout(context) {

}
~~~



此时只实现了View的一个构造方法，在代码中初始化并使用并没有问题，但是不能再XML中引用，因为自定义View需要实现类似以下的构造方法：



~~~kotlin
public class CustomViewTest extends FrameLayout {
    public CustomViewTest(@NonNull Context context) {
        super(context);
    }

    public CustomViewTest(@NonNull Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
    }

    public CustomViewTest(@NonNull Context context, @Nullable AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }

    @RequiresApi(api = Build.VERSION_CODES.LOLLIPOP)
    public CustomViewTest(@NonNull Context context, @Nullable AttributeSet attrs, int defStyleAttr, int defStyleRes) {
        super(context, attrs, defStyleAttr, defStyleRes);
    }
}
~~~



还好Kotlin有constructor关键字，用来在类名后指定主构造方法，或者单独在类中，指定次级构造方法。



~~~kotlin
class CustomViewTest: FrameLayout {
    constructor(context: Context):this(context,null)

    constructor(context: Context, attrs: AttributeSet?) : this(context,attrs,0)

    constructor(context: Context,attrs: AttributeSet?,defStyleAttr:Int):super(context,attrs,0)
}
~~~



上面的写法其实不是很好看，不太符合Kotlin极简思想，请参考更简单的实现：

~~~kotlin
class CustomViewTest @JvmOverloads constructor(context: Context,attrs:AttributeSet?,defStyleAttr: Int=0): FrameLayout(context,attrs,defStyleAttr) {
    
}
~~~



是不是够极简，但是在Java调用这个类的构造方法时候，因为Java没有默认参数的这种写法，需要全部指定所有的参数。



## 结论：全局Kotlin，使用最后一种极简的写法，Java-Kotlin混编，特别是需要Java初始化Kotlin自定义View，则使用Constructor写法。

---

原文：

​	[https://antonioleiva.com/custom-views-android-kotlin/](https://antonioleiva.com/custom-views-android-kotlin/)

