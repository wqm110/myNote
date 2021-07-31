# springMVC 注解

![image-20201225034528408](https://tva1.sinaimg.cn/large/0081Kckwgy1glzkjwzlluj317u0h5q8o.jpg)



## 简单应用

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.2</version>
</dependency>
```

```java
@Configuration
@ComponentScan(basePackages = {"com.wqm.cn"} //默认包扫描
 //排除
   ,excludeFilters = {   @ComponentScan.Filter(type = FilterType.ANNOTATION,classes = {Controller.class})  ,
 //指定需要类型 
    includeFilters = {
        @ComponentScan.Filter(type = FilterType.ANNOTATION, useDefaultFilters = false,//先禁用默认扫描规则)  }                 
   ) 
public class MainConfig {
    @Bean(name = "person")
    public Person person() {
        return new Person(1, "zhangshan");
    }
} 
```

```java
public class MainTest {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext annContext = new AnnotationConfigApplicationContext(MainConfig.class);
        Person person = (Person) annContext.getBean("person");
        String name = person.getName();
        System.out.println("name = " + name); 
    }
```

## 配置

### @ComponentScans

```java
@Configuration  //告诉Spring这是一个配置类

@ComponentScans(
      value = {
            @ComponentScan(value="com.atguigu",includeFilters = {
/*                @Filter(type=FilterType.ANNOTATION,classes={Controller.class}),
                  @Filter(type=FilterType.ASSIGNABLE_TYPE,classes={BookService.class}),*/
                  @Filter(type=FilterType.CUSTOM,classes={MyTypeFilter.class})
            },useDefaultFilters = false)   
      }
      )
//@ComponentScan  value:指定要扫描的包
//excludeFilters = Filter[] ：指定扫描的时候按照什么规则排除那些组件
//includeFilters = Filter[] ：指定扫描的时候只需要包含哪些组件
//FilterType.ANNOTATION：按照注解
//FilterType.ASSIGNABLE_TYPE：按照给定的类型；
//FilterType.ASPECTJ：使用ASPECTJ表达式
//FilterType.REGEX：使用正则指定
//FilterType.CUSTOM：使用自定义规则
public class MainConfig {
```

@ComponentScans 扫描指定规则

@ComponentScan可重复

FileterType

@ComponentScan.Filter(type = FilterType.ANNOTATION,

### @Scope 单实例、多实例 配置

```java
@Configuration
public class MainConfig_scop {
    //
//    ConfigurableBeanFactory#SCOPE_PROTOTYPE
//                    每一次产生一个 新的
//   ConfigurableBeanFactory#SCOPE_SINGLETON  默认
//                    容器初始化的时候创建 
//   org.springframework.web.context.WebApplicationContext#SCOPE_REQUEST
//   org.springframework.web.context.WebApplicationContext#SCOPE_SESSION
    @Scope("prototype")
    @Bean
    public Person person() {
        return new Person(2, "lisi");
    }
```

### @Lazy 懒加载 （单实例）

```java
@Bean
@Lazy  //第一次获取的时候创建  只会被创建一次
public Person person1() {
    return new Person(2, "lisi");
}
```

### @Condition 条件加载 

```java
package com.wqm.cn.config;  
/**
 * @ProjectName: springMVC_ano
 * @Package: com.wqm.cn.config
 * @ClassName: OsConditation
 * @Author: WQM
 * @Description: 系统条件判断 Mac
 * @Date: 2020/12/25 4:59 上午
 * @Version: 1.0
 */ 
public class MacConditation implements Condition {
    /**
     * ConditionContext  判断条件能使用的上下文
     * AnnotatedTypeMetadata 注释信息
     */
    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
//        context.getBeanFactory(); //获取bean工厂
        Environment environment = context.getEnvironment();//获取环境信息
//        context.getClassLoader(); // 获取类加载器
        BeanDefinitionRegistry registry = context.getRegistry();// 获取bean 定义
        String property = environment.getProperty("os.name");
        boolean person = registry.containsBeanDefinition("person");  //也可以判断容器中是否有persion 
        if (property.contains("Mac OS")) {
            return true;
        }
        return false;
    }
}
```

```java
package com.wqm.cn.config; 

/**
 * @ProjectName: springMVC_ano
 * @Package: com.wqm.cn.config
 * @ClassName: OsConditation
 * @Author: WQM
 * @Description: 系统条件判断 Linux
 * @Date: 2020/12/25 4:59 上午
 * @Version: 1.0
 */
public class LinuxConditation implements Condition {
    /**
     * ConditionContext  判断条件能使用的上下文
     * AnnotatedTypeMetadata 注释信息
     */
    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        Environment environment = context.getEnvironment();//获取运行环境信息
        String property = environment.getProperty("os.name");
        if (property.contains("Linux")) {
            return true;
        }
        return false;
    }
}
```

使用

```java
/**
 * @Conditional()
 *
 * */
@Bean
@Lazy
@Conditional({LinuxConditation.class})
public Person person1() {
    return new Person(2, "bill");
} 
/**
 * @Conditional()  也可放在类上类统一设置 如果不满足条件整个类不起作用
 *
 * */
@Bean("mac")
@Lazy
@Conditional({MacConditation.class})
public Person person2() {
    return new Person(2, "bill");
}
```

### @Import

注册组件的方式

- @Service @Controller @Repository

- @Bean 

- @Import

  + 1 .import

  ```java
  package com.wqm.cn.config;
  
  /**
   * @ProjectName: springMVC_ano
   * @Package: com.wqm.cn.config
   * @ClassName: Color
   * @Author: WQM
   * @Description: 测试import导入
   * @Date: 2020/12/25 5:23 上午
   * @Version: 1.0
   */
  public class Color {
  }
  ```

  ```java
  @Configuration
  @Import({Color.class,RedClass.class})  //可以定义的多个
  public class MainConfig_scop {
  ```

  + 2.importSelector

  ```java
  @Configuration
  @Import({Color.class,RedClass.class,MyImportSelector.class})
  public class MainConfig_scop {
  ```

  ```java
  package com.wqm.cn.config;
  
  import org.springframework.context.annotation.ImportSelector;
  import org.springframework.core.type.AnnotationMetadata;
  
  /**
   * @ProjectName: springMVC_ano
   * @Package: com.wqm.cn.config
   * @ClassName: MyImportSelector
   * @Author: WQM
   * @Description: 自定义导入选择器
   * @Date: 2020/12/25 5:29 上午
   * @Version: 1.0
   */
  public class MyImportSelector implements ImportSelector {
      /**
       * AnnotationMetadata
       */
      @Override
      public String[] selectImports(AnnotationMetadata importingClassMetadata) {
  //        可以返回空数组不能返回null
  //        importingClassMetadata
          return new String[]{"com.wqm.cn.config.Color.java","com.wqm.cn.config.RedClass.java"};
      }
  }
  ```

+ 3. ImportBeanDefinitionRegistrar

  ```java
  package com.wqm.cn.config; 
  /**
   * @ProjectName: springMVC_ano
   * @Package: com.wqm.cn.config
   * @ClassName: MyImportBeanDefinitionRegistrar
   * @Author: WQM
   * @Description: 导入
   * @Date: 2020/12/25 5:38 上午
   * @Version: 1.0
   */
  public class MyImportBeanDefinitionRegistrar implements ImportBeanDefinitionRegistrar {
      /**
       * BeanDefinitionRegistry  注册类
       */
      @Override
      public void registerBeanDefinitions(AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry, BeanNameGenerator importBeanNameGenerator) { 
      } 
      @Override
      public void registerBeanDefinitions(AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry) {
          boolean red = registry.containsBeanDefinition("com.wqm.cn.config.RedClass.java");
          boolean color = registry.containsBeanDefinition("com.wqm.cn.config.Color");
          if (red && color) {
              //指定别名
              RootBeanDefinition beanDefinition = new RootBeanDefinition();
              registry.registerBeanDefinition("rainBow", beanDefinition);
          }
  
      }
  }
  ```

+ 4.FactoryBean

  ```java 
  package com.wqm.cn.config; 
  import org.springframework.beans.factory.FactoryBean; 
  /**
   * @ProjectName: springMVC_ano
   * @Package: com.wqm.cn.config
   * @ClassName: ColorFactory
   * @Author: WQM
   * @Description: 工厂bean
   * @Date: 2020/12/25 5:50 上午
   * @Version: 1.0
   */
  public class ColorFactory implements FactoryBean<ColorFactory> {
      @Override
      public ColorFactory getObject() throws Exception {
          return new ColorFactory();//放回实例
      } 
      @Override
      public Class<?> getObjectType() {
          return ColorFactory.class;
      } 
      @Override
      public boolean isSingleton() {
          return true;//只在容器中保留一个
      }
  }
  ```

### bean的生命周期

1 指定初始化销毁方法

@Bean(initmethod="")

```java
@ComponentScan("com.atguigu.bean")
@Configuration
public class MainConfigOfLifeCycle { 
	//@Scope("prototype")
	@Bean(initMethod="init",destroyMethod="detory")
	public Car car(){
		return new Car();
	}
```

2.让bean 实现InitiallizBean

 	 afterPropertiesset

​		preDestoryd

3 JSR250

  @PostConstruct  对象创建并赋值之后创建

  @PreDestroy   在对象移除之前

4 BeanPostProcessor Bean 的后置处理器 

```
postProcessBeforeInitialization ()
postProcessAfterInitialization()
```

1 postProcessBeforeInitialization()

2 postProcessAfterInitialization()

3 constructor()

4 postProcessBeforeInitialization()

5 afterPropertiesSet()

6 postProcessAfterInitialization ()

```java
 

/**
 * bean的生命周期：
 * 		bean创建---初始化----销毁的过程
 * 容器管理bean的生命周期；
 * 我们可以自定义初始化和销毁方法；容器在bean进行到当前生命周期的时候来调用我们自定义的初始化和销毁方法
 * 
 * 构造（对象创建）
 * 		单实例：在容器启动的时候创建对象
 * 		多实例：在每次获取的时候创建对象\
 * 
 * BeanPostProcessor.postProcessBeforeInitialization
 * 初始化：
 * 		对象创建完成，并赋值好，调用初始化方法。。。
 * BeanPostProcessor.postProcessAfterInitialization
 * 销毁：
 * 		单实例：容器关闭的时候
 * 		多实例：容器不会管理这个bean；容器不会调用销毁方法；
 * 
 * 
 * 遍历得到容器中所有的BeanPostProcessor；挨个执行beforeInitialization，
 * 一但返回null，跳出for循环，不会执行后面的BeanPostProcessor.postProcessorsBeforeInitialization
 * 
 * BeanPostProcessor原理
 * populateBean(beanName, mbd, instanceWrapper);给bean进行属性赋值
 * initializeBean
 * {
 * applyBeanPostProcessorsBeforeInitialization(wrappedBean, beanName);
 * invokeInitMethods(beanName, wrappedBean, mbd);执行自定义初始化
 * applyBeanPostProcessorsAfterInitialization(wrappedBean, beanName);
 *}
 * 
 * 
 * 
 * 1）、指定初始化和销毁方法；
 * 		通过@Bean指定init-method和destroy-method；
 * 2）、通过让Bean实现InitializingBean（定义初始化逻辑），
 * 				DisposableBean（定义销毁逻辑）;
 * 3）、可以使用JSR250；
 * 		@PostConstruct：在bean创建完成并且属性赋值完成；来执行初始化方法
 * 		@PreDestroy：在容器销毁bean之前通知我们进行清理工作
 * 4）、BeanPostProcessor【interface】：bean的后置处理器；
 * 		在bean初始化前后进行一些处理工作；
 * 		postProcessBeforeInitialization:在初始化之前工作
 * 		postProcessAfterInitialization:在初始化之后工作
 * 
 * Spring底层对 BeanPostProcessor 的使用；
 * 		bean赋值，注入其他组件，@Autowired，生命周期注解功能，@Async,xxx BeanPostProcessor;
 * 
 * @author lfy
 *
 */
@ComponentScan("com.atguigu.bean")
@Configuration
public class MainConfigOfLifeCycle {
	
	//@Scope("prototype")
	@Bean(initMethod="init",destroyMethod="detory")
	public Car car(){
		return new Car();
	}

}

```

属性赋值

```
//使用@Value赋值；
//1、基本数值
//2、可以写SpEL； #{}
//3、可以写${}；取出配置文件【properties】中的值（在运行环境变量里面的值）

@Value("张三")
private String name;
@Value("#{20-2}")
private Integer age;

@Value("${person.nickName}")
private String nickName;
```

读取配置文件

```java
  
/**
 * Profile：
 *        Spring为我们提供的可以根据当前环境，动态的激活和切换一系列组件的功能；
 * 
 * 开发环境、测试环境、生产环境；
 * 数据源：(/A)(/B)(/C)；
 * 
 * 
 * @Profile：指定组件在哪个环境的情况下才能被注册到容器中，不指定，任何环境下都能注册这个组件
 * 
 * 1）、加了环境标识的bean，只有这个环境被激活的时候才能注册到容器中。默认是default环境
 * 2）、写在配置类上，只有是指定的环境的时候，整个配置类里面的所有配置才能开始生效
 * 3）、没有标注环境标识的bean在，任何环境下都是加载的；
 */

@PropertySource("classpath:/dbconfig.properties")
@Configuration
public class MainConfigOfProfile implements EmbeddedValueResolverAware{
   
   @Value("${db.user}")
   private String user;
   
   private StringValueResolver valueResolver;
   
   private String  driverClass;
   
   
   @Bean
   public Yellow yellow(){
      return new Yellow();
   }
   
   @Profile("test")
   @Bean("testDataSource")
   public DataSource dataSourceTest(@Value("${db.password}")String pwd) throws Exception{
      ComboPooledDataSource dataSource = new ComboPooledDataSource();
      dataSource.setUser(user);
      dataSource.setPassword(pwd);
      dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/test");
      dataSource.setDriverClass(driverClass);
      return dataSource;
   } 
   
   @Profile("dev")
   @Bean("devDataSource")
   public DataSource dataSourceDev(@Value("${db.password}")String pwd) throws Exception{
      ComboPooledDataSource dataSource = new ComboPooledDataSource();
      dataSource.setUser(user);
      dataSource.setPassword(pwd);
      dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/ssm_crud");
      dataSource.setDriverClass(driverClass);
      return dataSource;
   }
   
   @Profile("prod")
   @Bean("prodDataSource")
   public DataSource dataSourceProd(@Value("${db.password}")String pwd) throws Exception{
      ComboPooledDataSource dataSource = new ComboPooledDataSource();
      dataSource.setUser(user);
      dataSource.setPassword(pwd);
      dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/scw_0515");
      
      dataSource.setDriverClass(driverClass);
      return dataSource;
   }

   @Override
   public void setEmbeddedValueResolver(StringValueResolver resolver) {
      // TODO Auto-generated method stub
      this.valueResolver = resolver;
      driverClass = valueResolver.resolveStringValue("${db.driverClass}");
   }

}
```

### 自动注入

 @AUtowaire @Resorce @Inject @Primary

优先按照类型找对应的组件

```
//@Qualifier("bookDao")         //指定bean的名字
//@Autowired(required=false)
//@Resource(name="bookDao2")
@Inject
private BookDao bookDao;
```

![image-20210103054413341](https://tva1.sinaimg.cn/large/0081Kckwgy1gma2k8bjcgj31060cd443.jpg)

![image-20210103055044959](https://tva1.sinaimg.cn/large/0081Kckwgy1gma2r0k1iaj30y207rwih.jpg)

![image-20210103060506682](https://tva1.sinaimg.cn/large/0081Kckwgy1gma35yna0zj30zt04rac9.jpg)

```
//默认加在ioc容器中的组件，容器启动会调用无参构造器创建对象，再进行初始化赋值等操作
@Component
public class Boss { 
   private Car car; 
   //构造器要用的组件，都是从容器中获取
   public Boss(Car car){
      this.car = car;
      System.out.println("Boss...有参构造器");
   }  
   public Car getCar() {
      return car;
   } 
   //@Autowired 
   //标注在方法，Spring容器创建当前对象，就会调用方法，完成赋值；
   //方法使用的参数，自定义类型的值从ioc容器中获取
   public void setCar(Car car) {
      this.car = car;
   }
```

![image-20210103061340913](https://tva1.sinaimg.cn/large/0081Kckwgy1gma3evthz1j30z103i40a.jpg)

![image-20210103060745056](https://tva1.sinaimg.cn/large/0081Kckwgy1gma38piaovj30jp0ax43m.jpg)

```
@Component
public class Red implements ApplicationContextAware,BeanNameAware,EmbeddedValueResolverAware {
   
   private ApplicationContext applicationContext;

   @Override
   public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {
      // TODO Auto-generated method stub
      System.out.println("传入的ioc："+applicationContext);
      this.applicationContext = applicationContext;
   }

   @Override
   public void setBeanName(String name) {
      // TODO Auto-generated method stub
      System.out.println("当前bean的名字："+name);
   }

   @Override
   public void setEmbeddedValueResolver(StringValueResolver resolver) {
      // TODO Auto-generated method stub
      String resolveStringValue = resolver.resolveStringValue("你好 ${os.name} 我是 #{20*18}");
      System.out.println("解析的字符串："+resolveStringValue);
   }
```

### AOP

```java
/**
 * 切面类
 * @author lfy
 * 
 * @Aspect： 告诉Spring当前类是一个切面类
 *
 */
@Aspect
public class LogAspects {
   
   //抽取公共的切入点表达式
   //1、本类引用
   //2、其他的切面引用
   @Pointcut("execution(public int com.atguigu.aop.MathCalculator.*(..))")
   public void pointCut(){};
   
   //@Before在目标方法之前切入；切入点表达式（指定在哪个方法切入）
   @Before("pointCut()")
   public void logStart(JoinPoint joinPoint){
      Object[] args = joinPoint.getArgs();
      System.out.println(""+joinPoint.getSignature().getName()+"运行。。。@Before:参数列表是：{"+Arrays.asList(args)+"}");
   }
   
   @After("com.atguigu.aop.LogAspects.pointCut()")
   public void logEnd(JoinPoint joinPoint){
      System.out.println(""+joinPoint.getSignature().getName()+"结束。。。@After");
   }
   
   //JoinPoint一定要出现在参数表的第一位
   @AfterReturning(value="pointCut()",returning="result")
   public void logReturn(JoinPoint joinPoint,Object result){
      System.out.println(""+joinPoint.getSignature().getName()+"正常返回。。。@AfterReturning:运行结果：{"+result+"}");
   }
   
   @AfterThrowing(value="pointCut()",throwing="exception")
   public void logException(JoinPoint joinPoint,Exception exception){
      System.out.println(""+joinPoint.getSignature().getName()+"异常。。。异常信息：{"+exception+"}");
   }

}
```

```java
/**
 * AOP：【动态代理】
 *        指在程序运行期间动态的将某段代码切入到指定方法指定位置进行运行的编程方式；
 * 
 * 1、导入aop模块；Spring AOP：(spring-aspects)
 * 2、定义一个业务逻辑类（MathCalculator）；在业务逻辑运行的时候将日志进行打印（方法之前、方法运行结束、方法出现异常，xxx）
 * 3、定义一个日志切面类（LogAspects）：切面类里面的方法需要动态感知MathCalculator.div运行到哪里然后执行；
 *        通知方法：
 *           前置通知(@Before)：logStart：在目标方法(div)运行之前运行
 *           后置通知(@After)：logEnd：在目标方法(div)运行结束之后运行（无论方法正常结束还是异常结束）
 *           返回通知(@AfterReturning)：logReturn：在目标方法(div)正常返回之后运行
 *           异常通知(@AfterThrowing)：logException：在目标方法(div)出现异常以后运行
 *           环绕通知(@Around)：动态代理，手动推进目标方法运行（joinPoint.procced()）
 * 4、给切面类的目标方法标注何时何地运行（通知注解）；
 * 5、将切面类和业务逻辑类（目标方法所在类）都加入到容器中;
 * 6、必须告诉Spring哪个类是切面类(给切面类上加一个注解：@Aspect)
 * [7]、给配置类中加 @EnableAspectJAutoProxy 【开启基于注解的aop模式】
 *        在Spring中很多的 @EnableXXX;
 * 
 * 三步：
 *     1）、将业务逻辑组件和切面类都加入到容器中；告诉Spring哪个是切面类（@Aspect）
 *     2）、在切面类上的每一个通知方法上标注通知注解，告诉Spring何时何地运行（切入点表达式）
 *  3）、开启基于注解的aop模式；@EnableAspectJAutoProxy
 *  
 * AOP原理：【看给容器中注册了什么组件，这个组件什么时候工作，这个组件的功能是什么？】
 *        @EnableAspectJAutoProxy；
 * 1、@EnableAspectJAutoProxy是什么？
 *        @Import(AspectJAutoProxyRegistrar.class)：给容器中导入AspectJAutoProxyRegistrar
 *           利用AspectJAutoProxyRegistrar自定义给容器中注册bean；BeanDefinetion
 *           internalAutoProxyCreator=AnnotationAwareAspectJAutoProxyCreator
 * 
 *        给容器中注册一个AnnotationAwareAspectJAutoProxyCreator；
 * 
 * 2、 AnnotationAwareAspectJAutoProxyCreator：
 *        AnnotationAwareAspectJAutoProxyCreator
 *           ->AspectJAwareAdvisorAutoProxyCreator
 *              ->AbstractAdvisorAutoProxyCreator
 *                 ->AbstractAutoProxyCreator
 *                       implements SmartInstantiationAwareBeanPostProcessor, BeanFactoryAware
 *                    关注后置处理器（在bean初始化完成前后做事情）、自动装配BeanFactory
 * 
 * AbstractAutoProxyCreator.setBeanFactory()
 * AbstractAutoProxyCreator.有后置处理器的逻辑；
 * 
 * AbstractAdvisorAutoProxyCreator.setBeanFactory()-》initBeanFactory()
 * 
 * AnnotationAwareAspectJAutoProxyCreator.initBeanFactory()
 *
 *
 * 流程：
 *        1）、传入配置类，创建ioc容器
 *        2）、注册配置类，调用refresh（）刷新容器；
 *        3）、registerBeanPostProcessors(beanFactory);注册bean的后置处理器来方便拦截bean的创建；
 *           1）、先获取ioc容器已经定义了的需要创建对象的所有BeanPostProcessor
 *           2）、给容器中加别的BeanPostProcessor
 *           3）、优先注册实现了PriorityOrdered接口的BeanPostProcessor；
 *           4）、再给容器中注册实现了Ordered接口的BeanPostProcessor；
 *           5）、注册没实现优先级接口的BeanPostProcessor；
 *           6）、注册BeanPostProcessor，实际上就是创建BeanPostProcessor对象，保存在容器中；
 *              创建internalAutoProxyCreator的BeanPostProcessor【AnnotationAwareAspectJAutoProxyCreator】
 *              1）、创建Bean的实例
 *              2）、populateBean；给bean的各种属性赋值
 *              3）、initializeBean：初始化bean；
 *                    1）、invokeAwareMethods()：处理Aware接口的方法回调
 *                    2）、applyBeanPostProcessorsBeforeInitialization()：应用后置处理器的postProcessBeforeInitialization（）
 *                    3）、invokeInitMethods()；执行自定义的初始化方法
 *                    4）、applyBeanPostProcessorsAfterInitialization()；执行后置处理器的postProcessAfterInitialization（）；
 *              4）、BeanPostProcessor(AnnotationAwareAspectJAutoProxyCreator)创建成功；--》aspectJAdvisorsBuilder
 *           7）、把BeanPostProcessor注册到BeanFactory中；
 *              beanFactory.addBeanPostProcessor(postProcessor);
 * =======以上是创建和注册AnnotationAwareAspectJAutoProxyCreator的过程========
 * 
 *           AnnotationAwareAspectJAutoProxyCreator => InstantiationAwareBeanPostProcessor
 *        4）、finishBeanFactoryInitialization(beanFactory);完成BeanFactory初始化工作；创建剩下的单实例bean
 *           1）、遍历获取容器中所有的Bean，依次创建对象getBean(beanName);
 *              getBean->doGetBean()->getSingleton()->
 *           2）、创建bean
 *              【AnnotationAwareAspectJAutoProxyCreator在所有bean创建之前会有一个拦截，InstantiationAwareBeanPostProcessor，会调用postProcessBeforeInstantiation()】
 *              1）、先从缓存中获取当前bean，如果能获取到，说明bean是之前被创建过的，直接使用，否则再创建；
 *                 只要创建好的Bean都会被缓存起来
 *              2）、createBean（）;创建bean；
 *                 AnnotationAwareAspectJAutoProxyCreator 会在任何bean创建之前先尝试返回bean的实例
 *                 【BeanPostProcessor是在Bean对象创建完成初始化前后调用的】
 *                 【InstantiationAwareBeanPostProcessor是在创建Bean实例之前先尝试用后置处理器返回对象的】
 *                 1）、resolveBeforeInstantiation(beanName, mbdToUse);解析BeforeInstantiation
 *                    希望后置处理器在此能返回一个代理对象；如果能返回代理对象就使用，如果不能就继续
 *                    1）、后置处理器先尝试返回对象；
 *                       bean = applyBeanPostProcessorsBeforeInstantiation（）：
 *                          拿到所有后置处理器，如果是InstantiationAwareBeanPostProcessor;
 *                          就执行postProcessBeforeInstantiation
 *                       if (bean != null) {
                        bean = applyBeanPostProcessorsAfterInitialization(bean, beanName);
                     }
 * 
 *                 2）、doCreateBean(beanName, mbdToUse, args);真正的去创建一个bean实例；和3.6流程一样；
 *                 3）、
 *           
 *        
 * AnnotationAwareAspectJAutoProxyCreator【InstantiationAwareBeanPostProcessor】 的作用：
 * 1）、每一个bean创建之前，调用postProcessBeforeInstantiation()；
 *        关心MathCalculator和LogAspect的创建
 *        1）、判断当前bean是否在advisedBeans中（保存了所有需要增强bean）
 *        2）、判断当前bean是否是基础类型的Advice、Pointcut、Advisor、AopInfrastructureBean，
 *           或者是否是切面（@Aspect）
 *        3）、是否需要跳过
 *           1）、获取候选的增强器（切面里面的通知方法）【List<Advisor> candidateAdvisors】
 *              每一个封装的通知方法的增强器是 InstantiationModelAwarePointcutAdvisor；
 *              判断每一个增强器是否是 AspectJPointcutAdvisor 类型的；返回true
 *           2）、永远返回false
 * 
 * 2）、创建对象
 * postProcessAfterInitialization；
 *        return wrapIfNecessary(bean, beanName, cacheKey);//包装如果需要的情况下
 *        1）、获取当前bean的所有增强器（通知方法）  Object[]  specificInterceptors
 *           1、找到候选的所有的增强器（找哪些通知方法是需要切入当前bean方法的）
 *           2、获取到能在bean使用的增强器。
 *           3、给增强器排序
 *        2）、保存当前bean在advisedBeans中；
 *        3）、如果当前bean需要增强，创建当前bean的代理对象；
 *           1）、获取所有增强器（通知方法）
 *           2）、保存到proxyFactory
 *           3）、创建代理对象：Spring自动决定
 *              JdkDynamicAopProxy(config);jdk动态代理；
 *              ObjenesisCglibAopProxy(config);cglib的动态代理；
 *        4）、给容器中返回当前组件使用cglib增强了的代理对象；
 *        5）、以后容器中获取到的就是这个组件的代理对象，执行目标方法的时候，代理对象就会执行通知方法的流程；
 *        
 *     
 *     3）、目标方法执行  ；
 *        容器中保存了组件的代理对象（cglib增强后的对象），这个对象里面保存了详细信息（比如增强器，目标对象，xxx）；
 *        1）、CglibAopProxy.intercept();拦截目标方法的执行
 *        2）、根据ProxyFactory对象获取将要执行的目标方法拦截器链；
 *           List<Object> chain = this.advised.getInterceptorsAndDynamicInterceptionAdvice(method, targetClass);
 *           1）、List<Object> interceptorList保存所有拦截器 5
 *              一个默认的ExposeInvocationInterceptor 和 4个增强器；
 *           2）、遍历所有的增强器，将其转为Interceptor；
 *              registry.getInterceptors(advisor);
 *           3）、将增强器转为List<MethodInterceptor>；
 *              如果是MethodInterceptor，直接加入到集合中
 *              如果不是，使用AdvisorAdapter将增强器转为MethodInterceptor；
 *              转换完成返回MethodInterceptor数组；
 * 
 *        3）、如果没有拦截器链，直接执行目标方法;
 *           拦截器链（每一个通知方法又被包装为方法拦截器，利用MethodInterceptor机制）
 *        4）、如果有拦截器链，把需要执行的目标对象，目标方法，
 *           拦截器链等信息传入创建一个 CglibMethodInvocation 对象，
 *           并调用 Object retVal =  mi.proceed();
 *        5）、拦截器链的触发过程;
 *           1)、如果没有拦截器执行执行目标方法，或者拦截器的索引和拦截器数组-1大小一样（指定到了最后一个拦截器）执行目标方法；
 *           2)、链式获取每一个拦截器，拦截器执行invoke方法，每一个拦截器等待下一个拦截器执行完成返回以后再来执行；
 *              拦截器链的机制，保证通知方法与目标方法的执行顺序；
 *        
 *     总结：
 *        1）、  @EnableAspectJAutoProxy 开启AOP功能
 *        2）、 @EnableAspectJAutoProxy 会给容器中注册一个组件 AnnotationAwareAspectJAutoProxyCreator
 *        3）、AnnotationAwareAspectJAutoProxyCreator是一个后置处理器；
 *        4）、容器的创建流程：
 *           1）、registerBeanPostProcessors（）注册后置处理器；创建AnnotationAwareAspectJAutoProxyCreator对象
 *           2）、finishBeanFactoryInitialization（）初始化剩下的单实例bean
 *              1）、创建业务逻辑组件和切面组件
 *              2）、AnnotationAwareAspectJAutoProxyCreator拦截组件的创建过程
 *              3）、组件创建完之后，判断组件是否需要增强
 *                 是：切面的通知方法，包装成增强器（Advisor）;给业务逻辑组件创建一个代理对象（cglib）；
 *        5）、执行目标方法：
 *           1）、代理对象执行目标方法
 *           2）、CglibAopProxy.intercept()；
 *              1）、得到目标方法的拦截器链（增强器包装成拦截器MethodInterceptor）
 *              2）、利用拦截器的链式机制，依次进入每一个拦截器进行执行；
 *              3）、效果：
 *                 正常执行：前置通知-》目标方法-》后置通知-》返回通知
 *                 出现异常：前置通知-》目标方法-》后置通知-》异常通知
 *        
 * 
 * 
 */
@EnableAspectJAutoProxy
@Configuration
public class MainConfigOfAOP {
    
   //业务逻辑类加入容器中
   @Bean
   public MathCalculator calculator(){
      return new MathCalculator();
   }

   //切面类加入到容器中
   @Bean
   public LogAspects logAspects(){
      return new LogAspects();
   }
}
```

整合springmvc

```
1、web容器在启动的时候，会扫描每个jar包下的META-INF/services/javax.servlet.ServletContainerInitializer
2、加载这个文件指定的类SpringServletContainerInitializer
3、spring的应用一启动会加载感兴趣的WebApplicationInitializer接口的下的所有组件；
4、并且为WebApplicationInitializer组件创建对象（组件不是接口，不是抽象类）
   1）、AbstractContextLoaderInitializer：创建根容器；createRootApplicationContext()；
   2）、AbstractDispatcherServletInitializer：
         创建一个web的ioc容器；createServletApplicationContext();
         创建了DispatcherServlet；createDispatcherServlet()；
         将创建的DispatcherServlet添加到ServletContext中；
            getServletMappings();
   3）、AbstractAnnotationConfigDispatcherServletInitializer：注解方式配置的DispatcherServlet初始化器
         创建根容器：createRootApplicationContext()
               getRootConfigClasses();传入一个配置类
         创建web的ioc容器： createServletApplicationContext();
               获取配置类；getServletConfigClasses();
   
总结：
   以注解方式来启动SpringMVC；继承AbstractAnnotationConfigDispatcherServletInitializer；
实现抽象方法指定DispatcherServlet的配置信息；

===========================
定制SpringMVC；
1）、@EnableWebMvc:开启SpringMVC定制配置功能；
   <mvc:annotation-driven/>；

2）、配置组件（视图解析器、视图映射、静态资源映射、拦截器。。。）
   extends WebMvcConfigurerAdapter



         
   
```