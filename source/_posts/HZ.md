---
title: 汇总
date: 2020/09/04
sticky: 100
tags: 
    - 汇总
---

# 操作系统

## 基础
- {% post_link system/20210412 %}
- {% post_link system/20210413 %}
- {% post_link system/20210414 %}

## cpu
- 进程是资源分配的基本单位
- 线程是计算机调度（运行）的基本单位
    - 线程切换过程，重度消耗资源
        - 当前运行线程从cpu中移出或保存，包含当前线程的所有状态。
        - 加载需要执行线程的所有状态，加载完成后，继续执行线程中的线性逻辑。
- 状态

## Liunx
- {% post_link system/liunx/20190410 %}

## 网络
- {% post_link network/20190311 %}
- {% post_link network/20200612 %}

# java
## 基础类型
- {% post_link java/basics/20200508 %}

## 引用类型
- {% post_link java/basics/20200817 %}
- 数组
    - 连续的内存
- 自定义对象
    - runnable class（）主类（运行类）含有main方法，可以直接执行
    - java bean（） （不含有main方法，构造方法，set get 方法）
- {% post_link java/basics/20200909 %} 

## 枚举enum
- 单例模式的一种

## 面向对象 
- 封装（维护性）：隐藏成员变量和方法，隐藏共能实现的具体细节
- 继承（可扩展性）：子类继承父类的变量或者方法，也可以定义自己的 
    - {% post_link java/basics/20200701 %}
    - {% post_link java/basics/20190420 %}
- 多态（灵活性）：父类的引用指向子类的实例（上转型对象）

## 运算符
- {% post_link java/basics/20200915 %}
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
- {% post_link java/basics/20201014 %}

## 集合/容器
### Collection&lt;E&gt;
- List
    - ArrayList 实现类
        - 实现了RandomAccess接口，for循环比foreach快
        - 数组实现
        - 阀值是当前上限，扩充为x+(x>>1)，约为1.5倍
        - 无参构造，初始0，add的时候才会初始为10
        - 有参构造跟0比较，大于0，初始填值，小于0，报错IllegalArgumentException
        - {% post_link java/basics/20190417 %}
    - Linkedlist 实现类
        - 没有实现RandomAccess接口，foreach循环比for快
        - 实现了Deque，支持双端添加和删除
        - 双向链表实现
- Set
    - HashSet 实现类
        - 对象必须重写hashCode方法
        - 对象必须重写equals方法
        - 链表实现
        - 可以用作去重
    - TreeSet 实现类
        - 对象必须实现Comparable接口的子类型
        - 二叉树实现
- Queue
    - AbstractQueue 接口
        - 实现了Queue和Collection中部分函数
    - Deque 接口
        - 一个线性 collection，支持在两端插入和移除元素
        - 名称 deque 是“double ended queue(双端队列)”的缩写，通常读为“deck”
        - 大多数 Deque 实现对于它们能够包含的元素数没有固定限制，但此接口既支持有容量限制的双端队列，也支持没有固定大小限制的双端队列
    - ArrayDeque 实现类
        - 实现Deque
        - 可变数组实现
        - 线程不安全
        - 作为栈使用，效率高于Stack
        - 作为链表使用，效率高于Linkedlist
        - 不支持null值
    - BlockingQueue 接口
        - concurrent包下
    - PriorityQueue 实现类 优先级队列
        - 最大堆算法
        - 实现AbstractQueue
        - 数组实现

### Map&lt;K,V&gt;
- {% post_link java/basics/20190501 HashMap%} 包含ConcurrentHashMap
- TreeMap
    - 自带{% post_link dataStructure/20200525 %}（R-B tree）

### 工具类
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

### 其他容器
- Vector
    - Stack以Vector实现
- Dictonary
    - 已被map替代，过时接口。使用时必须静态使用
    - HashTable实现Dictonary，线程安全的hashMap，大部分方法用synchronized实现。
- BitSet
    - long数组实现。不能存重复数据，按位处理。

## 序列化和反序列化
- 序列化：将对象以二进制的形式存储到硬盘中
- 反序列化：将以二进制形式的对象读取到内存中】
    - 可以利用深拷贝，反序列化是创建对象的一种方式
    - 延伸，{% post_link daily/20210413 %}传输

> 要求：被序列化的对象必须要实现Serializable（标记接口）接口
> transient标记不被序列化的字段，SerializableID没有的话，反序列化会失败

## 多线程
- {% post_link java/basics/20200916 %}
- {% post_link java/basics/20201013 %}
- {% post_link java/basics/20201015 %}
- {% post_link java/basics/20201203 %}

## Lambda表达式
- 匿名方法的实现
    - 左侧：Lambda 表达式的参数列表
    - 右侧：Lambda 表达式中所需执行的功能， 即 Lambda 体

## 泛型
- 泛型类
- 泛型接口
- 泛型方法
- 泛型引用
    - extends
    - supper

## jvm
![](https://raw.githubusercontent.com/snmlm/resources/master/picture/HotSpot_JVM_Architecture.png)
- {% post_link java/jvm/20201110 %}
- {% post_link java/jvm/20201111 %}

### 类加载子系统
- {% post_link java/jvm/20201109 %}
- {% post_link java/jvm/20201112 %}

### 内存模型
内存是非常重要的系统资源，是硬盘和CPU的中间长裤及桥梁，承载着操作系统和应用程序的实时运行。JVM内存布局规定了Java在运行过程中的内存申请、分配、管理的策略，保证了JVM的高效稳定运行。
不同的JVM对于内存的划分方式和管理存在着部分差异，这里主要是HotSpot
每个线程：独立的程序计数器、栈、本地栈
线程间共享：堆、堆外内存（永久代/元空间、代码缓存）
Runtime对象是单例的。一个jvm实例，只有一个，getRuntime()可以获取;
线程是一个程序里的运行单元，JVM允许一个应用有多个线程并行的执行
在Hotspot JVM里，每个线程都与炒作系统的本地父线程直接映射。
操作系统负责所有线程的安排和调度到任何一个可用的CPU上，一旦本地线程初始化成功，它就会调用Java线程中的run（）方法。
守护线程、普通线程，当只剩守护线程时，可以关闭JVM
Hotspot JVM里主要线程
- 虚拟机线程：这种线程的做操作是需要JVM到达安全点才会出现。这些操作必须在不同的线程都到达到安全点，这样堆才不会变化。这种线程的执行类型包括“stop-the-world”的垃圾收集，线程栈收集，线程挂起以及偏向锁撤销。
- 周期任务线程：这种线程是时间周期时间的体现（比如中断）。他们一般用于周期性的调度操作。
- GC线程： 这种线程对在JVM里不同种类的垃圾收集行为提供支持。
- 编译线程：这种线程在运行时会将字字节码编译成本地代码。
- 信号调度线程：这种线程收集信号并发给JVM，在它内部通过调用适当的地方进行处理。


运行时数据区
- PC寄存器（程序计数器）
    - JVM中的PC寄存器是对物理PC寄存器的一种抽象模拟
    - 用来存储指向下一条指令的地址。由执行引擎读取下一条指令
    - 它是一块很小的内存空间，几乎可以忽略不计，也是运行速度最快的内存区域。
    - 每个线程多有它自己的程序计数器，线程私有，声明周期与线程的生命周期保持一致。
    - 任何时间，一个线程都只有一个方法在执行，所谓的当前方法。程序计数器会存储当前线程正在执行的Java方法的JVM指令地址，当执行的为native方法，则是未指定值（undefined）
    - 它是程序控制流的指示器，分支、循环、跳转、异常处理、线程恢复等基础功能需要依赖这个计数器来完成。
    - 字节码解释器工作时就是用过改变这个计数器的值来取下一条需要执行的字节码指令。
    - 它是唯一一个JVM规范中没有规定任何OOM情况的区域。
    - 没有GC
    - 使用PC寄存器存储字节码指令地址有什么用？
        - 因为CPU需要不停的切换各个线程，切回来的时候，需要知道从哪开始继续执行。JVM中的字节码需要通过改变PC寄存器的值，来明确下一步执行什么样的字节码指令。
    - PC寄存器为什么会被设定为线程私有？
        - CPU需要不停切换各个线程，当前只能有一个线程，为了PC寄存器准确记录线程当前的字节码指令地址。最好的办法就是线程私有，每个线程一个。当然寄存器共享的话，也会有其他结构来记录当前状态的。效果是一样的。
- 虚拟机栈
    - 由于跨平台的设计，Java的指令都是根据栈来设计的，不同平台的CPU架构不同，所以不能设计为基于寄存器的。
    - 优点是可以卡平台，指令集下，编译器容易实现。
    - 缺点是性能下降，实现同样的功能需要更多的指令。
    - 栈是运行时单位，堆是存储单位。
    - 每个线程在创建时都会创建一个虚拟机栈，其内部保存一个个的栈帧（Stack Frame），对应着一次次的java方法调试。
    - 线程私有
    - 声明周期与线程一致
    - 主管java程序的运行，保存方法的局部变量（8种基本数据类型、对象的地址（对象在堆中））、部分结果，并参与方法的调用和返回。
    - 一种快速有效的分配存储方式，访问速度仅次于程序计数器
    - 没有GC
    - SOF
        - StackOverFlowError 栈定长，无法插入更多的栈帧了，递归出现
    - OOM
        - java.lang.OutOfMemoryError:Java heap space 
            - 新建对象时 JVM内存不足 new
        - java.lang.OutOfMemoryError:GC overhead limit exceedec 
            - GC回收时间过长时会抛出该异常
            - 过长的定义是，超过98%的时间用来做GC并且回收了不到2%的堆内存
            - 连续多次GC都只回收了不到2%的极端情况下才会抛出。
            - 避免恶性循环 浪费CPU性能
        - java.lang.OutOfMemoryError:Direct buffer memory
            - 写NIO程序时经常使用ByteBuffer来读取或者写入数据，这是一种基于通道（channel）与缓冲区（buffer）的I/O方式，他可以使用Native函数库直接分配堆外内存，然后通过一个存储在Java堆里面的DirectByteBuffer对象作为这块内存的引用操作，这样能在一些场景中显著提高性能，因为避免了在Java堆和Native堆中来回复制数据
            - ByteBuffer.allocate(caoability)第一种方式是分配JVM堆内存，属于GC管辖范围，由于需要拷贝所以速度相对较慢
            - ByteBuffer.allocateDirect(caoability) 第2种方式是分配OS本地内存，不属于GC管辖范围，由于不需要内存拷贝所以速度相对较快。
            - 但如果不断分配本地内存，堆内存很少使用，那么JVM就不需要执行GC，DirectByteBuffer对象们就不会被回收，这时候堆内存充足，但本地内存可能已经使用光了，再次尝试分配本地内存就会出现OOM
        - java.lang.OutOfMemoryError:unable to create new native thread
            - 你的应用创建了太多线程，一个应用进程创建多个线程，超过系统承载极限
            - 你的服务器不允许你的应用程序创建这么多线程，linux系统默认允许单个进程可以创建的线程数是1024个
        - java.lang.OutOfMemoryError:Metaspace
    - -Xss 栈大小 eg：-Xss256k
    - 存储
        - 以栈帧（Stack Farme）的格式存在
        - 每个方法对应一个栈帧
    - 运行原理
        - JVM直接对java栈的操作只有两个：
            - 每个方法执行，伴随着进栈（入栈、压栈）
            - 执行结束后的出栈工作
        - 在一条活动线程中，一个时间点上，只会有一个活动的栈帧。只有当前正在执行的方法的栈帧（栈顶栈帧）是有效的，被称为当前栈帧（Current Frame），与当前栈帧相对应的方法就是当方法（current Method），定义这个方法的的类，就是当前类（Current Class）。
        - 执行引擎运行的所有字节码指令只针对当前栈帧进行操作。
        - 如果在该方法中调用了其他方法，对应新的栈帧会被创建出来，压入栈称为新的当前栈。
        - 不同线程所包含的栈帧是不循序存在相互引用的，即不可能在一个栈帧中引用另外一个线程的栈帧。
        - 如果当前方法调用了其他方法，方法返回之际，当前栈帧会传会此方法的执行结果给前一个栈帧。然后，虚拟机会丢弃当前栈帧，使得之前的栈帧重新成为当前栈帧。
        - java方法有两种返回的方式，无论哪种方式，都会使当前栈帧弹出
            - 正常返回的return
            - 抛出异常
    - 栈帧结构
        - 局部变量表（Local Variables）
        - 操作数栈（Operand Stack）(或表示式栈)
        - 动态链接（Dynamic Linking）(或指向运行时常量池的方法引用)
        - 方法返回地址（Return Address）（或方法正常退出或异常退出的定义）
        - 一些附加信息

方法区和堆区有GC，OOM
栈和本地方法栈有OOM
CPU时间片，分期给各个程序的时间，每个线程被分配一个时间段。


- 内存区域
- 内存溢出

### 垃圾回收
- 垃圾回收算法
- 垃圾回收器
- 垃圾回收过程
- 判断对象已无效

### 性能优化
- 常见问题
- 调优工具
- 优化方案

## 反射
- {% post_link java/basics/20200908 %}

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

## 常用类
- {% post_link java/basics/20200907 %}

## 其他
- {% post_link java/basics/20190416 %}

# 数据结构
- {% post_link dataStructure/20190502 %}
- {% post_link dataStructure/20200525 %}

# 设计模式
设计模式（Design Pattern）是前辈们对代码开发经验的总结，是解决特定问题的一系列套路。它不是语法规定，而是一套用来提高代码可复用性、可维护性、可读性、稳健性以及安全性的解决方案。
1995 年，GoF（Gang of Four，四人组/四人帮）合作出版了《设计模式：可复用面向对象软件的基础》一书，共收录了 23 种设计模式，从此树立了软件设计模式领域的里程碑，人称「GoF设计模式」。
这 23 种设计模式的本质是面向对象设计原则的实际运用，是对类的封装性、继承性和多态性，以及类的关联关系和组合关系的充分理解。
当然，软件设计模式只是一个引导，在实际的软件开发中，必须根据具体的需求来选择：
对于简单的程序，可能写一个简单的算法要比引入某种设计模式更加容易；
但是对于大型项目开发或者框架设计，用设计模式来组织代码显然更好。
- {% post_link designPattern/20210508 %}

# 算法
- {% post_link algorithm/offer/Offer_00 %}
- {% post_link algorithm/20190423 %}

# 数据库
## mysql
- 基础
    - {% post_link database/mysql/20190327 %}
    - {% post_link database/mysql/20190409 %}
    - {% post_link database/mysql/20190424 %}
    - {% post_link database/mysql/20190426 %}
    - {% post_link database/mysql/20200630 %}
    - {% post_link database/mysql/20201021 %}
- 优化
    - {% post_link database/mysql/20191009 %}
- 原理
    - {% post_link database/mysql/20190425 %}
- 报错
    - {% post_link database/mysql/20210615 %}

## orcale
- {% post_link database/orcale/20201102 %}

## redis
- {% post_link database/redis/20210427 %}
- {% post_link database/redis/20190517 %}
- {% post_link database/redis/20190927 %}
- {% post_link database/redis/20200730 %}
- {% post_link database/redis/20200804 %}

## mogondb
- {% post_link database/mongodb/20210427 %}
- {% post_link database/mongodb/20210428 %}

# 工具
## activitymq
- {% post_link tools/activitymq/20190422 %}

## dubbo
- {% post_link tools/dubbo/20190412 %}
- {% post_link tools/dubbo/20190414 %}

## elasticsearch
- {% post_link tools/elasticsearch/20210413 %}

## gateway
- {% post_link tools/gateway/20210617 %}

## git
- {% post_link tools/git/20210506 %}

## hexo
- {% post_link tools/hexo/20180928 %}
- {% post_link tools/hexo/20190328 %}

## idea
- {% post_link tools/idea/20210428 %}

## hibernate

## jdbc
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

## lombok
- {% post_link tools/lombok/20210517 %}

## markdown
- {% post_link tools/markdown/20210427 %}

## maven
- {% post_link tools/maven/20210511 %}

## mybatis
- {% post_link tools/mybatis/20210512 %}
- {% post_link tools/mybatis/20210621 %}

## nacos
- {% post_link tools/nacos/20210616 %}

## spring boot
- {% post_link tools/springboot/20190413 %}
- {% post_link tools/springboot/20190710 %}
- {% post_link tools/springboot/20210427 %}
- {% post_link tools/springboot/20210519 %}
- {% post_link tools/springboot/20210520 %}

###  spring could
- {% post_link tools/springboot/springcould/20210427 %}

## spring framework
- core 
    - {% post_link tools/spring/20200610 %}
    - {% post_link tools/spring/20210511 %}
    - {% post_link tools/spring/20200710 %}
    - {% post_link tools/spring/20210508 %}
- data access/intergration
- web
- test
- 其他
    - {% post_link tools/spring/20190411 %}
    - {% post_link tools/spring/20190421 %}
    - {% post_link tools/spring/20201202 %}

## spring mvc

## tomcat
- {% post_link tools/tomcat/20210413 %}
- {% post_link java/basics/20200608 %}

# 样例代码
- {% post_link demo/20190307 %}

# 正则表达式
# 前端
- {% post_link frontEnd/20210424 %}

# 杂项
- {% post_link daily/20181010 %}
- {% post_link daily/20190313 %}
- {% post_link daily/20190427 %}
- {% post_link daily/20190515 %}
- {% post_link daily/20200622 %}