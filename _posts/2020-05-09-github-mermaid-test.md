---
layout:     graph
title:      "Github Page中通过Mermaid画流程图"
subtitle:   ""
date:       2020-05-09
author:     "newstrong"
header-img: "img/in-post/anti-covid-19-by-chris.jpeg"
catalog: ture
tags:
    - Jekyll
    - Github Page
---
# 在GitHub Pages 中使用Mermaid 画图

> 传统画流程图通常使用 **Visio Studio**，使用比较复杂，毕竟要安装；本文简单介绍在GitHub Pages 中通过 mermaid 库，来绘制流程图、甘特图的前置步骤。 

## 原理

mermaid解析特定格式，转化为svg，显示到界面上

## 步骤

简单添加以下内容到你的markdown中，即可生产出如下图的内容：

~~~javascript
<script src='https://unpkg.com/mermaid@7.1.2/dist/mermaid.min.js'></script>
<script>mermaid.initialize({startOnLoad:true});</script>

<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
</div>
~~~

## 效果

<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
</div>

## 参考链接

- Mermaid Doc:[https://mermaidjs.github.io/#/](https://mermaidjs.github.io/#/)

- Mermaid Live Editor:[https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggVERcbiAgQVtDaHJpc3RtYXNdIC0tPnxHZXQgbW9uZXl8IEIoR28gc2hvcHBpbmcpXG4gIEIgLS0-IEN7TGV0IG1lIHRoaW5rfVxuICBDIC0tPnxPbmV8IERbTGFwdG9wXVxuICBDIC0tPnxUd298IEVbaVBob25lXVxuICBDIC0tPnxUaHJlZXwgRltmYTpmYS1jYXIgQ2FyXVxuXHRcdCIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In19](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggVERcbiAgQVtDaHJpc3RtYXNdIC0tPnxHZXQgbW9uZXl8IEIoR28gc2hvcHBpbmcpXG4gIEIgLS0-IEN7TGV0IG1lIHRoaW5rfVxuICBDIC0tPnxPbmV8IERbTGFwdG9wXVxuICBDIC0tPnxUd298IEVbaVBob25lXVxuICBDIC0tPnxUaHJlZXwgRltmYTpmYS1jYXIgQ2FyXVxuXHRcdCIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In19)
- Mermaid 使用教程:[https://www.jianshu.com/p/e3901c57b596](https://www.jianshu.com/p/e3901c57b596)



