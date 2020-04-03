---
layout: post
title: "jupyter使用指南"
date: 2019-03-24 17:02:54
categories: Jupyter
tags: Jupyter
excerpt: Jupyter
mathjax:
author: LJY
---
* content
{:toc}


### 服务器搭建jupyter远程访问环境

后台启动方式
```
$ nohup jupyter notebook > ~/.jupyter/jupyter.log 2>&1 &
```

nohup 是 no hang up 的缩写，就是不挂断的意思。nohup 命令运行由 Command参数和任何相关的 Arg参数指定的命令，忽略所有挂断（SIGHUP）信号。在注销后使用 nohup 命令运行后台中的程序。要运行后台中的 nohup 命令，添加 & （ 表示“and”的符号）到命令的尾部。如果你正在运行一个进程，而且你觉得在退出帐户时该进程还不会结束，那么可以使用nohup命令。该命令可以在你退出帐户/关闭终端之后继续运行相应的进程。在缺省情况下该作业的所有输出都被重定向到一个名为nohup.out的文件中。

### jupyter notebook更换主题

- 安装jupyter-themes的命令行如下所示：

```
pip install jupyter-themes
```
- 命令行的格式的解释如下表所示：

cl options |	arg	| default |
| :------: | :------: | :------: |
Usage help | 	-h | 	--
List Themes	 | -l	 | --
Theme Name to Install | 	-t | 	--
Code Font | 	-f | 	--
Code Font-Size | 	-fs	 | 11
Notebook Font	 | -nf	 | --
Notebook Font Size | 	-nfs | 	13
Text/MD Cell Font	 | -tf	 | --
Text/MD Cell Fontsize	 | -tfs	 | 13
Pandas DF Fontsize	 | -dfs | 	9
Output Area Fontsize	 | -ofs	 | 8.5
Mathjax Fontsize (%)	 | -mathfs | 	100
Intro Page Margins | 	-m	 | auto
Cell Width | 	-cellw | 	980
Line Height	 | -lineh | 	170
Cursor Width	 | -cursw | 	2
Cursor Color	 | -cursc | 	--

- 查看安装了哪些主题的命令行如下所示：
```
jt -l
```