---
layout: post
title: ThreadLocal小结
category: 技术
tags: Java
keywords: ThreadLocal 线程安全
---

# 前言 #
今年四月份面阿里，前一阵子面美团，一说JAVA基础，都会提到ThreadLocal，看来一句“多线程这方面做的不多”是不会让面试官客气的，好在亡羊补牢，为时未晚，在本文总我们来谈谈我对ThreadLocal的理解。本文的很多观点来自《深入理解java虚拟机》。

# 线程安全 #
我们很难想象在计算机的世界，程序执行时，被不停地中断，共享的数据可能会被修改和变“脏”。于是我们需要确保，共享数据在某一时刻只能被一个线程访问，即线程同步。而实现线程同步的一个常用手段便是“互斥”，具体到java代码，就是使用synchronized关键字。“互斥”后，线程访问时安全了，但并发执行的效率下降了，怎么办？

“互斥”之所以会引起效率下降，是因为就解决“线程安全”这个问题而言，它太“重量级”了，考虑的太过直接和全面。针对一些具体的使用场景，我们放宽要求甚至不采用互斥，也能达到“线程安全”。

考虑以下场景，

# 本地化变量 #

以上是从线程安全的角度出发，那么从线程本身角度看，线程操作时，往往需要一些对象（或变量），这些对象只有这个线程才可以使用。观察Java Thread类源码，可以发现其有一个ThreadLocalMap成员，这便是存这个变量的地方，之所以没有初始化，是因为Java开发者不知道用户要存什么样的对象。

# 原理 #

# 使用限制 #