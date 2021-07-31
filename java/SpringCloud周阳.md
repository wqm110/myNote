# SpringCloud第一季 讲师:尚硅谷周阳

## 1、微服务概述与SpringCloud

### 1.1  微服务与微服务架构

>  业界大牛马丁.福勒（Martin Fowler） 这样描述微服务： 论文网址： https://martinfowler.com/articles/microservices.html   微服务 强调的是服务的大小，它关注的是某一个点，是具体解决某一个问题/提供落地对应服务的一个服务应用, 狭意的看,可以看作Eclipse里面的一个个微服务工程/或者Module   ...

#### 技术维度理解

> 微服务化的核心就是将传统的一站式应用，根据业务拆分成一个一个的服务，彻底 地去耦合,每一个微服务提供单个业务功能的服务，一个服务做一件事， 从技术角度看就是一种小而独立的处理过程，类似进程概念，能够自行单独启动 或销毁，拥有自己独立的数据库。

### 1.2 微服务技术栈有哪些

> 微服务条目 落地技术 备注 服务开发 Springboot、Spring、SpringMVC 服务配置与管理 Netflix公司的Archaius、阿里的Diamond等 服务注册与发现 ==Eureka==、==Consul==、Zookeeper等 服务调用 Rest、RPC、gRPC 服务熔断器 Hystrix、Envoy等 负载均衡 Ribbon、Nginx等 服务接口调用(客户端调用服务的简化工具) Feign等 消息队列 Kafka、RabbitMQ、ActiveMQ等 服务配置中心管理 SpringCloudConfig、Chef等 ...

### 1.3 SpringCloud是什么

#### 官网说明

> SpringCloud，基于SpringBoot提供了一套微服务解决方案，包括服务注册与发现，配置中心，全链路监控，服务网关，负载均衡，熔断器等组件，除了基于NetFlix的开源组件做高度抽象封装之外，还有一些选型中立的开源组件。  SpringCloud利用SpringBoot的开发便利性巧妙地简化了分布式系统基础设施的开发，SpringCloud为开发人员提供了快速构建分布式系统的一些工具，包括配置管理、服务发现、断路器、路由、微代理、事件总线、全局锁、决策竞选、分布式会话等等,它们都可以用SpringBoot的开发风格做到一键启动和部署。  SpringBoot并没有重复制造轮子，它只是将目前各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过SpringBoot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包

  SpringCloud=分布式微服务架构下的一站式解决方案， 是各个微服务架构落地技术的集合体，俗称微服务全家桶

##### 1.4 All SpringCloud和SpringBoot是什么关系



> SpringBoot专注于快速方便的开发单个个体微服务。  SpringCloud是关注全局的微服务协调整理治理框架，它将SpringBoot开发的一个个单体微服务整合并管理起来， 为各个微服务之间提供，配置管理、服务发现、断路器、路由、微代理、事件总线、全局锁、决策竞选、分布式会话等等集成服务  SpringBoot可以离开SpringCloud独立使用开发项目，但是SpringCloud离不开SpringBoot，属于依赖的关系.  SpringBoot专注于快速、方便的开发单个微服务个体，SpringCloud关注全局的服务治理框架。

#### Dubbo是怎么到SpringCloud的？ 

哪些优缺点让你去技术选型

目前成熟的互联网架构（分布式+服务治理Dubbo）

###### 

我们把SpringCloud VS DUBBO进行一番对比

最大区别：

> SpringCloud抛弃了Dubbo的RPC通信，采用的是基于HTTP的REST方式。 严格来说，这两种方式各有优劣。虽然从一定程度上来说，后者牺牲了服务调用的性能，但也避免了上面提到的原生RPC带来的问题。

> 而且REST相比RPC更为灵活，服务提供方和调用方的依赖只依靠一纸契约，不存在代码级别的强依赖，这在强调快速演化的微服务环境下，显得更加合适。  品牌机与组装机的区别 很明显，Spring Cloud的功能比DUBBO更加强大，涵盖面更广，而且作为Spring的拳头项目，它也能够与Spring Framework、Spring Boot、Spring Data、Spring Batch等其他Spring项目完美融合，这些对于微服务而言是至关重要的。使用Dubbo构建的微服务架构就像组装电脑，各环节我们的选择自由度很高，但是最终结果很有可能因为一条内存质量不行就点不亮了，总是让人不怎么放心，但是如果你是一名高手，那这些都不是问题；而Spring Cloud就像品牌机，在Spring Source的整合下，做了大量的兼容性测试，保证了机器拥有更高的稳定性，但是如果要在使用非原装组件外的东西，就需要对其基础有足够的了解。...

总结Cloud与Dubbo

问题： 曾风靡国内的开源 RPC 服务框架 Dubbo 在重启维护后，令许多用户为之雀跃，但同时，也迎来了一些质疑的声音。互联网技术发展迅速，Dubbo 是否还能跟上时代？Dubbo 与 Spring Cloud 相比又有何优势和差异？是否会有相关举措保证 Dubbo 的后续更新频率？  人物：Dubbo重启维护开发的刘军，主要负责人之一  刘军，阿里巴巴中间件高级研发工程师，主导了 Dubbo 重启维护以后的几个发版计划，专注于高性能 RPC 框架和微服务相关领域。曾负责网易考拉 RPC 框架的研发及指导在内部使用，参与了服务治理平台、分布式跟踪系统、分布式一致性框架等从无到有的设计与开发过程。

参考资料

官网

http://projects.spring.io/spring-cloud/

参考书

https://springcloud.cc/spring-cloud-netflix.html

本次开发API说明

http://cloud.spring.io/spring-cloud-static/Dalston.SR1/

https://springcloud.cc/spring-cloud-dalston.html

springcloud中国社区

http://springcloud.cn/

springcloud中文网

https://springcloud.cc/

SpringCloud国内使用情况

国内公司

##### 

阿里云

##### 

## 1.4 Rest微服务构建 案例工程模块

### 总体介绍

>承接着我们的springmvc+mybatis+mysql初级高级课程，以Dept部门模块做一个微服务通用案例 Consumer消费者（Client）通过REST调用Provider提供者（Server）提供的服务

Maven的分包分模块架构复习

一个简单的Maven模块结构是这样的： ---- app-parent 一个父项目(app-parent)聚合很多子项目(app-util,app-dao,app-service,app-web) \|---- pom.xml (pom) \| \|-------- app-util \| \|-------- pom.xml (jar) \| \|-------- app-dao \| \|-------- pom.xml (jar)...

一个Project带着多个Module子模块

MicroServiceCloud父工程（Project）下初次带着3个子模块（Module）

microservicecloud-api

####### 封装的整体Entity/接口/公共配置等

microservicecloud-provider-dept-8001

####### 微服务落地的服务提供者

microservicecloud-consumer-dept-80

####### 微服务调用的客户端使用

####### 80端口

######## 80端口是为HTTP(HyperText Transport Protocol)即超文本传输协议开放的 此为上网冲浪使用次数最多的协议，主要用于WWW(World Wide Web)即万维网传输信息的协议。  可以通过HTTP地址(即常说的"网址")加":80"来访问网站，  因为浏览网页服务默认的端口号都是80，因此只需输入网址即可，不用输入":80"了。

直接动手干

##### 

本次springCloud版本

#### 

构建步骤

microservicecloud 整体父工程Project

新建父工程microservicecloud，切记是Packageing是pom模式

###### 

主要是定义POM文件，将后续各个子模块公用的jar包等统一提出来，类似一个抽象父类

POM

\<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html} \<`<packaging>`{=html}pom\<`</packaging>`{=html}...

microservicecloud-api 公共子模块Module

新建microservicecloud-api

###### 

创建完成后请回到父工程查看pom文件变化

修改POM

\<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html}\<`<!-- 子类里面显示声明才能有明确的继承表现，无意外就是父类的默认版本否则自己定义 -->`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

新建部门Entity且配合lombok使用

package com.atguigu.springcloud.entities;  import java.io.Serializable;  import lombok.Data; import lombok.NoArgsConstructor; import lombok.experimental.Accessors;  \@SuppressWarnings("serial") \@NoArgsConstructor...

mvn clean install后给其它模块引用，达到通用目的。 也即需要用到部门实体的话，不用每个工程都定义一份，直接引用本模块即可。

microservicecloud-provider-dept-8001 部门微服务提供者Module

新建microservicecloud-provider-dept-8001

###### 

创建完成后请回到父工程查看pom文件变化

POM

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> <modelversion></modelversion><parent><groupid>com.atguigu.springcloud\</groupid><artifactid></artifactid><version></version>
```

YML

```yaml
server: port: 8001  
mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \# mybatis配置文件所在路径 
	type-aliases-package: com.atguigu.springcloud.entities \# 所有Entity别名类所在包 
	mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \# mapper映射文件  
spring:...
```

工程src/main/resources目录下新建mybatis文件夹后新建mybatis.cfg.xml文件

< ¶ \< ¶ PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd"\>  \<`<configuration>`{=html}  \<`<settings>`{=html} \<`<setting name="cacheEnabled" value="true">`{=html}`</setting>`{=html}\<`<!-- 二级缓存开启 -->`{=html} \<`</settings>`{=html}...

##### MySQL创建部门数据库脚本

DROP DATABASE IF EXISTS cloudDB01; CREATE DATABASE cloudDB01 CHARACTER SET UTF8; USE cloudDB01; CREATE TABLE dept ( deptno BIGINT NOT NULL PRIMARY KEY AUTO_INCREMENT, dname VARCHAR(60), db_source VARCHAR(60) ); ...

DeptDao部门接口

package com.atguigu.springcloud.dao;  import java.util.List; import org.apache.ibatis.annotations.Mapper; import com.atguigu.springcloud.entities.Dept;  \@Mapper public interface DeptDao { public boolean addDept(Dept dept);...

工程src/main/resources/mybatis目录下新建mapper文件夹后再建DeptMapper.xml

< ¶ \< ¶ "http://mybatis.org/dtd/mybatis-3-mapper.dtd"\>  \<`<mapper namespace="com.atguigu.springcloud.dao.DeptDao">`{=html}  \<`<select id="findById" resulttype="Dept" parametertype="Long">`{=html} select deptno,dname,db_source from dept where deptno=\#{deptno}; \<`</select>`{=html} \<`<select id="findAll" resulttype="Dept">`{=html}...

DeptService部门服务接口

package com.atguigu.springcloud.service;  import java.util.List;  import com.atguigu.springcloud.entities.Dept;  public interface DeptService { public boolean add(Dept dept); public Dept get(Long id);...

DeptServiceImpl部门服务接口实现类

package com.atguigu.springcloud.service.impl;  import java.util.List;  import org.springframework.beans.factory.annotation.Autowired; import org.springframework.stereotype.Service;  import com.atguigu.springcloud.dao.DeptDao; import com.atguigu.springcloud.entities.Dept; import com.atguigu.springcloud.service.DeptService;...

DeptController部门微服务提供者REST

package com.atguigu.springcloud.controller;  import java.util.List;  import org.springframework.beans.factory.annotation.Autowired; import org.springframework.web.bind.annotation.PathVariable; import org.springframework.web.bind.annotation.RequestBody; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RequestMethod; import org.springframework.web.bind.annotation.RestController;...

DeptProvider8001_App主启动类DeptProvider8001_App

package com.atguigu.springcloud;  import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication;  \@SpringBootApplication public class DeptProvider8001_App { public static void main(String\[\] args) {...

测试

###### http://localhost:8001/dept/get/2

###### http://localhost:8001/dept/list

##### 最终工程展现

###### 

#### microservicecloud-consumer-dept-80 部门微服务消费者Module

##### 新建microservicecloud-consumer-dept-80

##### POM

```xml
\<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...
```

YML

```y
  server: port: 80

  com.atguigu.springcloud.cfgbeans包下ConfigBean的编写（类似spring里面的applicationContext.xml写入的注入Bean）

 
```

```java
 package com.atguigu.springcloud.cfgbeans;  import org.springframework.context.annotation.Bean; import org.springframework.context.annotation.Configuration; import org.springframework.web.client.RestTemplate;  \@Configuration public class ConfigBean { \@Bean...

##### com.atguigu.springcloud.controller包下新建DeptController_Consumer部门微服务消费者REST
```

 

###### RestTemplate

####### 是什么

######## RestTemplate提供了多种便捷访问远程Http服务的方法， 是一种简单便捷的访问restful服务模板类，是Spring提供的用于访问Rest服务的客户端模板工具集

####### 官网及使用

######## 官网地址  https://docs.spring.io/spring-framework/docs/4.3.7.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html   使用 使用restTemplate访问restful接口非常的简单粗暴无脑。 (url, requestMap, ResponseBean.class)这三个参数分别代表 REST请求地址、请求参数、HTTP响应转换被转换成的对象类型。

###### 代码

####### package com.atguigu.springcloud.controller;  import java.util.List;  import org.springframework.beans.factory.annotation.Autowired; import org.springframework.web.bind.annotation.PathVariable; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RestController; import org.springframework.web.client.RestTemplate; ...

##### DeptConsumer80_App主启动类

package com.atguigu.springcloud;  import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication;   \@SpringBootApplication public class DeptConsumer80_App { public static void main(String\[\] args)...

##### 测试

###### http://localhost/consumer/dept/get/2

###### http://localhost/consumer/dept/list

###### http://localhost/consumer/dept/add?dname=AI

## Eureka服务注册与发现

### 是什么

> Eureka是什么  Eureka是Netflix的一个子模块，也是核心模块之一。Eureka是一个基于REST的服务，用于定位服务，以实现云端中间层服务发现和故障转移。  服务注册与发现对于微服务架构来说是非常重要的，有了服务发现与注册，只需要使用服务的标识符，就可以访问到服务，而不需要修改服务调用的配置文件了。功能类似于dubbo的注册中心，比如Zookeeper。

#### 

### 原理讲解

Eureka的基本架构

>Spring Cloud 封装了 Netflix 公司开发的 Eureka 模块来实现服务注册和发现(请对比Zookeeper)。  Eureka 采用了 C-S 的设计架构。Eureka Server 作为服务注册功能的服务器，它是服务注册中心。  而系统中的其他微服务，使用 Eureka 的客户端连接到 Eureka Server并维持心跳连接。这样系统的维护人员就可以通过 Eureka Server 来监控系统中各个微服务是否正常运行。SpringCloud 的一些其他模块（比如Zuul）就可以通过 Eureka Server 来发现系统中的其他微服务，并执行相关的逻辑。 请注意和Dubbo的架构对比  ...

#### 三大角色

Eureka Server 提供服务注册和发现

Service Provider服务提供方将自身服务注册到Eureka，从而使服务消费方能够找到

Service Consumer服务消费方从Eureka获取注册服务列表，从而能够消费服务

构建步骤

microservicecloud-eureka-7001 eureka服务注册中心Module

新建microservicecloud-eureka-7001

POM

<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

YML

server: port: 7001  eureka: instance: hostname: localhost \#eureka服务端的实例名称 client: register-with-eureka: false \#false表示不向注册中心注册自己。 fetch-registry: false \#false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务 service-url:...

EurekaServer7001_App主启动类

package com.atguigu.springcloud;  import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication; import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;  \@SpringBootApplication \@EnableEurekaServer//EurekaServer服务器端启动类,接受其它微服务注册进来 public class EurekaServer7001_App {...

@EnableEurekaServer

测试

###### http://localhost:7001/

结果页面

####### 

####### No application available 没有服务被发现 O(∩\_∩)O 因为没有注册服务进来当然不可能有服务被发现

microservicecloud-provider-dept-8001 将已有的部门微服务注册进eureka服务中心

修改microservicecloud-provider-dept-8001

POM

修改部分

####### \<`<!-- 将微服务provider侧注册进eureka -->`{=html} \<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.cloud\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-cloud-starter-eureka\<`</artifactid>`{=html} \<`</dependency>`{=html} \<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.cloud\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-cloud-starter-config\<`</artifactid>`{=html} \<`</dependency>`{=html}

###### 完整内容

####### \<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

##### YML

###### 修改部分

####### eureka: client: \#客户端注册进eureka服务列表内 service-url: defaultZone: http://localhost:7001/eureka

###### 完整内容

####### server: port: 8001  mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \# mybatis配置文件所在路径 type-aliases-package: com.atguigu.springcloud.entities \# 所有Entity别名类所在包 mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \# mapper映射文件  spring:...

DeptProvider8001_App主启动类

package com.atguigu.springcloud;  import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication; import org.springframework.cloud.netflix.eureka.EnableEurekaClient;  \@SpringBootApplication \@EnableEurekaClient //本服务启动后会自动注册进eureka服务中 public class DeptProvider8001_App {...

\@EnableEurekaClient

测试

先要启动EurekaServer

###### http://localhost:7001/

####### 

微服务注册名配置说明

####### 

actuator与注册微服务信息完善

主机名称:服务名称修改

当前问题

####### 含有主机名称

修改microservicecloud-provider-dept-8001

####### YML

######## 修改部分

######### eureka: client: \#客户端注册进eureka服务列表内 service-url: defaultZone: http://localhost:7001/eureka instance: instance-id: microservicecloud-dept8001

######## 完整内容

######### server: port: 8001  mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \#mybatis所在路径 type-aliases-package: com.atguigu.springcloud.entities \#entity别名类 mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \#mapper映射文件  spring:...

修改之后

####### 

访问信息有IP信息提示

当前问题

####### 没有IP提示

修改microservicecloud-provider-dept-8001

####### YML

######## 修改部分

######### eureka: client: \#客户端注册进eureka服务列表内 service-url: defaultZone: http://localhost:7001/eureka instance: instance-id: microservicecloud-dept8001 \#自定义服务名称信息 prefer-ip-address: true \#访问路径可以显示IP地址

######## 完整内容

######### server: port: 8001  mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \#mybatis所在路径 type-aliases-package: com.atguigu.springcloud.entities \#entity别名类 mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \#mapper映射文件  spring:...

修改之后

####### 

微服务info内容详细信息

当前问题

####### 超链接点击服务报告ErrorPage

修改microservicecloud-provider-dept-8001

####### POM

######## 修改部分

######### \<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.boot\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-boot-starter-actuator\<`</artifactid>`{=html} \<`</dependency>`{=html}

######## 完整内容

######### \<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

总的父工程microservicecloud修改pom.xml添加构建build信息

####### POM

######## 修改部分

######### \<`<build>`{=html} \<`<finalname>`{=html}microservicecloud\<`</finalname>`{=html} \<`<resources>`{=html} \<`<resource>`{=html} \<`<directory>`{=html}src/main/resources\<`</directory>`{=html} \<`<filtering>`{=html}true\<`</filtering>`{=html} \<`</resource>`{=html} \<`</resources>`{=html} \<`<plugins>`{=html} \<`<plugin>`{=html}...

######## 完整内容

######### \<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html} \<`<packaging>`{=html}pom\<`</packaging>`{=html}...

###### 修改microservicecloud-provider-dept-8001

####### YML

######## 修改部分

######### info: app.name: atguigu-microservicecloud company.name: www.atguigu.com build.artifactId: $project.artifactId$ build.version: $project.version$

######## 完整内容

######### server: port: 8001  mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \#mybatis所在路径 type-aliases-package: com.atguigu.springcloud.entities \#entity别名类 mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \#mapper映射文件  spring:...

#### eureka自我保护

##### 演示Case

##### 故障现象

###### 

###### 

##### 导致原因

什么是自我保护模式？  默认情况下，如果EurekaServer在一定时间内没有接收到某个微服务实例的心跳，EurekaServer将会注销该实例（默认90秒）。但是当网络分区故障发生时，微服务与EurekaServer之间无法正常通信，以上行为可能变得非常危险了------因为微服务本身其实是健康的，此时本不应该注销这个微服务。Eureka通过"自我保护模式"来解决这个问题------当EurekaServer节点在短时间内丢失过多客户端时（可能发生了网络分区故障），那么这个节点就会进入自我保护模式。一旦进入该模式，EurekaServer就会保护服务注册表中的信息，不再删除服务注册表中的数据（也就是不会注销任何微服务）。当网络故障恢复后，该Eureka Server节点会自动退出自我保护模式。  在自我保护模式中，Eureka Server会保护服务注册表中的信息，不再注销任何服务实例。当它收到的心跳数重新恢复到阈值以上时，该Eureka Server节点就会自动退出自我保护模式。它的设计哲学就是宁可保留错误的服务注册信息，也不盲目注销任何可能健康的服务实例。一句话讲解：好死不如赖活着...

一句话：某时刻某一个微服务不可用了，eureka不会立刻清理，依旧会对该微服务的信息进行保存

集群配置

原理说明

新建microservicecloud-eureka-7002/microservicecloud-eureka-7003

按照7001为模板粘贴POM

修改7002和7003的主启动类

修改映射配置

找到C:\\Windows\\System32\\drivers\\etc路径下的hosts文件

###### 

修改映射配置添加进hosts文件

127.0.0.1 eureka7001.com

127.0.0.1 eureka7002.com

127.0.0.1 eureka7003.com

3台eureka服务器的yml配置

7001

server: port: 7001  eureka: instance: hostname: eureka7001.com \#eureka服务端的实例名称 client: register-with-eureka: false \#false表示不向注册中心注册自己。 fetch-registry: false \#false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务 service-url: ...

7002

server: port: 7002  eureka: instance: hostname: eureka7002.com \#eureka服务端的实例名称 client: register-with-eureka: false \#false表示不向注册中心注册自己。 fetch-registry: false \#false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务 service-url: ...

7003

server: port: 7003  eureka: instance: hostname: eureka7003.com \#eureka服务端的实例名称 client: register-with-eureka: false \#false表示不向注册中心注册自己。 fetch-registry: false \#false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务 service-url: ...

microservicecloud-provider-dept-8001 微服务发布到上面3台eureka集群配置中

YML

server: port: 8001  mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \#mybatis所在路径 type-aliases-package: com.atguigu.springcloud.entities \#entity别名类 mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \#mapper映射文件  spring:...

## Ribbon负载均衡

概述

是什么

Spring Cloud Ribbon是基于Netflix Ribbon实现的一套客户端 负载均衡的工具。  简单的说，Ribbon是Netflix发布的开源项目，主要功能是提供客户端的软件负载均衡算法，将Netflix的中间层服务连接在一起。Ribbon客户端组件提供一系列完善的配置项如连接超时，重试等。简单的说，就是在配置文件中列出Load Balancer（简称LB）后面所有的机器，Ribbon会自动的帮助你基于某种规则（如简单轮询，随机连接等）去连接这些机器。我们也很容易使用Ribbon实现自定义的负载均衡算法。

##### 

能干吗

LB（负载均衡）

LB，即负载均衡(Load Balance)，在微服务或分布式集群中经常用的一种应用。 负载均衡简单的说就是将用户的请求平摊的分配到多个服务上，从而达到系统的HA。 常见的负载均衡有软件Nginx，LVS，硬件 F5等。 相应的在中间件，例如：dubbo和SpringCloud中均给我们提供了负载均衡，SpringCloud的负载均衡算法可以自定义。

###### 集中式LB

####### 集中式LB  即在服务的消费方和提供方之间使用独立的LB设施(可以是硬件，如F5, 也可以是软件，如nginx), 由该设施负责把访问请求通过某种策略转发至服务的提供方；

###### 进程内LB

####### 进程内LB  将LB逻辑集成到消费方，消费方从服务注册中心获知有哪些地址可用，然后自己再从这些地址中选择出一个合适的服务器。  Ribbon就属于进程内LB，它只是一个类库，集成于消费方进程，消费方通过它来获取到服务提供方的地址。

#### 官网资料

##### https://github.com/Netflix/ribbon/wiki/Getting-Started

### Ribbon配置初步

修改microservicecloud-consumer-dept-80工程

修改pom.xml文件

内容

\<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

#### 修改application.yml 追加eureka的服务注册地址

内容

server: port: 80  eureka: client: register-with-eureka: false service-url: defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/,http://eureka7003.com:7003/eureka/

对ConfigBean进行新注解\@LoadBalanced 获得Rest时加入Ribbon的配置

package com.atguigu.springcloud.cfgbeans;  import org.springframework.cloud.client.loadbalancer.LoadBalanced; import org.springframework.context.annotation.Bean; import org.springframework.context.annotation.Configuration; import org.springframework.web.client.RestTemplate;  \@Configuration public class ConfigBean {...

主启动类DeptConsumer80_App添加\@EnableEurekaClient

package com.atguigu.springcloud;  import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication; import org.springframework.cloud.netflix.eureka.EnableEurekaClient;   \@SpringBootApplication \@EnableEurekaClient public class DeptConsumer80_App...

修改DeptController_Consumer客户端访问类

package com.atguigu.springcloud.controller;  import java.util.List;  import org.springframework.beans.factory.annotation.Autowired; import org.springframework.web.bind.annotation.PathVariable; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RestController; import org.springframework.web.client.RestTemplate; ...

先启动3个eureka集群后，再启动microservicecloud-provider-dept-8001并注册进eureka

##### 

启动microservicecloud-consumer-dept-80

测试

http://localhost/consumer/dept/get/1

http://localhost/consumer/dept/list

http://localhost/consumer/dept/add?dname=大数据部

小总结

Ribbon和Eureka整合后Consumer可以直接调用服务而不用再关心地址和端口号

###### 

### Ribbon负载均衡

架构说明

Ribbon在工作时分成两步 第一步先选择 EurekaServer ,它优先选择在同一个区域内负载较少的server. 第二步再根据用户指定的策略，在从server取到的服务注册列表中选择一个地址。 其中Ribbon提供了多种策略：比如轮询、随机和根据响应时间加权。

参考microservicecloud-provider-dept-8001，新建两份，分别命名为8002，8003

新建8002/8003数据库，各自微服务分别连各自的数据库

8002SQL脚本

DROP DATABASE IF EXISTS cloudDB02;  CREATE DATABASE cloudDB02 CHARACTER SET UTF8;  USE cloudDB02;  CREATE TABLE dept ( deptno BIGINT NOT NULL PRIMARY KEY AUTO_INCREMENT, dname VARCHAR(60),...

8003SQL脚本

DROP DATABASE IF EXISTS cloudDB03;  CREATE DATABASE cloudDB03 CHARACTER SET UTF8;  USE cloudDB03;   CREATE TABLE dept ( deptno BIGINT NOT NULL PRIMARY KEY AUTO_INCREMENT,...

修改8002/8003各自YML

8002YML

server: port: 8002  mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \#mybatis所在路径 type-aliases-package: com.atguigu.springcloud.entities \#entity别名类 mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \#mapper映射文件  spring:...

8003YML

server: port: 8003  mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \#mybatis所在路径 type-aliases-package: com.atguigu.springcloud.entities \#entity别名类 mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \#mapper映射文件  spring:...

备注

端口

数据库链接

####### 

对外暴露的统一的服务实例名

####### 

启动3个eureka集群配置区

启动3个Dept微服务启动并各自测试通过

##### http://localhost:8001/dept/list

##### http://localhost:8002/dept/list

##### http://localhost:8003/dept/list

启动microservicecloud-consumer-dept-80

客户端通过Ribbo完成负载均衡并访问上一步的Dept微服务

##### http://localhost/consumer/dept/list

注意观察看到返回的数据库名字，各不相同，负载均衡实现

总结：Ribbon其实就是一个软负载均衡的客户端组件， 他可以和其他所需请求的客户端结合使用，和eureka结合只是其中的一个实例。

## Feign负载均衡

概述

官网解释： http://projects.spring.io/spring-cloud/spring-cloud.html\#spring-cloud-feign  Feign是一个声明式WebService客户端。使用Feign能让编写Web Service客户端更加简单, 它的使用方法是定义一个接口，然后在上面添加注解，同时也支持JAX-RS标准的注解。Feign也支持可拔插式的编码器和解码器。Spring Cloud对Feign进行了封装，使其支持了Spring MVC标准注解和HttpMessageConverters。Feign可以与Eureka和Ribbon组合使用以支持负载均衡。 ；  Feign是一个声明式的Web服务客户端，使得编写Web服务客户端变得非常容易，...

#### 

### Feign使用步骤

参考microservicecloud-consumer-dept-80

新建microservicecloud-consumer-dept-feign

修改主启动类名字

DeptConsumer80_Feign_App

microservicecloud-consumer-dept-feign工程pom.xml修改，主要添加对feign的支持

\<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.cloud\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-cloud-starter-feign\<`</artifactid>`{=html} \<`</dependency>`{=html}

修改microservicecloud-api工程

POM

<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html}\<`<!-- 子类里面显示声明才能有明确的继承表现，无意外就是父类的默认版本否则自己定义 -->`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

新建DeptClientService接口并新增注解\@FeignClient

package com.atguigu.springcloud.service;  import java.util.List;  import org.springframework.cloud.netflix.feign.FeignClient; import org.springframework.web.bind.annotation.PathVariable; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RequestMethod;  import com.atguigu.springcloud.entities.Dept;...

@FeignClient

mvn clean

mvn install

microservicecloud-consumer-dept-feign工程修改Controller，添加上一步新建的DeptClientService接口

package com.atguigu.springcloud.controller;  import java.util.List;  import org.springframework.beans.factory.annotation.Autowired; import org.springframework.web.bind.annotation.PathVariable; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RestController;  import com.atguigu.springcloud.entities.Dept;...

microservicecloud-consumer-dept-feign工程修改主启动类

package com.atguigu.springcloud;  import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication; import org.springframework.cloud.netflix.eureka.EnableEurekaClient; import org.springframework.cloud.netflix.feign.EnableFeignClients;   \@SpringBootApplication \@EnableEurekaClient...

@EnableFeignClients

测试

启动3个eureka集群

启动3个部门微服务8001/8002/8003

启动Feign自己启动

##### http://localhost/consumer/dept/list

Feign自带负载均衡配置项

小总结

Feign通过接口的方法调用Rest服务（之前是Ribbon+RestTemplate）， 该请求发送给Eureka服务器（http://MICROSERVICECLOUD-DEPT/dept/list）, 通过Feign直接找到服务接口，由于在进行服务调用的时候融合了Ribbon技术，所以也支持负载均衡作用。

## Hystrix断路器

概述

分布式系统面临的问题

>分布式系统面临的问题 复杂分布式体系结构中的应用程序有数十个依赖关系，每个依赖关系在某些时候将不可避免地失败。   服务雪崩 多个微服务之间调用的时候，假设微服务A调用微服务B和微服务C，微服务B和微服务C又调用其它的微服务，这就是所谓的"扇出"。如果扇出的链路上某个微服务的调用响应时间过长或者不可用，对微服务A的调用就会占用越来越多的系统资源，进而引起系统崩溃，所谓的"雪崩效应".  对于高流量的应用来说，单一的后端依赖可能会导致所有服务器上的所有资源都在几秒钟内饱和。比失败更糟糕的是，这些应用程序还可能导致服务之间的延迟增加，备份队列，线程和其他系统资源紧张，导致整个系统发生更多的级联故障。这些都表示需要对故障和延迟进行隔离和管理，以便单个依赖关系的失败，不能取消整个应用程序或系统。

#### 是什么

Hystrix是一个用于处理分布式系统的延迟和容错的开源库，在分布式系统里，许多依赖不可避免的会调用失败，比如超时、异常等，Hystrix能够保证在一个依赖出问题的情况下，不会导致整体服务失败，避免级联故障，以提高分布式系统的弹性。  "断路器"本身是一种开关装置，当某个服务单元发生故障之后，通过断路器的故障监控（类似熔断保险丝），向调用方返回一个符合预期的、可处理的备选响应（FallBack），而不是长时间的等待或者抛出调用方无法处理的异常，这样就保证了服务调用方的线程不会被长时间、不必要地占用，从而避免了故障在分布式系统中的蔓延，乃至雪崩。

##### 

能干嘛

服务降级

服务熔断

服务限流

接近实时的监控

##### 。。。。。。

#### 官网资料

##### https://github.com/Netflix/Hystrix/wiki/How-To-Use

### 服务熔断

#### 

> 是什么
>
> 服务熔断 熔断机制是应对雪崩效应的一种微服务链路保护机制。 当扇出链路的某个微服务不可用或者响应时间太长时，会进行服务的降级，进而熔断该节点微服务的调用，快速返回"错误"的响应信息。当检测到该节点微服务调用响应正常后恢复调用链路。在SpringCloud框架里熔断机制通过Hystrix实现。Hystrix会监控微服务间调用的状况，当失败的调用到一定阈值，缺省是5秒内20次调用失败就会启动熔断机制。熔断机制的注解是

##### @HystrixCommand。

参考microservicecloud-provider-dept-8001

新建microservicecloud-provider-dept-hystrix-8001

POM

修改内容

<`<!--  hystrix -->`{=html} \<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.cloud\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-cloud-starter-hystrix\<`</artifactid>`{=html} \<`</dependency>`{=html}

全部内容

\<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

#### YML

server: port: 8001  mybatis: config-location: classpath:mybatis/mybatis.cfg.xml \#mybatis所在路径 type-aliases-package: com.atguigu.springcloud.entities \#entity别名类 mapper-locations: - classpath:mybatis/mapper/\*\*/\*.xml \#mapper映射文件  spring:...

修改DeptController

@HystrixCommand报异常后如何处理

###### 

一旦调用服务方法失败并抛出了错误信息后，会自动调用\@HystrixCommand标注好的fallbackMethod调用类中的指定方法

代码内容

package com.atguigu.springcloud.controller;   import org.springframework.beans.factory.annotation.Autowired; import org.springframework.web.bind.annotation.PathVariable; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RequestMethod; import org.springframework.web.bind.annotation.RestController;  import com.atguigu.springcloud.entities.Dept;...

修改主启动类DeptProvider8001_Hystrix_App并添加新注解\@EnableCircuitBreaker

#### 测试

3个eureka先启动

主启动类DeptProvider8001_Hystrix_App

###### 

Consumer启动microservicecloud-consumer-dept-80

##### http://localhost/consumer/dept/get/112

如果对应的ID：112，数据库里面没有这个记录，我们报错后统一返回。

### 服务降级

是什么

整体资源快不够了，忍痛将某些服务先关掉，待渡过难关，再开启回来。

服务降级处理是在客户端实现完成的，与服务端没有关系

修改microservicecloud-api工程， 根据已经有的DeptClientService接口新建一个实现了 FallbackFactory接口的类DeptClientServiceFallbackFactory

package com.atguigu.springcloud.service;  import java.util.List;  import org.springframework.stereotype.Component;  import com.atguigu.springcloud.entities.Dept;  import feign.hystrix.FallbackFactory; ...

千万不要忘记在类上面新增\@Component注解，大坑！！！

修改microservicecloud-api工程，DeptClientService接口在注解\@FeignClient中添加fallbackFactory属性值

package com.atguigu.springcloud.service;  import java.util.List;  import org.springframework.cloud.netflix.feign.FeignClient; import org.springframework.web.bind.annotation.PathVariable; import org.springframework.web.bind.annotation.RequestMapping; import org.springframework.web.bind.annotation.RequestMethod;  import com.atguigu.springcloud.entities.Dept;...

microservicecloud-api工程

mvn clean install

microservicecloud-consumer-dept-feign工程修改YML

YML

server: port: 80  feign: hystrix: enabled: true  eureka: client: register-with-eureka: false...

测试

3个eureka先启动

微服务microservicecloud-provider-dept-8001启动

microservicecloud-consumer-dept-feign启动

正常访问测试

###### http://localhost/consumer/dept/get/1

故意关闭微服务microservicecloud-provider-dept-8001

客户端自己调用提示

###### http://localhost/consumer/dept/get/1

###### 

此时服务端provider已经down了，但是我们做了服务降级处理，让客户端在服务端不可用时也会获得提示信息而不会挂起耗死服务器

### 服务监控hystrixDashboard

概述

>除了隔离依赖服务的调用以外，Hystrix还提供了准实时的调用监控（Hystrix Dashboard），Hystrix会持续地记录所有通过Hystrix发起的请求的执行信息，并以统计报表和图形的形式展示给用户，包括每秒执行多少请求多少成功，多少失败等。Netflix通过hystrix-metrics-event-stream项目实现了对以上指标的监控。Spring Cloud也提供了Hystrix Dashboard的整合，对监控内容转化成可视化界面。

#### Case步骤

新建工程microservicecloud-consumer-hystrix-dashboard

##### POM

###### 修改内容

####### \<`<!-- hystrix和 hystrix-dashboard相关-->`{=html} \<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.cloud\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-cloud-starter-hystrix\<`</artifactid>`{=html} \<`</dependency>`{=html} \<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.cloud\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-cloud-starter-hystrix-dashboard\<`</artifactid>`{=html} \<`</dependency>`{=html}

###### 全部内容

####### \<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

YML

server: port: 9001

主启动类改名+新注解\@EnableHystrixDashboard

package com.atguigu.springcloud;  import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication; import org.springframework.cloud.netflix.hystrix.dashboard.EnableHystrixDashboard;  \@SpringBootApplication \@EnableHystrixDashboard public class DeptConsumer_DashBoard_App...

所有Provider微服务提供类(8001/8002/8003)都需要监控依赖配置

\<`<!-- actuator监控信息完善 -->`{=html} \<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.boot\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-boot-starter-actuator\<`</artifactid>`{=html} \<`</dependency>`{=html}

启动microservicecloud-consumer-hystrix-dashboard该微服务监控消费端

###### http://localhost:9001/hystrix

####### 

##### 启动3个eureka集群

启动microservicecloud-provider-dept-hystrix-8001

###### http://localhost:8001/dept/get/1

###### http://localhost:8001/hystrix.stream

####### 

##### 启动的相关微服务工程

###### 

##### 监控测试

###### 多次刷新http://localhost:8001/dept/get/1

###### 观察监控窗口

####### 填写监控地址

######## 1：Delay：该参数用来控制服务器上轮询监控信息的延迟时间，默认为2000毫秒，可以通过配置该属性来降低客户端的网络和CPU消耗。  2：Title：该参数对应了头部标题Hystrix Stream之后的内容，默认会使用具体监控实例的URL，可以通过配置该信息来展示更合适的标题。

####### 监控结果

######## 如何看上图

####### 如何看？

######## 7色

######## 1圈

######### 实心圆：共有两种含义。它通过颜色的变化代表了实例的健康程度，它的健康度从绿色\<`<黄色<<橙色<<红色递减。<br>`{=html}该实心圆除了颜色的变化之外，它的大小也会根据实例的请求流量发生变化，流量越大该实心圆就越大。所以通过该实心圆的展示，就可以在大量的实例中快速的发现故障实例和高压力实例。

######## 1线

######### 曲线：用来记录2分钟内流量的相对变化，可以通过它来观察到流量的上升和下降趋势。

######## 整图说明

######### 

####### 搞懂一个才能看懂复杂的

######## 

## zuul路由网关

### 概述

是什么

> Zuul包含了对请求的路由和过滤两个最主要的功能： 其中路由功能负责将外部请求转发到具体的微服务实例上，是实现外部访问统一入口的基础而过滤器功能则负责对请求的处理过程进行干预，是实现请求校验、服务聚合等功能的基础.  Zuul和Eureka进行整合，将Zuul自身注册为Eureka服务治理下的应用，同时从Eureka中获得其他微服务的消息，也即以后的访问微服务都是通过Zuul跳转后获得。  注意：Zuul服务最终还是会注册进Eureka  提供=代理+路由+过滤三大功能

#### 能干嘛

##### 路由

##### 过滤

#### 官网资料

##### https://github.com/Netflix/zuul/wiki/Getting-Started

路由基本配置

新建Module模块microservicecloud-zuul-gateway-9527

POM

修改内容

\<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.cloud\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-cloud-starter-eureka\<`</artifactid>`{=html} \<`</dependency>`{=html} \<`<dependency>`{=html} \<`<groupid>`{=html}org.springframework.cloud\<`</groupid>`{=html} \<`<artifactid>`{=html}spring-cloud-starter-zuul\<`</artifactid>`{=html} \<`</dependency>`{=html}

全部内容

\<`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" <br>`{=html} xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"\> \<`<modelversion>`{=html}4.0.0\<`</modelversion>`{=html}  \<`<parent>`{=html} \<`<groupid>`{=html}com.atguigu.springcloud\<`</groupid>`{=html} \<`<artifactid>`{=html}microservicecloud\<`</artifactid>`{=html} \<`<version>`{=html}0.0.1-SNAPSHOT\<`</version>`{=html}...

YML

server: port: 9527  spring: application: name: microservicecloud-zuul-gateway  eureka: client: service-url: ...

hosts修改

127.0.0.1 myzuul.com

主启动类

package com.atguigu.springcloud;  import org.springframework.boot.SpringApplication; import org.springframework.boot.autoconfigure.SpringBootApplication; import org.springframework.cloud.netflix.zuul.EnableZuulProxy;  \@SpringBootApplication \@EnableZuulProxy public class Zuul_9527_StartSpringCloudApp {...

@EnableZuulProxy

启动

##### 

三个eureka集群

一个服务提供类microservicecloud-provider-dept-8001

一个路由

测试

不用路由

###### http://localhost:8001/dept/get/2

启用路由

###### http://myzuul.com:9527/microservicecloud-dept/dept/get/2

### 路由访问映射规则

工程microservicecloud-zuul-gateway-9527

代理名称

YML

before http://myzuul.com:9527/microservicecloud-dept/dept/get/2   zuul: routes: mydept.serviceId: microservicecloud-dept mydept.path: /mydept/\*\*  after...

此时问题

路由访问OK

####### http://myzuul.com:9527/mydept/dept/get/1

原路径访问OK

####### http://myzuul.com:9527/microservicecloud-dept/dept/get/2

原真实服务名忽略

YML

zuul: ignored-services: microservicecloud-dept routes: mydept.serviceId: microservicecloud-dept mydept.path: /mydept/\*\*

单个具体，多个可以用"\*"

zuul: ignored-services: "\*" routes: mydept.serviceId: microservicecloud-dept mydept.path: /mydept/\*\*

设置统一公共前缀

YML

zuul: prefix: /atguigu ignored-services: "\*" routes: mydept.serviceId: microservicecloud-dept mydept.path: /mydept/\*\*

##### http://myzuul.com:9527/atguigu/mydept/dept/get/1

最后YML

server: port: 9527  spring: application: name: microservicecloud-zuul-gateway  zuul: prefix: /atguigu ignored-services: "\*"...

## 为什么需要学习Spring Cloud

不论是商业应用还是用户应用，在业务初期都很简单，我们通常会把它实现为单体结构的应用。但是，随着业务逐渐发展，产品思想会变得越来越复杂，单体结构的应用也会越来越复杂。这就会给应用带来如下的几个问题：

- 代码结构混乱：业务复杂，导致代码量很大，管理会越来越困难。同时，这也会给业务的快速迭代带来巨大挑战；
- 开发效率变低：开发人员同时开发一套代码，很难避免代码冲突。开发过程会伴随着不断解决冲突的过程，这会严重的影响开发效率；
- 排查解决问题成本高：线上业务发现 bug，修复 bug 的过程可能很简单。但是，由于只有一套代码，需要重新编译、打包、上线，成本很高。

由于单体结构的应用随着系统复杂度的增高，会暴露出各种各样的问题。近些年来，微服务架构逐渐取代了单体架构，且这种趋势将会越来越流行。Spring Cloud是目前最常用的微服务开发框架，已经在企业级开发中大量的应用。

## 什么是Spring Cloud

Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、智能路由、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。Spring Cloud并没有重复制造轮子，它只是将各家公司开发的比较成熟、经得起实际考验的服务框架组合起来，通过Spring Boot风格进行再封装屏蔽掉了复杂的配置和实现原理，最终给开发者留出了一套简单易懂、易部署和易维护的分布式系统开发工具包。

## 设计目标与优缺点

### 设计目标

**协调各个微服务，简化分布式系统开发**。

### 优缺点

微服务的框架那么多比如：dubbo、Kubernetes，为什么就要使用Spring Cloud的呢？

优点：

- 产出于Spring大家族，Spring在企业级开发框架中无人能敌，来头很大，可以保证后续的更新、完善
- 组件丰富，功能齐全。Spring Cloud 为微服务架构提供了非常完整的支持。例如、配置管理、服务发现、断路器、微服务网关等；
- Spring Cloud 社区活跃度很高，教程很丰富，遇到问题很容易找到解决方案
- 服务拆分粒度更细，耦合度比较低，有利于资源重复利用，有利于提高开发效率
- 可以更精准的制定优化服务方案，提高系统的可维护性
- 减轻团队的成本，可以并行开发，不用关注其他人怎么开发，先关注自己的开发
- 微服务可以是跨平台的，可以用任何一种语言开发
- 适于互联网时代，产品迭代周期更短

缺点：

- 微服务过多，治理成本高，不利于维护系统
- 分布式系统开发的成本高（容错，分布式事务等）对团队挑战大

总的来说优点大过于缺点，目前看来Spring Cloud是一套非常完善的分布式框架，目前很多企业开始用微服务、Spring Cloud的优势是显而易见的。因此对于想研究微服务架构的同学来说，学习Spring Cloud是一个不错的选择。

## Spring Cloud发展前景

Spring Cloud对于中小型互联网公司来说是一种福音，因为这类公司往往没有实力或者没有足够的资金投入去开发自己的分布式系统基础设施，使用Spring Cloud一站式解决方案能在从容应对业务发展的同时大大减少开发成本。同时，随着近几年微服务架构和Docker容器概念的火爆，也会让Spring Cloud在未来越来越“云”化的软件开发风格中立有一席之地，尤其是在五花八门的分布式解决方案中提供了标准化的、全站式的技术方案，意义可能会堪比当年Servlet规范的诞生，有效推进服务端软件系统技术水平的进步。

## 整体架构

![img](https://tva1.sinaimg.cn/large/008eGmZEgy1gmio72rd7mj317o0mdn3h.jpg)

## 主要项目

Spring Cloud的子项目，大致可分成两类，一类是对现有成熟框架"Spring Boot化"的封装和抽象，也是数量最多的项目；第二类是开发了一部分分布式系统的基础设施的实现，如Spring Cloud Stream扮演的就是kafka, ActiveMQ这样的角色。

### Spring Cloud Config

集中配置管理工具，分布式系统中统一的外部配置管理，默认使用Git来存储配置，可以支持客户端配置的刷新及加密、解密操作。

### Spring Cloud Netflix

Netflix OSS 开源组件集成，包括Eureka、Hystrix、Ribbon、Feign、Zuul等核心组件。

- Eureka：服务治理组件，包括服务端的注册中心和客户端的服务发现机制；
- Ribbon：负载均衡的服务调用组件，具有多种负载均衡调用策略；
- Hystrix：服务容错组件，实现了断路器模式，为依赖服务的出错和延迟提供了容错能力；
- Feign：基于Ribbon和Hystrix的声明式服务调用组件；
- Zuul：API网关组件，对请求提供路由及过滤功能。

### Spring Cloud Bus

用于传播集群状态变化的消息总线，使用轻量级消息代理链接分布式系统中的节点，可以用来动态刷新集群中的服务配置。

### Spring Cloud Consul

基于Hashicorp Consul的服务治理组件。

### Spring Cloud Security

安全工具包，对Zuul代理中的负载均衡OAuth2客户端及登录认证进行支持。

### Spring Cloud Sleuth

Spring Cloud应用程序的分布式请求链路跟踪，支持使用Zipkin、HTrace和基于日志（例如ELK）的跟踪。

### Spring Cloud Stream

轻量级事件驱动微服务框架，可以使用简单的声明式模型来发送及接收消息，主要实现为Apache Kafka及RabbitMQ。

### Spring Cloud Task

用于快速构建短暂、有限数据处理任务的微服务框架，用于向应用中添加功能性和非功能性的特性。

### Spring Cloud Zookeeper

基于Apache Zookeeper的服务治理组件。

### Spring Cloud Gateway

API网关组件，对请求提供路由及过滤功能。

### Spring Cloud OpenFeign

基于Ribbon和Hystrix的声明式服务调用组件，可以动态创建基于Spring MVC注解的接口实现用于服务调用，在Spring Cloud 2.0中已经取代Feign成为了一等公民。

## Spring Cloud的版本关系

Spring Cloud是一个由许多子项目组成的综合项目，各子项目有不同的发布节奏。 为了管理Spring Cloud与各子项目的版本依赖关系，发布了一个清单，其中包括了某个Spring Cloud版本对应的子项目版本。 为了避免Spring Cloud版本号与子项目版本号混淆，Spring Cloud版本采用了名称而非版本号的命名，这些版本的名字采用了伦敦地铁站的名字，根据字母表的顺序来对应版本时间顺序，例如Angel是第一个版本，Brixton是第二个版本。 当Spring Cloud的发布内容积累到临界点或者一个重大BUG被解决后，会发布一个"service releases"版本，简称SRX版本，比如Greenwich.SR2就是Spring Cloud发布的Greenwich版本的第2个SRX版本。目前Spring Cloud的最新版本是Hoxton。

### Spring Cloud和SpringBoot版本对应关系

| Spring Cloud Version | SpringBoot Version |
| -------------------- | ------------------ |
| Hoxton               | 2.2.x              |
| Greenwich            | 2.1.x              |
| Finchley             | 2.0.x              |
| Edgware              | 1.5.x              |
| Dalston              | 1.5.x              |

### Spring Cloud和各子项目版本对应关系

| Component              | Edgware.SR6    | Greenwich.SR2 |
| ---------------------- | -------------- | ------------- |
| spring-cloud-bus       | 1.3.4.RELEASE  | 2.1.2.RELEASE |
| spring-cloud-commons   | 1.3.6.RELEASE  | 2.1.2.RELEASE |
| spring-cloud-config    | 1.4.7.RELEASE  | 2.1.3.RELEASE |
| spring-cloud-netflix   | 1.4.7.RELEASE  | 2.1.2.RELEASE |
| spring-cloud-security  | 1.2.4.RELEASE  | 2.1.3.RELEASE |
| spring-cloud-consul    | 1.3.6.RELEASE  | 2.1.2.RELEASE |
| spring-cloud-sleuth    | 1.3.6.RELEASE  | 2.1.1.RELEASE |
| spring-cloud-stream    | Ditmars.SR5    | Fishtown.SR3  |
| spring-cloud-zookeeper | 1.2.3.RELEASE  | 2.1.2.RELEASE |
| spring-boot            | 1.5.21.RELEASE | 2.1.5.RELEASE |
| spring-cloud-task      | 1.2.4.RELEASE  | 2.1.2.RELEASE |
| spring-cloud-gateway   | 1.0.3.RELEASE  | 2.1.2.RELEASE |
| spring-cloud-openfeign | 暂无           | 2.1.2.RELEASE |

**注意：Hoxton版本是基于SpringBoot 2.2.x版本构建的，不适用于1.5.x版本。随着2019年8月SpringBoot 1.5.x版本停止维护，Edgware版本也将停止维护。**

## SpringBoot和SpringCloud的区别？

SpringBoot专注于快速方便的开发单个个体微服务。

SpringCloud是关注全局的微服务协调整理治理框架，它将SpringBoot开发的一个个单体微服务整合并管理起来，

为各个微服务之间提供，配置管理、服务发现、断路器、路由、微代理、事件总线、全局锁、决策竞选、分布式会话等等集成服务

SpringBoot可以离开SpringCloud独立使用开发项目， 但是SpringCloud离不开SpringBoot ，属于依赖的关系

SpringBoot专注于快速、方便的开发单个微服务个体，SpringCloud关注全局的服务治理框架。

## 使用 Spring Boot 开发分布式微服务时，我们面临以下问题

（1）与分布式系统相关的复杂性-这种开销包括网络问题，延迟开销，带宽问题，安全问题。

（2）服务发现-服务发现工具管理群集中的流程和服务如何查找和互相交谈。它涉及一个服务目录，在该目录中注册服务，然后能够查找并连接到该目录中的服务。

（3）冗余-分布式系统中的冗余问题。

（4）负载平衡 --负载平衡改善跨多个计算资源的工作负荷，诸如计算机，计算机集群，网络链路，中央处理单元，或磁盘驱动器的分布。

（5）性能-问题 由于各种运营开销导致的性能问题。

（6）部署复杂性-Devops 技能的要求。

## 服务注册和发现是什么意思？Spring Cloud 如何实现？

当我们开始一个项目时，我们通常在属性文件中进行所有的配置。随着越来越多的服务开发和部署，添加和修改这些属性变得更加复杂。有些服务可能会下降，而某些位置可能会发生变化。手动更改属性可能会产生问题。 Eureka 服务注册和发现可以在这种情况下提供帮助。由于所有服务都在 Eureka 服务器上注册并通过调用 Eureka 服务器完成查找，因此无需处理服务地点的任何更改和处理。

## Spring Cloud 和dubbo区别?

（1）服务调用方式 dubbo是RPC springcloud Rest Api

（2）注册中心,dubbo 是zookeeper springcloud是eureka，也可以是zookeeper

（3）服务网关,dubbo本身没有实现，只能通过其他第三方技术整合，springcloud有Zuul路由网关，作为路由服务器，进行消费者的请求分发,springcloud支持断路器，与git完美集成配置文件支持版本控制，事物总线实现配置文件的更新与服务自动装配等等一系列的微服务架构要素。

## 负载平衡的意义什么？

在计算中，负载平衡可以改善跨计算机，计算机集群，网络链接，中央处理单元或磁盘驱动器等多种计算资源的工作负载分布。负载平衡旨在优化资源使用，最大化吞吐量，最小化响应时间并避免任何单一资源的过载。使用多个组件进行负载平衡而不是单个组件可能会通过冗余来提高可靠性和可用性。负载平衡通常涉及专用软件或硬件，例如多层交换机或域名系统服务器进程。

## 什么是 Hystrix？它如何实现容错？

Hystrix 是一个延迟和容错库，旨在隔离远程系统，服务和第三方库的访问点，当出现故障是不可避免的故障时，停止级联故障并在复杂的分布式系统中实现弹性。

通常对于使用微服务架构开发的系统，涉及到许多微服务。这些微服务彼此协作。

思考以下微服务

![img](https://tva1.sinaimg.cn/large/008eGmZEgy1gmio74zrvzj30fa07nwej.jpg)

假设如果上图中的微服务 9 失败了，那么使用传统方法我们将传播一个异常。但这仍然会导致整个系统崩溃。

随着微服务数量的增加，这个问题变得更加复杂。微服务的数量可以高达 1000.这是 hystrix 出现的地方 我们将使用 Hystrix 在这种情况下的 Fallback 方法功能。我们有两个服务 employee-consumer 使用由 employee-consumer 公开的服务。

简化图如下所示

![img](https://tva1.sinaimg.cn/large/008eGmZEgy1gmio73kbolj30fa04agli.jpg)

现在假设由于某种原因，employee-producer 公开的服务会抛出异常。我们在这种情况下使用 Hystrix 定义了一个回退方法。这种后备方法应该具有与公开服务相同的返回类型。如果暴露服务中出现异常，则回退方法将返回一些值。

## 什么是 Hystrix 断路器？我们需要它吗？

由于某些原因，employee-consumer 公开服务会引发异常。在这种情况下使用Hystrix 我们定义了一个回退方法。如果在公开服务中发生异常，则回退方法返回一些默认值。

![img](https://tva1.sinaimg.cn/large/008eGmZEgy1gmio75eq8vj30fa07bdfx.jpg)

如果 firstPage method() 中的异常继续发生，则 Hystrix 电路将中断，并且员工使用者将一起跳过 firtsPage 方法，并直接调用回退方法。 断路器的目的是给第一页方法或第一页方法可能调用的其他方法留出时间，并导致异常恢复。可能发生的情况是，在负载较小的情况下，导致异常的问题有更好的恢复机会 。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-nMSJX6ml-1582105816943)(https://user-gold-cdn.xitu.io/2019/12/30/16f55fbfd4e33ae7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)]

## 什么是 Netflix Feign？它的优点是什么？

Feign 是受到 Retrofit，JAXRS-2.0 和 WebSocket 启发的 java 客户端联编程序。

Feign 的第一个目标是将约束分母的复杂性统一到 http apis，而不考虑其稳定性。

在 employee-consumer 的例子中，我们使用了 employee-producer 使用 REST模板公开的 REST 服务。

但是我们必须编写大量代码才能执行以下步骤

（1）使用功能区进行负载平衡。

（2）获取服务实例，然后获取基本 URL。

（3）利用 REST 模板来使用服务。 前面的代码如下

```java
@Controller
public class ConsumerControllerClient {
@Autowired
private LoadBalancerClient loadBalancer;
public void getEmployee() throws RestClientException, IOException {
	ServiceInstance serviceInstance=loadBalancer.choose("employee-producer");
	System.out.println(serviceInstance.getUri());
	String baseUrl=serviceInstance.getUri().toString();
	baseUrl=baseUrl+"/employee";
	RestTemplate restTemplate = new RestTemplate();
	ResponseEntity<String> response=null;
	try{
		response=restTemplate.exchange(baseUrl,
					HttpMethod.GET, getHeaders(),String.class);
	}
	catch (Exception ex)
		{
		System.out.println(ex);
	}
	System.out.println(response.getBody());
}
123456789101112131415161718192021
```

之前的代码，有像 NullPointer 这样的例外的机会，并不是最优的。我们将看到如何使用 Netflix Feign 使呼叫变得更加轻松和清洁。如果 Netflix Ribbon 依赖关系也在类路径中，那么 Feign 默认也会负责负载平衡。

## 什么是 Spring Cloud Bus？我们需要它吗？

考虑以下情况：我们有多个应用程序使用 Spring Cloud Config 读取属性，而Spring Cloud Config 从 GIT 读取这些属性。

下面的例子中多个员工生产者模块从 Employee Config Module 获取 Eureka 注册的财产。

![img](https://tva1.sinaimg.cn/large/008eGmZEgy1gmio74gudsj30fa0ab3yp.jpg)

如果假设 GIT 中的 Eureka 注册属性更改为指向另一台 Eureka 服务器，会发生什么情况。在这种情况下，我们将不得不重新启动服务以获取更新的属性。

还有另一种使用执行器端点/刷新的方式。但是我们将不得不为每个模块单独调用这个 url。例如，如果 Employee Producer1 部署在端口 8080 上，则调用 http：// localhost：8080 / refresh。同样对于 Employee Producer2 http：//localhost：8081 / refresh 等等。这又很麻烦。这就是 Spring Cloud Bus 发挥作用的地方。

![img](https://tva1.sinaimg.cn/large/008eGmZEgy1gmio723964j30fa0anmxh.jpg)

Spring Cloud Bus 提供了跨多个实例刷新配置的功能。因此，在上面的示例中，如果我们刷新 Employee Producer1，则会自动刷新所有其他必需的模块。如果我们有多个微服务启动并运行，这特别有用。这是通过将所有微服务连接到单个消息代理来实现的。无论何时刷新实例，此事件都会订阅到侦听此代理的所有微服务，并且它们也会刷新。可以通过使用端点/总线/刷新来实现对任何单个实例的刷新。

## Spring Cloud断路器的作用

当一个服务调用另一个服务由于网络原因或自身原因出现问题，调用者就会等待被调用者的响应 当更多的服务请求到这些资源导致更多的请求等待，发生连锁效应（雪崩效应）

断路器有完全打开状态:一段时间内 达到一定的次数无法调用 并且多次监测没有恢复的迹象 断路器完全打开 那么下次请求就不会请求到该服务

半开:短时间内 有恢复迹象 断路器会将部分请求发给该服务，正常调用时 断路器关闭

关闭：当服务一直处于正常状态 能正常调用

## 什么是Spring Cloud Config?

在分布式系统中，由于服务数量巨多，为了方便服务配置文件统一管理，实时更新，所以需要分布式配置中心组件。在Spring Cloud中，有分布式配置中心组件spring cloud config ，它支持配置服务放在配置服务的内存中（即本地），也支持放在远程Git仓库中。在spring cloud config 组件中，分两个角色，一是config server，二是config client。

使用：

（1）添加pom依赖

（2）配置文件添加相关配置

（3）启动类添加注解@EnableConfigServer

## 什么是Spring Cloud Gateway?

Spring Cloud Gateway是Spring Cloud官方推出的第二代网关框架，取代Zuul网关。网关作为流量的，在微服务系统中有着非常作用，网关常见的功能有路由转发、权限校验、限流控制等作用。

使用了一个RouteLocatorBuilder的bean去创建路由，除了创建路由RouteLocatorBuilder可以让你添加各种predicates和filters，predicates断言的意思，顾名思义就是根据具体的请求的规则，由具体的route去处理，filters是各种过滤器，用来对请求做各种判断和修改。