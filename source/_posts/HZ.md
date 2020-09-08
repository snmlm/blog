---
title: 汇总
date: 2020/09/04
tags: 
    - 汇总
---

<!-- more -->
## java
### 基础类型
{% post_link java/basics/20200508 %}

### 枚举enum
单例模式的一种
### 引用类型
1、{% post_link daily/20200817 String %}
2、数组
3、自定义对象
&nbsp;&nbsp;&nbsp;&nbsp;a、runnable class（）主类（运行类）含有main方法，可以直接执行
&nbsp;&nbsp;&nbsp;&nbsp;b、java bean（） （不含有main方法，构造方法，set get 方法）
&nbsp;&nbsp;&nbsp;&nbsp;c、POJO对象（简单的java对象，只含有set get方法）
### 强引用,软引用,弱引用,虚引用
### 面向对象 
1、封装（维护性）：隐藏成员变量和方法，隐藏共能实现的具体细节
2、继承（可扩展性）：子类继承父类的变量或者方法，也可以定义自己的 {% post_link daily/20200701 %}
3、多态（灵活性）：父类的引用指向子类的实力（上转型对象）
### 运算符
1、位运算符
&nbsp;&nbsp;&nbsp;&nbsp;位运算在java速度是最快的
2、运算符优先级，{% post_link daily/20190507 %}
### 循环
1、for
2、foreach
3、do while
4、while
5、递归
&nbsp;&nbsp;&nbsp;&nbsp;a、构造方法不能递归、
&nbsp;&nbsp;&nbsp;&nbsp;b、必须有出口，if判断，否则死循环（肯定内存溢出）
&nbsp;&nbsp;&nbsp;&nbsp;c、次数不易过多，否则会出现内存溢出
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;递归解决问题的思想：（大->小）,将大问题拆成小问题
6、goto(无用，字段保留)
### 关键字
1、transient（在对象序列化的时候，如果某个属性不想被序列化就是该关键字修饰）
2、abstract：
&nbsp;&nbsp;&nbsp;&nbsp;a、修饰类（被他修饰的类为抽象类）
&nbsp;&nbsp;&nbsp;&nbsp;b、修饰方法（权限：public protected，抽象方法不能有方法体）
3、final：
&nbsp;&nbsp;&nbsp;&nbsp;a、修饰类：不能有子类
&nbsp;&nbsp;&nbsp;&nbsp;b、修饰方法：不能被重写 （不能修饰抽象方法）
&nbsp;&nbsp;&nbsp;&nbsp;c、修饰变量：常量（要赋初始值）
&nbsp;&nbsp;&nbsp;&nbsp;d、finally {% post_link daily/20200702 %}
&nbsp;&nbsp;&nbsp;&nbsp;e、finalize() {% post_link daily/GcAndFinalize %}
4、implements：实现接口
5、static：
&nbsp;&nbsp;&nbsp;&nbsp;a、修饰类：（内部类）
&nbsp;&nbsp;&nbsp;&nbsp;b、静态变量是属于类的，对象共享
&nbsp;&nbsp;&nbsp;&nbsp;c、修饰方法：静态方法只能调用的静态的东西
6、instanceof：
&nbsp;&nbsp;&nbsp;&nbsp;a instanceof A：判断对象a是不是类A及其子类创建的实力
### 对象的序列化和反序列化
1、序列化：将对象以二进制的形式存储到硬盘中
2、反序列化：将以二进制形式的对象读取到内存中
要求：被序列化的对象必须要实现Serializable（标记接口）接口
transient标记不被序列化的字段，SerializableID没有的话，反序列化会失败
### 泛型
1、泛型类
2、泛型接口
3、泛型方法
4、泛型引用
&nbsp;&nbsp;&nbsp;&nbsp;a、extends
&nbsp;&nbsp;&nbsp;&nbsp;b、supper
### Collection&lt;E&gt;
1、List
&nbsp;&nbsp;&nbsp;&nbsp;a、ArrayList：实现了RandomAccess接口，for循环比foreach快，数组实现，无参构造，初始0，add的时候才会初始为10，阀值是当前上限，扩充为x+(x>>1)，约为1.5倍，有参构造跟0比较，大于0，初始填值，小于0，报错IllegalArgumentException，remove的时候注意数据移动，倒叙删除，迭代器，转Set，{% post_link daily/20190417 %}
&nbsp;&nbsp;&nbsp;&nbsp;b、Linkedlist：双向链表实现
2、Set
&nbsp;&nbsp;&nbsp;&nbsp;a、HashSet：对象必须重写hashCode方法，对象必须重写equals方法，链表实现
&nbsp;&nbsp;&nbsp;&nbsp;b、TreeSet：对象必须实现Comparable接口的子类型，二叉树实现
3、Queue
&nbsp;&nbsp;&nbsp;&nbsp;没有实现的阻塞接口的LinkedList：实现了java.util.Queue接口和java.util.AbstractQueue接口
### Map&lt;K,V&gt;
1、HashMap
&nbsp;&nbsp;&nbsp;&nbsp;{% post_link daily/20190501 %}
2、TreeMap
&nbsp;&nbsp;&nbsp;&nbsp;自带红黑树（R-B tree）
### 工具类
1、Arrays
&nbsp;&nbsp;&nbsp;&nbsp;对数组的工具类
2、Collections（实现Collection的集合）
&nbsp;&nbsp;&nbsp;&nbsp;a、binarySearch-折半查找
&nbsp;&nbsp;&nbsp;&nbsp;b、sort-排序，集合实现Comparable接口，默认ascll码比较。可重写Comparator
&nbsp;&nbsp;&nbsp;&nbsp;c、copy-浅拷贝
&nbsp;&nbsp;&nbsp;&nbsp;d、emptyXXX()-得到空容器
&nbsp;&nbsp;&nbsp;&nbsp;e、max/min-获取最大/小元素，集合实现Comparable接口，默认ascll码比较。可重写Comparator
&nbsp;&nbsp;&nbsp;&nbsp;f、replaceAll-新值替换旧值
&nbsp;&nbsp;&nbsp;&nbsp;g、reverse-反转，集合实现Comparable接口，默认ascll码比较。可重写Comparator
&nbsp;&nbsp;&nbsp;&nbsp;h、shuffle-随机乱序，实现用Random，伪随机，真随机可以参考时间
&nbsp;&nbsp;&nbsp;&nbsp;i、syncronizedXXX-将线程不安全集合变成线程安全集合，装潢模式，创建一个syncronizedXXX新对象，内容指向原数据，所有方法添加syncronized关键字。常用于arraylist
&nbsp;&nbsp;&nbsp;&nbsp;j、unmodifiableXXX-将可以修改的容器变成不可变容器，不变模式，创建一个unmodifiableXXX新对象，内容指向原数据，新对象所有修改数据的方法直接返回异常UnsupportedOperationException。常用于arraylist
### 其他容器
1、Vector
&nbsp;&nbsp;&nbsp;&nbsp;Stack以Vector实现
2、Dictonary
&nbsp;&nbsp;&nbsp;&nbsp;已被map替代，过时接口。使用时必须静态使用
3、BitSet
&nbsp;&nbsp;&nbsp;&nbsp;long数组实现。不能存重复数据，按位处理。
### 类加载
1、类加载器（ClassLoader）
&nbsp;&nbsp;&nbsp;&nbsp;a、加载：通过一个类的全限定名获取该类的二进制流，将该二进制流中的静态存储结构转化为方法去运行时数据结构，在内存中生成该类的 Class 对象，作为该类的数据访问入口
&nbsp;&nbsp;&nbsp;&nbsp;b、加载
&nbsp;&nbsp;&nbsp;&nbsp;c、连接-验证：文件格式验证：验证字节流是否符合 Class 文件的规范，元数据验证:对字节码描述的信息进行语义分析，字节码验证：是整个验证过程中最复杂的一个阶段，通过验证数据流和控制流的分析，确定程序语义是否正确，主要针对方法体的验证，符号引用验证：这个动作在后面的解析过程中发生，主要是为了确保解析动作能正确执行
&nbsp;&nbsp;&nbsp;&nbsp;d、连接-准备：准备阶段是为类的静态变量分配内存并将其初始化为默认值，这些内存都将在方法区中进行分配。准备阶段不分配类中的实例变量的内存，实例变量将会在对象实例化时随着对象一起分配在 
&nbsp;&nbsp;&nbsp;&nbsp;e、连接-解析：该阶段主要完成符号引用到直接引用的转换动作。解析动作并不一定在初始化动作完成之前，也有可能在初始化之后
&nbsp;&nbsp;&nbsp;&nbsp;f、初始化：初始化时类加载的最后一步，前面的类加载过程，除了在加载阶段用户应用程序可以通过自定义类加载器参与之外，其余动作完全由虚拟机主导和控制。到了初始化阶段，才真正开始执行类中定义的Java 
&nbsp;&nbsp;&nbsp;&nbsp;g、使用
&nbsp;&nbsp;&nbsp;&nbsp;h、卸载：停止之后，自动卸载。
2、PDM（父亲委托机制）
&nbsp;&nbsp;&nbsp;&nbsp;a、根加载器
&nbsp;&nbsp;&nbsp;&nbsp;b、扩展加载器
&nbsp;&nbsp;&nbsp;&nbsp;c、系统加载器
3、获取Class对象方式
&nbsp;&nbsp;&nbsp;&nbsp;a、类.class
&nbsp;&nbsp;&nbsp;&nbsp;b、对象.getClass()
&nbsp;&nbsp;&nbsp;&nbsp;c、Class.forName("类的完全限定名")
### 反射
1、Class类操作
&nbsp;&nbsp;&nbsp;&nbsp;a、asSubclass(Class<U>clazz)-把传递的类的对象转换成代表其子类的对象
&nbsp;&nbsp;&nbsp;&nbsp;b、Cast-把对象转换成代表类或是接口的对象
&nbsp;&nbsp;&nbsp;&nbsp;c、getClassLoader()-获得类的加载器
&nbsp;&nbsp;&nbsp;&nbsp;d、getClasses()-返回一个数组，数组中包含该类中所有公共类和接口类的对象
&nbsp;&nbsp;&nbsp;&nbsp;e、getDeclaredClasses()-返回一个数组，数组中包含该类中所有类和接口类的对象
&nbsp;&nbsp;&nbsp;&nbsp;f、getName()-获得类的完整路径名字
&nbsp;&nbsp;&nbsp;&nbsp;g、getPackage()-获得类的包
&nbsp;&nbsp;&nbsp;&nbsp;h、getSimpleName()-获得类的名字
&nbsp;&nbsp;&nbsp;&nbsp;i、getSuperclass()-获得当前类继承的父类的名字
&nbsp;&nbsp;&nbsp;&nbsp;j、getInterfaces()-获得当前类实现的类或是接口
&nbsp;&nbsp;&nbsp;&nbsp;k、forName(String className)-根据类名返回类的对象
&nbsp;&nbsp;&nbsp;&nbsp;l、newInstance()-创建类的实例
2、Constructor类
&nbsp;&nbsp;&nbsp;&nbsp;newInstance(Object...args)
3、Field类
&nbsp;&nbsp;&nbsp;&nbsp;set(Object obj，Object value)
4、Method类
&nbsp;&nbsp;&nbsp;&nbsp;invoke(Object obj，Object...args)
### XML
1、解析方式
&nbsp;&nbsp;&nbsp;&nbsp;a、SAX
&nbsp;&nbsp;&nbsp;&nbsp;b、DOM
&nbsp;&nbsp;&nbsp;&nbsp;c、St
2、dom4j
### 异常
1、实现Throwable
&nbsp;&nbsp;&nbsp;&nbsp;a、Error
&nbsp;&nbsp;&nbsp;&nbsp;b、Exception
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1、检查异常
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2、RuntimeException
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3、自定义异常，继承Exception或其子类
### I/O
1、两种设计模式
2、字节流
3、字符流
4、BIO（blocking I/O）-同步并堵塞
5、NIO（no-blocking I/O）同步非堵塞
6、AIO（NIO2）（Asynchronous I/O）异步非堵塞
## 数据结构
### 排序
{% post_link daily/20190423 %}
# 数据库
# 框架