---
title: for与foreach用法的区别
date: 2018/10/10
url: \2018\10\10\TenGoodAdvice
categories: 知识点
tags: 
	- java
---
 <meta name="referrer" content="no-referrer" />

### for or foreach

* 当集合是实现了RandomAccess(随机存储接口),也就意味着，数据是随机访问的，例如arraylist，则尽量用for(int i = 0; i < size; i++) 来遍历。
* 反过来，如果List是Sequence List，例如linkedlist，则最好用迭代器来进行迭代。
* 数组特殊，for比foreach快