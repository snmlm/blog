---
title: 读java源码的顺序
date: 2018/09/30
url: \2018\09\30\ReadJava
categories: 知识点
tags: 
	- java
---
 <meta name="referrer" content="no-referrer" />


标题为包名，后面序号为优先级1-4，优先级递减

### java.lang

* Object 1
* String 1
<!-- more -->
* AbstractStringBuilder 1
* StringBuffer 1
* StringBuilder 1
* Boolean 2
* Byte 2
* Double 2
* Float 2
* Integer 2
* Long 2
* Short 2
* Thread 2
* ThreadLocal 2
* Enum 3
* Throwable 3
* Error 3
* Exception 3
* Class 4
* ClassLoader 4
* Compiler 4
* System 4
* Package 4
* Void 4

### java.util

* AbstractList 1
* AbstractMap 1
* AbstractSet 1
* ArrayList 1
* LinkedList 1
* HashMap 1
* Hashtable 1
* HashSet 1
* LinkedHashMap 1
* LinkedHashSet 1
* TreeMap 1
* TreeSet 1
* Vector 2
* Queue 2
* Stack 2
* SortedMap 2
* SortedSet 2
* Collections 3
* Arrays 3
* Comparator 3
* Iterator 3
* Base64 4
* Date 4
* EventListener 4
* Random 4
* SubList 4
* Timer 4
* UUID 4
* WeakHashMap 4

### java.util.concurrent

* ConcurrentHashMap 1
* Executor 2
* AbstractExecutorService 2
* ExecutorService 2
* ThreadPoolExecutor 2
* BlockingQueue 2
* AbstractQueuedSynchronizer 2
* CountDownLatch 2
* FutureTask 2
* Semaphore 2
* CyclicBarrier 2
* CopyOnWriteArrayList 3
* SynchronousQueue 3
* BlockingDeque 3
* Callable 4

### java.util.concurrent.atomic

* AtomicBoolean 2
* AtomicInteger 2
* AtomicLong 2
* AtomicReference 3

### java.lang.reflect

* Field 2
* Method 2

### java.lang.annotation

* Annotation 3
* Target 3
* Inherited 3
* Retention 3
* Documented 4
* ElementType 4
* Native 4
* Repeatable 4

### java.util.concurrent.locks

* Lock 2
* Condition 2
* ReentrantLock 2
* ReentrantReadWriteLock 2

### java.io

* File 3
* InputStream   3
* OutputStream  3
* Reader  4
* Writer  4

### java.nio

* Buffer 3
* ByteBuffer 4
* CharBuffer 4
* DoubleBuffer 4
* FloatBuffer 4
* IntBuffer 4
* LongBuffer 4
* ShortBuffer 4

### java.sql

* Connection 3
* Driver 3
* DriverManager 3
* JDBCType 3
* ResultSet 4
* Statement 4

### java.net

* Socket 3
* ServerSocket 3
* URI 4
* URL 4
* URLEncoder 4


# 阅读笔记简版

### Object

* wait(), notify(), notifyAll(), wait(timeout)
* hashCode(), equals()
* clone()

### String

* char[] value
* int hash
* equals(), startWith(), endWith(), replace

### AbstractStringBuilder

* char[] value
* int count
* 扩容：翻倍，不够取所需最小

### StringBuffer

* 继承AbstractStringBuilder
* synchronized方法保证线程安全
* char[] toStringCache
* StringBuilder 继承AbstractStringBuilder

### ArrayList

* Object[] elementData
* int size
* 默认大小10
* 扩容：翻倍，不够取所需最小

### LinkedList

* Node {E item, Node prev, Node next}
* int size
* Node first
* Node last
* linkFirst(), linkLast(), linkBefore(), unLinkFirst(), unLinkLast(), unLink(), indexOf()

### HashMap

* Node{int hash, K key, V value, Node next}
* 默认容量16，负载因子0.75f
* int size, modCount, threshold, float loadFactor
* Node[] table
* Set entrySet
* put():根据key算hash，根据容量和hash算index，table[index]没有直接添加到数组中，table[index]有，若index位置同一个key则更新，否则遍历next是否有，有则更新，无则新增，最后根据thread与size判断是否扩容。注：扩容时容量翻倍，重新算hash复制到新数组
* get()类似

> 注：先比较hash，若相等在比较equals

### Hashtable

* 结构实现与HashMap基本一致
* 通过synchronized方法保证线程安全

### HashSet：委托给HashMap，其Value是同一个默认对象

### LinkedHashMap继承HashMap

* Entry{HashMap.Node, Entry before, after}
* Entry head, tail
* 重写newNode()添加节点时，除像HashMap中添加外，保存before、after信息

### LinkedHashSet继承HashSet：不知道如何实现的顺序？

### AbstractMap维护EntrySet，AbstractSet维护Iterator，AbstractList维护Iterator

### ConcurrentHashMap

* JDK1.7及以前
  * Segment[] ,HashEntry[] , HashEntry{hash, k, v,next}
  * 根据key算hash，根据hash和Segment的大小算位置，每个segment拥有一个自己的HashEntry[]
  * get()：不加锁，volatile类型
  * put(): 对相应segment加锁
  * size()：各HashEntry[] 之和，先不加锁算两遍，若一致则返回，若不一致则加锁重新计算
* JDK1.8
  * Node{hash, key, value, next}
  * Node[] table
  * 大多数操作类似于HashMap，不同CAS方式设置，根据key算hash，在根据hash和容量算index，对table[index]加锁，从而达到更大的并发量
  * get(): 同HashMap
  * put(): 对table[index]加锁

### TreeMap

* 红黑树，即自平衡二叉查找树，时间复杂度O(logn)
* Entry{K k, V v, Entry parent, left, right, boolean color}
* Entry root，int size， int modeCount

### TreeSet：委托TreeMap实现