---
layout:     post
title:      "git类图形化log"
subtitle:   ""
date:       2017-04-07
author:     "newstrong"
header-img: "img/in-post/post-git-log/colored-pencils-upside-down-with-room-for-text-picjumbo-com.jpg"
tags:
    - 技术
    - Android
    - 开发
---



# git图形化log

git查看commit的命令是
~~~
git log
~~~
输入之后的效果如下:
![](/img/in-post/post-git-log/git-log.png)
上图非常不直观,没有分支的概念,只有每次提交的commit的相关信息.试一试下面的一段代码吧.
~~~
git config --global alias.gl "log --graph --all --relative-date --date=short --abbrev-commit --format=\"%x09 %h %Cgreen%cd%Creset [%Cblue%cn%Creset] %C(auto)%d%Creset %s\""
~~~
输入下面的代码,查看修改后的效果.
~~~
git gl
~~~

![](/img/in-post/post-git-log/git-color-log.png)






