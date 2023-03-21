# Android Gradle

#### 一、[Gradle](https://gradle.org/guides/#getting-started)基础

> Gradle是一种用于构建软件项目的自动化构建工具。它采用了基于Groovy语言的领域特定语言（DSL）来定义构建脚本，可以用于构建Java、C++、Python、Android等各种类型的项目。Gradle具有高度可配置性、可扩展性和灵活性，可以轻松地定制构建过程以满足不同的项目需求。它也具有优秀的依赖管理功能，能够自动下载和管理项目所需的依赖库，并且支持多个仓库和版本控制系统。Gradle还支持增量构建和并行构建，可以加快构建过程的速度。Gradle已成为许多开发者和企业的首选构建工具之一。

#### 二、[Gradle基本概概念](https://services.gradle.org/)

##### Distribution

##### Wrapper

##### GradleUserHome

##### Deamon



下载完的gradle项目是可以直接运行的。进行配置环境变量

![](https://gitee.com/LuHenChang/blog_pic/raw/master/android_gradle_02.png)

配置完成之后可以通过创建gradle项目文件，且在该目录下进行gradle init初始化一个gradle项目。

```
➜  ~ git:(master) ✗ /Users/wangfeiwangfei/Desktop/tem/wrapper-demo 
➜  wrapper-demo git:(master) ✗ tree .
.
├── build.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
└── settings.gradle
```

#### 三、Groovy基础

https://docs.gradle.org/current/userguide/build_lifecycle.html#sec:build_phases

生命周期：https://docs.gradle.org/current/userguide/build_lifecycle.html



afterEvaluate钩子函数

gradle执行引擎吧build.gradle代码脚本从上倒下执行一遍。

执行完成之后，我们就称为p roject完成了Evalueate就会去执行钩子函数

然后继续去执行任务
