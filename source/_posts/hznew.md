---
title: 汇总
date: 2024/01/29
sticky: 99
tags: 
    - 脑图
---

# 计算机原理基础
## 计算机基础原理
### CPU/内存/硬盘
### 软硬件关联
### 计算机内核原理
## Windows系统介绍
### 环境变量
### PATH/CLASSPATH
### DOS命令
## 虚拟机安装与使用
### VMWARE
### Linux Centos7安装
## Linux系统介绍
### 进程/文件命令
### 网络安全命令
### shell命令
## 网络通信介绍
### 网络分层
### 网络基础知识
### TCP
### UDP
### HTTP
### Socket
# JAVA核心基础（JAVA SE）
## 开发环境准备
### Java语言发展史
### JDk的下载与安装
### Path环境变量的配置
## Java入门语法
### HelloWorld
### 基本数据类型
### 常量
### 变量
### 数据类型转换
### 操作符
### 流控制
#### if
#### switch
#### for
#### 三元
#### while
#### do while
#### 递归
### 面对对象核心
#### 类和对象
#### 方法
#### 可变参数
#### 访问修饰符
#### this
#### super
#### 三大特性
##### 封装
##### 继承
##### 多态
### 异常
#### try catch finally
#### throws
#### throwable
#### exception error
#### 自定义异常
### 数组
#### 数组初始化
#### 多维数组
### 系统类
#### 基本类型包装类
#### String StringBuilder StringBufer
#### 日期类
#### Date LocalTime Dalendar
#### SimpleDateFormat
#### BigDecimal
#### System
#### 值传递和地址传递
### 集合和泛型
#### 迭代器
#### 泛型
#### List
##### ArrayList
##### LinkedList
#### Set
##### HashSet
##### TreeSet
#### Map
##### HashMap
##### TreeMap
#### Queue
#### Deque
#### Collections工具
### 线程
#### 进程与线程
#### 并行与串行
#### 多线程实现
##### Thread
##### Runnable
##### 线程池 Executors
###### 概念
###### 使用
#### 常用API
##### 设置优先级
##### 线程休眠
##### 线程让步
##### 线程重点
##### 线程中断
##### 线程守护
#### 线程生命周期
#### 线程安全性
##### 线程安全问题
##### 同步代码块
##### 同步方式
##### Lock锁
#### 并发容器 Concurrent包下
##### ConcurrentHashMap
##### CopyOnWriteArrayList
##### CopyOnWriteArraySet
#### 原子操作
##### 基本类型
###### AtomicInterger
###### AtomicLong
###### AtomicBoolean
##### 数组
###### AtomicIntergerArray
###### AtomicLongArray
###### AtomicReferenceArray
##### 引用类型
###### AtomicReference
###### AtomicReferenceFieldUpdater
###### AtomicMarkableReference
##### 字段类型
###### AtomicIntergerFieldUpdater
###### AtomicLongFieldUpdater
###### AtomicStampedReference
### IO流
#### InputStream
#### OutputStream
#### FileInputStream
#### FileOutputStream
#### FileReader
#### FileWrite
#### BufferInputStream
#### BufferOutputStream
#### 序列化、反序列化
#### Properties
### 反射
#### 反射机制
#### 获取Class
#### 获取方法
#### 获取成员变量
#### 修改变量值
#### 获取注解
### 网络
#### 三要素
##### ip
##### 端口
##### 协议
###### UDP
###### TCP
#### NIO
##### Buffer的使用
##### Channel的使用
##### Selector的使用
#### 自定义非阻塞式的HTTP静态服务器
### JDK7新特性
#### 改进的 switch 语句，支持字符串、枚举类型和数值型数据
#### try-with-resources 语句，自动关闭资源
#### 泛型实例化类型推断
#### 数字字面量可以使用下划线来分隔数字
#### 新增了 Fork/Join 框架，用于并行计算
#### NIO 2.0，支持异步 I/O 操作和文件系统操作
#### 动态语言支持，包括 InvokeDynamic 指令和 JSR 292 等
### JDk8新特性
#### Lambda 表达式，用于函数式编程
#### Stream API，用于处理集合和数组等数据流
#### 接口默认方法和静态方法
#### 新的日期时间 API，取代了旧的 Date 和 Calendar 类
#### Nashorn JavaScript 引擎，替代了 Rhino 引擎
### JDK9新特性
#### 模块化系统，提高了代码可重用性和安全性
#### JShell，交互式命令行工具，用于快速测试和调试代码
#### 改进的 HTTP 客户端，支持 HTTP/2 和 WebSocket
#### 多版本兼容的 JAR 文件，使得在不同版本的 Java 中使用相同的 JAR 文件更加容易
#### 改进的 GC，包括 G1 垃圾回收器
### JDK10新特性
#### 局部变量类型推断，可以使用 var 关键字代替具体类型
#### 改进的 ThreadLocalRandom 类，用于生成伪随机数
#### 废弃了一些不安全的加密算法
#### 安全地存储公私钥对，提高了安全性
### JDK11新特性
#### HTTP/2 标准化，成为默认的 HTTP 客户端实现
#### 改进的字符串 API，包括 strip() 和 repeat() 等方法
#### 新增了本地变量语法，用于声明局部变量
#### 废弃了一些废弃的模块和类
### JDK12新特性
#### 改进的 Switch 语句，支持 Lambda 表达式
#### 新增了一些 String 方法，包括 transform() 和 indent() 等
#### 新增了一个微型 GC，用于优化小堆内存分配的应用程序
### JDK13新特性
#### ZGC 垃圾回收器，支持大内存、低延迟应用程序
#### 改进的 Switch 语句，支持 Yield 语句
#### 改进的文本块语法，用于多行文本字符串
### JDK14新特性
#### 改进的 Switch 语句，支持 Pattern 匹配
#### 新增了 Records 类，用于定义不可变数据类
#### 改进的 NullPointerException 错误信息
### JDK15新特性
#### 改进的 GC，包括 ZGC 和 Shenandoah
#### 新增了 Sealed 类，用于限制继承和实现
#### 新增了 Text Blocks，用于处理多行字符串。
### JDK16新特性
#### 改进的垃圾回收器，包括 ZGC 和 Shenandoah
#### 新增了 Records 的扩展，包括 sealed 和 non-sealed 标注
#### 新增了 Vector API，用于并行计算
### JDK17新特性
#### 基于 OpenJDK 11 的长期支持（LTS）版本
#### 服务提供者接口（SPAPI），取代了旧的类路径扩展机制
#### 基于 CDS 归档的应用程序快照（Application Class-Data Sharing）
#### 改进的 ZGC 和 Shenandoah 垃圾回收器，包括堆外内存分配和统一 MappedByteBuffer 等改进
#### 预计还会包括随机生成器增强、G1 GC 的垃圾回收暂停时间预测等其他改进
#### Sealed Classes(密封类)
### JDK18新特性
#### 默认 UTF-8
#### 简单的 web 服务器
#### 重新实现核心的方法反射
#### 地址解析 SPI
#### java API 文档支持代码片段
#### 矢量 api (孵化)
#### 外部函数和内存 api 二次孵化
#### switch 模式匹配 (第二次预览)
#### ZGC,SerialGC,ParallelGC 支持字符串消除
#### 从 Filer 中传递始发元素(Originating Elements)到 JavaFileManager
#### Charset.forName() 采用默认值回退
#### 引入新的系统属性 java.properties.date
#### Messager 接口添加方法: printError, printWarning, 和 printNote
#### Elements 增加获取最外层元素方法
#### SourceVersion 与 Runtime.Version 朴素映射
#### 提升编译回放
#### 使卡表(card table)的卡片大小可配置
#### 关于卡表
#### 允许 将 G1 的分区大小设置到 512MB
#### JDK Flight Recorder Event for Finalization
#### SunPKCS11 Provider 支持部分 PKCS#11 v3.0 的 API
#### KeyStore 增加新方法 getAttributes
#### keytool 增加新选项 -version
#### PKCS12 KeyStore 保存和加载支持密码为空
#### finalize 方法被弃用
#### 内部类的封闭实例字段被省略
### JDK19新特性
#### Record 模式匹配 (Preview)
#### 虚拟线程 (预览)
#### Switch 模式匹配 (三次预览)
#### Linux/RISC-V Port
#### Vector API (四次孵化)
#### 外部函数 & 内存 API (Preview)
#### Structured Concurrency (Incubator)
# 数据库核心技术
## MySql
### 数据库设计
### 增删改查
### 函数与定义函数
### SQL
#### 多表关系
##### 一对多
##### 多对一
##### 一对一
##### 多对多
#### 多表关联查询
#### 子查询
#### 视图
#### 索引
#### 查询优化
#### 存储过程
#### 游标
#### 事务
#### 触发器
#### 数据结构
##### 二叉树
###### B树
###### B+数
#### 数据引擎
### JDBC
#### JDBC四大核心
#### JDBC的事务控制
#### JDBC的增删改查
#### DBUtils的使用
### 数据库连接池
#### C3P0连接池
#### Durid连接池
# WEB网页技术
## 静态Web基础
### HTML
#### HTML基础使用
#### HTML常用标签
#### HTML5新特性
### CSS
#### CSS选择器
#### 常用样式
#### 盒子模型与布局
#### CSS3新特性
### JavaScirpt
#### JS基本语法
#### 数组
#### 函数
#### 对象
#### js面向对象
#### 常用内置对象
#### js事件绑定、触发
#### jsDOM操作及api
#### jsBOM对象及api
#### ECMA6新特性
##### let&const
##### 结构&字符串
##### 箭头函数
##### 对象优化
##### map，reduce
##### promise异步编排
##### 模块化
### JQuery
#### jq语法
#### jq核心函数
#### jq选择器
#### jqDOM操作
#### jq事件
#### jq动画
#### jq遍历
### Vue.js
#### MVVM思想
#### 指令
#### 计算属性和监听器
#### 组件化
#### 生命周期和钩子函数
#### ajax请求
#### vue-cli
## JAVA EE
### Tomcat
#### 静态资源和动态资源
#### 系统结构 C/S和B/S
#### Tomcat目录
#### Tomcat部署项目
### Servlet
#### 实现
#### 生命周期
#### 线程安全
#### 上下文对象
#### 四大核心
##### Request
##### Response
##### ServletContext
##### ServletConfig
#### Cookie
#### Session
#### JSP
##### JSP语法
##### JSP原理
##### JSP脚本片段&表达式
##### JSP声明&指令
##### JSP九大隐式对象
#### EL表达式
##### 使用
##### 取值原理
##### 11大隐含对象
##### 函数库
#### JSTL
##### JSTL-核心标签库
##### JSTL-函数标签库
#### Filter、Listener
##### Filter原理及配置
##### Filter声明周期
##### Filter登陆验证
##### Listener原理及配置
#### 文件上传和下载
#### commons-io&commons-fileupload实现文件上传
#### 文件下载
##### 直接下载
##### 通过文件流下载
##### 文件下载响应头
##### 文件下载中文乱码&浏览器兼容
# Java后端框架
## Maven
### 配置
### 项目中pom.xml、依赖管理
### 微服务Spring Cloud
### 依赖
### 生命周期
## Git
### 常用操作
## Srping
### IOC
#### XmlClassPathApplicationContext容器
#### bean
#### DI
#### depends-on
#### 懒加载bean
#### 自动注入
#### Bean作用域
#### 生命周期
#### spring创建第三方bean对象
#### spring引用外部配置文件
#### SpEL的使用
#### 常用注解
##### @ComponetScan
##### @Componet
##### @Controller
##### @Service
##### @Repostiry
##### @AutoWired
##### @Resource
##### @Inject
##### @Bean
##### @Configuration
##### @Conditional
##### @Value
### AOP
#### JDK动态代理和CGLIB动态代理
#### AOP切入点表达式
#### 通知方法的执行顺序
#### @Before 在目标方法之前运行 前置通知
#### @After 在目标方法之后运行 后置通知
#### @AfterReturning 在目标方法正常返回之后运行 返回通知
#### @AfterThrowing 在目标方法抛出异常后运行 异常通知
#### @Around 环绕 环绕通知
### 声明式事务
#### Spring Jdbc Template
#### 设置隔离级别（isolation）
#### 事务的传播特性
#### 基于xml的事务配置
## SpringMVC
### SpringMVC实现原理
### 请求处理
#### 请求参数处理
##### @RequestParam
##### @RequestHeader
##### @CookieValue
#### 复杂数据类型处理
##### JavaBean数据绑定
##### 嵌套对象数据绑定
##### 数据、集合绑定
#### 乱码问题的解决
#### 请求映射处理
##### @RequestMapping
##### @GetMapping
##### @PostMapping
##### @PutMapping
##### @DeleteMapping
#### @PathVariable
#### RESTFul
### 静态资源的访问
### 响应处理
#### 视图解析器VIewResolver
#### 视图控制器\<view-controller>
#### Model、Map、ModelMap
#### ModelAndView
#### SpringMVC操作session
##### @SesscionAttribute
##### @SesscionAttributes
##### HttpSession
#### @ModelAttribute
#### SpringMVC的线程安全问题
#### forward实现页面跳转
#### redirect实现页面重定向
#### 重定向和转发的区别
#### 类型转换&数据格式化&数据验证
#### 内置类型转换器
#### 自定义类型转换器
#### 内置数据格式化
#### 数据校验
#### 使用SpringMVC标签库
#### JSON处理
#### @ResponeseBody 响应json
#### @RequestBody 接收json参数
#### 上传
#### MultipartResolver
##### 单个文件上传
##### 多个文件上传
##### 多文件多线程上传
##### 上传磁盘路径显示图片
#### 下载
#### servlet原生下载方式
#### ResponseEntity定制响应内容
#### ResponseEntity实现下载
#### 拦截器
#### 自定义拦截器
#### 拦截器的顺序
#### 拦截器和过滤器的区别
#### 国际化
#### 通过浏览器语言设置国际化
#### 通过超链接来切换国际化
#### 国际化类型转换和验证失败的信息
#### 国际化代码中的内容
#### 异常处理
#### 内置异常处理解析器
#### 统一异常处理
##### @ControllerAdvice
##### @ExceptionHandler
#### JRebel 热部署
### MyBatis
#### 数据库操作框架历程、
#### JDBC
#### DBUtils
#### JDBCTemplate
#### Hibernate
#### Mybatis
#### 配置
#### 日志的配置
#### 全局配置文件
#### MapperXML
#### 参数
#### ${}和#{}的区别
#### javaBean
#### map
#### @Param
#### 返回
#### ResultType
##### pojo
##### Map
##### List
#### ResultMap
#### 高级结果映射
#### 联合查询
#### 嵌套结果
##### 一对多
##### 多对一
#### 嵌套查询
##### 一对多
##### 多对一
#### 延迟查询
#### 动态sql
#### \<if>
#### \<where>
#### \<trim>
#### \<foreach> 
#### \<choose>、\<when>、\<otherwise>
#### \<set>
#### 缓存
#### 一级缓存
#### 二级缓存
##### 缓存的属性
##### 二级缓存的作用范围
##### 整合第三方缓存
#### 逆向工程
#### 分页插件
#### 自定义分页插件
#### PageHelper分页插件使用
#### PageHelper原理
#### SSM框架整合
### aaa 