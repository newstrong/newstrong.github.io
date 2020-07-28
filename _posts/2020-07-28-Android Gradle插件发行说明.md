---
layout:     post
title:      "Android Gradle插件发行说明"
subtitle:   ""
date:       2020-07-28
author:     "newstrong"
header-img: "img/20200519103730.png"
catalog: ture
tags:
    - 技术
    - Android
    - 开发
---
# Android Gradle插件发行说明

Android Studio构建系统基于Gradle，而Android Gradle插件添加了一些特定于构建Android应用的功能。尽管通常使用Android Studio同步更新Android插件，但该插件（以及Gradle系统的其余部分）可以独立于Android Studio运行，并且可以单独进行更新。

本页说明如何使您的Gradle工具保持最新状态以及最新更新。

有关如何使用Gradle配置Android构建的详细信息，请参见以下页面：

- [配置构建](https://developer.android.com/studio/build)
- [Android插件DSL参考](https://google.github.io/android-gradle-dsl/current/)
- [Gradle DSL参考](https://docs.gradle.org/current/dsl/)

有关Gradle构建系统的更多信息，请参阅[Gradle用户指南](https://docs.gradle.org/current/userguide/userguide.html)。

## 更新Android Gradle插件

更新Android Studio时，您可能会提示您自动将Android Gradle插件更新为最新的可用版本。您可以选择接受更新，也可以根据项目的构建要求手动指定版本。

您可以在Android Studio 的“ **文件”** >“ **项目结构”** >“ **项目”**菜单中或顶级`build.gradle`文件中指定插件版本。插件版本适用于该Android Studio项目中内置的所有模块。以下示例将插件从`build.gradle`文件设置为版本4.0.0 ：

```groovy
buildscript { 
    存储库{ // Gradle 4.1及更高版本使用// google（）方法来支持Google的Maven 存储库。并且您需要包含此仓库才能下载// Android Gradle插件3.0.0或更高版本。        google （）... }     依赖项{         classpath'com.android.tools.build :gradle:4.0.0' } }
        
        
        

        
    


    
```

**警告：**您不应在版本号中使用动态依赖项，例如`'com.android.tools.build:gradle:2.+'`。使用此功能可能会导致版本意外更新，并难以解决版本差异。

如果尚未下载指定的插件版本，则Gradle会在您下次构建项目时下载它，或 从Android Studio菜单栏中单击**工具** > **Android** > **与Gradle文件同步项目**。

## 更新摇篮

更新Android Studio时，可能会提示您也将Gradle更新到最新的可用版本。您可以选择接受更新，也可以根据项目的构建要求手动指定版本。

下表列出了每个版本的Android Gradle插件所需的Gradle版本。为了获得最佳性能，您应该使用Gradle和插件的最新版本。

| 插件版本    | 所需的Gradle版本 |
| :---------- | :--------------- |
| 1.0.0-1.1.3 | 2.2.1-2.3        |
| 1.2.0-1.3.1 | 2.2.1-2.9        |
| 1.5.0       | 2.2.1-2.13       |
| 2.0.0-2.1.2 | 2.10-2.13        |
| 2.1.3-2.2.3 | 2.14.1+          |
| 2.3.0+      | 3.3+             |
| 3.0.0+      | 4.1+             |
| 3.1.0+      | 4.4+             |
| 3.2.0-3.2.1 | 4.6+             |
| 3.3.0-3.3.3 | 4.10.1+          |
| 3.4.0-3.4.3 | 5.1.1+           |
| 3.5.0-3.5.4 | 5.4.1+           |
| 3.6.0-3.6.4 | 5.6.4+           |
| 4.0.0+      | 6.1.1+           |

您可以在Android Studio 的“ **文件”** >“ **项目结构”** >“ **项目”**菜单中指定Gradle版本，也可以在**文件中**编辑Gradle发行参考 `gradle/wrapper/gradle-wrapper.properties`。以下示例在`gradle-wrapper.properties`文件中将Gradle版本设置为6.1.1 。

```groovy
... 
distributionUrl = https \：//services.gradle.org/distributions/gradle-6.1.1-all.zip ...
```

## 4.0.0（2020年4月）

此版本的Android插件需要满足以下条件：

- [摇篮6.1.1](https://docs.gradle.org/6.1.1/release-notes.html)。要了解更多信息，请阅读有关[更新Gradle](https://developer.android.com/studio/releases/gradle-plugin#updating-gradle)的部分。
- [SDK Build Tools 29.0.2](https://developer.android.com/studio/releases/build-tools#notes)或更高版本。

**4.0.1（2020年7月）**



此次更新支持与新的默认设置和[Android 11中软件包可见性的](https://developer.android.com/preview/privacy/package-visibility)功能兼容。

在以前的Android版本中，可以查看设备上安装的所有应用程序的列表。从Android 11（API级别30）开始，默认情况下，应用程序只能访问已过滤的已安装软件包列表。要查看系统上更广泛的应用程序列表，您现在需要 在应用程序或库的Android清单中[添加一个``元素](https://developer.android.com/preview/privacy/package-visibility#package-name)。

Android Gradle插件4.1+已经与新`<queries>`声明兼容 ；但是，旧版本不兼容。如果添加`<queries>`元素，或者开始依赖支持目标Android 11的库或SDK，则在构建应用程序时可能会遇到清单合并错误。

为解决此问题，我们发布了AGP 3.3及更高版本的一组补丁。如果您使用的是AGP的旧版本，请 [升级](https://developer.android.com/studio/releases/gradle-plugin?buildsystem=ndk-build#updating-plugin) 到以下版本之一：

| **如果您使用的是 AGP版本...** | **...升级到：** |
| :---------------------------: | :-------------: |
|            4.0。*             |      4.0.1      |
|            3.6。*             |      3.6.4      |
|            3.5。*             |      3.5.4      |
|            3.4。*             |      3.4.3      |
|            3.3。*             |      3.3.3      |

有关此新功能的更多信息，请参阅 [Android 11中的程序包可见性](https://developer.android.com/preview/privacy/package-visibility)。

### 新功能

此版本的Android Gradle插件包含以下新功能。

#### 支持Android Studio构建分析器

“ **构建分析器”**窗口可帮助您了解和诊断构建过程中的问题，例如禁用的优化和配置不正确的任务。当您将Android Studio 4.0及更高版本与Android Gradle插件`4.0.0`及更高版本配合使用时，此功能可用。您可以 从Android Studio 打开“ **构建分析器”**窗口，如下所示：

1. 如果尚未执行此操作，请通过从菜单栏中选择**Build> Make Project**来构建您的应用程序。

2. 从菜单栏中选择**查看>工具窗口>构建**。

3. 在“ 

   生成”

   窗口中，以下列方式之一打开“ 

   生成分析器”

   窗口：

   - Android Studio完成构建项目后，单击“ **构建分析器”**选项卡。
   - Android Studio完成构建项目后，单击“ **构建输出”**窗口右侧的链接。

![img](https://developer.android.com/build/build-analyzer/plugins-breakdown.png)

“ **构建分析器”**窗口在左侧的树中组织了可能的构建问题。您可以检查并单击每个问题，以在右侧面板中调查其详细信息。当Android Studio分析您的构建时，它将计算确定构建持续时间的一组任务，并提供可视化帮助您了解每个任务的影响。您还可以通过展开“ **警告”**节点来获取有关警告的详细信息。

要了解更多信息，请阅读[识别构建速度回归](https://developer.android.com/studio/build/build-analyzer)。

#### Java 8库在D8和R8中逐渐消失

Android Gradle插件现在支持使用多种Java 8语言API，而无需为您的应用设置最低API级别。

通过一个称为*desugaring*的过程，Android Studio 3.0及更高版本中的DEX编译器D8已经为Java 8语言功能（例如lambda表达式，默认接口方法，尝试资源等）提供了实质性支持。在Android Studio 4.0中，已将废糖处理引擎扩展为能够对Java语言API进行糖化。这意味着您现在可以在`java.util.streams`支持较早版本的Android的应用程序中包含仅在最新的Android版本（例如）中可用的标准语言API 。

此版本支持以下一组API：

- 顺序流（`java.util.stream`）
- 的子集 `java.time`
- `java.util.function`
- 最近添加到 `java.util.{Map,Collection,Comparator}`
- 选配（`java.util.Optional`，`java.util.OptionalInt`和 `java.util.OptionalDouble`）和其他一些新的类与上述API有用
- 一些补充`java.util.concurrent.atomic`（在新的方法 `AtomicInteger`，`AtomicLong`和`AtomicReference`）
- `ConcurrentHashMap` （已修复Android 5.0的错误）

为了支持这些语言API，D8会编译一个单独的库DEX文件，其中包含缺少的API的实现，并将其包含在您的应用程序中。取消调试过程将重写您的应用程序代码，以在运行时使用此库。

要启用对这些语言API的支持，请在模块`build.gradle`文件中包括以下内容：

```groovy
android {
  defaultConfig {
    // Required when setting minSdkVersion to 20 or lower
    multiDexEnabled true
  }

  compileOptions {
    // Flag to enable support for the new language APIs
    coreLibraryDesugaringEnabled true
    // Sets Java compatibility to Java 8
    sourceCompatibility JavaVersion.VERSION_1_8
    targetCompatibility JavaVersion.VERSION_1_8
  }
}

dependencies {
  coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:1.0.4'
}
```

#### 启用或禁用构建功能的新选项

Android Gradle插件4.0.0引入了一种新方法来控制您要启用和禁用的构建功能，例如视图绑定和数据绑定。添加新功能后，默认情况下将禁用它们。然后，您可以使用该`buildFeatures`块仅启用所需的功能，它可以帮助您优化项目的构建性能。您可以在模块级`build.gradle`文件中为每个模块设置选项，如下所示：

```groovy
android {
    // The default value for each feature is shown below. You can change the value to
    // override the default behavior.
    buildFeatures {
        // Determines whether to generate a BuildConfig class.
        buildConfig = true
        // Determines whether to support View Binding.
        // Note that the viewBinding.enabled property is now deprecated.
        viewBinding = false
        // Determines whether to support Data Binding.
        // Note that the dataBinding.enabled property is now deprecated.
        dataBinding = false
        // Determines whether to generate binder classes for your AIDL files.
        aidl = true
        // Determines whether to support RenderScript.
        renderScript = true
        // Determines whether to support injecting custom variables into the module’s R class.
        resValues = true
        // Determines whether to support shader AOT compilation.
        shaders = true
    }
}
```

您还可以通过在项目的`gradle.properties`文件中包含以下一项或多项内容，为项目中所有模块指定这些功能的默认设置 ，如下所示。请记住，您仍然可以使用`buildFeatures`模块级`build.gradle`文件中的 块来覆盖这些项目范围的默认设置。

```
android.defaults.buildfeatures.buildconfig=true
android.defaults.buildfeatures.aidl=true
android.defaults.buildfeatures.renderscript=true
android.defaults.buildfeatures.resvalues=true
android.defaults.buildfeatures.shaders=true
```

#### 功能上的依存关系

在早期版本的Android Gradle插件中，所有动态功能模块都只能依赖于应用程序的基本模块。现在，当使用Android Gradle插件4.0.0时，您可以包括一个依赖于另一个功能模块的功能模块。也就是说，`:video`功能可以取决于`:camera`功能，而功能取决于基础模块，如下图所示。

![功能依赖功能](https://developer.android.com/images/app-bundle/feature-on-feature.png)

动态功能`:video`取决于feature `:camera`，后者取决于基本`:app`模块。



这意味着当您的应用程序请求下载动态功能模块时，该应用程序还会下载其依赖的其他功能模块。您之后[创建动态功能模块，](https://developer.android.com/studio/projects/dynamic-delivery/on-demand-delivery) 为您的应用程序，你可以声明在模块的一个功能上特征依赖 `build.gradle`文件。例如，`:video`模块声明对`:camera`以下项的依赖关系 ：

```groovy
// In the build.gradle file of the ':video' module.
dependencies {
    // All dynamic feature modules must declare a dependency
    // on the base module.
    implementation project(':app')
    // Declares that this module also depends on the 'camera'
    // dynamic feature module.
    implementation project(':camera')
    ...
}
```

此外，您应该通过在菜单栏中单击“ **帮助”>“编辑自定义VM选项** ”并启用以下功能，启用Android Studio中的“功能对功能的依赖关系”功能（例如，在编辑“运行”配置时支持该功能）：

```
-Drundebug.feature.on.feature=true
```

#### 依赖元数据

使用Android Gradle插件4.0.0及更高版本构建应用时，该插件包含描述已编译到应用中的依赖项的元数据。上载应用程序时，Play控制台会检查此元数据，为您提供以下好处：

- 获取有关您的应用使用的SDK和依赖项的已知问题的警报
- 收到可行的反馈来解决这些问题

数据经过压缩，通过Google Play签名密钥加密，并存储在发布应用的签名栏中。但是，您可以自己在以下目录中的本地中间构建文件中检查元数据： `<project>/<module>/build/outputs/sdk-dependencies/release/sdkDependency.txt`。

如果您不想共享此信息，可以通过在模块`build.gradle`文件中添加以下内容来退出：

```groovy
android {
    dependenciesInfo {
        // Disables dependency metadata when building APKs.
        includeInApk = false
        // Disables dependency metadata when building Android App Bundles.
        includeInBundle = false
    }
}
```

#### 从AAR依赖项导入本机库

现在，您可以从应用程序的AAR依赖项导入C / C ++库。当您遵循以下描述的配置步骤时，Gradle会自动使这些本机库可用于您的外部本机构建系统（例如CMake）。请注意，Gradle仅使这些库可用于您的构建。您仍然必须配置构建脚本以使用它们。

使用[Prefab](https://google.github.io/prefab/)软件包格式导出库。

每个依赖项最多可以公开一个包含一个或多个模块的Prefab软件包。预制模块是单个库，可以是共享库，静态库或仅标头库。

通常，程序包名称与Maven工件名称匹配，模块名称与库名称匹配，但这并不总是正确的。因为您需要知道库的包和模块名称，所以可能需要查阅依赖项的文档来确定这些名称是什么。

##### 配置您的外部本机构建系统

要查看您需要执行的步骤，请单击您计划使用的外部本机构建系统。

CMake的 ndk构建

AAR中包含的本机依赖项通过[CMAKE_FIND_ROOT_PATH](https://cmake.org/cmake/help/latest/variable/CMAKE_FIND_ROOT_PATH.html)变量公开给您的CMake项目 。调用CMake时，Gradle会自动设置此值，因此，如果您的构建系统修改了此变量，请确保附加而不是分配给它。

每个依赖项都会向您的CMake构建公开一个[配置文件包](https://cmake.org/cmake/help/latest/manual/cmake-packages.7.html#config-file-packages)，您可以使用[`find_package`](https://cmake.org/cmake/help/latest/command/find_package.html)命令将其导入。此命令搜索与给定软件包名称和版本匹配的配置文件软件包，并公开它定义要在构建中使用的目标。例如，如果您的应用程序定义 `libapp.so`并使用curl，则应在`CMakeLists.txt`文件中包含以下内容 ：

```cmake
add_library(app SHARED app.cpp)

# Add these two lines.
find_package(curl REQUIRED CONFIG)
target_link_libraries(app curl::curl)
```

您现在可以`#include "curl/curl.h"`在中指定`app.cpp`。当你建立你的项目，你的外部原始构建系统自动链接`libapp.so` 反对`libcurl.so`和包`libcurl.so`的APK或应用捆绑。有关其他信息，请参见[curl预制样本](https://github.com/android/ndk-samples/tree/master/prefab/curl-ssl)。

### 行为改变

使用此版本的插件时，您可能会遇到以下行为更改。

#### 删除了“功能”和“ instantapp” Android Gradle插件

Android Gradle插件3.6.0不推荐使用Feature插件（`com.android.feature`）和Instant App插件（`com.android.instantapp`），而建议使用Dynamic Feature插件（`com.android.dynamic-feature`）使用[Android App Bundles](https://developer.android.com/guide/app-bundle)构建和打包您的即时应用[程序](https://developer.android.com/guide/app-bundle)。

在Android Gradle插件4.0.0及更高版本中，这些不推荐使用的插件已被完全删除。因此，要使用最新的Android Gradle插件，您需要[迁移即时应用程序以支持Android App Bundles](https://developer.android.com/topic/google-play-instant/feature-module-migration)。通过迁移即时应用程序，您可以利用应用程序包的好处并[简化应用程序的模块化设计](https://android-developers.googleblog.com/2019/04/google-play-instant-feature-plugin.html)。

**注意：**要在Android Studio 4.0及更高版本中打开使用已删除插件的项目，该项目必须使用Android Gradle插件3.6.0或更低版本。

#### 单独的注释处理功能已删除

将注释处理分离为专用任务的功能已被删除。当仅Java项目中使用非增量注释处理器时，此选项用于维护增量Java编译。通过在文件中设置`android.enableSeparateAnnotationProcessing`来启用 `true`该功能 `gradle.properties`，该功能将不再起作用。

相反，您应该迁移到[使用增量注释处理器](https://developer.android.com/studio/build/optimize-your-build#annotation_processors)来提高构建性能。

#### includeCompileClasspath已弃用

Android Gradle插件不再检查或包括您在编译类路径上声明的注释处理器，并且 `annotationProcessorOptions.includeCompileClasspath`DSL属性不再起作用。如果在编译类路径上包含注释处理器，则可能会出现以下错误：

```
Error: Annotation processors must be explicitly declared now.
```

若要解决此问题，您必须`build.gradle`使用`annotationProcessor`依赖项配置在文件中包括注释处理器 。要了解更多信息，请阅读[添加注释处理器](https://developer.android.com/studio/build/dependencies#annotation_processor)。

### 自动打包CMake使用的预构建依赖项

早期版本的Android Gradle插件要求您使用显式打包CMake外部本机内部版本使用的所有预构建库 `jniLibs`。您可能在`src/main/jniLibs`模块目录中或您的`build.gradle` 文件中配置的其他目录中具有库：

```groovy
sourceSets {
    main {
        // The libs directory contains prebuilt libraries that are used by the
        // app's library defined in CMakeLists.txt via an IMPORTED target.
        jniLibs.srcDirs = ['libs']
    }
}
```

使用Android Gradle Plugin 4.0时，不再需要上述配置，并且会导致构建失败：

```
* What went wrong:
Execution failed for task ':app:mergeDebugNativeLibs'.
> A failure occurred while executing com.android.build.gradle.internal.tasks.Workers$ActionFacade
   > More than one file was found with OS independent path 'lib/x86/libprebuilt.so'
```

现在，外部本机构建会自动打包这些库，因此将`jniLibs`结果与库明确打包在一起。为避免构建错误，请将预构建的库移到外部位置`jniLibs`或`jniLibs`从`build.gradle` 文件中删除配置。

### 已知的问题

本部分描述了Android Gradle插件4.0.0中存在的已知问题。

#### Gradle工作者机制中的比赛条件

在使用`--no-daemon`Gradle 6.3和更低版本以及更低版本运行时，Android Gradle插件4.0中的更改可能会在Gradle中触发竞争条件，从而导致构建在构建完成后挂起。

此问题将在Gradle 6.4中修复。

## 3.6.0（2020年2月）

此版本的Android插件需要满足以下条件：

- [摇篮5.6.4](https://docs.gradle.org/5.6.4/release-notes.html)。要了解更多信息，请阅读有关[更新Gradle](https://developer.android.com/studio/releases/gradle-plugin#updating-gradle)的部分。
- [SDK Build Tools 28.0.3](https://developer.android.com/studio/releases/build-tools#notes)或更高版本。

**3.6.4（2020年7月）**



此次更新支持与新的默认设置和[Android 11中软件包可见性的](https://developer.android.com/preview/privacy/package-visibility)功能兼容 。

有关详细信息，请参见[4.0.1发行说明](https://developer.android.com/studio/releases/gradle-plugin#4.0.1)。

### 新功能

此版本的Android Gradle插件包含以下新功能。

#### 视图绑定

在代码中引用视图时，视图绑定可提供编译时安全性。现在`findViewById()`，您可以替换为自动生成的绑定类参考。要开始使用View绑定，请在每个模块的`build.gradle`文件中包括以下内容 ：

```groovy
android {
    viewBinding.enabled = true
}
```

要了解更多信息，请阅读[View Binding文档](https://developer.android.com/topic/libraries/view-binding)。

#### 支持Maven Publish插件

Android Gradle插件包括对[Maven Publish Gradle插件的](https://docs.gradle.org/current/userguide/publishing_maven.html)支持，该 [插件](https://docs.gradle.org/current/userguide/publishing_maven.html)使您可以将构建工件发布到Apache Maven存储库。Android的摇篮插件创建一个 [*组件*](https://docs.gradle.org/current/userguide/dependency_management_terminology.html#sub:terminology_component) 在您的应用程序或者库模块，您可以使用自定义每个构建变量神器 [*发布*](https://docs.gradle.org/current/userguide/publishing_maven.html#publishing_maven:publications) 到Maven仓库。

要了解更多信息，请转至有关如何[使用Maven Publish插件的页面](https://developer.android.com/studio/build/maven-publish-plugin)。

#### 新的默认打包工具

在构建应用程序的调试版本时，该插件使用名为*zipflinger*的新打包工具来构建APK。此新工具应可提高构建速度。如果新的打包工具无法正常运行，请[报告错误](https://developer.android.com/studio/report-bugs)。您可以通过在`gradle.properties`文件中包含以下内容来恢复使用旧的打包工具：

```
android.useNewApkCreator=false
```

#### 本机版本归因

现在，您可以确定Clang构建和链接项目中每个C / C ++文件所花费的时间。Gradle可以输出包含这些编译器事件时间戳的Chrome跟踪，因此您可以更好地了解构建项目所需的时间。要输出此构建归因文件，请执行以下操作：

1. `-Pandroid.enableProfileJson=true`运行Gradle构建时添加标志。例如：

   `gradlew assembleDebug -Pandroid.enableProfileJson=true`

2. 打开Chrome浏览器，然后`chrome://tracing`在搜索栏中输入。

3. 单击**加载**按钮，然后导航`project-root/build/android-profile` 以找到文件。该文件名为。`profile-timestamp.json.gz`

您可以在查看器顶部附近看到本机构建归因数据：

![Chrome中的本机版本归因跟踪](https://developer.android.com/studio/images/releases/native-build-attribution.png)

### 行为改变

使用此版本的插件时，您可能会遇到以下行为更改。

#### 本地库默认打包为未压缩

现在，当您构建应用程序时，该插件默认设置`extractNativeLibs`为`"false"`。也就是说，您的本机库是页面对齐的，并且未经压缩打包。虽然这会导致较大的上载大小，但您的用户将从以下方面受益：

- 应用程序安装尺寸较小，因为平台可以直接从已安装的APK访问本机库，而无需创建库的副本。
- 下载大小较小，因为当您在APK或Android App Bundle中包含未压缩的本机库时，Play Store压缩通常会更好。

如果您想让Android Gradle插件打包压缩的本机库，请在应用清单中添加以下内容：

```xml
<application
    android:extractNativeLibs="true"
    ... >
</application>
```

#### 默认的NDK版本

如果您下载了多个版本的NDK，则Android Gradle插件现在会选择一个默认版本来编译您的源代码文件。以前，该插件选择了NDK的最新下载版本。使用`android.ndkVersion`模块`build.gradle`文件中的 属性来覆盖插件选择的默认值。

#### 简化的R类生成

Android Gradle插件通过为项目中的每个库模块仅生成一个R类并与其他模块依赖项共享这些R类来简化编译类路径。此优化应该可以加快构建速度，但是需要牢记以下几点：

- 因为编译器与上游模块依赖项共享R类，所以项目中的每个模块都使用唯一的包名称非常重要。
- 库的R类对其他项目依赖项的可见性由用于将库包括为依赖项的配置确定。例如，如果库A将库B包含为“ api”依赖项，则库A和其他依赖库A的库都可以访问库B的R类。但是，如果库A使用`implementation`依赖项配置，则其他库可能无法访问库B的R类。要了解更多信息，请阅读有关[依赖项配置](https://developer.android.com/studio/build/dependencies#dependency_configurations)。

#### 删除默认配置中缺少的资源

对于库模块，如果包含的语言资源未包含在默认资源集中（例如，如果包含 `hello_world`为字符串资源，`/values-es/strings.xml`但未在其中定义该资源）`/values/strings.xml`，则Android Gradle插件在编译项目时，不再包含该资源。此行为更改应导致更少的`Resource Not Found`运行时异常并提高构建速度。

#### D8现在遵守CLASS注释保留策略

现在，在编译应用程序时，D8会考虑注释何时应用CLASS保留策略，并且这些注释在运行时不再可用。当将应用程序的目标SDK设置为API级别23时，也会出现此行为，该行为以前允许在运行时使用较旧版本的Android Gradle插件和D8编译应用程序时访问这些批注。

#### 其他行为改变

- `aaptOptions.noCompress` 不再在所有平台上都区分大小写（对于APK和bundle），并尊重使用大写字符的路径。
- 现在，默认情况下，数据绑定是增量的。要了解更多信息，请参阅 [问题＃110061530](https://issuetracker.google.com/110061530)。
- 现在，所有单元测试（包括Roboelectric单元测试）都可以完全缓存。要了解更多信息，请参阅 [问题＃115873047](https://issuetracker.google.com/115873047)。

### Bug修复

此版本的Android Gradle插件包含以下错误修复：

- 现在，使用数据绑定的库模块支持Robolectric单元测试。要了解更多信息，请参阅 [问题＃126775542](https://issuetracker.google.com/126775542)。
- 现在，`connectedAndroidTest`在启用Gradle的[并行执行模式](https://guides.gradle.org/performance/#parallel_execution)的[情况下，](https://guides.gradle.org/performance/#parallel_execution)您可以跨多个模块运行任务。

### 已知的问题

本节介绍了Android Gradle插件3.6.0中存在的已知问题。

#### Android Lint任务的性能降低

由于分析基础结构的回归，Android Lint可能需要更长的时间才能完成某些项目，从而导致在某些代码构造中对lambda的推断类型的计算速度较慢。

该问题被报告为[IDEA中的错误，](https://youtrack.jetbrains.com/issue/IDEA-229655) 并将在Android Gradle Plugin 4.0中修复。

#### 缺少舱单

如果您的应用在清单中定义了自定义权限，则Android Gradle插件通常会生成一个`Manifest.java`包含您的自定义权限作为字符串常量的类。该插件将此类与您的应用程序打包在一起，因此您可以在运行时更轻松地引用这些权限。

Android Gradle插件3.6.0中中断了生成清单类的过程。如果使用此版本的插件构建应用程序，并且该应用程序引用了清单类，则可能会看到`ClassNotFoundException`异常。要解决此问题，请执行以下任一操作：

- 通过其完全限定的名称引用您的自定义权限。例如， `"com.example.myapp.permission.DEADLY_ACTIVITY"`。

- 定义自己的常量，如下所示：

  ```java
  public final class CustomPermissions {
    public static final class permission {
      public static final String DEADLY_ACTIVITY="com.example.myapp.permission.DEADLY_ACTIVITY";
    }
  ```

## 3.5.0（2019年8月）

Android Gradle插件3.5.0和[Android Studio 3.5](https://developer.android.com/studio/releases#3-5-0)是一个主要版本，是Project Marble的结果，Project Marble致力于改善Android开发人员工具的三个主要方面：系统运行状况，功能改进和修复错误。值得注意的是，[提高项目构建速度](https://medium.com/androiddevelopers/improving-build-speed-in-android-studio-3e1425274837) 是此更新的主要重点。

有关这些更新和其他Project Marble更新的信息，请阅读[Android Developers博客文章](https://android-developers.googleblog.com/2019/05/android-studio-35-beta.html) 或以下部分。

此版本的Android插件需要满足以下条件：

- [摇篮5.4.1](https://docs.gradle.org/5.4.1/release-notes.html)。要了解更多信息，请阅读有关[更新Gradle](https://developer.android.com/studio/releases/gradle-plugin#updating-gradle)的部分。
- [SDK Build Tools 28.0.3](https://developer.android.com/studio/releases/build-tools#notes)或更高版本。

**3.5.4（2020年7月）**



此次更新支持与新的默认设置和[Android 11中软件包可见性的](https://developer.android.com/preview/privacy/package-visibility)功能兼容 。

有关详细信息，请参见[4.0.1发行说明](https://developer.android.com/studio/releases/gradle-plugin#4.0.1)。

**3.5.3（2019年12月）**

此次要更新支持Android Studio 3.5.3，并包括各种错误修复和性能改进。

**3.5.2（2019年11月）**

此次要更新支持Android Studio 3.5.2，并包括各种错误修复和性能改进。要查看重要的错误修复列表，请阅读[ Release Updates博客](https://androidstudio.googleblog.com/2019/11/android-studio-352-available.html)上的相关文章 。

**3.5.1（2019年10月）**

此次更新支持Android Studio 3.5.1，并包括各种错误修复和性能改进。要查看重要的错误修复列表，请阅读[ Release Updates博客](https://androidstudio.googleblog.com/2019/10/android-studio-351-available.html)上的相关文章 。

### 增量注释处理

该[数据绑定](https://developer.android.com/reference/android/databinding/package-summary)注释处理器支持[增量标注处理](https://docs.gradle.org/current/userguide/java_plugin.html#sec:incremental_annotation_processing) ，如果你设置`android.databinding.incremental=true` 你的`gradle.properties`文件。这种优化可以提高增量构建性能。有关优化注释处理器的完整列表，请参阅[增量注释处理器](https://docs.gradle.org/current/userguide/java_plugin.html#state_of_support_in_popular_annotation_processors)表。

此外，KAPT 1.3.30和更高版本还支持增量注释处理器，您可以通过将其包含`kapt.incremental.apt=true`在`gradle.properties`文件中来启用它们。

### 可缓存的单元测试

通过将设置[`includeAndroidResources`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.TestOptions.UnitTestOptions.html#com.android.build.gradle.internal.dsl.TestOptions.UnitTestOptions:includeAndroidResources) 为来启用单元测试以使用Android资源，资产和清单时`true`，Android Gradle插件会生成包含绝对路径的测试配置文件，这会破坏缓存的可重定位性。您可以指示插件改为使用相对路径生成测试配置，这可以`AndroidUnitTest`通过在`gradle.properties`文件中包含以下内容来使任务完全可缓存：

```
android.testConfig.useRelativePath = true
```

### 已知的问题

- 使用Kotlin Gradle插件1.3.31或更早版本时，在构建或同步项目时可能会看到以下警告：

  ```
  WARNING: API 'variant.getPackageLibrary()' is obsolete and has been replaced
           with 'variant.getPackageLibraryProvider()'.
  ```

  要解决[此问题](https://youtrack.jetbrains.com/issue/KT-30784)，请将插件升级到1.3.40或更高版本。

## 3.4.0（2019年4月）

此版本的Android插件需要满足以下条件：

- [Gradle 5.1.1](https://docs.gradle.org/5.1.1/release-notes.html)或更高版本。要了解更多信息，请阅读有关[更新Gradle](https://developer.android.com/studio/releases/gradle-plugin#updating-gradle)的部分。

  **注意：**使用Gradle 5.0和更高版本时，[默认的Gradle守护程序内存堆大小](https://docs.gradle.org/current/userguide/upgrading_version_4.html#rel5.0:default_memory_settings) 从1 GB减小到512 MB。这可能会导致构建性能下降。要覆盖此默认设置，请 在项目的文件中[指定Gradle守护程序堆大小](https://docs.gradle.org/current/userguide/build_environment.html#sec:configuring_jvm_memory)`gradle.properties`。

- [SDK Build Tools 28.0.3](https://developer.android.com/studio/releases/build-tools#notes)或更高版本。

**3.4.3（2020年7月）**



此次更新支持与新的默认设置和[Android 11中软件包可见性的](https://developer.android.com/preview/privacy/package-visibility)功能兼容 。

有关详细信息，请参见[4.0.1发行说明](https://developer.android.com/studio/releases/gradle-plugin#4.0.1)。

**3.4.2（2019年7月）**

此次要更新支持Android Studio 3.4.2，并包括各种错误修复和性能改进。要查看重要的错误修复列表，请阅读[ Release Updates博客](https://androidstudio.googleblog.com/2019/07/android-studio-342-available.html)上的相关文章 。

**3.4.1（2019年5月）**

此次更新支持Android Studio 3.4.1，并包括各种错误修复和性能改进。要查看重要的错误修复列表，请阅读[ Release Updates博客](https://androidstudio.googleblog.com/2019/05/android-studio-341-available.html)上的相关文章 。

### 新功能

- **新的棉绒检查依赖项配置：**的行为`lintChecks`已更改`lintPublish`，并且引入了新的依赖项配置，使您可以更好地控制将哪些棉绒检查打包在Android库中。

  - `lintChecks`：这是一个现有配置，您应该将其用于只在本地构建项目时才运行的lint检查。如果您以前使用`lintChecks`依赖项配置在已发布的AAR中包括了lint检查，则需要迁移这些依赖项以改为使用`lintPublish`下面描述的新配置。
  - `lintPublish`：如下所示，在库项目中使用此新配置进行要包含在已发布的AAR中的棉绒检查。这意味着占用您的库的项目也会应用这些皮棉检查。

  以下代码示例在本地Android库项目中同时使用了两种依赖项配置。

  ```groovy
  dependencies {
    // Executes lint checks from the ':lint' project at build time.
    lintChecks project(':lint')
    // Packages lint checks from the ':lintpublish' in the published AAR.
    lintPublish project(':lintpublish')
  }
  ```

- 通常，打包和签名任务应使整体构建速度有所提高。如果您发现与这些任务有关的性能下降，请[报告错误](https://developer.android.com/studio/report-bugs)。

### 行为改变

- **Android Instant Apps功能插件已弃用警告：**如果您仍在使用该`com.android.feature`插件来构建即时应用，则Android Gradle插件3.4.0会向您抛出弃用警告。为了确保您仍可以在该插件的未来版本上构建即时应用程序，请将您的即时应用程序迁移到使用 [动态功能插件](https://developer.android.com/studio/projects/dynamic-delivery)，它还允许您从单个Android应用程序包发布已安装和即时应用程序的体验。

- **默认情况下启用R8：** R8一步就集成了除糖，缩小，模糊，优化和脱色功能- [显着提高了构建性能](https://www.google.com/url?q=https://android-developers.googleblog.com/2018/11/r8-new-code-shrinker-from-google-is.html&sa=D&ust=1551922493258000&usg=AFQjCNH0N1wuMX645n7giw0wjikzjm3WCA)。R8是在Android Gradle插件3.3.0中引入的，现在默认情况下使用插件3.4.0及更高版本对应用程序和Android库项目都启用了R8。

  下图简要介绍了R8引入之前的编译过程。

  ![在R8之前，ProGuard是与Dexing和Deugaring不同的编译步骤。](https://developer.android.com/studio/images/build/r8/compile_with_d8_proguard.png)

  现在，使用R8，消糖，收缩，模糊，优化和变形（D8）都可以一步完成，如下所示。

  ![使用R8，可以在单个编译步骤中执行除糖，缩小，模糊，优化和解密。](https://developer.android.com/studio/images/build/r8/compile_with_r8.png)

  请记住，R8旨在与您现有的ProGuard规则配合使用，因此您可能无需采取任何措施即可从R8中受益。但是，由于ProGuard是专为Android项目设计的与ProGuard不同的技术，因此缩小和优化可能会删除ProGuard可能没有的代码。因此，在这种不太可能的情况下，您可能需要添加其他规则以将该代码保留在构建输出中。

  如果您在使用R8时遇到问题，请阅读 [R8兼容性常见问题解答，](https://r8.googlesource.com/r8/+/refs/heads/master/compatibility-faq.md) 以检查是否有解决问题的方法。如果未记录解决方案，请[报告错误](https://issuetracker.google.com/issues/new?component=326788&template=1025938)。您可以通过在项目`gradle.properties`文件中添加以下行之一来禁用R8 ：

  ```
  # Disables R8 for Android Library modules only.
  android.enableR8.libraries = false
  # Disables R8 for all modules.
  android.enableR8 = false
  ```

  **注意：**对于给定的构建类型，如果您在应用模块的文件中设置`useProguard`为，则无论您是否在项目文件中禁用R8，Android Gradle插件都会使用R8缩小该构建类型的应用代码。`false``build.gradle``gradle.properties`

- **`ndkCompile`不建议使用：**现在，如果您尝试使用它`ndkBuild`来编译本机库，则会出现构建错误 。您应该改用CMake或ndk-build将 [C和C ++代码添加到项目中](https://developer.android.com/studio/projects/add-native-code)。

### 已知的问题

- 当前未强制正确使用唯一的软件包名称，但在更高版本的插件上将变得更加严格。在Android Gradle插件版本3.4.0上，您可以通过在`gradle.properties` 文件中添加以下行来选择检查项目是否声明了可接受的包名称。

  ```
  android.uniquePackageNames = true
  ```

  要了解有关通过Android Gradle插件设置软件包名称的更多信息，请参阅[设置应用程序ID](https://developer.android.com/studio/build/application-id)。

## 3.3.0（2019年1月）

此版本的Android插件需要满足以下条件：

- [Gradle 4.10.1](https://docs.gradle.org/4.10.1/release-notes.html)或更高版本。要了解更多信息，请阅读有关[更新Gradle](https://developer.android.com/studio/releases/gradle-plugin#updating-gradle)的部分。

  **注意：**使用Gradle 5.0和更高版本时，[默认的Gradle守护程序内存堆大小](https://docs.gradle.org/current/userguide/upgrading_version_4.html#rel5.0:default_memory_settings) 从1 GB减小到512 MB。这可能会导致构建性能下降。要覆盖此默认设置，请 在项目的文件中[指定Gradle守护程序堆大小](https://docs.gradle.org/current/userguide/build_environment.html#sec:configuring_jvm_memory)`gradle.properties`。

- [SDK Build Tools 28.0.3](https://developer.android.com/studio/releases/build-tools#notes)或更高版本。

**3.3.3（2020年7月）**



此次更新支持与新的默认设置和[Android 11中软件包可见性的](https://developer.android.com/preview/privacy/package-visibility)功能兼容 。

有关详细信息，请参见[4.0.1发行说明](https://developer.android.com/studio/releases/gradle-plugin#4.0.1)。

**3.3.2（2019年3月）**

此次要更新支持Android Studio 3.3.2，并包括各种错误修复和性能改进。要查看重要的错误修复列表，请阅读[ Release Updates博客](https://androidstudio.googleblog.com/2019/03/android-studio-332-available.html)上的相关文章 。

**3.3.1（2019年2月）**

此次要更新支持Android Studio 3.3.1，并包括各种错误修复和性能改进。

### 新功能

- **改进的类路径同步：**解决运行时的依赖关系并编译时的类路径时，Android Gradle插件会尝试修复某些跨多个类路径的依赖项的某些下游版本冲突。

  例如，如果运行时类路径包括Library A版本2.0，而编译类路径包括Library A版本1.0，则插件会自动将对编译类路径的依赖关系更新为Library A版本2.0，以避免发生错误。

  但是，如果运行时类路径包含库A版本1.0，而编译库包含库A版本2.0，则该插件不会将对编译类路径的依赖关系降级为库A版本1.0，因此会出现错误。要了解更多信息，请参见 [修复类路径之间的冲突](https://developer.android.com/studio/build/dependencies#classpath_conflicts)。

- **使用注释处理器时改进了增量Java编译：** 此更新通过改进对使用注释处理器时对增量Java编译的支持，减少了构建时间。

  **注意：**此功能与Gradle 4.10.1及更高版本兼容，但由于[Gradle问题8194](https://github.com/gradle/gradle/issues/8194)导致Gradle 5.1除外。

  - **对于使用Kapt的项目（大多数仅限Kotlin的项目和Kotlin-Java混合项目）：**即使使用数据绑定或retro-lambda插件，也会启用增量Java编译。Kapt任务的注释处理尚未增量。

  - **对于不使用Kapt（纯Java的项目）的项目：**如果您使用所有支持注解处理器 [增量注释处理](https://docs.gradle.org/4.10.1/userguide/java_plugin.html#sec:incremental_annotation_processing)，增量Java编译默认情况下启用。要监视增量注释处理器的采用，请观看 [Gradle问题5277](https://github.com/gradle/gradle/issues/5277)。

    但是，如果一个或多个注释处理器不支持增量构建，则不会启用增量Java编译。相反，您可以在`gradle.properties`文件中包含以下标志：

    ```
    android.enableSeparateAnnotationProcessing=true
    ```

    当包含此标志时，Android Gradle插件将在单独的任务中执行注释处理器，并允许Java编译任务以增量方式运行。

- **使用过时的API时可以提供更好的调试信息：**当插件检测到您正在使用不再受支持的API时，它现在可以提供更详细的信息来帮助您确定该API的使用位置。要查看其他信息，您需要在项目`gradle.properties`文件中包括以下内容：

  ```
  android.debug.obsoleteApi=true
  ```

  您还可以通过`-Pandroid.debug.obsoleteApi=true` 从命令行传递来启用该标志。

- 您可以从命令行在动态功能模块上运行检测测试。

### 行为改变

- **惰性任务配置：**插件现在使用 [Gradle的新任务创建API](https://docs.gradle.org/current/userguide/task_configuration_avoidance.html) 来避免初始化和配置完成当前构建不需要的任务（或不在执行任务图上的任务）。例如，如果您有多个构建变体，例如“ release”和“ debug”构建变体，而您正在构建应用程序的“ debug”版本，则该插件可以避免初始化和配置“ release”版本的任务。您的应用。

  在Variants API中调用某些较旧的方法（例如 `variant.getJavaCompile()`）可能仍会强制执行任务配置。为确保您的构建针对延迟任务配置进行了优化，请调用新方法以返回 `TaskProvider` 对象，例如`variant.getJavaCompileProvider()`。

  如果您执行自定义构建任务，请学习如何 [适应Gradle的新任务创建API](https://docs.gradle.org/current/userguide/task_configuration_avoidance.html#sec:old_vs_new_configuration_api_overview)。

- 对于给定的构建类型，在设置时`useProguard false`，插件现在使用R8而不是ProGuard来缩小和模糊应用程序的代码和资源。要了解有关R8的更多信息，请阅读 Android开发者博客中的[这篇博客文章](https://android-developers.googleblog.com/2018/11/r8-new-code-shrinker-from-google-is.html)。

- **为图书馆项目更快地生成R类：**以前，Android Gradle插件将为`R.java`项目的每个依赖项生成一个文件，然后将这些R类与应用程序的其他类一起编译。现在，该插件会直接生成一个JAR，其中包含应用程序的已编译R类，而无需首先构建中间`R.java`类。此优化可以显着提高包含许多库子项目和依赖项的项目的构建性能，并提高Android Studio中的索引编制速度。

- 在构建[Android应用程序捆绑包时](https://developer.android.com/guide/app-bundle)，默认情况下，从该应用程序捆绑包生成的，面向Android 6.0（API级别23）或更高版本的APK现在包括本机库的未压缩版本。这种优化避免了设备制作库副本的需要，从而减小了应用程序的磁盘大小。如果您想禁用此优化，请在`gradle.properties`文件中添加以下内容：

  ```
  android.bundle.enableUncompressedNativeLibs = false
  ```

- 该插件会强制执行某些第三方插件的最低版本。

- **单变量项目同步**：使 [项目](https://developer.android.com/studio/build#sync-files) 与构建配置[同步](https://developer.android.com/studio/build#sync-files)是让Android Studio了解项目结构的重要一步。但是，此过程对于大型项目可能很耗时。如果您的项目使用多个构建变体，则现在可以通过将项目同步限制为仅当前选择的变体来优化项目同步。

  您需要将Android Studio 3.3或更高版本与Android Gradle Plugin 3.3.0或更高版本配合使用才能启用此优化。当满足这些要求时，IDE会在同步项目时提示您启用此优化。默认情况下，还会在新项目上启用优化。

  要手动启用此优化，请点击**文件>设置>实验** **> Gradle**（在Mac上为**Android Studio>首选项>实验> Gradle**），然后选中**仅同步活动的变体**复选框。

  **注意**：此优化完全支持包括Java和C ++语言的项目，并且对Kotlin有所支持。为具有Kotlin内容的项目启用优化时，Gradle同步会退回到内部使用完整变体的方式。

- **自动下载缺少的SDK软件包**：此功能已扩展为支持NDK。要了解更多信息，请阅读 [使用Gradle自动下载缺少的软件包](https://developer.android.com/studio/intro/update#download-with-gradle)。

### Bug修复

- Android Gradle插件3.3.0修复了以下问题：
  - `android.support.v8.renderscript.RenderScript` 尽管启用了Jetifier，但构建过程将调用而不是AndroidX版本
  - 由于`androidx-rs.jar`包含静态捆绑 而引起的冲突`annotation.AnyRes`
  - 使用RenderScript时，您不再需要在`build.gradle`文件中手动设置Build Tools版本

## 3.2.0（2018年9月）

此版本的Android插件需要满足以下条件：

- [Gradle 4.6](https://docs.gradle.org/4.6/release-notes.html)或更高。要了解更多信息，请阅读有关[更新Gradle](https://developer.android.com/studio/releases/gradle-plugin#updating-gradle)的部分 。
- [SDK Build Tools 28.0.3](https://developer.android.com/studio/releases/build-tools#notes)或更高版本。

**3.2.1（2018年10月）**

使用此更新，您不再需要为SDK生成工具指定版本。Android Gradle插件现在默认使用28.0.3版本。

### 新功能

- **支持构建Android应用程序捆绑包：**应用程序捆绑包是一种新的上传格式，其中包括您应用程序的所有已编译代码和资源，同时推迟了APK的生成并登录到Google Play商店。您不再需要构建，签名和管理多个APK，并且用户可以获得针对其设备进行了优化的较小下载量。要了解更多信息，请阅读 [关于Android应用程序捆绑包](https://developer.android.com/guide/app-bundle)。

- **使用注解处理器时提高增量编译速度支持：** 在[`AnnotationProcessorOptions`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.AnnotationProcessorOptions.html) DSL现在扩展[`CommandLineArgumentProvider`](https://docs.gradle.org/current/javadoc/org/gradle/process/CommandLineArgumentProvider.html)，使您或注解处理器笔者注释参数为使用处理器 [增量生成属性类型注释](https://docs.gradle.org/current/userguide/more_about_tasks.html#sec:up_to_date_checks)。使用这些注释可以提高增量和缓存的干净构建的正确性和性能。要了解更多信息，请阅读将 [参数传递给注释处理器](https://developer.android.com/studio/build/dependencies#processor-arguments)。

- **适用于AndroidX的迁移工具：**在Android 3.2和更高版本中使用Android Gradle插件3.2.0时，可以通过从菜单栏中选择“ **重构”>“迁移到AndroidX”**，来迁移项目的本地和Maven依赖项以使用新的AndroidX库 。使用此迁移工具还将`true`在`gradle.properties`文件中设置以下标志：

  - **`android.useAndroidX`：**设置`true`为时，Android插件将使用适当的AndroidX库而不是支持库。如果未指定此标志，则插件`false`默认将其设置为。
  - **`android.enableJetifier`：**设置`true`为时，Android插件会通过重写二进制文件来自动迁移现有的第三方库以使用AndroidX。如果未指定此标志，则插件`false`默认将其设置为。您可以将此标志设置为`true`仅在，同时 `android.useAndroidX`还将设置为`true`，否则会出现构建错误。

  要了解更多信息，请阅读[AndroidX概述](https://developer.android.com/topic/libraries/support-library/androidx-overview)。

- **新的代码收缩器R8：** R8是替代ProGuard的用于代码收缩和混淆的新工具。您可以通过在项目的`gradle.properties`文件中包含以下内容来开始使用R8的预览版：

  ```groovy
  android.enableR8 = true
  ```

### 行为改变

- D8的脱糖功能现在默认启用。

- AAPT2现在在Google的Maven回购中。要使用AAPT2，请确保文件中具有 `google()`依赖项`build.gradle`，如下所示：

  ```groovy
  buildscript {
        repositories {
            google() // here
            jcenter()
        }
        dependencies {
            classpath 'com.android.tools.build:gradle:3.2.0'
        }
    }
    allprojects {
        repositories {
            google() // and here
            jcenter()
    }
  ```

- 现在默认启用本机multidex。将应用程序的调试版本部署到运行Android API级别21或更高版本的设备时，早期版本的Android Studio会启用本机multidex。现在，无论您是要部署到设备上还是构建要发布的APK，Android Gradle插件均可为所有已设置`minSdkVersion=21`或更高版本的模块启用本机multidex 。

- 现在，该插件将强制执行protobuf插件（0.8.6），Kotlin插件（1.2.50）和Crashlytics插件（1.25.4）的最低版本。

- `com.android.feature`指定模块名称时，功能模块插件现已强制仅使用字母，数字和下划线。例如，如果功能模块名称包含破折号，则会出现构建错误。此行为与动态功能模块插件的行为匹配。

### Bug修复

- JavaCompile现在可以在具有数据绑定的项目中缓存。（[问题＃69243050](https://issuetracker.google.com/69243050)）
- 对于具有数据绑定的库模块，可以更好地避免编译。（[问题＃77539932](https://issuetracker.google.com/77539932)）
- 如果由于某些不可预测的构建错误而在较早版本中将其禁用，则现在可以重新启用 [按需配置](https://docs.gradle.org/current/userguide/multi_project_builds.html#sec:configuration_on_demand)。（[问题＃77910727](https://issuetracker.google.com/77910727)）

## 3.1.0（2018年3月）

此版本的Android插件需要满足以下条件：

- [Gradle 4.4](https://docs.gradle.org/current/release-notes.html)或更高版本。要了解更多信息，请阅读有关[更新Gradle](https://developer.android.com/studio/releases/gradle-plugin#updating-gradle)的部分 。
- [构建工具27.0.3](https://developer.android.com/studio/releases/build-tools#notes)或更高版本。请记住，您不再需要使用`android.buildToolsVersion`属性为构建工具指定版本-插件默认使用最低要求版本。

### 新的DEX编译器D8

默认情况下，Android Studio现在使用名为D8的新DEX编译器。DEX编译是将`.class` 字节码转换`.dex`为适用于Android运行时（或Dalvik，适用于旧版Android）的字节码的过程。与以前的DX编译器相比，D8编译速度更快，输出的DEX文件更小，同时具有相同或更好的应用程序运行时性能。

D8不应更改您日常的应用程序开发工作流程。但是，如果遇到与新编译器有关的任何问题，请 [报告错误](https://developer.android.com/studio/report-bugs)。您可以通过在项目`gradle.properties`文件中包含以下内容来暂时禁用D8并使用DX ：

```
android.enableD8=false
```

对于[使用Java 8语言功能的](https://developer.android.com/studio/write/java8-support)项目， 默认情况下启用增量删除。您可以通过在项目`gradle.properties`文件中指定以下内容来禁用它：

```
android.enableIncrementalDesugaring=false.
```

**预览用户：**如果您已经在使用D8的预览版，请注意，它现在可以根据[SDK生成工具（](https://developer.android.com/studio/releases/build-tools)而非JDK）中包含的库进行编译 。因此，如果您访问的是JDK中存在的API，而不是SDK生成工具库中存在的API，则会出现编译错误。

### 行为改变

- 当[建立多个APK](https://developer.android.com/studio/build/configure-apk-splits)每个目标不同的ABI，插件不再生成的APK用于通过缺省以下的ABI： ，`mips`，`mips64`和`armeabi`。

  如果要构建针对这些ABI的APK，则必须使用 [NDK r16b或更低版本，](https://developer.android.com/ndk/downloads/revision_history)并在`build.gradle`文件中指定ABI ，如下所示：

  ```groovy
  拆分{
    abi {
        包括'armeabi' ，'mips' ，'mips64'  
        ...
    }
  }
  ```

- 当[构建配置的APK](https://developer.android.com/topic/instant-apps/guides/config-splits) 为Android的即时应用，语言配置分裂正在由默认的根语言分组。例如，如果您的应用程序包含用于`zh-TW`或`zh-CN`语言环境的资源，则Gradle会将这些资源打包为一种`zh`语言配置拆分。您可以通过使用`include`属性定义自己的组来覆盖此行为，如下所示：

  ```groovy
  splits {
      language {
          enable true
          // Each string defines a group of locales that
          // Gradle should package together.
          include "in,id",
                  "iw,he",
                  "fil,tl,tgl",
                  "yue,zh,zh-TW,zh-CN"
      }
  }
  ```

- 现在，Android插件的[构建缓存会](https://developer.android.com/studio/build/build-cache)逐出超过30天的缓存条目。

- 传递`"auto"`到 [`resConfig`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.ProductFlavor.html#com.android.build.gradle.internal.dsl.ProductFlavor:resConfig(java.lang.String)) 不再自动选择字符串资源以打包到您的APK中。如果您继续使用`"auto"`，该插件会打包您的应用及其依赖项提供的所有字符串资源。因此，您应该指定您希望插件打包到APK中的每个区域设置。

- 由于本地模块不能依赖于您应用程序的测试APK，因此使用`androidTestApi` 配置（而不是）将依赖项添加到您的检测测试中`androidTestImplementation`会导致Gradle发出以下警告：

  ```groovy
    WARNING: Configuration 'androidTestApi' is obsolete
    and has been replaced with 'androidTestImplementation'
  ```

### 修正

- 修复了Android Studio无法正确识别复合体版本中的依赖项的问题。
- 修复了在单个构建中多次加载Android插件时（例如，当多个子项目各自在其buildscript类路径中包含Android插件时）出现项目同步错误的问题。

## 3.0.0（2017年10月）

Android Gradle插件3.0.0包含多种更改，旨在解决大型项目的性能问题。

例如，在 具有约130个模块和大量外部依赖项（但没有代码或资源）的 [示例框架项目中](https://github.com/jmslau/perf-android-large.git)，您可以体验到与以下类似的性能改进：

| Android插件版本+ Gradle版本        | Android插件2.2.0 + Gradle 2.14.1 | Android插件2.3.0 + Gradle 3.3 | Android插件3.0.0 + Gradle 4.1 |
| :--------------------------------- | :------------------------------- | :---------------------------- | :---------------------------- |
| 配置（例如运行）`./gradlew --help` | 〜2分钟                          | 约9秒                         | 〜2.5秒                       |
| 1行Java更改（实现更改）            | 〜2分钟15 s                      | 〜29秒                        | 约6.4秒                       |

其中一些更改会破坏现有版本。因此，在使用新插件之前，您应该考虑迁移项目的工作。

如果您没有体验到上述的性能改进，请 [提交一个错误，](https://issuetracker.google.com/issues/new?component=192708&template=840533) 并使用[Gradle Profiler](https://github.com/gradle/gradle-profiler)跟踪您的构建 。

此版本的Android插件需要满足以下条件：

- [Gradle 4.1](https://docs.gradle.org/current/release-notes.html)或更高版本。要了解更多信息，请阅读有关[更新Gradle](https://developer.android.com/studio/releases/gradle-plugin#updating-gradle)的部分 。
- [构建工具26.0.2](https://developer.android.com/studio/releases/build-tools#notes)或更高版本。使用此更新，您不再需要为构建工具指定版本-插件默认使用最低要求的版本。因此，您现在可以删除该`android.buildToolsVersion`属性。

**3.0.1（2017年11月）**

这是一个次要更新，以支持Android Studio 3.0.1，并包括常规的错误修复和性能改进。

### 最佳化

- 通过细粒度的任务图为多模块项目提供更好的并行性。
- 在对依赖项进行更改时，Gradle通过不重新编译无法访问该依赖项的API的模块来执行更快的构建。您应该限制其依赖通过泄露其API给其他模块 [使用摇篮的新的相关配置](https://developer.android.com/studio/build/dependencies#dependency_configurations)： `implementation`，`api`，`compileOnly`，和`runtimeOnly`。
- 由于每个类的分解，增量构建速度更快。现在，每个类都被编译到单独的DEX文件中，并且仅对修改后的类进行重新排序。您还应该期望将设置`minSdkVersion`为20或更低并使用[旧版multi-dex的](https://developer.android.com/studio/build/multidex#mdex-pre-l)应用程序的构建速度提高。
- 通过优化某些任务以使用chached输出，提高了构建速度。要从此优化中受益，您需要首先 [启用Gradle构建缓存](https://docs.gradle.org/current/userguide/build_cache.html#sec:build_cache_enable)。
- 使用AAPT2改进了增量资源处理，默认情况下已启用。如果您在使用AAPT2时遇到问题，请 [报告错误](https://developer.android.com/studio/report-bugs)。您还可以通过`android.enableAapt2=false`在`gradle.properties`文件中进行设置并通过`./gradlew --stop`从命令行运行来重新启动Gradle守护程序来禁用AAPT2 。

### 新功能

- [变体感知依赖管理](https://developer.android.com/studio/build/dependencies#variant_aware)。现在，在构建模块的特定变体时，插件会自动将本地库模块依赖项的变体与要构建的模块的变体匹配。

- 包括一个新的功能模块插件，以支持 [Android Instant Apps](https://developer.android.com/topic/instant-apps)和Android Instant Apps SDK（可以[使用SDK管理器](https://developer.android.com/studio/intro/update#sdk-manager)下载 ）。要了解有关使用新插件创建功能模块的更多信息，请阅读 [具有多个功能的即时应用的结构](https://developer.android.com/topic/instant-apps/getting-started/structure#structure_of_an_instant_app_with_multiple_features)。

- 对使用某些Java 8语言功能和Java 8库的内置支持。 **现在已弃用Jack，不再需要它**，您应该首先禁用Jack以使用默认工具链中内置的改进的Java 8支持。有关更多信息，请阅读[使用Java 8语言功能](https://developer.android.com/studio/write/java8-support)。

- 添加了对使用

  Android Test Orchestrator

  运行测试的支持 ，该功能使您可以在自己的调用中运行每个应用程序的测试

  ```
  Instrumentation
  ```

  。由于每个测试都在其自己的

  ```
  Instrumentation
  ```

  实例中运行，因此测试之间的任何共享状态都不会累积在设备的CPU或内存上。而且，即使一个测试崩溃了，它也只会删除其自己的实例 

  ```
  Instrumentation
  ```

  ，因此您的其他测试仍然可以运行。

  - 已添加`testOptions.execution`以确定是否使用设备上的测试流程。如果要 [使用Android Test Orchestrator](https://developer.android.com/training/testing/junit-runner#using-android-test-orchestrator)，则需要指定`ANDROID_TEST_ORCHESTRATOR`，如下所示。默认情况下，此属性设置为`HOST`，这将禁用设备编排，并且是运行测试的标准方法。

```groovy
android {
  testOptions {
    执行“ ANDROID_TEST_ORCHESTRATOR”
  }
}
```

- 新的`androidTestUtil`依赖项配置允许您在运行检测测试之前安装另一个测试助手APK，例如Android Test Orchestrator：

```groovy
依赖项{
  androidTestUtil'com.android.support.test ：orchestrator：1.0.0'
  ...
}
```

- 已添加

  ```
  testOptions.unitTests.includeAndroidResources
  ```

  以支持需要Android资源的单元测试，例如

  Roboelectric

  。当您将此属性设置为时

  ```
  true
  ```

  ，插件将在运行单元测试之前执行资源，资产和清单合并。然后，您的测试可以

  ```
  com/android/tools/test_config.properties
  ```

  在类路径上检查以下键：

  - ```
    android_merged_assets
    ```

    ：合并资产目录的绝对路径。

    **注意：**对于库模块，合并的资产不包含依赖项的资产（请参阅[问题＃65550419](https://issuetracker.google.com/65550419)）。

  - `android_merged_manifest`：合并清单文件的绝对路径。

  - `android_merged_resources`：合并资源目录的绝对路径，该目录包含模块中的所有资源及其所有依赖项。

  - `android_custom_package`：最终R类的包名称。如果您动态修改应用程序ID，则此程序包名称可能与`package`应用程序清单中的属性不匹配。

- 支持[字体作为资源](https://developer.android.com/guide/topics/ui/look-and-feel/fonts-in-xml) （这是[Android 8.0（API级别26）中](https://developer.android.com/about/versions/oreo)引入的新功能）。

- [Android Instant Apps SDK 1.1](https://developer.android.com/topic/instant-apps/release-notes#android_instant_apps_development_sdk_v110) 及更高版本支持特定于语言的APK 。有关更多信息，请参阅 [为纯拆分配置构建](https://developer.android.com/topic/instant-apps/guides/config-splits)。

- 现在，您可以更改外部本机生成项目的输出目录，如下所示：

```groovy
android {
    ...
    externalNativeBuild {
        //对于ndk-build，请改用ndkBuild块。
        cmake {
            ...
            //指定外部本机输出的相对路径
            //构建。您可以指定不是子目录的任何路径
            //项目临时构建目录的//。
            buildStagingDirectory “ ./outputs/cmake”
        }
    }
}
```

- 现在， 从Android Studio构建本机项目时，可以[使用CMake 3.7或更高](https://developer.android.com/studio/projects/install-ndk#vanilla_cmake)版本。
- 新的`lintChecks`依赖项配置允许您构建定义自定义棉绒规则的JAR，并将其打包到AAR和APK项目中。您的自定义棉绒规则必须属于一个单独的项目，该项目输出一个JAR，并且仅包含 [`compileOnly`](https://docs.gradle.org/current/userguide/java_plugin.html#sec:java_plugin_and_dependency_management) 依赖项。然后，其他应用程序和库模块可以使用以下`lintChecks`配置依赖于您的lint项目：

```groovy
依赖项{
    //这告诉Gradle插件将'：lint-checks'构建到lint.jar文件中
    //并将其与您的模块打包。如果模块是Android库，
    //其他依赖它的项目会自动使用lint检查。
    //如果模块是应用程序，则分析应用程序时，lint会包含以下规则。
    lintChecks项目（'：lint-checks' ）
}
```

### 行为改变

- Android插件3.0.0删除了某些API，如果使用它们，构建会中断。例如，您不能再使用Variants API来访问 `outputFile()`对象或用于`processManifest.manifestOutputFile()`获取每个变量的清单文件。要了解更多信息，请阅读 [API更改](https://developer.android.com/studio/known-issues#variant_api)。
- 您不再需要为构建工具指定版本（因此，您现在可以删除该`android.buildToolsVersion`属性）。默认情况下，该插件会自动使用您所使用的Android插件版本所需的最低构建工具版本。
- 现在，您可以在`buildTypes`块中启用/禁用PNG压缩，如下所示。默认情况下，除调试版本外，所有版本均启用PNG压缩，因为它会增加包含许多PNG文件的项目的生成时间。因此，要缩短其他构建类型的构建时间，应禁用PNG压缩或 [将图像转换为WebP](https://developer.android.com/studio/write/convert-webp#convert_images_to_webp)。

```groovy
android {
  buildTypes {
    发布{
      //禁用发布版本类型的PNG处理。
      crunchPngs 错误
    }
  }
}
```

- 现在，Android插件会自动构建您在外部CMake项目中配置的可执行目标。
- 现在，您必须 使用依赖项配置[将注释处理器添加](https://developer.android.com/studio/build/dependencies#annotation_processor)到处理器类路径`annotationProcessor`。
- `ndkCompile`现在不建议使用已弃用的软件。相反，您应该迁移到使用CMake或ndk-build来编译要打包到APK中的本机代码。要了解更多信息，请阅读 [从ndkcompile迁移](https://developer.android.com/studio/projects/add-native-code#ndkCompile)。

## 2.3.0（2017年2月）

**2.3.3（2017年6月）**

这是一个次要更新，增加了与[Android Studio 2.3.3的](https://developer.android.com/studio/releases#Revisions)兼容性 。

**2.3.2（2017年5月）**

这是一个次要更新，增加了与[Android Studio 2.3.2的](https://developer.android.com/studio/releases#Revisions)兼容性 。

**2.3.1（2017年4月）**

这是对Android插件2.3.0的次要更新，修正了一些物理Android设备无法在[ Instant Run上](https://developer.android.com/studio/run#instant-run)正常[运行的问题](https://developer.android.com/studio/run#instant-run)（请参见[ Issue＃235879](https://code.google.com/p/android/issues/detail?id=235879)）。

- 依存关系：

  Gradle 3.3或更高版本。[构建工具25.0.0](https://developer.android.com/tools/revisions/build-tools) 或更高版本。

- 新：

  使用Gradle 3.3，其中包括性能改进和新功能。有关更多详细信息，请参见[Gradle发行说明](https://docs.gradle.org/3.3/release-notes)。**构建缓存**：存储构建项目时Android插件生成的某些输出（例如未打包的AAR和预先定义的远程依赖项）。使用缓存时，您的干净构建速度要快得多，因为构建系统可以在后续构建过程中简单地重用那些缓存的文件，而不用重新创建它们。使用Android插件2.3.0及更高版本的项目默认情况下使用构建缓存。要了解更多信息，请阅读“ [使用构建缓存提高构建速度”](https://developer.android.com/studio/build/build-cache)。包括[清除构建缓存](https://developer.android.com/studio/build/build-cache#clear_the_build_cache)的`cleanBuildCache`任务。如果您正在使用实验版本的构建缓存（包含在该插件的早期版本中），则应[将您的插件更新](https://developer.android.com/studio/releases/gradle-plugin#updating-plugin)为最新版本。

- 变化：

  支持对[Android Studio 2.3中](https://developer.android.com/studio/releases)包含的Instant Run的更改。大型项目的配置时间应该明显更快。修复了[约束布局库](https://developer.android.com/training/constraint-layout)自动下载的问题。插件现在使用[ProGuard版本5.3.2](https://www.guardsquare.com/en/proguard/manual/versions)。包括许多已[ 报告错误的](https://code.google.com/p/android/issues/list?can=1&q=Component%3DTools++Subcomponent%3DTools-gradle%2CTools-build%2CTools-instantrun%2CTools-cpp-build+Target%3D2.3+status%3AFutureRelease%2CReleased+&sort=priority+-status&colspec=ID+Status+Priority+Owner+Summary+Stars+Reporter+Opened&cells=tiles)修复程序。遇到问题时，请继续[提交错误报告](https://developer.android.com/studio/report-bugs)。

## 2.2.0（2016年9月）

- 依存关系：

  Gradle 2.14.1或更高版本。[构建工具23.0.2](https://developer.android.com/tools/revisions/build-tools) 或更高版本。

- 新：

  使用Gradle 2.14.1，其中包括性能改进和新功能，并修复了一个安全漏洞，该漏洞可在使用Gradle守护程序时允许本地特权升级。有关更多详细信息，请参见[ Gradle发行说明](https://docs.gradle.org/2.14.1/release-notes)。使用DSL，Gradle现在可让您链接到本机源，并使用CMake或ndk-build编译本机库。构建本机库后，Gradle将它们打包到您的APK中。要了解有关将CMake和ndk-build与Gradle结合使用的更多信息，请阅读[向项目添加C和C ++代码](https://developer.android.com/studio/projects/add-native-code)。 [`externalNativeBuild {}`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.ExternalNativeBuild.html)当您[从命令行运行构建时](https://developer.android.com/studio/build/building-cmdline)，Gradle现在尝试自动下载项目依赖的所有缺少的SDK组件或更新。要了解更多信息，请阅读[使用Gradle自动下载缺少的软件包](https://developer.android.com/studio/intro/update#download-with-gradle)。一项新的实验性缓存功能使Gradle通过预删除，存储和重新使用库的预删除版本来加快构建时间。要了解有关使用此实验功能的更多信息，请阅读[Build Cache](https://developer.android.com/studio/build/build-cache)指南。通过采用新的默认打包管道来提高构建性能，该默认打包管道可在一项任务中处理[zip](https://developer.android.com/studio/command-line/zipalign)，签名和[zipaligning](https://developer.android.com/studio/command-line/zipalign)。您可以通过添加`android.useOldPackaging=true`到 `gradle.properties`文件中恢复使用较旧的打包工具 。使用新的打包工具时，该`zipalignDebug`任务不可用。但是，您可以通过调用`createZipAlignTask(String taskName, File inputFile, File outputFile)`方法自己创建一个 。现在，除了传统的JAR签名外，APK签名还使用[APK签名方案v2](https://developer.android.com/about/versions/nougat/android-7.0#apk_signature_v2)。所有Android平台均接受生成的APK。签名后对这些APK进行的任何修改都会使其v2签名无效，并阻止在设备上安装。要禁用此功能，请将以下内容添加到模块级`build.gradle`文件中：`android { ... signingConfigs {  配置{   ...   v2SigningEnabled false  } }}`对于multidex构建，您现在可以使用ProGuard规则来确定Gradle应将哪些类编译到应用程序的*主* DEX文件中。因为Android系统在启动应用程序时会首先加载主DEX文件，所以您可以在启动时通过将某些类编译为主DEX文件来对它们进行优先级排序。在专门为您的主DEX文件创建ProGuard配置文件后，请使用将配置文件的路径传递到Gradle `buildTypes.multiDexKeepProguard`。使用此DSL与使用DSL不同，后者使用DSL 为您的应用程序提供常规的ProGuard规则，而不为主DEX文件指定类。 [`buildTypes.proguardFiles`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.BuildType.html#com.android.build.gradle.internal.dsl.BuildType:proguardFiles(java.lang.Object[]))添加了对该`android:extractNativeLibs`标志的支持，可以在将应用程序安装到设备上时减小其大小。当您`false`在 [``](https://developer.android.com/guide/topics/manifest/application-element) 应用清单元素中将此标志设置为时，Gradle会将原生库的未压缩版本和对齐版本与APK打包在一起。这样可以防止[`PackageManager`](https://developer.android.com/reference/android/content/pm/PackageManager) 在安装过程中将本机库从APK复制到设备的文件系统中，并具有使应用程序的增量更新变小的额外好处。现在，您可以指定和用于产品口味。（[问题59614](http://b.android.com/59614)） [`versionNameSuffix`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.ProductFlavor.html#com.android.build.gradle.internal.dsl.ProductFlavor:versionNameSuffix)[ `applicationIdSuffix`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.ProductFlavor.html#com.android.build.gradle.internal.dsl.ProductFlavor:applicationIdSuffix)

- 变化：

  `getDefaultProguardFile` 现在返回用于Gradle的Android插件提供的默认ProGuard文件，并且不再使用Android SDK中的文件。改进的Jack编译器性能和功能：杰克现在支持Jacoco测试范围设定时 `testCoverageEnabled`到`true`。改进了对注释处理器的支持。类路径上的注释处理器（例如所有`compile` 依赖项）将自动应用于构建。您还可以在构建中指定注释处理器，并通过使用模块级文件中的DSL来传递参数： [`javaCompileOptions.annotationProcessorOptions {}`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.AnnotationProcessorOptions.html)`build.gradle``android { ... defaultConfig {  ...  javaCompileOptions {   注解ProcessorOptions {    className'com.example.MyProcessor '    //参数是可选的。    arguments = [ foo ：'bar' ]      }  } }}`如果要在编译时应用注释处理器但不将其包含在APK中，请使用 `annotationProcessor`依赖项范围：`依赖项{  编译'com.google.dagger：dagger：2.0'  注解处理器'com.google.dagger：dagger-compiler：2.0'  //或使用buildVariantAnnotationProcessor定位特定的构建变体}`您可以使用来为Jack设置其他标志。以下代码段将参数设置为： [`jackOptions.additionalParameters()`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.JackOptions.html#com.android.build.gradle.internal.dsl.JackOptions:additionalParameters)`jack.incremental``true``android { defaultConfig {  ...  jackOptions {   启用true   additionalParameters （“jack.incremental” ：真）    } }}`有关可以设置的参数的列表，请从命令行运行以下命令：`java -jar /build-tools/jack.jar --help-properties `默认情况下，如果Gradle守护程序的堆大小至少为1.5 GB，则Jack现在将在与Gradle相同的进程中运行。要调整守护程序堆大小，请在`gradle.properties`文件中添加以下内容 ：`＃将守护程序堆大小设置为1.5GB。 org.gradle.jvmargs = -Xmx1536M `

## 2.1.0（2016年4月）

**2.1.3（2016年8月）**

此更新要求Gradle 2.14.1及更高版本。Gradle 2.14.1包括性能改进，新功能和重要的[安全修复程序](https://docs.gradle.org/2.14/release-notes#local-privilege-escalation-when-using-the-daemon)。有关更多详细信息，请参见 [Gradle发行说明](https://docs.gradle.org/2.14.1/release-notes)。

- 依存关系：

  Gradle 2.10或更高版本。[构建工具23.0.2](https://developer.android.com/tools/revisions/build-tools) 或更高版本。

- 新：

  使用Jack工具链增加了对N Developer Preview，JDK 8和[Java 8语言功能](https://developer.android.com/preview/j8-jack)的支持。要了解更多信息，请阅读《[N预览指南》](https://developer.android.com/preview/overview)。**注意：** [Instant Run](https://developer.android.com/tools/building/building-studio#instant-run)当前不适用于Jack，在使用新工具链时将被禁用。如果您正在开发N预览版并且想要使用受支持的Java 8语言功能，则仅需要使用Jack。添加了对增量Java编译的默认支持，以减少开发过程中的编译时间。它仅通过重新编译源代码中已更改或需要重新编译的部分来执行此操作。要禁用此功能，请将以下代码添加到模块级 `build.gradle`文件中：`android { ... compileOptions {  增量错误 }}`增加了对进行中脱胶的支持，该功能可在构建过程中而不是在单独的外部VM进程中执行脱色。这不仅使增量构建更快，而且加快了完整构建。对于已将Gradle守护程序的最大堆大小设置为至少2048 MB的项目，默认情况下启用此功能。您可以通过在项目`gradle.properties`文件中添加以下内容来实现：`org 。摇篮。jvmargs = - Xmx2048m `如果您在模块级 文件中定义了的值，则需要将其设置为 + 1024 MB。例如，如果您设置 为“ 2048m”，则需要在项目文件中添加以下内容： [`javaMaxHeapSize`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.DexOptions.html#com.android.build.gradle.internal.dsl.DexOptions:javaMaxHeapSize)`build.gradle``org.gradle.jvmargs``javaMaxHeapSize``javaMaxHeapSize``gradle.properties``org 。摇篮。jvmargs = - Xmx3072m `要禁用进程中的删除，请将以下代码添加到模块级`build.gradle`文件中：`android { ... dexOptions {   dexInProcess false }}`

## 2.0.0（2016年4月）

- 依存关系：

  Gradle 2.10或更高版本。[构建工具21.1.1](https://developer.android.com/tools/revisions/build-tools) 或更高版本。

- 新：

  通过支持字节码注入并将代码和资源更新推送到仿真器或物理设备上正在运行的应用程序，来启用[即时运行](https://developer.android.com/tools/building/building-studio#instant-run)。添加了对增量构建的支持，即使该应用未运行也是如此。通过将增量更改通过[Android调试桥](https://developer.android.com/tools/help/adb)推送到连接的设备，可以缩短完整的构建时间 。添加以控制可以同时产生多少个从属dex进程。模块级文件中的以下代码 将并发进程的最大数量设置为4： [`maxProcessCount`](https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.DexOptions.html#com.android.build.gradle.internal.dsl.DexOptions:maxProcessCount)`build.gradle``android { ... dexOptions {  maxProcessCount = 4 //这是默认值   }}`添加了实验性代码收缩器以支持预删除和减少依赖项的重新删除，而Proguard不支持。这样可以提高调试构建变体的构建速度。由于实验性收缩器不支持优化和模糊处理，因此应为发布版本启用Proguard。要为调试版本启用实验性收缩器，请将以下内容添加到模块级`build.gradle`文件中：`android { ... buildTypes {  调试{   minifyEnabled 是   useProguard 假  }  发布{   minifyEnabled 是   useProguard true //这是默认设置   } }}`添加了日志记录支持并提高了资源缩减器的性能。现在，资源缩减器将其所有操作记录到`resources.txt` 与Proguard日志文件位于同一文件夹中的文件中。

- 更改的行为：

  当`minSdkVersion`设置为18或更高，APK签约使用SHA256。DSA和ECDSA密钥现在可以对APK软件包进行签名。**注：**在[Android的密钥存储](https://developer.android.com/training/articles/keystore)提供商不再支持[ 在Android 6.0 DSA密钥](https://developer.android.com/about/versions/marshmallow/android-6.0-changes#behavior-keystore)（API等级23）和更高。

- 解决的问题：

  修复了导致测试和主要构建配置中重复的AAR依赖关系的问题。