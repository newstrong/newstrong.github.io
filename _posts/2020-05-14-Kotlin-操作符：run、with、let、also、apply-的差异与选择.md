---
layout:     graph
title:      "Kotlin 操作符：run、with、let、also、apply 的差异与选择"
subtitle:   ""
date:       2020-05-14
author:     "newstrong"
header-img: "img/in-post/bg-kotlin-logo.jpg"
tags:
    - Android
    - Kotlin
    - Mermaid
---
# Kotlin 操作符：run、with、let、also、apply 的差异与选择

原文：[Kotlin 操作符：run、with、let、also、apply 的差异与选择](https://juejin.im/post/5a1be4cc51882512a86108f8)

通过参考原文，通过mermaid画出流程图，没有任何新东西。/笑脸

<div class="mermaid">
graph TD
  A(选择标准函数) --> B{"需要返回自身(this)" }
  B -->|NO| C{"需要扩展函数?(空检查,链式调用)"}
  C -->|NO| D{"传递this作为参数"}
  D -->|NO| E("使用run()")
  D -->|YES| F("使用with(T)")
  C -->|YES| G{"传递it/this作为参数"}
  G -->|传递this| H("使用T.run()")
  G -->|传递it| I("使用T.let()")

  B -->|YES| J{"传递it/this作为参数"}
  J-->|传递this| K("使用T.apply()")
  J-->|传递it| L("使用T.also()")
		
</div>