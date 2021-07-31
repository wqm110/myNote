# Lombok的基本使用

# Basic use of Lombok

[![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f7bh5onj302o02owea.jpg)](https://www.jianshu.com/u/953d57f301c0)

[忞触动心灵 Minding the soul](https://www.jianshu.com/u/953d57f301c0)关注 Attention

32019.05.11 10:47:06 2019.05.1110:47:06字数 1,223 Word count 1,223阅读 334,147 Read 334,147

**以前的Java项目中，充斥着太多不友好的代码：POJO的getter/setter/toString；异常处理；I/O流的关闭操作等等，这些样板代码既没有技术含量，又影响着代码的美观，Lombok应运而生。**

Previous Java projects have been full of unfriendly code: Getter/setter/toString on pojos; exception handling; I/O stream shutdown operations, and so on. The boilerplate code was neither technical nor aesthetically pleasing, and Lombok was born.



# **为什么推荐使用Lombok:**

# Why Lombok is recommended:

**[@Lombok有啥牛皮的？SpringBoot和IDEA官方都要支持它！](https://links.jianshu.com/go?to=https%3A%2F%2Fmp.weixin.qq.com%2Fs%2FYs6ksYasfUj7TSCGICHM8w)
**

@ What’s Lombok got to hide? Springboot and IDEA both officially support it!

> **最近[IDEA 2020最后一个版本发布了](https://links.jianshu.com/go?to=https%3A%2F%2Fmp.weixin.qq.com%2Fs%3F__biz%3DMzU1Nzg4NjgyMw%3D%3D%26mid%3D2247488358%26idx%3D1%26sn%3D6eee5162428ff64d6c5a2b72552c58db%26scene%3D21%23wechat_redirect)，已经内置了Lombok插件，SpringBoot 2.1.x之后的版本也在Starter中内置了Lombok依赖。为什么他们都要支持Lombok呢？今天我来讲讲Lombok的使用，看看它有何神奇之处！**
>
> Recently the last version of Idea 2020 was released, with the Lombok plugin already built in, Springboot 2.1. Versions after X also include Lombok dependencies in Starter. Why do they all support Lombok? Today I’m going to talk about the use of Lombok and see what’s amazing about it!



任何技术的出现都是为了解决某一类问题，如果在此基础上再建立奇技淫巧，不如回归Java本身，应该保持合理使用而不滥用。

Any technology that comes along is designed to solve a certain type of problem, and if you build on that, it’s better to go back to Java itself and keep it in reasonable use and not abuse it.

***Lombok的使用非常简单：\***

Lombok is very simple to use:

### 1）引入相应的maven包

### 1) introduce the appropriate Maven package

>   <dependency>
>
> ​     <groupId>org.projectlombok</groupId>
>
> < groupid > org.projectlombok </groupid >
>
> ​     <artifactId>lombok</artifactId>
>
> ​     <version>1.16.18</version>
>
> ​     <scope>provided</scope>
>
>   </dependency>
>
> </dependency >

Lombok的scope=provided，说明它只在编译阶段生效，不需要打入包中。事实正是如此，Lombok在编译期将带Lombok注解的Java文件正确编译为完整的Class文件。

Lombok’s scope = provided means that it only works during the compilation phase and does not need to be inserted into the package. As it happens, Lombok compiles Lombok-annotated Java files into full-Class files at compile time.

## 2）添加IDE工具对Lombok的支持 

## 2) add IDE tools to support Lombok

  IDEA中引入Lombok支持如下：

Lombok support is included in IDEA as follows:

  点击File-- Settings设置界面，安装Lombok插件:

Click filesettings to install the Lombok plug-in:





![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f79ilbej30o00dpac4.jpg)

点击File-- Settings设置界面，开启 AnnocationProcessors：

Click on the file -- Settings screen to open any complaints processors:

![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f77eaj6j30ts0hnwh1.jpg)

开启该项是为了让Lombok注解在编译阶段起到作用。

This is to make Lombok annotations work during the compile phase.

> Eclipse的Lombok插件安装可以自行百度，也比较简单，值得一提的是，由于Eclipse内置的编译器不是Oracle javac，而是eclipse自己实现的Eclipse Compiler for Java (ECJ).要让ECJ支持Lombok，需要在eclipse.ini配置文件中添加如下两项内容：
>
> Eclipse’s Lombok plug-in installation is self-contained and relatively simple, since the built-in Compiler for Eclipse is not Oracle javac, but Eclipse’s own Eclipse Compiler for Java (ECJ) . To get ECJ to support Lombok, you need to install it in Eclipse. . Add the following two items to the. Ini Configuration File:
>
>   -Xbootclasspath/a:[lombok.jar所在路径
>
> \- xbootclasspath/A: [ Lombo. Jar Path

## 3）Lombok实现原理

## 3) how Lombok works

自从Java 6起，javac就支持“JSR 269 Pluggable Annotation Processing API”规范，只要程序实现了该API，就能在javac运行的时候得到调用。

Since Java 6, javac has supported the “JSR 269 Pluggable Annotation Processing API”specification. Once the API is implemented, it can be invoked while javac is running.

Lombok就是一个实现了"JSR 269 API"的程序。在使用javac的过程中，它产生作用的具体流程如下：

Lombok is a program that implements the JSR 269 API. Here’s how it works when using javac:

------

\1. javac对源代码进行分析，生成一棵抽象语法树(AST)

\1. Javac parses the source code to generate an abstract syntax tree (AST)

\2. javac编译过程中调用实现了JSR 269的Lombok程序

\2. The Lombok program that implements JSR 269 is invoked during the javac compilation process

\3. 此时Lombok就对第一步骤得到的AST进行处理，找到Lombok注解所在类对应的语法树    (AST)，然后修改该语法树(AST)，增加Lombok注解定义的相应树节点

\3. At this point, Lombok processes the AST from step one, finds the syntax tree (AST) for the class Lombok annotates, and then modifies that syntax tree (AST) to add the corresponding tree node defined by Lombok annotations

\4. javac使用修改后的抽象语法树(AST)生成字节码文件

\4. Javac uses the modified abstract syntax tree (AST) to generate bytecode files

------

## 4) Lombok注解的使用

## 4) use of Lombok annotations

#### POJO类常用注解:

#### Common annotations for POJO classes:

**@Getter/@Setter: 作用类上，生成所有成员变量的getter/setter方法；作用于成员变量上，生成该成员变量的getter/setter方法。可以设定访问权限及是否懒加载等。**

@ Getter/@setter: the Getter/Setter method that generates all member variables on the class, and the Getter/setter method that generates all member variables on the member variable. You can set access rights and lazy loading, etc. .

```java
package com.kaplan.pojo;

import lombok.*;
Import lombok. * ;
import lombok.extern.log4j.Log4j;

@Getter
@ getter
@Setter
@ setter
public class TestDemo {


private String name;


private int age ; private String email;


private String address; private String password;


@Getter @Setter private boolean funny;

@ getter@Setter private boolean funny;

}
```



**@ToString：作用于类，覆盖默认的toString()方法，可以通过of属性限定显示某些字段，通过exclude属性排除某些字段。**

@ Tostring : Acts on classes, overrides the default ToString () method, and can display certain fields qualified by the of attribute and exclude certain fields by the exclude attribute.

![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f792m4qj30dc04zweq.jpg)

**
@EqualsAndHashCode：作用于类，覆盖默认的equals和hashCode**

@ EQUALSANDHASHCODE : acts on the class, overriding the default equals and Hashcode

**@NonNull：主要作用于成员变量和参数中，标识不能为空，否则抛出空指针异常。**

@ Nonnull : mainly in member variables and parameters, the id can not be empty, otherwise a null pointer exception is thrown.

![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f784422j30dc04zweq.jpg)

@NoArgsConstructor, @RequiredArgsConstructor, @AllArgsConstructor：作用于类上，用于生成构造函数。有staticName、access等属性。

@ NOARGSCONSTRUCTOR ,@RequiredArgsConstructor ,@AllArgsConstructor : applied to classes, used to generate constructors. staticName, access, and so on.

**staticName属性一旦设定，将采用静态方法的方式生成实例，access属性可以限定访问权限。**

Once set, the staticName property generates the instance in a static way, and the access property qualifies access.

**@NoArgsConstructor：生成无参构造器；**

@ Noargsconstructor : Nullary constructor;

**@RequiredArgsConstructor：生成包含final和@NonNull注解的成员变量的构造器；**

Requiredargsconstructor : a constructor that generates member variables that contain final and@NonNull annotations;

**@AllArgsConstructor：生成全参构造器**

@ AllArgsConstructor : generating all parameter constructors

![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f7ccm3rj30g806eaar.jpg)

**@Data：作用于类上，是以下注解的集合：@ToString @EqualsAndHashCode @Getter @Setter @RequiredArgsConstructor
**

Data : applied to a class, it’s a collection of notes:@ToString@EqualsAndHashCode Getter@Setter@RequiredArgsConstructor

**@Builder：作用于类上，将类转变为建造者模式**

@ BUILDER : Acts on classes, turning them into builders

**@Log：作用于类上，生成日志变量。针对不同的日志实现产品，有不同的注解：**

@ Log : applies to a class, generating a Log variable. There are different annotations for different log implementation products:

#### 其他重要注解：

#### Other important notes:

**@Cleanup：自动关闭资源，针对实现了java.io.Closeable接口的对象有效，如：典型的IO流对象**

@ Cleanup : automatically shut down resources for implementations of Java. Io. Objects that are valid for the Closeable interface, such as typical IO stream objects

![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f7b4hgbj30f404tt93.jpg)

**编译后结果如下：**

The results are as follows:

![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f78nzzjj30fw09yt9f.jpg)

**@SneakyThrows：可以对受检异常进行捕捉并抛出，可以改写上述的main方法如下：**

@ SNEAKYTHROWS : the checked exception can be caught and thrown, and the main method can be overridden as follows:

![img](https://tva1.sinaimg.cn/large/008i3skNly1gs1f7bwf0lj30ew04z74p.jpg)

@Synchronized：作用于方法级别，可以替换synchronize关键字或lock锁，用处不大.

@ Synchronized : at the method level, you can replace the synchronize keyword or lock, which is not very useful.

[@作者原文](https://links.jianshu.com/go?to=https%3A%2F%2Fmp.weixin.qq.com%2Fs%2Fb8bKuoaJAgGdFx9nTaFpgg)

HTTP: www.newyorker.comonlineblogsnewsdesk2012012012012012012