---
layout:     post
title:      "提升团队开发效率 - Nexus Repository"
subtitle:   ""
date:       2020-05-14
author:     "newstrong"
header-img: "https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/bg-purple-lavender.png"
catalog: true
tags:
    - Nexus
    - Maven
---

# 提升团队开发效率 - Nexus Repository

原文链接：[https://blog.51cto.com/14579491/2451530](https://blog.51cto.com/14579491/2451530)

> 关于提升团队开发效率有很多可以讲，这里讨论一个比较简单易行并且"效果明显"的方法。
> 在有些公司，如果对访问外网做了限制的话，可能需要走统一的代理才能访问外网。并且管理更> > 加严格的可能还会对访问的外部资源签发自签名的证书，这样会导致几个问题
>
> + 每个人需要在工作电脑上配置代理
> + 不同的软件/平台配置代理的方式并不统一
> + 访问速度较慢
> + 可能需要把自签名的证书import到对应的trust store中，并且可能要定期或不定期更新
> + 以上这些问题可能会影响到多种角色的人，无论是开发，测试，甚至运维。(只要和打包扯上关系的，或多或少都有影响)。假如1个人要花30分钟处理以上问题，那么10个人就要5个小时，总体算下来时间还是很可观的，非常影响整体的效率。(如果是个人开发者，可能意义就不大了)有什么解决的方法没有?或许Nexus Repository是一个选择。

## 什么是Nexus，有什么用?
* 在开发当中经常要使用各种依赖库，比如Java/Android中的maven central，Python中的pypi等等。
* Nexus Repository是一个仓库管理器，通过它，我们可以代理各种public的仓库，也可以构建自己的私有仓库。使得软件开发中的依赖管理、编译、发布、部署等更加方便和高效。
* Nexus Repository有Pro的付费版本，但是一般我们使用它的免费OSS版本即可。

## 如何使用Nexus?

### 安装

这里我使用docker来安装，当然你也可以直接下载安装包安装。

#### 下载nexus的最新image

```shell
$ docker pull sonatype/nexus3
```

#### 绑定端口，运行

```shell
$ docker run -d -p 8081:8081 --name nexus sonatype/nexus3
```

#### 本机测试

	打开浏览器输入http://localhost:8081/

看到这个界面，就说明安装成功了

![](https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/20200519154442.png)

首次安装成功，会提示我们修改默认的admin密码，我们需要shell进去，拿到密码

```shell
$ docker exec -it nexus bash
```
根据提示，进入对应目录，查看密码
如果要stop或者start nexus的话，执行以下命令

```shell
$ docker stop/start nexus
```


前边我们并没有设置自启动，如果需要container随着docker启动而自启动的话，可以执行以下命令

```shell
$ docker update --restart=always nexus
```

### 应用

#### Android、Java
默认的repo：
![](https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/20200519154847.png)

Android和Java会共用大部分的public maven，常见的有

* google
* maven central
* jcenter
* fabric

除此之外，Android还会用到

* gradle plugin
* gradle distribution

以gradle distribution为例，看看如何添加这个配置

![](https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/20200519155152.png)

**这里注意，它的type是raw(proxy)**

常用的maven，以及对应的type

![](https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/20200519155355.png)

依次创建完对应的repo之后，调整一下maven-public，把所有的maven2类型的repo都加进去

![](https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/20200519155440.png)

Android客户端配置

​	以Android项目为例，看看我们需要修改哪些配置

1. 首先用任意文本编辑器打开项目(不要用Android Studio或IDEA，它会自动触发gradle sync)

修改项目build.gradle的repo，把现有的repo全部删掉或者注释掉，然后换成

```
maven { url 'http://localhost:8081/repository/maven-public/' }
```

2. 修改项目settings.gradle，配置gradle plugin的repo，在文件顶部加入

```groovy
pluginManagement {
    repositories {
        maven { url 'http://localhost:8081/repository/maven-public/' }
    }
}
```

如图：

![](https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/20200519160123.png)

3. 修改文件gradle/wrapper/gradle-wrapper.properties

![](https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/20200519160238.png)

如图：

![](https://raw.githubusercontent.com/newstrong/newstrong.github.io/master/img/20200519160123.png)

#### NodeJs
		创建一个npm (proxy)的repo，remote url是
		https://registry.npmjs.org/

---

		查看当前npm的registry - $ npm get registry
		设置npm mirror
		替换称你自己的地址
		$ npm set http://localhost:8081/repository/npm-registry/
		还原npm registry
		$ npm set registry https://registry.npmjs.org/

#### Python

		创建一个pypi (proxy)的repo，remote url是
		https://pypi.org

----

		查看当前的配置信息，$ pip3 config list -v
		在用户目录下创建文件~/.pip/pip.conf(如果不存在的话)，加入以下配置
		
		[global]
		index-url = http://localhost:8081/repository/pypi-proxy/simple
		trusted-host = localhost

这里要特别注意，index-url最后的simple是必须要有的。simple之前的地址就是nexus的访问地址，请替换成自己的地址。
因为我们没有使用https，所以需要在trusted-host里边加入我们的host

#### iOS
		创建一个cocoapods (proxy)的repo，remote url是
		https://cdn.cocoapods.org/

---
		cocoapods比较麻烦的地方在于客户端只支持https，我暂时没有做测试。解决方案是使用自签名证书来开启https。
		有兴趣的同学可以根据官方文档的说明去调调看 - CocoaPods Repositories

### Summary

​		总结一下，我们了解了Nexus Repository作为一种包依赖管理器，可以解决在公司内部的依赖下载配置繁琐以及慢的问题然后讲解了如何安装配置Nexus
随后，针对不同的平台分别做了配置讲解，如Android/Java, NodeJs, Python, 和iOS
​		这里只是列举了一部分，实际上Nexus支持的还有很多，比如**apt**, **conda**, **docker**, **go**, **nuget**, **rubygems**, **yum** 等等。如果有相应的需要，可以找对应的资料进行配置使用。
