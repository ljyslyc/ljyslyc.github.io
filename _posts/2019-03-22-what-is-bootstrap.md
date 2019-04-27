---
layout: post
title: "Bootstrap简介(转）"
date: 2019-03-22 16:01:54
categories: html css javascript
tags: html css javascript
excerpt: Bootstrap是一套易用、优雅、灵活、可扩展的前端工具集。
mathjax:
author: LJY
---
* content
{:toc}


Bootstrap是一套易用、优雅、灵活、可扩展的前端工具集。

*   简单灵活可用于架构流行的用户界面和交互接口的html、css、             javascript工具集。

*   基于html5、css3的bootstrap，具有大量的诱人特性：友好的学习     曲线，卓越的兼容性，响应式设计，12列格网，样式向导文档。

*   自定义JQuery插件，完整的类库，基于Less等。

### Bootstrap框架结构
-----

```html
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/

    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2

```
ps：Bootstrap中的JS插件依赖于jQuery，所以jQuery要在Bootstrap之前引用

## 基本模板
----

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- 定义页面编码 -->
    <meta charset="utf-8">
    <!-- 在IE运行最新的渲染模式 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- 初始化移动浏览显示 -->
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
    <title>Bootstrap 101 Template</title>
    
    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet">
    
    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.3/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>Hello, world!</h1>

    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="js/bootstrap.min.js"></script>
  </body>
</html>
```
ps：一般把css的引用放head标签中，js的引用放body标签的最下面。

## 排版
----
#### 标题
----
```
标题 <h1><h2><h3><h4><h5><h6>

副标题 <small>

例如：<h1>Bootstrap标题<small>我是副标题</small></h1>
```
----
#### 段落

----
```
段落 <p>

强调内容 通过类名”.lead”实现，作用是增大文本字号，加粗文本

例如：<p class=”lead”>这部分内容需要特别的强调</p>

文本对其风格

.text-left：左对齐

.text-center：居中对齐

.text-right：右对齐

.text-justify：两端对齐

例如：<p class=”text-center”>居中</p>
```
----
#### 加粗
----
```
加粗 <b>或者<strong>
```
----
#### 强调相关的类
----
```
.text-muted：提示，使用浅灰色（#999）
.text-primary：主要，使用蓝色（#428bca）
.text-success：成功，使用浅绿色(#3c763d)
.text-info：通知信息，使用浅蓝色（#31708f）
.text-warning：警告，使用黄色（#8a6d3b）
.text-danger：危险，使用褐色（#a94442
```
---
#### 列表
---
```
无序列表 <ul> <li>

有序列表 <ol> <li>

取点列表 .list-unstyled

内联列表 .list-inline 把垂直列表换成水平列表

定义列表 <dl><dt><dd>

水平定义列表 .dl-horizontal
```
---
#### 代码
---
```
<code>：一般是针对于单个单词或单个句子的代码

<pre>：一般是针对于多行代码（也就是成块的代码）

<kbd>：一般是表示用户要通过键盘输入的内容

ps：不管使用哪种代码风格，在代码中碰到小于号（<）要使用硬编码“&lt;”来替代，大于号(>)使用“&gt;”来替代。

在<pre>上添加类名”.pre-scrolable”，可以控制代码块区域最大高度为340px，一旦超出这个高度，就会在Y轴出现滚动条。
```
----
#### 表格
----
```
Bootstrap为表格提供了1种基础样式和4种附加样式以及1各支持响应式的表格。

.table：基础表格 <table class=”table”>

.table-striped：斑马线表格 <table class=”table table-striped”>

.table-bordered：带边框的表格 <table class=”table table-bordered”>

.table-hover：鼠标悬停高亮的表格 <table class=”table table-hover”>

.table-condensed：紧凑型表格 <table class=”table table-condensed”>

.table-responsive：响应式表格 <div class=”table-responsive”><table class=”table table-bordered”>
```
---
#### 表格行的类
---
```
Bootstrap为表格的行元素<tr>提供了五种不同的类名，每种类名控制了行的不同背景颜色。

.active 表示当前活动的信息 #f5f5f5

.success 表示成功或者正确的行为 #dff0d8

.info 表示中立的信息或行为 #d9edf7

.warning 表示警告，需要特别注意 #fcf8e3

.danger 表示危险或者可能是错误的行为 #f2dede
```
----

## 表单
---
#### 水平表单
----
水平表单即标签居左，表单控件居右的显示风格。
```
在Bootstrap框架中要实现水平表单效果，必须满足以下两个条件：
1、在<form>元素是使用类名“form-horizontal”。
2、配合Bootstrap框架的网格系统。（网格布局会在以后的章节中详细讲解）
在<form>元素上使用类名“form-horizontal”主要有以下几个作用：
1、设置表单控件padding和margin值。
2、改变“form-group”的表现形式，类似于网格系统的“row”。
```
---
#### 内联表单
---
```
内联表格即将表单的控件都在一行内显示。

只需要在<form>元素中添加类名“form-inline”即可。

内联表单实现原理非常简单，欲将表单控件在一行显示，就需要将表单控件设置成内联块元素（display:inline-block）。
```
---
#### 表单控件
单行输入框
```
<input type="text" class="form-control" placeholder="Enter Username">

```
下拉选择框
```
<select class="form-control">
    <option>1</option>
    <option>2</option>
    <option>3</option>
    <option>4</option>
    <option>5</option>
</select>
```
文本域
```
<textarea class="form-control" rows="3"></textarea>
```
复选框 checkbox

单选择按钮 radio

注意

1、如果checkbox需要水平排列，只需要在label标签上添加类名“checkbox-inline”
2、如果radio需要水平排列，只需要在label标签上添加类名“radio-inline”

---
#### 表单控件状态
---
```
.has-warning:警告状态（黄色）
.has-error：错误状态（红色）
.has-success：成功状态（绿色）
```
---
#### 表单提示信息
---
.help-block样式，将提示信息以块状显示，并且显示在控件底部。
```
<span class="help-block">你输入的信息是正确的</span>
```
#### 按钮
```
<button class="btn" type="button">按钮</button>
```
#### 按钮定制风格:

`默认按钮 .btn-default`

`主要按钮 .btn-primary`

`成功按钮 .btn-success`

`信息按钮 .btn-info`

`警告按钮 .btn-warning`

`危险按钮 .btn-danger`

`链接按钮 .btn-link`

#### 按钮大小：

`变大 .btn-lg`

`变小 .btn-sm`

`超小 .btn-xs`

#### 图像
----
```
<img  alt="140x140" src="http://placehold.it/140x140">
````
#### 样式风格：

 `   .img-responsive 响应式图片，主要针对于响应式设计    `

`.img-rounded 圆角图片`

`.img-circle 圆形图片`

`.img-thumbnail 缩略图片`

----

## 网格系统
----
#### 基本原理
---
1、数据行(.row)必须包含在容器（.container）中，以便为其赋予合适的对齐方式和内距(padding)。如：
```
<div class="container">
<div class="row"></div>
</div>
```
2、在行(.row)中可以添加列(.column)，但列数之和不能超过平分的总列数，比如12。如：
```
<div class="container">
<div class="row">
  <div class="col-md-4"></div>
  <div class="col-md-8"></div>
</div>
</div>
```
3、具体内容应当放置在列容器（column）之内，而且只有列（column）才可以作为行容器(.row)的直接子元素

4、通过设置内距（padding）从而创建列与列之间的间距。然后通过为第一列和最后一列设置负值的外距（margin）来抵消内距(padding)的影响

---
#### 基本用法
---
1.列组合

2.列偏移

3.列排序

4.列的嵌套

---

#### 下拉菜单
---
使用方法：

1、使用一个名为“dropdown”的容器包裹了整个下拉菜单元素
```
<div class="dropdown"></div>
```
<p>
2、使用了一个  < button > 按钮做为父菜单，并且定义类名“dropdown-toggle”和自定义“data-toggle”属性，且值必须和最外容器类名一致
</p>

```
data-toggle="dropdown"
```
3、下拉菜单项使用一个ul列表，并且定义一个类名为“dropdown-menu”

```
<ul class="dropdown-menu">
```
分割线：

`.divider`

菜单头部：

`.dropdown-header`

对齐方式：

默认是左对齐

要相对于父容器右对齐可以添加类.pull-right或.dropdown-menu-right

---
####  按钮
---
按钮组

```
<div class="btn-group">
```
.btn-group-lg 大按钮组

.btn-group-sm 小按钮组

.btn-group-xs 超小按钮组

按钮工具栏

```
<div class="btn-toolbar">
```
垂直分组

```
<div class="btn-group-vertical">
```
等分按钮

```
<div class="btn-group btn-group-justified">
```
## 导航
标签形tab导航

```
<ul class="nav nav-tabs">
```
在其标签上添加类名class=”active”的为默认的当前选中项

胶囊形导航

```
<ul class="nav nav-pills">
```
垂直堆叠的导航

```
<ul class="nav nav-pills nav-stacked">
```
面包屑式导航
```
<ol class="breadcrumb">
  <li><a href="#">首页</a></li>
  <li><a href="#">博文</a></li>
  <li class="active">Bootstrap</li>
</ol>
```

#### 导航条
基础导航条
```
<div class="navbar navbar-default" role="navigation">
     <ul class="nav navbar-nav">
     	<li class="active"><a href="##">首页</a></li>
        <li><a href="##">教程</a></li>
        <li><a href="##">介绍</a></li>
        <li><a href="##">案例</a></li>
        <li><a href="##">我们</a></li>
     </ul>
</div>
```
标题
```
<div class="navbar-header">
    <a href="##" class="navbar-brand">导航标题</a>
</div>
```
固定导航条
```

.navbar-fixed-top：导航条固定在浏览器窗口顶部

.navbar-fixed-bottom：导航条固定在浏览器窗口底部
```

反色导航条

`.navbar-inverse`

分页导航
```
<ul class="pagination">
   <li><a href="#">&laquo;</a></li>
   <li><a href="#">1</a></li>
   <li><a href="#">2</a></li>
   <li><a href="#">3</a></li>
   <li><a href="#">4</a></li>
   <li><a href="#">5</a></li>
   <li><a href="#">&raquo;</a></li>
</ul>
```
`.pagination-lg 让分页导航变大`

`.pagination-sm 让分页导航变小`

翻页分页导航

```
<ul class="pager">
   <li><a href="#">&laquo;上一页</a></li>
   <li><a href="#">下一页&raquo;</a></li>
</ul>
```
标签

```
<h3>Example heading <span class="label label-default">New</span></h3>
```

样式：

`.label-deafult:默认标签，深灰色`

`.label-primary：主要标签，深蓝色`

`.label-success：成功标签，绿色`

`.label-info：信息标签，浅蓝色`

`.label-warning：警告标签，橙色`

`.label-danger：错误标签，红色`

徽章
```
<a href="#">Inbox <span class="badge">7</span></a>
```
缩略图

`.thumbnail`

`.caption`
```
<div class="container">
    <div class="row">
        <div class="col-xs-6 col-md-3">
            <a href="#" class="thumbnail">
                <img src="图片地址" style="height: 180px; width: 100%; display: block;" alt="">
            </a>
            <div class="caption">
                <h3>标题</h3>
                <p>说明</p>
                <p>
                    <a href="##" class="btn btn-primary">按钮</a>
                </p>
            </div>
        </div>
    …
    </div>
</div>
```
---
## 警示框
---

#### 基础的警示框
---
```
<div class="alert" role="alert">test</div>
```
成功警示框：告诉用用户操作成功，在“alert”样式基础上追加“alert-success”样式，具体呈现的是背景、边框和文本都是绿色；

信息警示框：给用户提供提示信息，在“alert”样式基础上追加“alert-info”样式，具体呈现的是背景、边框和文本都是浅蓝色；

警告警示框：提示用户小心操作（提供警告信息），在“alert”样式基础上追加“alert-warning”样式，具体呈现的是背景、边框、文本都是浅黄色；

错误警示框：提示用户操作错误，在“alert”样式基础上追加“alert-danger”样式，具体呈现的是背景、边框和文本都是浅红色。

---
#### 可关闭的警示框
---
需要在基本警示框“alert”的基础上添加“alert-dismissable”样式。
在button标签中加入class=”close”类，实现警示框关闭按钮的样式。
要确保关闭按钮元素上设置了自定义属性：“data-dismiss=”alert””（因为可关闭警示框需要借助于Javascript来检测该属性，从而控制警示框的关闭）。
```
<div class="alert alert-success alert-dismissable" role="alert">
    <button class="close" type="button" data-dismiss="alert">&times;</button>
    恭喜您操作成功！
</div>
```
---
#### 警示框的链接

---

添加一个名为”alert-link”的类名

```
<div class="alert alert-success" role="alert">
    <strong>Well done!</strong> 
    You successfully read 
    <a href="#" class="alert-link">this important alert message</a>
    .
</div>
```
