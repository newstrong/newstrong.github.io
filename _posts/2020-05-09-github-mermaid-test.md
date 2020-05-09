---
layout:     graph
title:      "Github Page中通过Mermaid画流程图"
subtitle:   ""
date:       2020-05-09
author:     "newstrong"
header-img: "img/in-post/anti-covid-19-by-chris.jpeg"
tags:
    - Jekyll
    - Github Page
---
# 在GitHub Pages 中使用Mermaid 画图
~~~

简单添加以下内容到你的markdown中，即可生产出如下图的内容：
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

<div class="mermaid">
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
</div>


