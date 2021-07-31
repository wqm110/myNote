# SpringMVC





## 0 .基本配置

### 加入依赖

```
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.2</version>
</dependency>
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.3.2</version>
</dependency>
```

### Web.xml 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://java.sun.com/xml/ns/javaee"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
	id="WebApp_ID" version="2.5">
<!-- 
配置 org.springframework.web.filter.HiddenHttpMethodFilter: 可以把 POST 请求转为 DELETE 或 POST 请求 
-->
<filter>
	<filter-name>HiddenHttpMethodFilter</filter-name>
	<filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>

<filter-mapping>
	<filter-name>HiddenHttpMethodFilter</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>

<!-- 配置 DispatcherServlet -->
<servlet>
	<servlet-name>dispatcherServlet</servlet-name>
	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	<!-- 配置 DispatcherServlet 的一个初始化参数: 配置 SpringMVC 配置文件的位置和名称 -->
	<!-- 
		实际上也可以不通过 contextConfigLocation 来配置 SpringMVC 的配置文件, 而使用默认的.
		默认的配置文件为: /WEB-INF/<servlet-name>-servlet.xml
	-->
	<!--  
	<init-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>classpath:springmvc.xml</param-value>
	</init-param>
	-->
	<load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
	<servlet-name>dispatcherServlet</servlet-name>
	<url-pattern>/</url-pattern>
</servlet-mapping>
</web-app>
```

。。。。

## 1 . 处理请求 RequestMaping使用

![image-20201225015614362](https://tva1.sinaimg.cn/large/0081Kckwgy1glzheab371j31b80u0wq0.jpg)



![image-20201225015643102](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhernpjqj316u0u0qac.jpg)



![image-20201225015716357](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhfconk4j31b20u0dut.jpg)

### 基本请求

![image-20201225015853188](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhgzxqdpj31cl0u0q95.jpg)

### ant 风格

### ![image-20201225015932857](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhhpgi94j31cm0u0n60.jpg)

### 绑定站位符

![image-20201225020012421](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhifc6nsj31cm0u0dqw.jpg)

![image-20201225020205448](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhkfisl5j317v0u0x03.jpg)

![image-20201225020650672](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhpae9noj31de0u0tfm.jpg)

![image-20201225020758601](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhqh04vpj319y0u0qea.jpg)

![image-20201225020913247](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhrs439cj31dm0u0135.jpg)

#### @RequestParm

![image-20201225021112270](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhtukdpdj31jk0u047n.jpg)

#### @RequestHeader

![image-20201225021212477](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhuwefnwj31lg0rojz5.jpg)

#### @Cookie

![image-20201225021312209](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhvxfpc7j31ki0mc43u.jpg)

#### 对像

![image-20201225021336560](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhwc5cokj31i00ru46c.jpg)

#### Servlet 对象

![image-20201225021518131](https://tva1.sinaimg.cn/large/0081Kckwgy1glzhy3d6xlj31bi0u0wpt.jpg)

#### Request Mapping 可接受的参数

![image-20201225021735894](https://tva1.sinaimg.cn/large/0081Kckwgy1glzi0hqv26j31c40u0tek.jpg)

## 2 . 处理数据



![image-20201225022236874](https://tva1.sinaimg.cn/large/0081Kckwgy1glzi5qb5ptj31h20u0qeh.jpg)

#### 输出 ModelAndView

![image-20201225022352600](https://tva1.sinaimg.cn/large/0081Kckwgy1glzi70fcccj31ii0u0dn2.jpg)



![image-20201225022520235](https://tva1.sinaimg.cn/large/0081Kckwgy1glzi8jb4tbj31900u0k3z.jpg)

![image-20201225022545988](https://tva1.sinaimg.cn/large/0081Kckwgy1glzi8ztuf3j31990u0n4n.jpg)

#### @SessionAttributes

![image-20201225022632916](https://tva1.sinaimg.cn/large/0081Kckwgy1glzi9tvcv9j31c20u0wr2.jpg)

![image-20201225022723181](https://tva1.sinaimg.cn/large/0081Kckwgy1glziaoraawj31ng0sk487.jpg)

![image-20201225022743854](https://tva1.sinaimg.cn/large/0081Kckwgy1glzib15c46j31960u0dkz.jpg)

![image-20201225022820747](https://tva1.sinaimg.cn/large/0081Kckwgy1glzibo8za4j319d0u0q8v.jpg)

#### @ModelAttribute

![image-20201225022855231](https://tva1.sinaimg.cn/large/0081Kckwgy1glzic950dij31ke0raaja.jpg)

![image-20201225023055471](https://tva1.sinaimg.cn/large/0081Kckwgy1glzieemorzj31gr0u0qer.jpg)

## 3 。视图解析

#### 基本流程

![image-20201225023238885](https://tva1.sinaimg.cn/large/0081Kckwgy1glzig522l7j31330u0q7g.jpg)

![image-20201225023321681](https://tva1.sinaimg.cn/large/0081Kckwgy1glzigwzekjj31ln0u04b8.jpg)

#### 视图解析器

![image-20201225023415901](https://tva1.sinaimg.cn/large/0081Kckwgy1glzihubm85j31h10u0ne5.jpg)

![image-20201225023518658](https://tva1.sinaimg.cn/large/0081Kckwgy1glziixym7zj31ch0u04cs.jpg)

![image-20201225023606605](https://tva1.sinaimg.cn/large/0081Kckwgy1glzijyhn0qj31c00u0kjl.jpg)



![image-20201225023732182](https://tva1.sinaimg.cn/large/0081Kckwgy1glzilag9huj31ch0u0h17.jpg)

##### 常用的视图解析器实现类

![image-20201225023813430](https://tva1.sinaimg.cn/large/0081Kckwgy1glzim04wgfj31bf0u0k72.jpg)

![image-20201225023855293](https://tva1.sinaimg.cn/large/0081Kckwgy1glzimosknnj31o20san5c.jpg)

![image-20201225024017949](https://tva1.sinaimg.cn/large/0081Kckwgy1glzio4a2jvj31dg0u0tju.jpg)



![image-20201225024052281](https://tva1.sinaimg.cn/large/0081Kckwgy1glzioqoqy5j319c0u0wrm.jpg)

![image-20201225024123906](https://tva1.sinaimg.cn/large/0081Kckwgy1glzipafk2jj316w0u0qg1.jpg)

## 4 form表单

![image-20201225024255880](https://tva1.sinaimg.cn/large/0081Kckwgy1glziqukcnsj31pi0j6dm6.jpg)

![image-20201225024323717](https://tva1.sinaimg.cn/large/0081Kckwgy1glzirce5d5j31hp0u07fc.jpg)

![image-20201225024409968](https://tva1.sinaimg.cn/large/0081Kckwgy1glzis5e5o3j31kg0u0thh.jpg)

![image-20201225024645232](https://tva1.sinaimg.cn/large/0081Kckwgy1glziuupb50j31aj0u013o.jpg)

![image-20201225024729649](https://tva1.sinaimg.cn/large/0081Kckwgy1glzivm520lj31gs0u0tkx.jpg)

## 5 静态资源处理![image-20201225024817403](https://tva1.sinaimg.cn/large/0081Kckwgy1glziwgxguyj31e00u0apz.jpg)

## 6.数据绑定流程

![image-20201225025016449](https://tva1.sinaimg.cn/large/0081Kckwgy1glziyj3t6qj31cj0u0k5k.jpg)

![image-20201225025120335](https://tva1.sinaimg.cn/large/0081Kckwgy1glzizmj66qj319a0u0dsc.jpg)

![image-20201225025218715](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj0nj61pj311n0u049k.jpg)

![image-20201225025240585](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj12s6njj31es0u0trg.jpg)

### 自定义类型转换器

![image-20201225025316733](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj1oviw7j31aw0u0k6d.jpg)

### spring中支持的3种类型转换器

![image-20201225025350394](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj29nlrdj31hi0u0n90.jpg)

![image-20201225025515625](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj3o9byfj319b0u048x.jpg)

### 关于注解

![image-20201225025552218](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj4cz19kj31d10u0tj9.jpg)

![image-20201225025702884](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj5kgha4j31810u0wrh.jpg)

![image-20201225025753557](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj6g9mlhj319w0u0k3l.jpg)

####  数据格式化

![image-20201225025925358](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj81j8qfj31ez0u0tjq.jpg)

![image-20201225030016354](https://tva1.sinaimg.cn/large/0081Kckwgy1glzj8xgbomj31bc0u0qh1.jpg)

#### 日期

![image-20201225030117565](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjad5927j31cl0u07h5.jpg)

#### 数值

![image-20201225030145093](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjawuf25j31nb0u07cz.jpg)

![image-20201225030218094](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjb0o1ktj310z0u045e.jpg)

![image-20201225030322783](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjc81cqmj31980u07pk.jpg)

#### hibernate扩展

![image-20201225030430009](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjdabw2bj31pe0p2qbq.jpg)

数据校验

![image-20201225030556359](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjeu8xwsj31bd0u0h0e.jpg)

![image-20201225030654214](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjfvn0l2j319q0u0nbr.jpg)

![image-20201225030721609](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjgisxhxj31b70u0qcc.jpg)

![image-20201225030752679](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjgswshcj31jg0tado0.jpg)

![image-20201225030809983](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjh4zj3vj31au0u0495.jpg)

#### 示例

![image-20201225030830431](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjhfwneej31cj0u0grf.jpg)

![image-20201225030858007](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjhzxrw3j30u00xhgs0.jpg)

![image-20201225030946980](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjitfw20j31980u0wrn.jpg)

![image-20201225031044332](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjjt8pxyj319s0u07gg.jpg)

## 7 JSON 处理

![image-20201225031204921](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjl7edkdj310n0u0n5b.jpg)

### MessageConverter

![image-20201225031254936](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjm3gywtj318m0u0ncd.jpg)

![image-20201225031353984](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjn55u7tj31jc0q81b2.jpg)

![image-20201225031422932](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjnnk3asj31e70u0gyz.jpg)

![image-20201225031546519](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjp1dcxpj31i30u0ajo.jpg)

![image-20201225031623153](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjpoi904j31bx0u0k0p.jpg)

![image-20201225031643939](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjq2cjtyj31ma0t24bo.jpg)

![image-20201225031746912](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjr591usj31bb0u0aow.jpg)

![image-20201225031805713](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjrgvb45j318k0u0493.jpg)

## 8 国际化

![image-20201225031857972](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjscuqxej31jg0u0wn5.jpg)

#### LocalResolver 工作流程

![image-20201225032013423](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjtnkdqej319v0u047g.jpg)

#### 配置国际化

![image-20201225032037740](https://tva1.sinaimg.cn/large/0081Kckwgy1glzju34yudj31c10u0151.jpg)

## 9 文件上传

![image-20201225032103697](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjulxlxbj31jw0pkwmd.jpg)

#### 配置文件上传

![image-20201225032152508](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjve737sj31jg0u0ti5.jpg)

![image-20201225032221040](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjvvv9tfj31950u0aj7.jpg)

## 10 自定义拦截器

![image-20201225032252386](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjwgbqkjj319r0u0qio.jpg)

![image-20201225032331824](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjx38to9j319c0u0wj6.jpg)

#### 配置自定义拦截器

![image-20201225032357872](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjxjfweoj31os0ksgtb.jpg)

![image-20201225032558777](https://tva1.sinaimg.cn/large/0081Kckwgy1glzjzn0g65j318p0u0tea.jpg)

![image-20201225032641693](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk0g3pzrj314k0u0n9o.jpg)

##  11 异常处理

![image-20201225032705170](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk0ti208j316j0u049x.jpg)

![image-20201225032756097](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk1p35kdj31c70u0dp8.jpg)

![image-20201225032818534](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk238tebj31f40u0n85.jpg)

![image-20201225032840481](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk2ibsptj315u0u07jz.jpg)

![image-20201225032910802](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk300fcyj31ke0m0qbl.jpg)

![image-20201225032933737](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk3dsixtj31g50u0guf.jpg)

## 12 Spring MVC 的运行流程

![image-20201225033003521](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk40rw8qj314a0u04qp.jpg)

## 13 使用

![image-20201225033314968](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk77dtgcj31dl0u0wur.jpg)

![image-20201225033448611](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk8ug42vj31l20rsqaj.jpg)

![image-20201225033509512](https://tva1.sinaimg.cn/large/0081Kckwgy1glzk979uavj31d20m80vb.jpg)

