---
layout: post
title: reStructuredText语法
date: 2017-11-20
tag: reStructuredText
---
### 参考资料

1. [reStructuredText官网-使用手册](http://docutils.sourceforge.net/docs/user/rst/quickref.html)
2. [reStructuredTex官方语法](http://docutils.sourceforge.net/docs/user/rst/quickstart.html)
3. [关于TOC树](http://www.pythondoc.com/sphinx/markup/toctree.html)
4. [博客1](https://www.cnblogs.com/zzqcn/p/5096876.html)
5. [博客2](http://blog.csdn.net/u012150179/article/details/37743605)
6. [博客3](http://www.jianshu.com/p/1885d5570b37)



### 说明

一般语法可以参考上述所有资料，本文记录reStructedText的重要结构和特殊语法。

### 文档结构

* 入口文件：

  ```
  .. toctree::
     :maxdepth: 2
     :hidden:

     README
     book/UOS4.0介绍
     book/快速入门/index
     book/UOS项目平台/index
     book/UOS管理平台/index
     book/UOS计费系统/index
     book/UOS审批系统/index
     book/UOS存储平台/index
     book/UOS工单系统/index
  ```

  * `.. toctree::`：这个指令用来设置文档组织结构，其中
    * `:maxdepth: 2` ：用来设置目录显示层级
    * `:hidden: 用来设置是否在每个主页（index）中显示该目录`
    * `:number:`用来设置是否在目录前列出编号
  * 下面的部分表示组织起来的结构，这里分别是各个章节的主页，会显示章节标题。每个章节的主页中再以此种形式列出各自的结构组织。

### 特殊语法

* 文档内链接跳转语法

  1. 在目标前 标识：

     ```
     .. highlight:: rst
     .. _3.1.1 云主机服务:
     ```

     ..后有一个空格，::后有一个空格

  2. 在起始处 标识：

     ```
      :ref:`“3.4.1 报警” <3.4.1 报警>` 
     ```

     前后各有一个空格，<>前有一个空格










