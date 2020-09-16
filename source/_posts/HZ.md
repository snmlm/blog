---
title: 汇总
date: 2020/09/04
sticky: 100
tags: 
    - 汇总
---

<!-- more -->
# java

## {% post_link java/basics/20200508 %}

## 引用类型
- {% post_link java/basics/20200817 %}
- 数组
    - 连续的内存
- 自定义对象
    - runnable class（）主类（运行类）含有main方法，可以直接执行
    - java bean（） （不含有main方法，构造方法，set get 方法）
- {% post_link java/basics/20200909 %} 

## 枚举enum
单例模式的一种

## 面向对象 
- 封装（维护性）：隐藏成员变量和方法，隐藏共能实现的具体细节
- 继承（可扩展性）：子类继承父类的变量或者方法，也可以定义自己的 
    - {% post_link java/basics/20200701 %}
    - {% post_link java/basics/20190420 %}
- 多态（灵活性）：父类的引用指向子类的实力（上转型对象）

## {% post_link java/basics/20200915 %}
- {% post_link algorithm/20190507 %}
- {% post_link java/basics/20190418 %}

## 循环
- for
- foreach
    - {% post_link java/basics/20181010 %}
- do while
- while
- 递归
    - 构造方法不能递归
    - 必须有出口，if判断，否则死循环（肯定内存溢出）
    - 次数不易过多，否则会出现内存溢出
        - 递归解决问题的思想：（大->小）,将大问题拆成小问题
- if go(无用，字段保留)

## 关键字
- abstract：
    - 修饰类（被他修饰的类为抽象类）
    - 修饰方法（权限：public protected，抽象方法不能有方法体）
- final：
    - 修饰类：不能有子类
    - 修饰方法：不能被重写 （不能修饰抽象方法）
    - 修饰变量：常量（要赋初始值）
    - finally {% post_link java/basics/20200702 %}
    - finalize() {% post_link java/basics/20181011 %}
- implements：实现接口
- static：
    - 修饰类：（内部类）
    - 静态变量是属于类的，对象共享
    - 修饰方法：静态方法只能调用的静态的东西
- instanceof：
    - a instanceof A：判断对象a是不是类A及其子类创建的实力
- {% post_link java/basics/20200914 %}

## Collection&lt;E&gt;
- List
    - ArrayList：实现了RandomAccess接口，for循环比foreach快，数组实现，无参构造，初始0，add的时候才会初始为10，阀值是当前上限，扩充为x+(x>>1)，约为1.5倍，有参构造跟0比较，大于0，初始填值，小于0，报错IllegalArgumentException，remove的时候注意数据移动，倒叙删除，迭代器，转Set，{% post_link java/basics/20190417 %}
    - Linkedlist：双向链表实现
- Set
    - HashSet：对象必须重写hashCode方法，对象必须重写equals方法，链表实现，可以用作去重
    - TreeSet：对象必须实现Comparable接口的子类型，二叉树实现
- Queue
    - 没有实现的阻塞接口的LinkedList：实现了java.util.Queue接口和java.util.AbstractQueue接口

## Map&lt;K,V&gt;
- {% post_link java/basics/20190501 HashMap%}
- TreeMap
    - 自带{% post_link dataStructure/20200525 %}（R-B tree）

## 工具类
- Arrays
    - 对数组的工具类
- Collections（实现Collection的集合）
    - binarySearch-折半查找
    - sort-排序（二分法），集合实现Comparable接口，默认ascll码比较。可重写Comparator
    - copy-浅拷贝
    - emptyXXX()-得到空容器
    - max/min-获取最大/小元素，集合实现Comparable接口，默认ascll码比较。可重写Comparator
    - replaceAll-新值替换旧值
    - reverse-反转，集合实现Comparable接口，默认ascll码比较。可重写Comparator
    - shuffle-随机乱序，实现用Random，伪随机，真随机可以参考时间
    - syncronizedXXX-将线程不安全集合变成线程安全集合，装潢模式，创建一个syncronizedXXX新对象，内容指向原数据，所有方法添加syncronized关键字。常用于arraylist
    - unmodifiableXXX-将可以修改的容器变成不可变容器，不变模式，创建一个unmodifiableXXX新对象，内容指向原数据，新对象所有修改数据的方法直接返回异常UnsupportedOperationException。常用于arraylist。

## 其他容器
- Vector
    - Stack以Vector实现
- Dictonary
    - 已被map替代，过时接口。使用时必须静态使用
    - HashTable实现Dictonary，线程安全的hashMap，大部分方法用synchronized实现。
- BitSet
    - long数组实现。不能存重复数据，按位处理。

## 对象的序列化和反序列化
- 序列化：将对象以二进制的形式存储到硬盘中
- 反序列化：将以二进制形式的对象读取到内存中】
    - 可以利用深拷贝，反序列化是创建对象的一种方式
    - 延伸，0拷贝传输

> 要求：被序列化的对象必须要实现Serializable（标记接口）接口
> transient标记不被序列化的字段，SerializableID没有的话，反序列化会失败

## {% post_link java/basics/20200916 %}
- 创建线程
    - 继承Thread类，重写run方法
        - Thread类中的方法
            - 对象方法
                - start()-启动线程
                - setPriority(int)/getPriority()-设置/获取优先级
                - setDaemon(boolean)-设置守护线程（后台线程）
                - interrupt()-中断线程
                - join()-加塞线程，等到本线程结束
            - 静态方法
                - sleep(long)-休眠
                - yield()-让出cpu
                - currentThread()-获得当前线程
    - 实现Runnable接口，重写run方法
    - 实现Callable<T>接口，重写call方法
        - 利用Future<T>接收结果，并且可以监控中间状态
- 线程同步
    - java5之前
        - synchronized
            - 直接以关键字的方式修饰类，方法
            - 代码块中，synchronized(对象){代码}
    - java5+
        - Lock
            - lock()-加锁
            - unlock()-解锁
            - trylock()-尝试获得锁
        - Semaphore
            - acquire()-获取资源
            - release()-释放资源
        - CountDownLatch
- 线程通信
    - 基于共享内存的通信
        - 共享上下文
        - 内部类
        - 管道
    - 基于线程调度的通信
        - java5之前
            - wait()-线程暂停/等待
            - notify()/notifyAll()-唤醒等待的线程
        - java5+
            - Condition
                - await()-线程等待
                - signal()/signalAll()-唤醒等待的线程
- 线程池
    - 空间换时间的操作，事先创建多个线程，放入线程池中，省去单个线程的创建于销毁的时间
    - 创建线程池
        - Executors工具类
            - newFixedThreadPool(int)
                - 推荐在服务器变成使用
            - newCachedThreadPool
    - ExecutorService
        - execute(Runnable)-启动线程分配任务
        - submit(Callable<T>)-启动线程分配任务
            - Future<T>
                - 获取线程结果
        - shutdown()-等待线程执行完毕关闭线程池
        - shutdownNow()-立即关闭线程池返回等待执行的线程
        - isTerminated()-是否执行完所有线程

## Lambda表达式
匿名方法的实现
左侧：Lambda 表达式的参数列表
右侧：Lambda 表达式中所需执行的功能， 即 Lambda 体

## 泛型
- 泛型类
- 泛型接口
- 泛型方法
- 泛型引用
    - extends
    - supper

## jvm

### 类加载
- 类加载器（ClassLoader）
    - 加载：通过一个类的全限定名获取该类的二进制流，将该二进制流中的静态存储结构转化为方法去运行时数据结构，在内存中生成该类的 Class 对象，作为该类的数据访问入口
    - 加载
    - 连接-验证：文件格式验证：验证字节流是否符合 Class 文件的规范，元数据验证:对字节码描述的信息进行语义分析，字节码验证：是整个验证过程中最复杂的一个阶段，通过验证数据流和控制流的分析，确定程序语义是否正确，主要针对方法体的验证，符号引用验证：这个动作在后面的解析过程中发生，主要是为了确保解析动作能正确执行
    - 连接-准备：准备阶段是为类的静态变量分配内存并将其初始化为默认值，这些内存都将在方法区中进行分配。准备阶段不分配类中的实例变量的内存，实例变量将会在对象实例化时随着对象一起分配在 
    - 连接-解析：该阶段主要完成符号引用到直接引用的转换动作。解析动作并不一定在初始化动作完成之前，也有可能在初始化之后
    - 初始化：初始化时类加载的最后一步，前面的类加载过程，除了在加载阶段用户应用程序可以通过自定义类加载器参与之外，其余动作完全由虚拟机主导和控制。到了初始化阶段，才真正开始执行类中定义的Java 
    - 使用
    - 卸载：停止之后，自动卸载。
- PDM（父亲委托机制）
    - 、根加载器
    - 扩展加载器
    - 系统加载器
- 获取Class对象方式
    - 类.class
    - 对象.getClass()
    - Class.forName("类的完全限定名")

## {% post_link java/basics/20200908 %}

## XML
- 解析方式
    - SAX
    - DOM
    - St
- dom4j

## 异常
- 实现Throwable
    - Error
    - Exception
        - 检查异常
        - RuntimeException
        - 自定义异常，继承Exception或其子类

## I/O
- 两种设计模式
- 字节流
- 字符流
- BIO（blocking I/O）-同步并堵塞
- NIO（no-blocking I/O）同步非堵塞
- AIO（NIO2）（Asynchronous I/O）异步非堵塞

# 数据结构

## {% post_link algorithm/20190423 %}

# 数据库
## mysql
- {% post_link database/mysql/20190327 %}
- {% post_link database/mysql/20190409 %}
- {% post_link database/mysql/20190424 %}
- {% post_link database/mysql/20190425 %}
- {% post_link database/mysql/20190426 %}
- {% post_link database/mysql/20191009 %}
- {% post_link database/mysql/20200630 %}

## redis
## mogondb
# 框架
## spring
- core 
    - {% post_link java/spring/20200610 %}
- aop
- data access/intergration
- web
- test

## springboot
## 微服务
### dubbo
### springCould
## 数据库框架
### jdbc
- 操作顺序
    - 加载驱动
    - 创建连接
    - 创建语句
    - 执行语句
    - 操作结果集
    - 释放资源
- api
    - DriverManager
    - Driver
    - Connection
    - Statement
    - ResultSet
    - RowSet
    - DatabaseMetaData
    - ResultSetMetaData
    - Types
    - SQLException
- 事务
- 连接池

### mybatis
### hibernate


# web容器
## tomcat


# 系统
## Liunx

# 网络
# 正则表达式

