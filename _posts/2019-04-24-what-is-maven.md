---
layout: post
title: "maven到底是个啥玩意!"
date: 2019-04-24 15:14:54
categories: Maven
tags: Maven
excerpt: 简述maven
mathjax: true
---

* content
{:toc}

## maven到底是个啥玩意~
* 参考博文：[通俗理解maven](http://blog.csdn.net/shuzhe66/article/details/45009175)
&ensp; 该篇文章篇幅很长，大概的思路如下：maven的介绍，初步认识，获取jar包的三个关键属性:
> 介绍仓库(获取的jar包从何而来)
>用命令行管理maven项目(创建maven项目)
> 用myeclipse创建maven项目 
>详细介绍pom.xml中的依赖关系(坐标获取、定位jar包的各种属性讲解。
                        
     
  
#### 一、简单的小问题？

##### 1.1、假如你正在Eclipse下开发两个Java项目，姑且把它们称为A、B，其中A项目中的一些功能依赖于B项目中的某些类，那么如何维系这种依赖关系的呢？
&ensp; 很简单，这不就是跟我们之前写程序时一样吗，需要用哪个项目中的哪些类，也就是用别人写好了的功能代码，导入jar包即可。所以这里也如此，可以将B项目打成jar包，然后在A项目的Library下导入B的jar文件，这样，A项目就可以调用B项目中的某些类了。

&ensp;&ensp;这样做几种缺陷

* &ensp; 如果在开发过程中，发现B中的bug，则必须将B项目修改好，并重 新将B打包并对A项目进行重编译操作

* &ensp; 在完成A项目的开发后，为了保证A的正常运行，就需要依赖B(就像在使用某个jar包时必须依赖另外一个jar一样)，两种解决方案，第一种，选择将B打包入A中，第二种，将B也发布出去，等别人需要用A时，告诉开发者，想要用A就必须在导入Bjar包。两个都很麻烦，前者可能造成资源的浪费(比如，开发者可能正在开发依赖B的其它项目，B已经存储到本地了，在导入A的jar包的话，就有了两个B的jar)，后者是我们常遇到的，找各种jar包，非常麻烦(有了maven就不一样了)

##### 1.2、我们开发一个项目，或者做一个小demo，比如用SSH框架，那么我们就必须将SSH框架所用的几十个依赖的jar包依次找出来并手动导入，超级繁琐。　

上面两个问题的描述，其实都属于项目与项目之间依赖的问题[A项目使用SSH的所有jar，就说A项目依赖SSH]，人为手动的去解决，很繁琐，也不方便，所以使用maven来帮我们管理
* * *
### 二、maven到底是什么？

* * *

&ensp; Maven是基于项目对象模型(POM project object model)，可以通过一小段描述信息（配置）来管理项目的构建，报告和文档的软件项目管理工具
&ensp; 我自己觉得，Maven的核心功能便是合理叙述项目间的依赖关系，通俗点讲，就是通过pom.xml文件的配置获取jar包，而不用手动去添加jar包，而这里pom.xml文件对于学了一点maven的人来说，就有些熟悉了，怎么通过pom.xml的配置就可以获取到jar包呢？pom.xml配置文件从何而来？等等类似问题我们需要搞清楚，如果需要使用pom.xml来获取jar包，那么首先该项目就必须为maven项目，maven项目可以这样去想，就是在java项目和web项目的上面包裹了一层maven，本质上java项目还是java项目，web项目还是web项目，但是包裹了maven之后，就可以使用maven提供的一些功能了(通过pom.xml添加jar包)。
&ensp; 所以，根据上一段的描述，我们最终的目的就是学会如何在pom.xml中配置获取到我们想要的jar包，在此之前我们就必须了解如何创建maven项目，maven项目的结构是怎样，与普通java,web项目的区别在哪里，还有如何配置pom.xml获取到对应的jar包等等，这里提前了解一下我们如何通过pom.xml文件获取到想要的jar的，具体后面会详细讲解该配置文件。
***pom.xml获取junit的jar包的编写。***　

&ensp;为什么通过groupId、artifactId、version三个属性就能定位一个jar包？
&ensp; 加入上面的pom.xml文件属于A项目，那么A项目肯定是一个maven项目，通过上面这三个属性能够找到junit对应版本的jar包，那么junit项目肯定也是一个maven项目，junit的maven项目中的pom.xml文件就会有三个标识符，比如像下图这样，然后别的maven项目就能通过这三个属性来找到junit项目的jar包了。所以，在每个创建的maven项目时都会要求写上这三个属性值的。
* * *

### 三、maven的安装
* * *

&ensp; 这一步maven环境的配置，我觉得有必要安装一下，目的为了使用命令行创建maven项目，和使用命令行操作maven项目。这里不细讲，给出链接，跟安装jdk环境类似，[maven的安装教程和配置](http://jingyan.baidu.com/article/4f7d5712a1306c1a21192746.html)

* * *
### 四、仓库的概念

* * *

&ensp; 通过pom.xml中的配置，就能够获取到想要的jar包(还没讲解如何配置先需要了解一下仓库的概念)，但是这些jar是在哪里呢？就是我们从哪里获取到的这些jar包？答案就是仓库。
&ensp; 仓库分为：本地仓库、第三方仓库(私服)、中央仓库
######4.1、本地仓库
&ensp; Maven会将工程中依赖的构件(Jar包)从远程下载到本机一个目录下管理，每个电脑默认的仓库是在 `$user.home/.m2/repository`下

&ensp; 一般我们会修改本地仓库位置，自己创建一个文件夹，在从网上下载一个拥有相对完整的所有jar包的结合，都丢到本地仓库中，然后每次写项目，直接从本地仓库里拿就行了
&ensp; 这里面有很多各种各样我们需要的jar包。
&ensp; 修改本地库位置：`在$MAVEN_HOME/conf/setting.xml`文件中修改，

&ensp;` D:\java\maven\repository：`就是我们自己创建的本地仓库，将网上下载的所有jar包，都丢到该目录下，我们就可以直接通过maven的pom.xml文件直接拿。


###### 4.2、第三方仓库
&ensp; 第三方仓库，又称为内部中心仓库，也称为私服
> 私服：一般是由公司自己设立的，只为本公司内部共享使用。它既可以作为公司内部构件协作和存档，也可作为公用类库镜像缓存，减少在外部访问和下载的频率。（使用私服为了减少对中央仓库的访问)

* 私服可以使用的是局域网，中央仓库必须使用外网

* 也就是一般公司都会创建这种第三方仓库，保证项目开发时，项目所需用的jar都从该仓库中拿，每个人的版本就都一样。

*注意：连接私服，需要单独配置。如果没有配置私服，默认不使用

######4.3、中央仓库
&ensp; Maven内置了远程公用仓库：`http://repo1.maven.org/maven2`
&ensp; 这个公共仓库是由Maven自己维护，里面有大量的常用类库，并包含了世界上大部分流行的开源项目构件。目前是以java为主

*  工程依赖的jar包如果本地仓库没有，默认从中央仓库下载

*　总结：获取jar包的过程

* * *
### 五、使用命令行管理maven项目

* * *

######5.1、创建maven java项目
&ensp; 自己创建一个文件夹，在该文件夹下按shift+右击，点开使用命令行模式，这样创建的maven[java]项目就在该文件夹下了。

*命令：`mvn archetype:create -DgroupId=com.wuhao.maven.quickstart -DartifactId=simple -DarchetypeArtifactId=maven-archetype-quickstart'

* mvn：核心命令

* `archetype:create`：创建项目，现在maven高一点的版本都弃用了create命令而使用generate命令了。
* `DgroupId=com.wuhao.maven.quickstart `：创建该maven项目时的groupId是什么，该作用在上面已经解释了。一般使用包名的写法。因为包名是用公司的域名的反写，独一无二
* `DartifactId=simple`：创建该maven项目时的artifactId是什么，就是项目名称
* `DarchetypeArtifactId=maven-archetype-quickstart`：表示创建的是[maven]java项目

运行的前提：
&ensp; 需要联网，必须上网下载一个小文件
运行成功后

&ensp; 在D:\java\maven\demo下就会生成一个simple的文件，该文件就是我们的maven java项目

#### 5.2、maven java项目结构
![avatar](https://pic002.cnblogs.com/images/2012/274814/2012070509215570.gif)

