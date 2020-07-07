---
title: java Object
date: 2018/10/10
url: \2018\10\10\JavaObject
categories: 源码
tags: 
	- java
---
 <meta name="referrer" content="no-referrer" />

## Object
Object类，所有类的父类，也成超级类。
在java.lang包下
java.lang包包含着Java最基础和核心的类，在编译时会自动导入。
<!-- more -->
Object类没有定义属性，一共有13个方法
### public Object();

* Java中规定：在类定义过程中，对于未定义构造函数的类，默认会有一个无参数的构造函数，作为所有类的基类，Object类自然要反映出此特性，在源码中，未给出Object类构造函数定义，但实际上，此构造函数是存在的。

### private static native void registerNatives();

* `registerNatives`函数前面有`native`关键字修饰，Java中，用`native`关键字修饰的函数表明该方法的实现并不是在Java中去完成，而是由C/C++去完成，并被编译成了.dll，由Java去调用。例如：对于`java.lang.Object.registerNatives`，对应的C函数命名为`Java_java_lang_Object_registerNatives`。
* 也就是说`registerNatives`的方法在C/C++的dll中，jvm运行后，`registerNatives`的实体方法会映射到java中，并在java中使用，但是本方法是私有静态的，无法子类继承去实现调用，所以在这句代码后有一个静态代码块去调用：

```
static {
        registerNatives();
 }
```

* 为了加深对java本地方法的理解，在网上找到了该方法的C源码部分，如下：

```
static JNINativeMethod methods[] = 
{
    {"hashCode",    "()I",                    (void *)&JVM_IHashCode},
    {"wait",        "(J)V",                   (void *)&JVM_MonitorWait},
    {"notify",      "()V",                    (void *)&JVM_MonitorNotify},
    {"notifyAll",   "()V",                    (void *)&JVM_MonitorNotifyAll},
    {"clone",       "()Ljava/lang/Object;",   (void *)&JVM_Clone},
};

JNIEXPORT void JNICALL
Java_java_lang_Object_registerNatives(JNIEnv *env, jclass cls)
{
    (*env)->RegisterNatives(env, cls,methods, sizeof(methods)/sizeof(methods[0]
}
```

* 因为要用`registerNatives`去初始化其他方法，做对应的映射。这样理解起来会更容易。

### protected native Object clone() throws CloneNotSupportedException;

* `clone`也是一个`native`方法，可以知道`clone`不是一个原生方法。
* Java术语表述为：`clone`函数返回的是一个引用，指向的是新的`clone`出来的对象，此对象与原对象分别占用不同的堆空间。
* `clone`运用的时候存在问题，`object`的`clone()`方法直接是调用不了的，提示出`The method clone() from the type Object is not visible`
（类型对象的方法克隆（）不可见），子类直接调用`clone`的话，虽然能调用，但是会报错`CloneNotSupportedException`，意为无法支持拷贝，子类必须继承`Cloneable`接口才行。
* `Cloneable`接口是一个标记接口，接口内无任何方法，跟变量。

> 拷贝有深拷贝和浅拷贝之分：
深拷贝是对象中的所有东西进行拷贝，拷贝对象内的非基本类型的属性，并不是指向同一引用，而是创建了新对象。
浅拷贝中的非基本类型的对象，指向的是同一引用。

* 拷贝时需实现`Cloneable`接口，并重写`clone`方法，根据方法写的编写的功能，实现浅拷贝和深拷贝。
* 由于native方法的效率一般来说都是远高于java的非`native`方法，这也解释了为什么要用`clone`方法，而不是先`new`一个对象，然后把对象进行赋值，虽然也算是实现了拷贝。

### public final native Class<?> getClass();

* `getClass()`也是一个native方法，返回的是此`Object`对象的类对象/运行时类对象`Class<?>`。效果与`Object.class`相同。
* 首先解释下"类对象"的概念：在Java中，类是是对具有一组相同特征或行为的实例的抽象并进行描述，对象则是此类所描述的特征或行为的具体实例。作为概念层次的类，其本身也具有某些共同的特性，如都具有类名称、由类加载器去加载，都具有包，具有父类，属性和方法等。于是，Java中有专门定义了一个类，`Class`，去描述其他类所具有的这些特性，因此，从此角度去看，类本身也都是属于`Class`类的对象。为与经常意义上的对象相区分，在此称之为"类对象"。

### public boolean equals(Object obj);

* 在object中看来，`==`和`equals`没区别。

```
public boolean equals(Object obj){
    return (this == obj);
}
```

* `==`是比较引用或者是地址，`equals`是比较内容。比较片面，这个要看具体的比较规则，重写此方法。

### public native int hashCode();

* 即严格的数学逻辑表示为： 两个对象相等 <=>  `equals()`相等  => `hashCode()`相等。因此，重写`equlas()`方法必须重写`hashCode()`方法，以保证此逻辑严格成立，同时可以推理出：`hasCode()`不相等 => `equals()`不相等 <=> 两个对象不相等。

> 其中`hesCode()`相等推不出`equals()`相等

* 用于集合中遍历，不需要重头到尾遍历，减少遍历时间。

### public String toString();
toString()方法相信大家都经常用到，即使没有显式调用，但当我们使用System.out.println(obj)时，其内部也是通过toString()来实现的。
getClass()返回对象的类对象，getClassName()以String形式返回类对象的名称（含包名）。Integer.toHexString(hashCode())则是以对象的哈希码为实参，以16进制无符号整数形式返回此哈希码的字符串表示形式。

### public final native void notify();

* 随机选择一个在该对象上调用wait方法的线程，解除其阻塞状态。该方法只能在同步方法或同步块内部调用。如果当前线程不是锁的持有者，该方法抛出一个`IllegalMonitorStateException`异常。

### public final native void notifyAll();

* 解除所有那些在该对象上调用wait方法的线程的阻塞状态。该方法只能在同步方法或同步块内部调用。如果当前线程不是锁的持有者，该方法抛出一个`IllegalMonitorStateException`异常。

### public final void wait() throws InterruptedException;

* 此方法调用`public final native void wait(long timeout) throws InterruptedException`

```
public final void wait() throws InterruptedException {
    wait(0);
}
```
### public final native void wait(long timeout) throws InterruptedException;

* 等待时间为毫秒级。

### public final void wait(long timeout,int nanos) throws InterruptedException;

* 等待时间为毫秒级，`nanos`为附加时间，如果附加时间不在0-999999之间或`timeout`小于0，都会抛出`InterruptedException`异常，最终的停止时间为`time`+1;

```
public final void wait(long timeout, int nanos) throws InterruptedException {
    if (timeout < 0) {
        throw new IllegalArgumentException("timeout value is negative");
    }
    if (nanos < 0 || nanos > 999999) {
        throw new IllegalArgumentException("nanosecond timeout value out of range");
    }
    if (nanos > 0) {
        timeout++;
    }
    wait(timeout);
}
```

### proteced void finalize();
可以看一下[sysout.gc()和finalize的区别](/2018/10/11/GcAndFinalize)

* 用于销毁或者说是回收资源



