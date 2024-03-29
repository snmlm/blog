---
title: 手把手教你落地DDD
date: 2023/5/31
tags: 
    - 架构
---

## 1. 前言

常见的 DDD 实现架构有很多种，如经典四层架构、六边形（适配器端口）架构、整洁架构（Clean Architecture）、CQRS 架构等。架构无优劣高下之分，只要熟练掌握就都是合适的架构。本文不会逐个去讲解这些架构，感兴趣的读者可以自行去了解。

本文将带领大家从日常的三层架构出发，精炼推导出我们自己的应用架构，并且将这个应用架构实现为 Maven Archetype，最后使用我们 Archetype 创建一个简单的 CMS 项目作为本文的落地案例。

需要明确的是，本文只是给读者介绍了 DDD 应用架构，还有许多概念没有涉及，例如实体、值对象、聚合、领域事件等，如果读者对完整落地 DDD 感兴趣，可以到本文最后了解更多。



## 2. 应用架构演化

我们很多项目是基于三层架构的，其结构如图：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2ccf1da9c8a148ad91e7c6ce008d981a~tplv-k3u1fbpfcp-zoom-1.image)

我们说三层架构，为什么还画了一层 Model 呢？因为 Model 只是简单的 Java Bean，里面只有数据库表对应的属性，有的应用会将其单独拎出来作为一个
Maven Module，但实际上可以合并到 DAO 层。

接下来我们开始对这个三层架构进行抽象精炼。



### 2.1 第一步、数据模型与 DAO 层合并

为什么数据模型要与 DAO 层合并呢？

首先，数据模型是贫血模型，数据模型中不包含业务逻辑，只作为装载模型属性的容器；

其次，数据模型与数据库表结构的字段是一一对应的，数据模型最主要的应用场景就是 DAO 层用来进行 ORM，给 Service 层返回封装好的数据模型，供 Service 获取模型属性以执行业务；

最后，数据模型的 Class 或者属性字段上，通常带有 ORM 框架的一些注解，跟 DAO 层联系非常紧密，可以认为数据模型就是 DAO 层拿来查询或者持久化数据的，数据模型脱离了 DAO 层，意义不大。



### 2.2 第二步、Service 层抽取业务逻辑

下面是一个常见的 Service 方法的伪代码，既有缓存、数据库的调用，也有实际的业务逻辑，整体过于臃肿，要进行单元测试更是无从下手。

```
public class Service {

    @Transactional
    public void bizLogic(Param param) {

        checkParam(param);//校验不通过则抛出自定义的运行时异常

        Data data = new Data();//或者是mapper.queryOne(param);

        data.setId(param.getId());

        if (condition1 == true) {
            biz1 = biz1(param.getProperty1());
            data.setProperty1(biz1);
        } else {
            biz1 = biz11(param.getProperty1());
            data.setProperty1(biz1);
        }

        if (condition2 == true) {
            biz2 = biz2(param.getProperty2());
            data.setProperty2(biz2);
        } else {
            biz2 = biz22(param.getProperty2());
            data.setProperty2(biz2);
        }

        //省略一堆set方法
        mapper.updateXXXById(data);
    }
}
```

这是典型的事务脚本的代码：先做参数校验，然后通过 biz1、biz2 等子方法做业务，并将其结果通过一堆 Set 方法设置到数据模型中，再将数据模型更新到数据库。

由于所有的业务逻辑都在 Service 方法中，造成 Service 方法非常臃肿，Service 需要了解所有的业务规则，并且要清楚如何将基础设施串起来。同样的一条规则，例如 if (condition1=true)，很有可能在每个方法里面都出现。

专业的事情就该让专业的人干，既然业务逻辑是跟具体的业务场景相关的，我们想办法把业务逻辑提取出来，形成一个模型，让这个模型的对象去执行具体的业务逻辑。这样 Service 方法就不用再关心里面的 if/else 业务规则，只需要通过业务模型执行业务逻辑，并提供基础设施完成用例即可。

将业务逻辑抽象成模型，这样的模型就是领域模型。

要操作领域模型，必须先获得领域模型，但此时我们先不管领域模型怎么得到，假设是通过 `loadDomain` 方法获得的。通过 Service 方法的入参，我们调用 `loadDomain` 方法得到一个模型，我们让这个模型去做业务逻辑，最后执行的结果也都在模型里，我们再将模型回写数据库。当然，怎么写数据库的我们也先不管，假设是通过 `saveDomain` 方法。

Service 层的方法经过抽取之后，将得到如下的伪代码：

```
public class Service {

    public void bizLogic(Param param) {

        //如果校验不通过，则抛一个运行时异常
        checkParam(param);
        //加载模型
        Domain domain = loadDomain(param);
        //调用外部服务取值
	    SomeValue someValue=this.getSomeValueFromOtherService(param.getProperty2());
        //模型自己去做业务逻辑，Service不关心模型内部的业务规则
        domain.doBusinessLogic(param.getProperty1(), someValue);
        //保存模型
        saveDomain(domain);
    }
}
```

根据代码，我们已经将业务逻辑抽取出来了，领域相关的业务规则封闭在领域模型内部。此时 Service 方法非常直观，就是获取模型、执行业务逻辑、保存模型，再协调基础设施完成其余的操作。

抽取完领域模型后，我们工程的结构如下图：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/56d98269753846f7bee9957a4f226101~tplv-k3u1fbpfcp-zoom-1.image)



### 2.3 第三步、维护领域对象生命周期

在上一步中，`loadDomain`、`saveDomain` 这两个方法还没有得到讨论，这两个方法跟领域对象的生命周期息息相关。

关于领域对象的生命周期的详细知识，读者可以自行学习了解。

不管是 loadDomain 还是 saveDomain，我们一般都要依赖于数据库，所以这两个方法对应的逻辑，肯定是要跟 DAO 产生联系的。

保存或者加载领域模型，我们可以抽象成一种组件，通过这种组件进行封装模型加载、保存的操作，这种组件就是 Repository。

注意，Repository 是对加载或者保存领域模型（这里指的是聚合根，因为只有聚合根才会有 Repository）的抽象，必须对上层屏蔽领域模型持久化的细节，因此其方法的入参或者出参，一定是基本数据类型或者领域模型，不能是数据库表对应的数据模型。

以下是 Repository 的伪代码：

```
public interface DomainRepository {

    void save(AggregateRoot root);

    AggregateRoot load(EntityId id);
}
```

接下来我们要考虑在哪里实现 `DomainRepository`。既然 DomainRepository 与底层数据库有关联，但是我们现在 DAO 层并没有引入 Domain 这个包，DAO 层自然无法提供 DomainRepository 的实现，我们初步考虑是不是可以将 DomainRepository 实现在 Service 层。

但是，如果我们在 Service 中实现 DomainRepository，势必需要在 Service 层操作数据模型：查询出来数据模型再封装为领域模型、或者将领域模型转为数据模型再通过 ORM 保存，这个过程不该是 Service 层关心的。

因此，我们决定在 DAO 层直接引入 Domain 包，并在 DAO 层提供 DomainRepository 接口的实现，DAO 层查询出数据模型之后，封装成领域模型供 DomainRepository 返回。

这样调整之后， DAO 层不再向 Service 返回数据模型，而是返回领域模型，这就隐藏了数据库交互的细节，我们也把 DAO 层换个名字称之为 Repository。

现在，我们项目的架构图是这样的了：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/59fa52edc0344b32adf589fbb6339b80~tplv-k3u1fbpfcp-zoom-1.image)

> 由于数据模型属于贫血模型，自身没有业务逻辑，并且只有 Repository 这个包会用到，因此我们将之合并到 Repository 中，接下来不再单独列举。



### 2.4 第四步、泛化抽象

在第三步中，我们的架构图已经跟经典四层架构非常相似了，我们再对某些层进行泛化抽象。

- Infrastructure

Repository 仓储层其实属于基础设施层，只不过其职责是持久化和加载聚合，所以，我们将 Repository 层改名为 `infrastructure-persistence`，可以理解为基础设施层持久化包。

之所以采取这种 infrastructure-XXX 的格式进行命名，是由于 Infrastructure 可能会有很多的包，分别提供不同的基础设施支持。

例如：一般的项目，还有可能需要引入缓存，我们就可以再加一个包，名字叫 `infrastructure-cache`。

对于外部的调用，DDD 中有防腐层的概念，将外部模型通过防腐层进行隔离，避免污染本地上下文的领域模型。我们使用入口（Gateway）来封装对外部系统或资源的访问（详细见《企业应用架构模式》，18.1 入口（Gateway）），因此将对外调用这一层称之为 `infrastructure-gateway`。

> 注意：Infrastructure 层的门面接口都应先在 Domain 层定义，其方法的入参、出参，都应该是领域模型（实体、值对象）或者基本类型。

- User Interface

Controller 层其实就是用户接口层，即 User Interface 层，我们在项目简称 ui。当然了可能很多开发者会觉得叫 UI 好像很别扭，认为 UI 就是 UI 设计师设计的图形界面。

Controller 层的名字有很多，有的叫 Rest，有的叫 Resource，考虑到我们这一层不只是有 Rest 接口，还可能还有一系列 Web 相关的拦截器，所以我一般称之为 Web。因此，我们将其改名为 ui-web，即用户接口层的 Web 包。

同样，我们可能会有很多的用户接口，但是他们通过不同的协议对外提供服务，因而被划分到不同的包中。

我们如果有对外提供的 RPC 服务，那么其服务实现类所在的包就可以命名为 `ui-provider`。

有时候引入某个中间件会同时增加 Infrastructure 和 User Interface。

例如，如果引入 Kafka 就需要考虑一下，如果是给 Service 层提供调用的，例如逻辑执行完发送消息通知下游，那么我们再加一个包 `infrastructure-publisher`；如果是消费 Kafka 的消息，然后调用 Service 层执行业务逻辑的，那么就可以命名为 `ui-subscriber`。

- Application

至此，Service 层目前已经没有业务逻辑了，业务逻辑都在 Domain 层去执行了，Service 只是协调领域模型、基础设施层完成业务逻辑。

所以，我们把 Service 层改名为 `Application Service` 层。

经过第四步的抽象，其架构图为：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ffe366c738a1468fbfd7095e01dcb43a~tplv-k3u1fbpfcp-zoom-1.image)



### 2.5 第五步、完整的包结构

我们继续对第四步中出现的包进行整理，此时还需要考虑一个问题，我们的启动类应该放在哪里？

由于有很多的 User Interface，所以启动类放在任意一个 User Interface 中都不合适，放置在 Application Service 中也不合适，因此，启动类应该存放在单独的模块中。又因为 application 这个名字被应用层占用了，所以将启动类所在的模块命名为 launcher，一个项目可以存在多个 launcher，按需引用 User Interface。

加入启动包，我们就得到了完整的 maven 包结构。

包结构如图所示：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4027144f9524fa7b81dbc0dc9042bd2~tplv-k3u1fbpfcp-zoom-1.image)

至此，DDD 项目的整体结构基本讲完了。



### 2.6 精炼后的思考

在经过前面五步精炼得到这个架构图中，经典四层架构的四层都出现了，而且长得跟六边形架构也很像。这是为什么呢？

其实，不管是经典四层架构、还是六边形架构，亦或者整洁架构，都是对系统应用的描述，也许描述的侧重点不一样，但是描述的是同一个事物。既然描述的是同一个事物，长得像才是理所当然的，不可能只是换一个描述方式，系统就从根本上发生了改变。

对于任何一个应用，都可以看成 “输入 - 处理 - 输出” 的过程。

“输入” 环节：通过某种协议对外暴露领域的能力，这些协议可能是 REST、可能是 RPC、可能是 MQ 的订阅者，也可能是 WebSocket，也可能是一些任务调度的 Task；

” 处理 “环节：处理环节是整个应用的核心，代表了应用具备的核心能力，是应用的价值所在，应用在这个环节执行业务逻辑，贫血模型由 Service 执行业务处理，充血模型则是由模型进行业务处理。

“输出” 环节，业务逻辑执行完成之后将结果输出到外部。

不管我们采用的什么架构，其描述的应用的核心都是这个过程，不必生搬硬套非得用什么应用架构。

正如《金刚经》所言：一切有为法，如梦幻泡影，如露亦如电，应作如是观；凡所有相，皆是虚妄；若见诸相非相，即见如来。



## 3. ddd-archetype



### 3.1 Maven Archetype 介绍

Maven Archetype 是一个 Maven 插件，可以帮助开发人员快速创建项目的基础结构，大大减少开发人员在创建项目时所需的时间和精力，并且可以确保项目结构的一致性和可重用性，从而提高代码质量和可维护性。

我们在介绍 DDD 应用架构时，对项目的结构进行了介绍。我们将项目分为多个 Maven Module，如果每个项目都手工创建一次，是比较繁琐的工作，也不利项目结构的统一。

我们使用 Maven Archetype 创建 DDD 项目初始化的脚手架，使其在初始化时完整实现上文第五步的应用架构。



### 3.2 ddd-archetype 的使用



#### 3.2.1 项目介绍

ddd-archetype 是一个 Maven Archetype 的原型工程，我们将其克隆到本地之后，可以安装为 Maven Archetype，帮助我们快速创建 DDD 项目脚手架。

项目链接：

```
https://github.com/feiniaojin/ddd-archetype
```



#### 3.2.2 安装过程

以下将以 IDEA 为例展示 ddd-archetype 的安装使用过程，主要过程是：

```
克隆项目` -->`archetype:create-from-project`-->`install`-->`archetype:crawl
```



#### 3.2.3 克隆项目

将项目克隆到本地：

```
git clone https://github.com/feiniaojin/ddd-archetype.git
```

直接使用主分支即可，然后使用 IDEA 打开该项目

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/901e420a433645019866bacc98ce945d~tplv-k3u1fbpfcp-zoom-1.image)



#### 3.2.4 archetype:create-from-project

配置打开 IDEA 的 `run/debug configurations` 窗口，如下：
![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b6204621f6804aa78266f7c85f6ee738~tplv-k3u1fbpfcp-zoom-1.image)

选择 `add new configurations`，弹出以下窗口：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a2b0c92102ff4fd08297fb4f58f0f5f2~tplv-k3u1fbpfcp-zoom-1.image)

其中，上图中 1～4 各个标识的值为：

标识 `1` - 选择 "+" 号；

标识 `2` - 选择 "Maven";

标识 `3` - 命令为：

```
archetype:create-from-project -Darchetype.properties=archetype.properties
```

> 注意，在 IDEA 中添加的命令默认不需要加 mvn

标识 `4` - 选择 `ddd-archetype` 的根目录

以上配置完成后，点击执行该命令。



#### 3.2.5 install

上一步执行完成且无报错之后，配置 `install` 命令。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/097a3de912bb47ee9421e349d22bbe67~tplv-k3u1fbpfcp-zoom-1.image)

其中，上图中 1～2 各个标识的值为：

标识 `1` - 值为 `install`；

标识 `2` - 值为上一步运行的结果，路径为：

```
ddd-archetype/target/generated-sources/archetype
```

`install` 配置完成之后，点击执行。



#### 3.2.6 archetype:crawl

`install` 执行完成且无报错，接着配置 `archetype:crawl` 命令。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5fffdf6cdb294cad8d45d93cea61a6d5~tplv-k3u1fbpfcp-zoom-1.image)

其中，标识 1 中的值为：

```
archetype:crawl
```

配置完成，点击执行即可。



### 3.3 使用 ddd-archetype 初始化项目

- 创建项目时，点击 `manage catalogs`：
    ![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0052122d025648d3b3e4bc1b28051ed0~tplv-k3u1fbpfcp-zoom-1.image)
- 将本地的 maven 私服中的 `archetype-catalog.xml` 加入到 catalogs 中：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5e80d4d547f943718d5d8d7c444ed239~tplv-k3u1fbpfcp-zoom-1.image)

添加成功，如下：
![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/daa47804e3194a7ea66f9c22bac2ddd8~tplv-k3u1fbpfcp-zoom-1.image)

- 创建项目时，选择本地 archetype-catalog，并且选择 `ddd-archetype`，填入项目信息并创建项目：
    ![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3558d5adc57642c99bbde1b852f57a4f~tplv-k3u1fbpfcp-zoom-1.image)
- 项目创建完成后：
    ![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f48d56d0bd1b43b3b4e2e51c62101fd4~tplv-k3u1fbpfcp-zoom-1.image)



## 4. 代码案例

本文提供了配套的代码案例，该案例使用 DDD 和本文的应用架构实现了简单的 CMS 系统。案例项目采用前后端分离的方式，因此有后端和前端两个代码库。



### 4.1 后端

后端项目使用本文的 `ddd-archetype` 创建，实现了部分 CMS 的功能，并落地部分 DDD 的概念。

GitHub 链接：[https://github.com/feiniaojin/ddd-example-cms](https://www.oschina.net/action/GoToLink?url=https%3A%2F%2Fgithub.com%2Ffeiniaojin%2Fddd-example-cms)

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b1033102259e4e2aa6c7a7231b0253e6~tplv-k3u1fbpfcp-zoom-1.image)

实现的 DDD 概念有：实体、值对象、聚合根、Factory、Repository、CQRS。

技术栈：

- Spring Boot
- H2 内存数据库
- Spring Data JDBC

无外部中间件依赖 ，clone 到本地即可编译运行，非常方便。



### 4.2 前端

前端项目基于 `vue-element-admin` 开发，详细安装方式见代码库的 README。

GitHub 链接：[https://github.com/feiniaojin/ddd-example-cms-front](https://www.oschina.net/action/GoToLink?url=https%3A%2F%2Fgithub.com%2Ffeiniaojin%2Fddd-example-cms-front)

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a384f82e2c6c4294a2f7e5edadf1b810~tplv-k3u1fbpfcp-zoom-1.image)



### 4.3 运行截图

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/98e986e8f48c46e09ca8a2c492b72dfd~tplv-k3u1fbpfcp-zoom-1.image)



## 5. 总结以及进一步学习

本文通过对贫血三层架构进行精炼，推导出适合我们落地的应用架构，并且将之实现为 Maven Archetype 以应用到实际开发，然而应用架构只是落地 DDD 的一个知识点，要完整落地 DDD 还必须体系化地掌握限界上下文、上下文映射、充血模型、实体、值对象、领域服务、Factory、Repository 等知识点。

> 作者：京东物流 覃玉杰



摘自https://my.oschina.net/u/4090830/blog/9428733
