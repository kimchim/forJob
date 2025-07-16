https://www.bilibili.com/video/BV1S142197x7?spm_id_from=333.788.videopod.episodes&vd_source=894e8da7f6c8924a0eb7144cc518c1a9&p=36



笔记https://b11et3un53m.feishu.cn/wiki/R4Sdwvo8Si4kilkSKfscgQX0niB

百度网盘https://pan.baidu.com/s/1JX0fhmV82mgPeBBbAMNV0w&pwd=7988#list/path=%2Fsharelink3232509500-557912393106311%2F0%E3%80%812024%E6%9C%80%E6%96%B0SpringCloud%E5%BE%AE%E6%9C%8D%E5%8A%A1%E5%BC%80%E5%8F%91%E4%B8%8E%E5%AE%9E%E6%88%98%2FSpringCloud%E5%BE%AE%E6%9C%8D%E5%8A%A1%E2%80%94%E8%B5%84%E6%96%99%2Fday03-%E5%BE%AE%E6%9C%8D%E5%8A%A101%2F%E8%B5%84%E6%96%99&parentPath=%2Fsharelink3232509500-557912393106311

# 准备--单体架构

MobaXterm

导入项目

centos + docker的环境

- mysql:虚拟机上
  - 使用docker安装的话不用自己去一一配置，只需要docker run，没有镜像会自动下载
  - 注意需要去把相关的conf init做挂载
- 前端
  - 这里也是本地跑的，直接运行**nginx**
- 后端
  - springboot的配置可以有多个，按照环境来配
  - 代码中的profile都是dev，这个可以切换配置，但是不要去改这里的，否则提交的时候还需要改
  - 本机跑的话配置启动项就可以了，启动的时候可以配置Active profiles:选local就会按照local启动了
  - 这里直接本地机器跑到

# 微服务01

## 1---认识微服务

https://www.bilibili.com/video/BV1S142197x7?spm_id_from=333.788.videopod.episodes&vd_source=894e8da7f6c8924a0eb7144cc518c1a9&p=37

#### 单体架构

单体架构（monolithic structure）：顾名思义，**<u>整个项目中所有功能模块都在一个工程中开发；项目部署时需要对所有模块一起编译、打包；</u>**项目的架构设计、开发模式都非常简单。

> 上面那个就是单体的

- 优点：
  - 架构简单

  - 部署成本低

- 缺点：但随着项目的业务规模越来越大，团队开发人员也不断增加，单体架构就呈现出越来越多的问题：
  - **团队协作成本高**：试想一下，你们团队数十个人同时协作开发同一个项目，由于所有模块都在一个项目中，不同模块的代码之间物理边界越来越模糊。最终要把功能合并到一个分支，你绝对会陷入到解决冲突的泥潭之中。
  - **系统发布效率低**：任何模块变更都需要发布整个系统，而系统发布过程中需要多个模块之间制约较多，需要对比各种文件，任何一处出现问题都会导致发布失败，往往一次发布需要数十分钟甚至数小时。
  - **系统可用性差**：单体架构各个功能模块是作为一个服务部署，相互之间会互相影响，一些热点功能会耗尽系统资源，导致其它服务低可用。

单体架构适合开发功能相对简单，规模较小的项目。大型复杂项目就需要微服务架构了



#### 微服务架构

==微服务架构，是**<u>服务化思想</u>**指导下的一套最佳实践**<u>架构方案</u>**。服务化**<u>，就是把单体架构中的功能模块拆分为多个独立项目。</u>**==

功能拆分的要求：

- **单一职责**：一个微服务负责一部分业务功能，并且其核心数据不依赖于其它模块。
- **团队自治**：每个微服务都有自己独立的开发、测试、发布、运维人员，团队人员规模不超过10人（2张披萨能喂饱）
- **服务自治**：每个微服务都==独立打包部署==，访问自己独立的数据库。并且要做好服务隔离，避免对其它服务产生影响





#### 微服务架构技术栈springcloud

> 拆分后肯定也会有问题，比如服务之间的一些交互等，就需要框架来解决

**微服务拆分以后会遇到各种问题，这些问题都有对应的解决方案和微服务组件**，而SpringCloud框架可以说是目前Java领域最全面的微服务组件的集合了。

SpringCloud是目前国内使用最广泛的==微服务框架==.官网地址:https://spring.io/projects/spring-cloud.

<u>**==SpringCloud集成了各种微服务功能组件,并基于SpringBoot实现了这些组件的自动装配,从而提供了良好的开箱即用体验:==**</u>

> Spring Cloud Alibaba  / Spring Cloud for Amazon Web Services /Spring Cloud Bus / Spring Cloud Circuit 这些微服务组件早就有了，soringcloud集成之后才火的
>
> springcloud指定了标准，接口，所有组件都来实现。所以很多这些组件，在使用上差别不大，依赖不一样。
>
> springboot⚠️自动装配，依赖管理
>
>  
>
> **Spring Cloud 是一个基于 Spring Boot 的微服务开发工具包**，它为微服务架构中的**常见问题提供了标准化解决方案**，帮助开发者快速搭建分布式系统。
> 其核心目标是**简化微服务架构的开发与维护**，屏蔽底层复杂的分布式技术细节（如服务注册与发现、负载均衡、配置管理等）。
>
> Spring Cloud 包含多个子项目（组件）
>
> Spring Cloud 的典型应用场景
>
> - **快速搭建微服务架构**：基于 Spring Boot 的约定优于配置理念，减少开发成本。
> - **企业级分布式系统**：提供熔断、限流、安全认证等企业级功能。
> - **云原生应用**：与 Docker、Kubernetes 等容器化技术深度集成，支持弹性部署。



依赖管理方式：

使用的时候，直接引入spring-cloud-dependencies，其实是一个pom文件定义了相关组件的版本

导入进来相关组件的版本不用自己指定，后续如果使用的话直接指定名称就可以，不用指定版本信息









------

------

## 2---==微服务拆分==

#### 商城项目分析

- 用户模块：eg登陆

  token 会存储到前端，实际上就是jwt的令牌

  这里是使用了jwt进行登陆，实际上就是会服务器会查询数据库校验用户信息后，调用jwt生成工具生成jwt的token ，token和用户信息封装成vo返回给浏览器保存

  后面就会携带这个令牌到服务端

  在http请求头中有一个authorization，携带的就是token信息，也就是每次请求都携带jwt

  服务端就可以获取这个authorization请求头信息

  很多业务都需要判断，不在controller中去做这个工作，而是通过拦截器去做

  springmvc的拦截器，取出请求头中的token，校验后存到上下文中：也就是一个threadlocal中，也就是请求访问一个tomcat，默认都是一个线程中，那么放入这个threadlocal后，后续都可以从这个threadlocal中去取用户信息

  ![image-20250212154034349](/Users/chim/Library/Application Support/typora-user-images/image-20250212154034349.png)



- 商品模块

- 购物车模块：历史价格功能--比加入时便宜xx / 库存限制功能 / 下架功能等

  也就是购物车可以查询到商品的实时信息

  但是实际上数据库中购物车表记录的是老的信息，也就是在点击购物车的时候，u斤查询购物车表信息，还会去查询出商品的最新信息，以此可以做出对比

- 订单模块

  订单表是这样的：![image-20250212155845339](/Users/chim/Library/Application Support/typora-user-images/image-20250212155845339.png)

- 支付模块

  对应一个支付的表

#### 拆分原则

接下来就可以吧上面的一个单体项目进行拆分

**什么时候拆分？**

- 创业型项目：先采用单体架构，快速开发，快速试错。随着规模扩大，逐渐拆分。

- 确定的大型项目：资金充足，目标明确，可以直接选择微服务架构，避免

  后续拆分的麻烦。

**怎么拆分？**

- 从拆分目标来说，要做到：

  - 高内聚：每个微服务的**职责要尽量单一，包含的业务相互关联度高**、完整度高。


  - 低耦合：每个微服务的**功能要相对独立，尽量减少对其它微服务的依赖。**

    > 比如修改某些功能的时候大部分都修改一个微服务就可以
    >
    > 跨服务合作的不可避免，但是还是要尽量减少

- 从拆分方式来说，一般包含两种方式：

  - ==纵向拆分==：按照**<u>业务</u>**模块来拆分

  - ==横向拆分==：抽取**<u>公共服务</u>**，提高复用性

    > 完整的登陆是：记录日志 + 短信提示，其他业务也需要这些功能，这些属于风控功能，不需要重复编写，而是拆分出来横向拆分

黑马商城：纵向拆分

完整的项目，纵向拆分和横向拆分都要有



#### 拆分后的工程结构

项目结构需要改变

现在的是一个project，下面有common和service

工程结构有两种：

- **独立project**

  ==每一个微服务都拆分为一个独立的project==，也就是在idea中是独立的窗口，磁盘中是独立的目录，耦合度最低。

- **maven聚合**

  ==整个项目是一个project，每个微服务是这个project下的module==。每一个module将来都是独立去进行打包和部署的。单体架构中虽然也有多个module但是代码都写在一起，是统一的。



#### 拆分实操

- 将hm-service中与商品管理相关功能拆分到一个微服务module中，命名为**item-service** 
- 将hm-service中与购物车有关的功能拆分到一个微服务module中，命名为**cart-service**



eg商品管理

1. 创建新的module

2. 依赖管理 pom文档修改

3. 创建各种包和启动类

4. 配置文件改动：三个，resources目录下

   Server：port配置的端口需要改

   Spring：

   ​	application：name：注意每一个微服务都需要起一个名字，需要不一样

   ​    profiles： active：当前激活的运行环境的配置

   ​    datasource：每个微服务，操作自己的数据库，所以需要去创建一个新的mysql实例，使用docker去运行一个新的，端口记得变化：：这里的做法是一个mysql，操作不同的数据库，起到一个隔离的效果

5. 具体代码 从domain实体类 -- mapper -- service--controller

   从下往上copy，因为是逐层依赖的

6. 启动项配置，配置springboot的运行配置，选好启动类，本地运行的profile也要记得修改（因为配置文件的固定时dev

   这样切换启动项目很方便



拆分购物车的时候，只做购物车功能，但是其中涉及到了商品服务的查询功能，好实现价格的比对，原本的项目中直接调用商品的service就可以，拆分微服务之后连数据库的位置都不知道在哪里，并且类的结构也不知道，所以不能直接调用service。





#### ==远程调用--resttemplate==

> 购物车模块存在问题：
>
> 购物车的基础没问题
>
> 但是涉及到商品管理微服务的一些业务，需要处理
>
> 还有拿到当前用户的功能，也需要处理
>
> 
>
> ？？？rpc？？？？



**问题：每个服务都是分开的，数据库也是独立的<u>。原本单体项目直接调用service就可以了，微服务就不能这样操作，也不能调用对方的数据库。</u>**

**思路：微服务做了拆分，物理上是隔离的不能像之前那样做本地调用，但是从网络上是可以连接的。也就是通过网络发起请求。**

**问题就变成：java代码向另外的java代码发网络请求，也就是购物车模块向商品模块发送http请求**

**之前：前端可以向java发请求（axios），那么java也可以向java发请求**



```
resttemplate是什么
RestTemplate 是 Spring Framework 提供的同步 HTTP 客户端工具，用于在 Java 应用中调用 RESTful API。它简化了与 HTTP 服务的交互流程，封装了底层的 HTTP 连接（如 Apache HttpClient、OkHttp 等），提供了统一的模板方法。
```

==<u>**Spring给我们提供了一个RestTemplate工具，可以方便的实现Http请求的发送。使用步骤如下：**</u>==

注意这里的1:文件位置是在：public class CartApplication 也就是启动类的下面，启动类也是一个配置类，可以写一些简单的配置

1的意思也就是**<u>创建了一个resttemplate并且交给spring容器去管理</u>**，这样在其他位置也可以直接使用不用自己new了

同时注意，相关dto结构仍然需要拷贝到购物车服务中

![image-20250213151506883](/Users/chim/Library/Application Support/typora-user-images/image-20250213151506883.png)



可以自动json反序列化为指定的类

resttemplate是发送http请求，get post delete等都可以，返回的结果是http响应，有响应头，响应体响应的状态码。结果在响应体中

![image-20250213153600842](/Users/chim/Library/Application Support/typora-user-images/image-20250213153600842.png)



发送 HTTP 请求的常用方法

| **方法**            | **描述**                                                     |
| ------------------- | ------------------------------------------------------------ |
| `getForObject()`    | 发送 GET 请求，返回响应体并自动转换为指定类型的对象。        |
| `getForEntity()`    | 发送 GET 请求，返回包含响应体、状态码和响应头的 `ResponseEntity` 对象。 |
| `postForObject()`   | 发送 POST 请求，携带请求体（如 JSON/XML），返回响应对象。    |
| `postForEntity()`   | 发送 POST 请求，返回 `ResponseEntity` 对象。                 |
| `postForLocation()` | 发送 POST 请求，返回新创建资源的 URL（通常用于 REST 的 POST 操作）。 |
| `put()`             | 发送 PUT 请求（常用于更新资源）。                            |
| `delete()`          | 发送 DELETE 请求（常用于删除资源）。                         |
| **`exchange()`**    | **通用方法，支持自定义请求头、请求方法和响应类型。**         |
| `execute()`         | 最底层的方法，允许完全自定义请求处理流程。                   |









## 3--服务治理

==上面实现了服务的拆分和远程调用，不过是基于resttemplate的，请求的时候需要写url和端口号。a 请求b==

==如果压力大，b可能会部署多份，形成负载均衡的集群，那么如果上述方法，**<u>服务是写死的</u>**，无法负载均衡并且请求故障无法处理。==

==所以需要服务治理。==

#### 注册中心原理

> 调用者不知道提供者的地址，提供者也不知道调用者的地址，通过注册中心，只要知道注册中心的地址就可以了，注册中心返回所有的服务⚠️

![image-20250213165811628](/Users/chim/Library/Application Support/typora-user-images/image-20250213165811628.png)

心跳，如果服务不可用了，注册中心就从服务列表中把这个服务删除掉，并且重新推送给消费方变更



服务治理中的三个角色分别是什么？

- 服务提供者：暴露服务接口，供其它服务调用
- 服务消费者：调用其它服务提供的接口
- 注册中心：记录并监控微服务各实例状态，推送服务变更信息

消费者如何知道提供者的地址？

●服务提供者会在启动时注册自己信息到注册中心，消费者可以从注册中心订阅和拉取服务信息

消费者如何得知服务状态变更？

- 服务提供者通过心跳机制向注册中心报告自己的健康状态，当心跳异常时注册中心会将异常服务剔除，并通知订阅了该服务的消费者

当提供者有多个实例时，消费者该选择哪一个？

●消费者可以通过负载均衡算法，从多个实例中选择一个Nacos注册中心



#### nacos注册中心

开源的注册中心组件：Nacos是目前国内企业中占比最多的注册中心组件。它是阿里巴巴的产品，目前已经加入SpringCloudAlibaba中。

> SpringCloudAlibaba SpringCloudnetflix：Eureka注册中心组件，都有自己的注册中心组件
>
> 由于都遵循spring cloud的规范，所以使用起来的差别不大
>
> https://nacos-io.apifox.cn/



==介绍一下nacos：动态服务发现、配置管理和服务管理平台==。Nacos 支持几乎所有主流类型的“服务”的发现、配置和管理。**Nacos 支持服务发现和服务健康监测**。

> 也就是服务注册到nacos，从nacos中拿

[Kubernetes Service](https://kubernetes.io/docs/concepts/services-networking/service/)

[gRPC](https://grpc.io/docs/guides/concepts.html#service-definition) & [Dubbo RPC Service](https://dubbo.incubator.apache.org/)

[Spring Cloud RESTful Service](https://spring.io/projects/spring-restdocs)



**基于Docker来部署Nacos的注册中心**

- 首先我们要准备MySQL数据库表，用来存储Nacos的数据。由于是Docker部署，所以大家需要将资料中的SQL文件导入到你Docker中的MySQL容器中。

- 需要配置文件，custom.env文件，主要配置nacos和mysql连接的一些信息

- 配置文件上传到虚拟机的/root目录

- 执行docker命令

  docker run -d \

  --name nacos2 \

  --env-file ./nacos/custom.env \    读取环境变量

  -p 8848:8848 \ 		nacos需要三个端口，这里要映射三个

  -p 9848:9848 \

  -p 9849:9849 \

  --restart=always \			开机自启动

  nacos/nacos-server:v2.1.0-slim		ancos版本



**之前的rpc项目是直接本机部署了nacos**：rpc笔记04

- 在官网下载了nacos后进入bin目录

- 这里根据官方手册 mac：`sh startup.sh -m standalone`

  standalone 表示是单机模式，就可以启动了

  默认端口是8848，用户名和





==这里nacos的端口是8848，也就是后面找nacos注册服务或者发现服务，都要通过8848来连接==

> 我的理解
>
> 服务器 --- 调用8848连接nacos服务器（管理ip+端口，就能找到服务）



#### nacos：服务注册

也就是所有的微服务在启动的时候都要提交自己的服务信息到nacos，也就是服务注册

![image-20250213173028199](/Users/chim/Library/Application Support/typora-user-images/image-20250213173028199.png)



==<u>**只需要这两步就服务注册了，**</u>==

> rpc框架不是这样做的，rpc框架目的是可以通过注解的方式去调用远程服务
>
> 服务注册是：使用Netty，构建nettyserver服务端，的时候通过反射拿到service.getClass().getInterfaces()[0].getCanonicalName()，然后手动依次注册到nacos

多实例部署，也就是一份代码，可以在idea中运行多份（修改运行配置的vm options：-Dserver.port），这种情况能不能服务部署呢？可以的

在nacos管理界面可以看到，服务名就是微服务起的名字，默认分组，实例数量为2，健康实例数量为2



#### nacos：服务发现

也就是使用服务的时候不是自己去写服务的地址了，需要去nacos拉取服务的**列表**，然后拿到之后从中负载均衡的选一个

![image-20250213174230695](/Users/chim/Library/Application Support/typora-user-images/image-20250213174230695.png)

传入想要知道的服务名称

拿到所有实例

随机选一个

这里也就是通过ip + 端口，就可以访问服务了，ip + 端口 = uri

![image-20250213174955668](/Users/chim/Library/Application Support/typora-user-images/image-20250213174955668.png)



nacos自动有心跳机制

这里断开某个服务或者启动某个服务，nacos会感应到，自动的通知调用者







## 4--==OpenFeign==

> 前面nacos只是解决了部署了多个服务的情况下，服务注册和发现的问题，也就是ip+端口不用写死了，**但是发送请求的过程还是自己手动去使用resttemplate去发送的，并且还需要自己手动去封装返回的结果**
>
> 1. 传入nacos想要知道的服务名称
> 2. 拿到nacos中所有实例
> 3. 随机选一个
>
> 4. 这里也就是通过ip + 端口，就可以访问服务了
>
> 太麻烦了，
>
> openfeign可以把原来自己写的这一长串发送请求，直接反向代理实现用户只需要定义简单接口
>
> openfeign也就是用来发送http请求的

```
openfeign和rpc区别
https://blog.csdn.net/qq_46130027/article/details/134613851

也就是http 和 rpc的区别：https://cloud.tencent.com/developer/article/2028662

Dubbo和OpenFeign是两个常用的远程调用框架,分别适用于不同的场景。Dubbo是一个高性能的Java RPC框架,而OpenFeign是Spring Cloud生态中的声明式HTTP客户端
```



OpenFeign作用：简化远程**<u>调用</u>**的代码，==服务的拉取、负载均衡、结果的封装都由openfeign==使用**<u>反向代理</u>**来实现，使用者只需要定义简单的接口就可以了

==让**远程调用像本地方法调用一样简单**==

原本是service的调用，现在是基于feign客户端的调用



#### 4步实现远程调用

OpenFeign是一个声明式的http客户端==,**<u>用来发送http请求</u>**==

是SpringCloud在Eureka公司开源的Feign基础上改造而来.官方地址:

https://github.com/0penFeign/feign

其作用就是基于SpringMVC的常见注解,帮我们优雅的实现http请求的发送.



1. 引入依赖

2. 在==启动类==上添加配置，也就是一个开关， 开启openfeign

3. ==**编写openfeign的client客户端**，定义请求方法，openfeign会 自动实现，也就是：自动去请求服务名称，负载均衡的去拿服务，最后会返回封装好的结果==

   也就是原本是购物车服务---发送请求---访问商品服务

   这里是购物车服务---/item/访问client客户端，客户端----客户端帮我们去实现访问商品服务，以及封装返回结果的工作

4. **注入客户端**

5. **进行调用** 后续直接客户端.方法，请求-拿-封装的过程就是自动执行的了



![image-20250214104519193](/Users/chim/Library/Application Support/typora-user-images/image-20250214104519193.png)

![image-20250214105205671](/Users/chim/Library/Application Support/typora-user-images/image-20250214105205671.png)

注意可以在上面3中的方法中定义很多方法，只要都是item-service提供的接口就可以



声明完接口后再类中注入，之前的查询变为1行代码 ，就跟直接调用service接口一样

![image-20250214105622653](/Users/chim/Library/Application Support/typora-user-images/image-20250214105622653.png)





#### 实现原理

> 这里去复习一下动态代理
>
> 底层整体流程放到

- 自己定义的client只定义了接口，没有实现相关的实现类，所以实际上运行的是代理对象

- 代理对象执行的都在invocationhandler中的invoke方法实现

- invoke中，**从注解上拿到信息，拿到了服务的名称信息**，请求还不能发出，不是ip+端口

- **拉取实例列表，然后负载均衡的选择出一个服务serviceinstance，这个里面就有ip + port了，替换服务名称。**
- **然后发送请求，交给一个代理的client去发送**，底层是有一个client的默认实现，使用httpurlconnection来发送的，（默认，这个是jdk自带的）
  - 可以自己配置选择使用哪个client去发请求，比如配置了okhttp的话，支持连接池，就会交给okHttpClient来发送请求



> 自己发请求用的是resttemplate，这里是client，每一次都要重新创建连接，效率比较低。所以可以优化为连接池



#### 连接池

OpenFeign对Http请求做了优雅的伪装,不过==<u>**其底层发起http请求,依赖于其它的框架.**</u>==**<u>这些框架可以自己选择,包括以下三种:</u>**

> 也就是说这个框架简化了发请求的流程，json-->对象的转换，但是底层的http请求怎么发送依赖其他框架，可以自己选择

- HttpURLConnection:默认实现,不支持连接池

- Apache HttpClient :支持连接池

- OKHttp:支持连接池


具体源码可以参考FeignBlockingLoadBalancerClient类中的delegate成员变量.



整体的连接池只需要在pom中添加依赖，然后在配置文件中开启连接池就可以了

![image-20250214161053608](/Users/chim/Library/Application Support/typora-user-images/image-20250214161053608.png)





#### 最佳实践

也就是购物车，订单都拆成微服务的话，都调用商品服务的话，那么在**<u>购物车微服务和订单微服务就要都有ItemClient，需要写2个，同时如果服务修改了，购物车微服务和订单微服务都需要修改。</u>**

- 由ItemClient写

**<u>也就是商品微服务来维护client</u>**，其他服务要想调用的话就引入依赖，然后直接调用就可以

（如果不写client，引入依赖还是要自己写到controller之类的，耦合度太高）

适合一个每一个微服务都是一个独立项目的情况

![image-20250217231217065](/Users/chim/Library/Application Support/typora-user-images/image-20250217231217065.png)

- **<u>写一个统一管理各种api的服务，</u>**也就是所有需要暴露接口的微服务，都需要定义feign客户端到api模块，同时定义dto到api模块。这样其他服务想要使用的时候直接引入依赖就可以了

适合每个微服务是一个module的情况

![image-20250217231358910](/Users/chim/Library/Application Support/typora-user-images/image-20250217231358910.png)

这种情况在使用的时候注意，比如cart服务引入了api的依赖，但是默认cart包扫描路径是com hmall cart，itemclient不会被扫描到，也就是在cart服务中这个类不会被扫描到



**在cart使用openfeign的时候，需要在cartapplication上添加这个注解，@EnableFeignClients**

![image-20250218104633996](/Users/chim/Library/Application Support/typora-user-images/image-20250218104633996.png)





#### 日志

openfeign默认没有日志

**OpenFeign只会在FeignClient所在包的日志级别为DEBuG时，才会输出日志。而且其日志级别有4级：**

- **NONE：不记录任何日志信息，这是默认值。**
- BASIC：仅记录请求的方法，URL以及响应状态码和执行时间

- HEADERS：在BASIC的基础上，额外记录了请求和响应的头信息 )
- FULL：记录所有请求和响应的明细，包括头信息、请求体、元数据。

由于Feign默认的日志级别就是NONE，所以默认我们看不到请求日志。



1:FeignClient所在包的日志级别为DEBuG

日志的配置在application.yaml中

logging：level：

com.hmall：debug

2:要**<u>自定义日志级别</u>**，需要声明一个类型为Logger.Level的Bean，在其中定义日志级别：

```java
public class DefaultFeignConfig {

	@Bean
	public Logger.Level feignLogLevel(){ 
			retun Logger.Level.FuLL； //这里有默认好的日志级别
  }
}
```

但此时这个Bean并未生效,声明的bean要想被spring创建，所在的类需要是配置类才可以，这里需要在做配置

- 要想配置某个FeignClient的日志,可以在@FeignClient注解中声明:


@FeignClient(value = "item-service", **configuration** = **DefaultFeignConfig.class**)

FeignClient是每一个client的上面都会有这个注解，也就是每一个客户端都需要写这个注解，也就是只对局部的client生效

- 如果想要全局配置,让所有FeignClient都按照这个日志配置,则需要在@EnableFeignClients注解中声明:


@EnableFeignclients(**defaultConfiguration** **=DefaultFeignConfig.class**)

EnableFeignClients是放到启动类上的注解，也就是在cartaplication上面的注解，所以是一个全局生效的



> 调试的时候开启日志就可以
>
> 因为日志内容有很多，连接池信息，请求头 请求体 还有响应头响应体，所以一般开发不开启日志，而是调试的时候开启



#### openfeign和rpc

ai：

OpenFeign 是 Spring Cloud 生态中用于实现声明式 HTTP 客户端的工具，它简化了微服务之间的 HTTP 调用，虽然在概念上与传统 RPC（远程过程调用）有相似之处，但严格来说它属于 **HTTP 客户端** 而非传统 RPC 框架。以下是详细介绍：



http调用和rpc调用的区别

HTTP 调用和 RPC（远程过程调用）是两种不同的分布式通信方式，主要区别体现在 **设计目标、协议机制、适用场景** 等方面。以下是详细对比：

| **维度**     | **HTTP 调用**                                      | **RPC 调用**                                   |
| ------------ | -------------------------------------------------- | ---------------------------------------------- |
| **本质**     | 基于 **HTTP 协议** 的应用层通信方式                | 一种 **跨进程函数调用** 的抽象机制             |
| **设计目标** | 实现 **资源的网络访问**（如 RESTful API）          | 实现 **远程函数的本地调用体验**                |
| **核心思想** | 以 **资源为中心**（URI 定位资源，Method 操作资源） | 以 **接口 / 函数为中心**（调用远程服务的方法） |

| **维度**     | **HTTP 调用**                                | **RPC 调用**                               |
| ------------ | -------------------------------------------- | ------------------------------------------ |
| **传输协议** | 基于 **TCP/IP**，通常使用 HTTP/1.1 或 HTTP/2 | 可基于 **TCP/IP**（如 gRPC）或自定义协议   |
| **消息格式** | 常用 **JSON、XML 等文本格式**                | 常用 **二进制格式**（如 Protobuf、Thrift） |
| **协议开销** | 较高（HTTP 头部字段冗余）                    | 较低（二进制协议更紧凑）                   |
| **跨平台性** | 天然跨平台（HTTP 是通用协议）                | 需依赖序列化 / 反序列化库（跨语言需适配）  |

| **维度**       | **HTTP 调用**                                           | **RPC 调用**                                       |
| -------------- | ------------------------------------------------------- | -------------------------------------------------- |
| **调用方式**   | **显式请求**：需手动构造 HTTP 请求（URL、Method、Body） | **隐式调用**：通过本地代理（Stub）直接调用远程函数 |
| **开发复杂度** | 较高（需处理请求 / 响应解析、连接管理等）               | 较低（框架自动处理底层通信细节）                   |
| **代码生成**   | 通常不需要（直接通过 HTTP 客户端库调用）                | 通常需要（根据接口定义生成客户端 / 服务端代码）    |
| **典型工具**   | `RestTemplate`、`OkHttp`、`Postman`                     | `gRPC`、`Thrift`、`Dubbo`、`Spring Cloud Stream`   |



zeromq是rpc框架吗

ZeroMQ（简称 ZMQ）不是传统意义上的 RPC 框架，而是一个**高性能消息队列库**，它提供了异步、低延迟的消息传递机制，可用于构建分布式系统。虽然可以基于 ZeroMQ 实现自定义 RPC，但它本身并不属于 RPC 框架。





# 微服务02

## 网关

> 每一个功能，ip和端口都不一样
>
> 前端写代码的时候，需要写需要向哪个端口要数据，后面变得话需要改
>
> 而且原本都是在一个端口下，比如登陆后，所有的模块都能拿到登陆的用户信息了。
>
> 总不能每一个服务都重新拿jwt密钥去验证
>
> （前面是后端调用后端，可以用nacos）
>
> 



服务拆分后 两个问题：

1:地址变化，并且过多，前端不知道请求谁：

2:每个服务可能都需要登录用户信息

**网关：就是网络的关口，负责==请求==的路由、转发、身份校验。**

> 访问网关，网关会做身份校验，验证后告诉在哪里，并且找不到会带着请求过去。也就是身份校验 路由 转发



以后前端只需要知道网关的地址就可以了，网关根据前端的请求判断应该访问哪一个微服务（路由），然后网关把这个请求转发给谁（地址通过注册中心）。在前端看来后端是一个黑盒子，网关现在是必不可少的了

springcloud提供了网关组件

![image-20250530104458192](/Users/chim/Library/Application Support/typora-user-images/image-20250530104458192.png)



==**<u>Spring Cloud Gateway</u>**==

- Spring官方出品


- 基于WebFlux==响应式编程== 
- 无需调优即可获得优异性能

Netfilx Zuul

- Netflix出品


- 基于Servlet的阻塞式编程
- 需要调优才能获得与SpringCloudGateway 类似的性能



#### 快速入门

> 网关路由：跟业务有关，网关自己没法做，就需要开发者告诉他。剩下的网关可以自动执行

- 创建新模块

- 引入网关依赖

- 编写启动类（前三步就是启动网关微服务，网关也是一个微服务，也就是一个module）

- 配置路由规则

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250530111332918.png" alt="image-20250530111332918" style="zoom:50%;" />

predicates就是判断根据，判断请求是否符合规则

-path表示按照路径判断

路由到哪里？uri lb：//item-service 就是微服务的名称了。lb是loadbalance，负载均衡

也就是网关会自动去注册中心拿到所有item-service微服务中的所有可用服务，然后负载均衡的挑出来一个返回

但是规则到uri这个需要自己去配置，





前面创建这个微服务的过程

- 创建项目
- 引入依赖
- 启动类

main-java下面创建启动类

⚠️复习一下创建一个springboot的启动类

![image-20250530111931348](/Users/chim/Library/Application Support/typora-user-images/image-20250530111931348.png)

- 配置路由规则

resources下创建application。yaml

除了路由规则的配置，还需要配一些其他的

这里还有一个需要注意的就是一个微服务对应一套

id-uri-predicates

一个微服务下可能有多个controller， 每个controller：有规定请求路径，需要针对微服务下所有可能的都配路由

如果多个微服务就是多套id-uri-predicates

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250530112820457.png" alt="image-20250530112820457" style="zoom:50%;" />



测试：localhost:8080/search/list和localhost:8081/search/list的效果一样，网关是8080 微服务是8081

#### 路由属性

> 所有的配置都有一个java类对应
>
> RouteDefinition：在yaml配置类中点击routes就能进去源码，内部就是一个个的RouteDefinition，每一个RouteDefinition都有id uri filer 等属性，filter还有predicates属性都是 list的，也就是可以配置多个

网关路由对应的Java类型是**<u>RouteDefinition</u>**，其中常见的属性有：

- id：路由唯一标示
- uri：路由目标地址
- predicates：路由断言，判断请求是否符合当前路由。
- filters：路由过滤器，对请求或响应做特殊处理。
  - 不是拦截谁

==路由断言==

![image-20250530114907163](/Users/chim/Library/Application Support/typora-user-images/image-20250530114907163.png)

> 底层是工厂？？？？后面看看



==路由过滤器==

![image-20250530115153917](/Users/chim/Library/Application Support/typora-user-images/image-20250530115153917.png)

> stripprefix
>
> 比如前端发请求经常加一个/api/item/list
>
> 但是微服务都是/item/list
>
> 可以把/api去掉
>
> （在这里好像是nginx处理过了，/api发到后端拿到就没有了）
>
>  
>
> 添加请求头
>
> 不是在uri路径上加，是在**<u>请求头</u>** requestheader【请求头请求体】
>
> 

过滤器配置位置：

- 想要单个微服务生效：路由配在routes，每个微服务下面，这样针对每个微服务单独写过滤器
- 想所有路由都生效，可以配置和routes同一级别，default-filters，就可以对的路由都生效了

​     





## 02 网关登陆校验

> jwt登陆，
>
> 很多微服务都需要知道用户的信息，不能每个微服务区做校验，而是网关去做校验。一定要网关把请求转发给微服务之前来做

网关底层没有业务逻辑，要做的事情就是基于我们配置的路由规则，来判断

![image-20250530151128328](/Users/chim/Library/Application Support/typora-user-images/image-20250530151128328.png)



- 如何在网关转发之前做登录校验？

- 网关如何将用户信息传递给微服务？

- 如何在微服务之间传递用户信息？

> 如果在请求转发之前要做登陆校验的逻辑，应该放到pre阶段，保证在nettyroutingfilter之前。
>
> 在pre阶段的，执行失败就结束，不继续向下了
>
> 并且网关还需要把用户信息传递给微服务，（网关也是一个独立的微服务，放到本地的话不互通）
>
> 所以也就是从一个服务到另一个服务，其实相当于发请求，所以保存用户到请求头中
>
> 还有问题：微服务之间也会有调用，也需要去传递用户信息
>
> 微服务之间是openfeign去发的：网关是内部实现的



##### step1 ：自定义网关过滤器

网关过滤器有两种，分别是：

- GatewayFilter：路由过滤器，作用于任意指定的路由；默认不生效，要配置到路由后生效。

- <u>**GlobalFilter：全局过滤器，作用范围是所有路由；声明后自动生效。**</u>：常用

两种过滤器的过滤方法签名完全一致

内部有filter方法，后面自己实现就是需要重写filter方法

==Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain);==

参数

ServerWebExchange exchange：请求上下文，包含整个过滤器链内共享数据，例如request、response等。（请求头 体 路径等都在request中）

 GatewayFilterChain chain：过滤器链。当前过滤器执行完后，要调用过滤器链中的下一个过滤器

返回值

网关是非阻塞的编程，也就是有一个回调函数，

> 我的理解
>
> pre阶段处理完，还需要后面处理完，并且依次返回，才能在post阶段拿到返回值
>
> 非阻塞 回调 也就是不用等待了，后续执行到了，就调用回调函数



![image-20250530154625189](/Users/chim/Library/Application Support/typora-user-images/image-20250530154625189.png)



过滤器执行顺序值越小优先级越高，netty的那个是int的最大值也就是最后一个执行



【自定义GatewayFilter比较少用】需要的时候去看：https://www.bilibili.com/video/BV1S142197x7?spm_id_from=333.788.player.switch&vd_source=894e8da7f6c8924a0eb7144cc518c1a9&p=63





##### step2 ：实现网关过滤器的登陆校验

需求：在网关中基于过滤器实现登录校验功能

> jwt实现的需要用到一些jwt的工具  
>
> 这里直接引入了，然后使用了jwtTool的parseToken
>
> 如果出错就会抛出，说明没有登陆



![image-20250530161758186](/Users/chim/Library/Application Support/typora-user-images/image-20250530161758186.png)



注意路径匹配规则怎么写呢

比如配置了/login/**

用户/login/1 和login/2都要放行，就不能用equals了

java提供了private final AntPathMatcher antPathMatcher = new AntPathMatcher();

private boolean isExclude(String path) {

​	for (String pathPattern : authProperties.getExcludePaths()) {

​		 if (antPathMatcher.match(pathPattern, path)) { 

​			return true;

}

return false;



##### step3： 网关传递用户

==网关把请求传递给微服务的时候，保存用户信息到请求头中，转发请求的时候传递给微服务：globalfilter==

==接下来需要微服务从中取出来用户信息，定义拦截器，把网关传递来的用户信息，保存到threadlocal中（微服务内部一般就是一个线程来回调用，就可以用线程域保存用户信息）==  

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250530163352139.png" alt="image-20250530163352139" style="zoom:50%;" />

1: 网关把用户信息保存到请求头，**在网关把请求发给微服务的时候，带上用户信息**

2:在微服务内部，编写拦截器，这样就能拦截到请求，然后拿出来用户信息存储了

> 注意微服务可能有很多业务，可能有很多都需要用户信息，肯定不能每个业务都传递
>
> 那么就需要在微服务执行之前去拿到用户信息：springmvc拦截器，保存到threadlocal
>
> 同时与有很多微服务都需要，每个微服务都重复的写拦截器吗
>

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250530163820533.png" alt="image-20250530163820533" style="zoom:50%;" />



<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250603160537729.png" alt="image-20250603160537729" style="zoom:50%;" />

上面是网关拦截到信息之后发给用户了，那么接下来就需要用户的微服务，拦截到请求之后从请求头中拿出来这个信息。

可以在每一个需要的服务中去加：

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250603160752174.png" alt="image-20250603160752174" style="zoom:50%;" />

但是这样太麻烦了，一样的需要每个都写

可以用微服务拦截器

但是多个微服务的时候，微服务拦截器变成通用common拦截器

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250530163837891.png" alt="image-20250530163837891" style="zoom:50%;" />

也就是在通用的这个模块去写一个拦截器，拿到用户信息存储到本地。注意common这个不做拦截，都放行

==本地就是一个ThreadLocal类型的数据==。⚠️

> 这个类型

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250530164524751.png" alt="image-20250530164524751" style="zoom:50%;" />



> ⚠️为什么这里拦截器是springmvc的
>
> 拦截器并非 Spring MVC 所独有，在 Java 以及其他编程语言的不同框架中，都有类似的概念，只是名称和实现方式存在差异。下面为你详细介绍：
>
> Spring MVC 的拦截器（`HandlerInterceptor`）是专门用于 **<u>Web 请求</u>**处理的，它的作用范围是整个请求的生命周期。**典型应用**：常用于身份验证、日志记录、性能监控、请求参数处理等操作。
>
> Servlet Filter（Servlet 过滤器）
> Servlet Filter 是 **<u>Java EE（</u>**现称 Jakarta EE）的标准组件，它的拦截范围比 Spring MVC 拦截器更广，能够对**<u>所有 Servlet 请求</u>**进行拦截。需要实现`javax.servlet.Filter`接口的doFilter，并在`web.xml`中进行配置，或者通过`@WebFilter`注解来配置。
>
> Spring AOP 的拦截器能够对方法调用进行拦截，它的关注点在于**<u>业务逻辑层面</u>**，而不是 Web 请求。可以使用`@Aspect`注解和`@Around`、`@Before`、`@After`等通知注解来实现。

拦截器定义

> 自己写一个拦截器，注意要实现HandlerInterceptor接口（prehandle，aftercompletion）

![image-20250530164800137](/Users/chim/Library/Application Support/typora-user-images/image-20250530164800137.png)



拦截器生效

> 实现完了之后并不会生效
>
> springmvc的拦截器生效需要配置
>
> 需要创建一个配置类，实现`WebMvcConfigurer`接口，重写`addInterceptors`方法，将自定义拦截器注册到 Spring MVC 中
>
> **<u>若你使用的是 Spring Boot 项目，在添加了上述代码后，拦截器会自动生效。若为传统的 Spring MVC 项目，则需要确保在 Spring 配置文件中正确配置了 JavaConfig 类。</u>**
>
> 

![image-20250530165055408](/Users/chim/Library/Application Support/typora-user-images/image-20250530165055408.png)



引入common还没生效，需要被spring扫描到才可以

原因是：比如在-item微服务下，扫描包是com hmall item，放到common下，别的微服务扫描不到（我的理解是item会自动扫描自己下面的包，如果是在item中去写的话就可以被spring自动扫描到了）

> spring 自动装配原理
>
> 在不同包下扫不到的类，需要定义文件记录配置类

![image-20250530165321396](/Users/chim/Library/Application Support/typora-user-images/image-20250530165321396.png)



❓--问题启动网关，会报错file not found 

原因是这个拦截器放到了common下，common不仅仅是被微服务引用了，**<u>还被网关引用了</u>**（这样网关中也有这个mvcconfig配置类了）

因为网关底层不是springmvc这一套，这个配置类实现webmvcconfigurer，没有webmvcconfigurer，所以会报错

==就需要让这个配置类，在有些情况下生效，有些情况下不生效==

> 依然是springboot'自动装配的原理，⚠️springboot'自动装配可以是带条件的
>
> 对比差别 网关没有springmvc 其他都有，springmvc核心api：dispatcherservlet，有的话才会有webmvcconfigurer



<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250603160229557.png" alt="image-20250603160229557" style="zoom:50%;" />



至此从网关到微服务的实现了



##### step4 ：openfeign传递用户

> 前面实现了网关发给微服务的，可以拿到用户信息
>
> 调用链长的时候，需要微服务之间相互调用：也就是需要微服务之间传递登陆用户信息

微服务项目中的很多业务要多个微服务共同合作完成，而这个过程中也需要传递登录用户信息，例如：





扣减库存不需要用户信息，清理购物车，就需要指定用户信息

原来的代码是

![image-20250603161418440](/Users/chim/Library/Application Support/typora-user-images/image-20250603161418440.png)

发起远程调用购物车服务，用户信息没有传递为null，没有成功删除



![image-20250603161833824](/Users/chim/Library/Application Support/typora-user-images/image-20250603161833824.png)

因为购物车删除逻辑，现在不是说把用户id放到请求参数中，而是直接从上下文中取

usercontext要想有：微服务的拦截器，拦截到的时候需要从请求头中拿到数据，然后放到usercontext中

需要请求头中有，现在从交易微服务发过来的，是openfeign发的，是没有放的

怎么让openfeign放呢？：

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250603162442302.png" alt="image-20250603162442302" style="zoom:50%;" />



现在就需要定义openfeign的拦截器了：放到公共的

这个项目所有openfeign的借口，都放到了hm-api中（没有一个微服务一个openfeign，而是放到一起了）

所以可以放到hm-api中，引用了hm-api的微服务，自带这个拦截器了

（这里匿名内部类简单的声明，也可以单独写一个config）

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250603163201914.png" alt="image-20250603163201914" style="zoom:50%;" />

这个配置要添加到，对应微服务的启动类上，才会生效

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250603163249528.png" alt="image-20250603163249528" style="zoom:50%;" />





总回顾

网关过滤器：登陆校验获取token的用户信息

<img src="/Users/chim/Library/Application Support/typora-user-images/image-20250603164239067.png" alt="image-20250603164239067" style="zoom:50%;" />



## 03 配置管理-nacos

https://www.bilibili.com/video/BV1S142197x7?spm_id_from=333.788.player.switch&vd_source=894e8da7f6c8924a0eb7144cc518c1a9&p=67



- 微服务重复配置过多，维护成本高（共享配置）

- 业务**配置**经常变动，每次修改都要重启服务（最大重试次数等等业务配置）
- 网关路由配置写死，如果变更要重启网关



1:配置共享

2:热更新

配置管理服务可以监听，如果发现变更，推送配置变更

这样无需重启立即生效



==nacos不仅可以作为注册中心，同样具有配置管理的功能==



01配置共享

02 配置热更新

03 动态路由

看pdf笔记























# ==学习过程中的知识点 /面试题==

- jwt
- springmvc的过程
- 拦截器
- threadlocal 线程域

- springboot自动装配