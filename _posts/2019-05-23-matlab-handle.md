---
layout: post
title: "Matlab中的函数句柄"
date: 2019-05-23 11:14:54
categories: Matlab
tags: Matlab
excerpt: 简述
mathjax: true
author: LJY
---
* content
{:toc}

`@` 是Matlab中的句柄函数的标志符，即间接的函数调用方法。

## 1.句柄函数

主要有两种语法：

+ `handle = @functionname`
+ `handle = @(arglist)anonymous_function`

`handle = @functionname`：返回一个特别的Matlab函数句柄，它提供了一种间接访问函数的方式，也被成为函数的函数(`function functions`)，是一种标准的Matlab数据类型。在C/C++中，有个类似的用法称为引用（使用标识符`&`），引用只是它绑定的对象的另一个名字，作用在应用上的所有操作事实上都会作用在该引用绑定的对象上。Matlab里句柄函数，与前面讲得引用有些类似，我们通过语句`handle = @functionname`给名为`functionname`的函数取了个别名`handle`，也就是说你既可以用函数`functionname`实现你要实现的功能，也可以使用handle实现同样的功能。在Python里，你大可直接用变量赋值的方式`handle = functionname`达到这一目的。

基本用法如下：
```
% .m 文件函数句柄
>>fh_mFile = @humps
fh_mFile = 
    @humps

% 内置函数句柄
>>fh_builtin = @cos
fh_builtin = 
    @cos
>>fh_builtin(pi)
ans =   -1
```
`handle = @(arglist)anonymous_function`：也称为匿名函数，@左边为一个函数句柄，`@`后定义了匿名函数的输入参数（多个参数用逗号分隔开），最后一部分为匿名函数的表达式。基本用法如下：
```
>>sqr = @(x) x.^2
>>a = sqr([1, 2, 3])
a =
     1     4     9
```

## 2.句柄处理函数
这里列举四个常见的句柄处理函数，如下表：
|函数|说明|
|---|---|
|`functions`|返回一个句柄的详细信息|
|`str2func`|将一个函数名作为字符串传递给此函数，创建该函数的函数句柄|
|`func2str`|从一个函数句柄中提取函数名，对于内置函数或m文件函数句|柄，返回函数的名称，对于匿名函数，返回其表达式|
|`structfun`|将句柄结构体数组的每一个句柄函数的依次作用于数组，返回每个句柄函数的作用于数组的值|
逐一给出示例：
```
>> functions(sqr)
ans = 
     function: '@(x)x.^2'
         type: 'anonymous'
         file: ''
    workspace: {[1x1 struct]}


>>fh2 = str2func('sqr')
fh2 = 
    @sqr

>> func2str(fh2)
ans =
sqr
>> func2str(sqr)
ans =
@(x)x.^2

>> S.a = @sin; S.b = @cos; S.c = @tan;
>> structfun(@(x)x(linspace(1, 4, 3)), S, 'UniformOutput', false)
ans = 
    a: [0.8415 0.5985 -0.7568]
    b: [0.5403 -0.8011 -0.6536]
    c: [1.5574 -0.7470 1.1578]

```