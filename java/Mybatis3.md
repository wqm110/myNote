# Mybatis3

## 高级查询

```java
    public void test01() {
        SqlSession openSession = build.openSession();
        DeptMapper mapper = openSession.getMapper(DeptMapper.class);
        DeptExample example = new DeptExample();
//所有的条件都在example中封装
        Criteria criteria = example.createCriteria();
//select id, deptName, locAdd from tbl_dept WHERE 
//( deptName like ? and id > ? ) 
        criteria.andDeptnameLike("%部%");
        criteria.andIdGreaterThan(2);
        List<Dept> list = mapper.selectByExample(example);
        for (Dept dept : list) {
            System.out.println(dept);
        }
    }
```

分页

```
新版不需要
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>最新版本</version>
</dependency>
新版不需要

     <!--        分页插件  只加这一个依赖--> 
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper-spring-boot-starter</artifactId>
            <version>1.2.13</version>
        </dependency>
        
          #pagehelper
#  pagehelper:
#      helperDialect: mysql
#      reasonable: true
#      supportMethodsArguments: true
#      params: count=countSql

在需要分页的方法上添加下面 一句 即可完成分页
  PageHelper.startPage(pageNo,pageSize);
  
        List<Meitu> meituList =   meituMapper.findByPage(meitu);

例三，使用PageInfo的用法：
//获取第1页，10条内容，默认查询总数count
PageHelper.startPage(1, 10);
List<User> list = userMapper.selectAll();
//用PageInfo对结果进行包装
PageInfo page = new PageInfo(list);
//测试PageInfo全部属性
//PageInfo包含了非常全面的分页属性
assertEquals(1, page.getPageNum());
assertEquals(10, page.getPageSize());
assertEquals(1, page.getStartRow());
assertEquals(10, page.getEndRow());
assertEquals(183, page.getTotal());
assertEquals(19, page.getPages());
assertEquals(1, page.getFirstPage());
assertEquals(8, page.getLastPage());
assertEquals(true, page.isFirstPage());
assertEquals(false, page.isLastPage());
assertEquals(false, page.isHasPreviousPage());
assertEquals(true, page.isHasNextPage());
```

经验

```
#  configuration:      Property 'configuration' and 'configLocation' can not specified with together
#    cache-enabled: true
```



## 历史

![image-20201225061929627](https://tva1.sinaimg.cn/large/0081Kckwgy1glzp06a1m8j30wu0hin0t.jpg)

![image-20201225062238407](https://tva1.sinaimg.cn/large/0081Kckwgy1glzp3fabj2j30vz0eztai.jpg)

![image-20201225062301679](https://tva1.sinaimg.cn/large/0081Kckwgy1glzp3vfmivj30uh0hzn9l.jpg)

![image-20201225062334902](https://tva1.sinaimg.cn/large/0081Kckwgy1glzp4ev64ij30l80egtex.jpg)

## HELLO WORLD

### 四大护法

#### 主配置文件

```xml
<!--mybatis.xml-->
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
<!--                <property name="driver" value="${driver}"/>-->
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
<!--                <property name="url" value="${url}"/>-->
                <property name="url" value="jdbc:mysql://localhost:3306/java"/>
<!--                <property name="username" value="${username}"/>-->
                <property name="username" value="java"/>
<!--                <property name="password" value="${password}"/>-->
                <property name="password" value="java"/>
            </dataSource>
        </environment>
    </environments>
    <mappers>
        <mapper resource="User.xml"/>  //映射文件路径
    </mappers>
</configuration>
```

#### 映射文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--
    名称空间： 
-->
<mapper namespace="com.wqm.cn.mapper.User">									              //对象全类名
    <select id="com.wqm.cn.selectUser" resultType="com.wqm.cn.vo.User">   //id： sql的唯一标识
        select * from user2 where id = #{id}                              //sql语句
    </select>
</mapper>
```

#### jar

#### log4j 

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">
 
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
 
 <appender name="STDOUT" class="org.apache.log4j.ConsoleAppender">
   <param name="Encoding" value="UTF-8" />
   <layout class="org.apache.log4j.PatternLayout">
    <param name="ConversionPattern" value="%-5p %d{MM-dd HH:mm:ss,SSS} %m  (%F:%L) \n" />
   </layout>
 </appender>
 <logger name="java.sql">
   <level value="debug" />
 </logger>
 <logger name="org.apache.ibatis">
   <level value="info" />
 </logger>
 <root>
   <level value="debug" />
   <appender-ref ref="STDOUT" />
 </root>
</log4j:configuration>
```



## 全局配置文件

提示 



![image-20201225073111678](https://tva1.sinaimg.cn/large/0081Kckwgy1glzr2rpa99j30fi0iqtav.jpg)

### mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <!--        类路径的资源
                    resource:类路径
                    url:网络 远程
    -->
    <properties resource="mybatis.properties" url="">

    </properties>
    <settings>
        <!--        开启转驼峰-->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
      !--        lazyLoadingEnabled	延迟加载的全局开关。当开启时，所有关联对象都会延迟加载。 特定关联关系中可通过设置 fetchType 属性来覆盖该项的开关状态。	true | false	false-->
<!--        aggressiveLazyLoading	开启时，任一方法的调用都会加载该对象的所有延迟加载属性。 否则，每个延迟加载属性会按需加载（参考 lazyLoadTriggerMethods)。	true | false	false （在 3.4.1 及之前的版本中默认为 true）-->
   
    </settings>
    <typeAliases>
        <!--        为某个类起别名
                    type：指定要起别名的全类名，默认就是全类名小写user
                    alias:新别名 对应 映射文件的resultType
        -->
        <typeAlias type="com.wqm.cn.vo.User" alias="User"/>
        <!--        批量指定别名
                          name:当前包和后代包都会默认 类型 不区分大小写
                          批量冲突时：在类上使用 @Alias("user") public class User {}
                          系统也有默认别名 https://mybatis.org/mybatis-3/zh/configuration.html#typeAliases
        -->
        <package name="com.wqm.cn.vo"/>
    </typeAliases>
    <!--    可配置多种环境 default="xx" 指定 当前使用的数据源
            https://mybatis.org/mybatis-3/zh/configuration.html#environments
                enviroment:可配置一个具体环境信息 id代表当前环境的id
                    transactionManager 事务管理器
                        type:事务管理器
                            jdbc   ：
                            managed：
                    dataSource
                            UNPOOLED
                            |POOLED  链接池
                            |JNDI]

    -->
    <environments default="development">
        <environment id="test">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED"></dataSource>
        </environment>
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <!-- <property name="driver" value="com.mysql.cj.jdbc.Driver"/>-->
                <property name="url" value="${url}"/>
                <!--<property name="url" value="jdbc:mysql://localhost:3306/java"/>-->
                <property name="username" value="${username}"/>
                <!-- <property name="username" value="java"/>-->
                <property name="password" value="${password}"/>
                <!-- <property name="password" value="java"/>-->
            </dataSource>
        </environment>

        <environment id="dev_oracle">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${orcl.driver}"/>
                <property name="url" value="${orcl.url}"/>
                <property name="username" value="${orcl.username}"/>
                <property name="password" value="${orcl.password}"/>
            </dataSource>
        </environment>

    </environments>
    <!--    支持多厂商数据库
            https://mybatis.org/mybatis-3/zh/configuration.html#databaseIdProvider
            type DB_VENDOR 驱动自带的
            value 对应 SQL中的databaseid
                        <select id="selectUser" resultType="User" databaseId="mysql"> //User.xml
            在properties文件中
    -->
    <databaseIdProvider type="DB_VENDOR">
        <property name="MySQL" value="mysql"/>
        <property name="Oracle" value="oracle"/>
        <property name="SQL Service" value="oracle"/>
    </databaseIdProvider>
    <!--
    mappers 将映射注册到全局
    -->
    <mappers>
        <!--        mapper  https://mybatis.org/mybatis-3/zh/configuration.html#mappers
                        注册文件
                          resource:类路径下的 sql映射文件
                          url     ：磁盘路径下 或网路路径
                        注册接口
                        class:引用接口全名
                           1 必须有映射文件名和接口同名   和接口统一路径下
                           2 利用注解 执行sql
        -->
        <mapper resource="User.xml"/>
        <!--        将mapper映射文件放到resources 和 Mapper 的通报下-->
        <mapper class="com.wqm.cn.mapper.UserMpper"/>
    </mappers>
</configuration>
```

## SQL映射文件 User.xml

### 基本使用

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--
    名称空间：

-->
<mapper namespace="com.wqm.cn.mapper.UserMapper">
    <select id="selectUser" resultType="User" databaseId="mysql">
        select *
        from user2
        where id = #{id}
    </select>

    <!-- public void addEmp(Employee employee); -->
    <!-- parameterType：参数类型，可以省略，
    获取自增主键的值：
        mysql支持自增主键，自增主键值的获取，mybatis也是利用statement.getGenreatedKeys()；
        useGeneratedKeys="true"；使用自增主键获取主键值策略
        keyProperty；指定对应的主键属性，也就是mybatis获取到主键值以后，将这个值封装给javaBean的哪个属性
    -->
    <insert id="insertUser" parameterType="user" useGeneratedKeys="true" keyProperty="id" >
        insert into user2 (email, lastname, gender)
        values (email = #{email}, lastname = #{lastName}, gender = #{gender})
    </insert>
  <!-- 
	获取非自增主键的值：
		Oracle不支持自增；Oracle使用序列来模拟自增；
		每次插入的数据的主键是从序列中拿到的值；如何获取到这个值；
	 -->
	<insert id="addEmp" databaseId="oracle">
		<!-- 
		keyProperty:查出的主键值封装给javaBean的哪个属性
		order="BEFORE":当前sql在插入sql之前运行
			   AFTER：当前sql在插入sql之后运行
		resultType:查出的数据的返回值类型
		
		BEFORE运行顺序：
			先运行selectKey查询id的sql；查出id值封装给javaBean的id属性
			在运行插入的sql；就可以取出id属性对应的值
		AFTER运行顺序：
			先运行插入的sql（从序列中取出新值作为id）；
			再运行selectKey查询id的sql；
		 -->
		<selectKey keyProperty="id" order="BEFORE" resultType="Integer">  //oracle
			<!-- 编写查询主键的sql语句 -->
			<!-- BEFORE-->
			select EMPLOYEES_SEQ.nextval from dual 
			<!-- AFTER：
			 select EMPLOYEES_SEQ.currval from dual -->
		</selectKey>
		
		<!-- 插入时的主键是从序列中拿到的 -->
		<!-- BEFORE:-->
		insert into employees(EMPLOYEE_ID,LAST_NAME,EMAIL) 
		values(#{id},#{lastName},#{email<!-- ,jdbcType=NULL -->}) 
		<!-- AFTER：
		insert into employees(EMPLOYEE_ID,LAST_NAME,EMAIL) 
		values(employees_seq.nextval,#{lastName},#{email}) -->
	</insert>
    <update id="updateUser" parameterType="user">
        update user2
        set email=#{email},
            lastname=#{lastName},
            gender=#{gender}
        where id = #{id}
    </update>
    <delete id="deleteUser" parameterType="user">
        delete
        from user2
        where id = #{id}
    </delete>
</mapper>
```

```java
import com.wqm.cn.mapper.UserMapper;
import com.wqm.cn.mapper.UserMpper;
import com.wqm.cn.vo.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.jupiter.api.Test;

import java.io.IOException;
import java.io.InputStream;

/**
 * @ProjectName: Mybatis
 * @Package: PACKAGE_NAME
 * @ClassName: Test
 * @Author: WQM
 * @Description:
 * @Date: 2020/12/25 6:53 上午
 * @Version: 1.0
 */
public class TestMybatis {
    //        资源文件
    String resource = "mybatis.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    //        获取SQLSessionFactory
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //        获取session
    SqlSession sqlSession = sqlSessionFactory.openSession();

    public TestMybatis() throws IOException {
    }

    @Test
    public void test() throws IOException {
        //        获取session
        SqlSession sqlSession = sqlSessionFactory.openSession();
        User selectBlog = sqlSession.selectOne("selectUser", 1);
        System.out.println("selectBlog = " + selectBlog);
        sqlSession.close();
    }

    @Test
    public void testMapper() throws IOException {
        //        获取session
        SqlSession sqlSession = sqlSessionFactory.openSession();
//        获取接口
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        System.out.println("mapper = " + mapper.getClass());//mapper = class com.sun.proxy.$Proxy11
        User user = mapper.selectUser(1);
        System.out.println("user = " + user);
        sqlSession.close();
    }

    @Test
    public void testAnnotation() throws IOException {
        //        获取session
        SqlSession sqlSession = sqlSessionFactory.openSession();
//        获取接口
        UserMpper mapper = sqlSession.getMapper(UserMpper.class);
        User user = mapper.selectById(1);
        System.out.println("user = " + user);
    }

    @Test
    public void testCRUD() {
        //        获取session
        SqlSession sqlSession = sqlSessionFactory.openSession(true);  //开启默认提交
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = new User("zhangshan", "man", "10003@162.com");
        try {
            mapper.insertUser(user);
            System.out.println("user = " + user.getId());       //开启了useGeneratedKeys后可以获取主键
//            user.setId(4);
//            mapper.updateUser(user);
//             mapper.deleteUser(user);
//            sqlSession.commit();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            sqlSession.close();
        }


    }
}
```

### Mybatis 参数处理

#### 单个参数：mybatis不会做特殊处理，

​	#{参数名/任意名}：取出参数值。

#### 多个参数：mybatis会做特殊处理。

​	多个参数会被封装成 一个map，
​		key：param1...paramN,或者参数的索引也可以
​		value：传入的参数值
​	#{}就是从map中获取指定的key的值；
​	

	异常：
	org.apache.ibatis.binding.BindingException: 
	Parameter 'id' not found. 
	Available parameters are [1, 0, param1, param2]
	操作：
		方法：public Employee getEmpByIdAndLastName(Integer id,String lastName);
		取值：#{id},#{lastName}

【命名参数】：明确指定封装参数时map的key；@Param("id")
	多个参数会被封装成 一个map，
		key：使用@Param注解指定的值
		value：参数值
	#{指定的key}取出对应的参数值

#### POJO：

如果多个参数正好是我们业务逻辑的数据模型，我们就可以直接传入pojo；
	#{属性名}：取出传入的pojo的属性值	

##### Map：

如果多个参数不是业务模型中的数据，没有对应的pojo，不经常使用，为了方便，我们也可以传入map
	#{key}：取出map中对应的值

##### TO：

如果多个参数不是业务模型中的数据，但是经常要使用，推荐来编写一个TO（Transfer Object）数据传输对象
Page{
	int index;
	int size;
}

========================思考================================	
public Employee getEmp(@Param("id")Integer id,String lastName);
	取值：id==>#{id/param1}   lastName==>#{param2}

public Employee getEmp(Integer id,@Param("e")Employee emp);
	取值：id==>#{param1}    lastName===>#{param2.lastName/e.lastName}

#### Collection List set

##特别注意：如果是Collection（List、Set）类型或者是数组，

​		 也会特殊处理。也是把传入的list或者数组封装在map中。
​			key：Collection（collection）,如果是List还可以使用这个key(list)
​				数组(array)
public Employee getEmpById(List<Integer> ids);
​	取值：取出第一个id的值：   #{list[0]}
​	
========================结合源码，mybatis怎么处理参数==========================

总结：参数多时会封装map，为了不混乱，我们可以使用@Param来指定封装时使用的key；
#{key}就可以取出map中的值；

(@Param("id")Integer id,@Param("lastName")String lastName);
ParamNameResolver解析参数封装map的；
//1、names：{0=id, 1=lastName}；构造器的时候就确定好了

	确定流程：
	1.获取每个标了param注解的参数的@Param的值：id，lastName；  赋值给name;
	2.每次解析一个参数给map中保存信息：（key：参数索引，value：name的值）
		name的值：
			标注了param注解：注解的值
			没有标注：
				1.全局配置：useActualParamName（jdk1.8）：name=参数名
				2.name=map.size()；相当于当前元素的索引
	{0=id, 1=lastName,2=2}


args【1，"Tom",'hello'】: 

```java
public Object getNamedParams(Object[] args) {
    final int paramCount = names.size();
    //1、参数为null直接返回
    if (args == null || paramCount == 0) {
      return null;
//2、如果只有一个元素，并且没有Param注解；args[0]：单个参数直接返回
} else if (!hasParamAnnotation && paramCount == 1) {
  return args[names.firstKey()];
  
//3、多个元素或者有Param标注
} else {
  final Map<String, Object> param = new ParamMap<Object>();
  int i = 0;
  
  //4、遍历names集合；{0=id, 1=lastName,2=2}
  for (Map.Entry<Integer, String> entry : names.entrySet()) {
  
  	//names集合的value作为key;  names集合的key又作为取值的参考args[0]:args【1，"Tom"】:
  	//eg:{id=args[0]:1,lastName=args[1]:Tom,2=args[2]}
    param.put(entry.getValue(), args[entry.getKey()]);    
    // add generic param names (param1, param2, ...)param
    //额外的将每一个参数也保存到map中，使用新的key：param1...paramN
    //效果：有Param注解可以#{指定的key}，或者#{param1}
    final String genericParamName = GENERIC_NAME_PREFIX + String.valueOf(i + 1);
    // ensure not to overwrite parameter named with @Param
    if (!names.containsValue(genericParamName)) {
      param.put(genericParamName, args[entry.getKey()]);
    }
    i++;
  }
  return param;
 }
 }
}
```

##### $ #     

  ===========================参数值的获取======================================
#{}：可以获取map中的值或者pojo对象属性的值；
${}：可以获取map中的值或者pojo对象属性的值；

select * from tbl_employee where id=${id} and last_name=#{lastName}
Preparing: select * from tbl_employee where id=2 and last_name=?
	区别：
		#{}:是以预编译的形式，将参数设置到sql语句中；PreparedStatement；防止sql注入
		${}:取出的值直接拼装在sql语句中；会有安全问题；
		大多情况下，我们去参数的值都应该去使用#{}；
		

		原生jdbc不支持占位符的地方我们就可以使用${}进行取值
		比如分表、排序。。。；按照年份分表拆分
			select * from ${year}_salary where xxx;
			select * from tbl_employee order by ${f_name} ${order}

#{}:更丰富的用法：
	规定参数的一些规则：
	javaType、 jdbcType、 mode（存储过程）、 numericScale、
	resultMap、 typeHandler、 jdbcTypeName、 expression（未来准备支持的功能）；

	jdbcType通常需要在某种特定的条件下被设置：
		在我们数据为null的时候，有些数据库可能不能识别mybatis对null的默认处理。比如Oracle（报错）；
		
		JdbcType OTHER：无效的类型；因为mybatis对所有的null都映射的是原生Jdbc的OTHER类型，oracle不能正确处理;
		
		由于全局配置中：jdbcTypeForNull=OTHER；oracle不支持；两种办法
		1、#{email,jdbcType=OTHER};
		2、jdbcTypeForNull=NULL
			<setting name="jdbcTypeForNull" value="NULL"/>
### 返回值类型 resultType

集合型  resultType

#### list

```java
List<User> getUsersByLastNameLike(String lastName);
```

```xml
<!--    List<User> getUsersByLastNameLike(String lastName);-->
<select id="getUsersByLastNameLike" resultType="com.wqm.cn.vo.User" parameterType="java.lang.String">
    select *
    from user2
    where lastname like #{lastName}
</select>
```

#### map

1

```java
Map<String, Object> getUsersByLastId(Integer id);
```

```xml
<select id="getUsersByLastId" resultType="map" parameterType="java.lang.Integer">
    select *
    from user2
    where id = #{id}
</select>
```

2

```java
@MapKey("id")
Map<String, User> getUsersByLike(String name); 
```

```xml
<!--    Map<String, User> getUsersByLike(String name);-->
<select id="getUsersByLike" resultType="java.util.Map" parameterType="java.lang.String">
    select *
    from user2
    where lastname like #{lastName}
</select>
```

```
Map<String, User> usersByLike = mapper.getUsersByLike("%a%");
System.out.println("usersByLike = " + usersByLike);
```

### 返回值类型 resultMap

```
public interface UserMapperPlus {
    User findByResultMap(Integer id);
}
```

```xml
<resultMap id="myMap" type="user">                    
  <!--指定主键列的封装规则
		id定义主键会底层有优化；
		column：指定哪一列
		property：指定对应的javaBean属性
		  -->
    <id property="id" column="id"/>										 
  <!-- 定义普通列封装规则 -->
    <result column="lastname" property="lastName"/>   
  <!-- 其他不指定的列会自动封装：我们只要写resultMap就把全部的映射规则都写上。 //其他列和属性的对应 不返回可以不写 ，最好都写上
-->
    <result column="email" property="email"/>
    <result column="gender" property="gender"/>
</resultMap>

<select id="findByResultMap" resultMap="myMap" parameterType="java.lang.Integer">
    select *
    from user2
    where id = #{id}
</select>
```

```java
@Test
public void testResultMap() {
    SqlSession sqlSession = sqlSessionFactory.openSession(true);
    UserMapperPlus mapper = sqlSession.getMapper(UserMapperPlus.class);
    User byResultMap = mapper.findByResultMap(1);
    System.out.println("byResultMap = " + byResultMap);
    sqlSession.close();
}
```

#### 关联属性

```java
User findByIdWithDept(Integer id);
```

```xml
<resultMap id="userInfoDept" type="User">
    <id column="uid" property="id"/>
    <result column="lastname" property="lastName"/>
    <result column="email" property="email"/>
    <result column="gender" property="gender"/>
    <result column="dept_name" property="dept.dept_name"/>
</resultMap>
<select id="findByIdWithDept" resultMap="userInfoDept" parameterType="java.lang.Integer">
    select u.id as uid,u.lastname,u.email,u.gender,d.dept_name,d.id as did from user2 as u,tab_dept as d
    where u.id= #{id}
    and u.deptid = d.id
</select>
```

```java
User findByIdWithDept = mapper.findByIdWithDept(1);
System.out.println("findByIdWithDept = " + findByIdWithDept.getDept().getDept_name());
```

#### 联合查询1

```xml
<resultMap id="userInfoDept" type="User">
        <id column="uid" property="id"/>
        <result column="lastname" property="lastName"/>
        <result column="email" property="email"/>
        <result column="gender" property="gender"/>
<!--        <result column="dept_name" property="dept.dept_name"/>-->
        <association property="dept" javaType="com.wqm.cn.vo.Dept">  //关联属性 关联类型（不能省略）
            <id column="did" property="id"/>                         //结果集中的那个字段 对应 关联表的字段
            <result column="dept_name" property="dept_name"/>        //那个字段要显示结果
        </association>
    </resultMap>
    <select id="findByIdWithDept" resultMap="userInfoDept" parameterType="java.lang.Integer">
        select u.id as uid,u.lastname,u.email,u.gender,d.dept_name,d.id as did from user2 as u,tab_dept as d
        where u.id= #{id}
        and u.deptid = d.id
    </select>
```

#### 分步查询

```java
public interface DeptMapper {
    Dept selectByDeptId(Integer id);
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.wqm.cn.mapper.DeptMapper">
    <select id="selectByDeptId" resultType="com.wqm.cn.vo.Dept">
        select id, dept_name
        from tab_dept
        where id = #{id}
    </select>
</mapper>
```

 

```java
//
User selectByStep(Integer id);
```



```xml
<resultMap id="setResult" type="com.wqm.cn.vo.User">
    <id property="id" column="id"/>
    <result column="lastname" property="lastName"/>
    <result column="gender" property="gender"/>
    <result property="email" column="email"/>
    <!--        property: 本表关联字段  column ：关联表的字段（主键）-->
    <association property="dept" select="com.wqm.cn.mapper.DeptMapper.selectByDeptId"
                 column="id"> <!--//column：关联表 的主键-->
    </association>
</resultMap>
<select id="selectByStep" resultMap="setResult" parameterType="java.lang.Integer">
    select *
    from user2
    where id = #{id}
</select>
```

测试

```java
User findByIdWithDept = mapper.selectByStep(1);
System.out.println("findByIdWithDept = " + findByIdWithDept.getDept().getDeptName());
```

结果

DEBUG 12-26 00:35:48,004 ==>  Preparing: select * from user2 where id = ?  (BaseJdbcLogger.java:137) 
DEBUG 12-26 00:35:48,054 ==> Parameters: 1(Integer)  (BaseJdbcLogger.java:137) 
DEBUG 12-26 00:35:48,087 ====>  Preparing: select id, dept_name from tab_dept where id = ?  (BaseJdbcLogger.java:137) 
DEBUG 12-26 00:35:48,088 ====> Parameters: 1(Integer)  (BaseJdbcLogger.java:137) 
DEBUG 12-26 00:35:48,091 <====      Total: 1  (BaseJdbcLogger.java:137) 
DEBUG 12-26 00:35:48,094 <==      Total: 1  (BaseJdbcLogger.java:137) 
findByIdWithDept = 技术部

##### 延迟加载

```xml
<configuration>
    <settings>
        <!--插入为空时插入空值避免报空指针-->
        <setting name="jdbcTypeForNull" value="NULL"/>
        <setting name="mapUnderscoreToCamelCase" value="true"/>
        <setting name="lazyLoadingEnabled" value="true"/>
      <!--        lazyLoadingEnabled	延迟加载的全局开关。当开启时，所有关联对象都会延迟加载。 特定关联关系中可通过设置 fetchType 属性来覆盖该项的开关状态。	true | false	false-->
<!--        aggressiveLazyLoading	开启时，任一方法的调用都会加载该对象的所有延迟加载属性。 否则，每个延迟加载属性会按需加载（参考 lazyLoadTriggerMethods)。	true | false	false （在 3.4.1 及之前的版本中默认为 true）-->
   
        <setting name="aggressiveLazyLoading" value="false"/>
    </settings>
```

#### 关联集合类型（嵌套结果集）

```java
public class Dept {
    private Integer id;
    private String deptName;
    private List<User> users;
```

```java
//查询部门的时候查出所有员工信息
Dept findDeptAndUsersByid(Integer id);
```

```xml
<resultMap id="dinfoAndUsers" type="com.wqm.cn.vo.Dept">
    <id column="did" property="id"/>
    <result column="dept_name" property="deptName"/>
    <!--        关联集合类型的属性规则
                    ofType
       -->
    <collection property="users" ofType="com.wqm.cn.vo.User">
        <id property="id" column="uid"/>
        <result column="lastname" property="lastName"/>
        <result column="gender" property="gender"/>
        <result property="email" column="email"/>
    </collection>
</resultMap>
<select id="findDeptAndUsersByid" resultMap="dinfoAndUsers" parameterType="java.lang.Integer">
    select d.id as did, d.dept_name, u.id as uid, u.lastname, u.gender, u.email
    from tab_dept as d
             left join user2 u on d.id = u.deptid
    where d.id = #{id}
</select>
```

```java
Dept deptAndUsersByid = mapper.findDeptAndUsersByid(1);
System.out.println("deptAndUsersByid.getUsers() = " + deptAndUsersByid.getUsers());
```

DEBUG 12-26 01:12:27,800 ==>  Preparing: select d.id as did, d.dept_name, u.id as uid, u.lastname, u.gender, u.email from tab_dept as d left join user2 u on d.id = u.deptid where d.id = ?  (BaseJdbcLogger.java:137) 
DEBUG 12-26 01:12:27,853 ==> Parameters: 1(Integer)  (BaseJdbcLogger.java:137) 
DEBUG 12-26 01:12:27,889 <==      Total: 1  (BaseJdbcLogger.java:137) 
deptAndUsersByid.getUsers() = [User{id=1, lastName='James', gender='man', email='110@ss.com'}]

分步查询

```java
//userMapper
//根据部门编号查询所有成员
List<User> setectUesersById(Integer id);
```

```xml
<!--userMapper.xml-->
<select id="setectUesersById" resultType="com.wqm.cn.vo.User">
    select *
    from user2
    where deptid = #{dept.id}
</select>
```

```java
//DeptMapper
Dept findDeptAndUsersByidStep(Integer id);
```

```xml
<!--DeptMapper.xml-->
<select id="findDeptAndUsersByid" resultMap="dinfoAndUsers" parameterType="java.lang.Integer">
    select d.id as did, d.dept_name, u.id as uid, u.lastname, u.gender, u.email
    from tab_dept as d
             left join user2 u on d.id = u.deptid
    where d.id = #{id}
</select>
<resultMap id="dinfoUsersStep" type="com.wqm.cn.vo.Dept">
    <id column="id" property="id"/>
    <result column="deptname" property="deptName"/>
    <collection property="users" column="id" select="com.wqm.cn.mapper.UserMapper.setectUesersById" fetchType="lazy" > //支持懒加载
    </collection>
</resultMap>
<select id="findDeptAndUsersByidStep" resultMap="dinfoUsersStep" parameterType="java.lang.Integer">
    select * from tab_dept
    where id = #{id}
</select>
```

```
Dept deptAndUsersByid = mapper.findDeptAndUsersByidStep(1);
System.out.println("deptAndUsersByid.getUsers() = " + deptAndUsersByid.getUsers());
```

DEBUG 12-26 01:29:06,389 ==>  Preparing: select * from tab_dept where id = ?  (BaseJdbcLogger.java:137) 
DEBUG 12-26 01:29:06,448 ==> Parameters: 1(Integer)  (BaseJdbcLogger.java:137) 
DEBUG 12-26 01:29:06,531 <==      Total: 1  (BaseJdbcLogger.java:137) 
DEBUG 12-26 01:29:06,535 ==>  Preparing: select * from user2 where deptid = ?  (BaseJdbcLogger.java:137) 
DEBUG 12-26 01:29:06,537 ==> Parameters: 1(Integer)  (BaseJdbcLogger.java:137) 
DEBUG 12-26 01:29:06,541 <==      Total: 1  (BaseJdbcLogger.java:137) 
deptAndUsersByid.getUsers() = [User{id=1, lastName='James', gender='man', email='110@ss.com'}]

#### 鉴别器

```java
//查出女生
// 如果是男生 吧lastname 给email
List<User> findGirls();
```

```xml
<resultMap id="girls" type="com.wqm.cn.vo.User">
        <id column="id" property="id"/>
        <result column="lastname" property="lastName"/>
        <result column="gender" property="gender"/>
        <result column="email" property="email"/>
        <discriminator javaType="string" column="gender">
            <case value="0" resultType="com.wqm.cn.vo.User">
                <association property="dept" select="com.wqm.cn.mapper.DeptMapper.selectByDeptId"
                             column="id"> <!--//column：关联表 的主键-->
                </association>
            </case>
            <case value="1" resultType="com.wqm.cn.vo.User">
                <id column="id" property="id"/>
                <result column="lastname" property="email"/>
                <result column="lastname" property="email"/>
<!--                <result column="email" property="email"/>-->
            </case>
        </discriminator>
    </resultMap>
    <select id="findGirls" resultMap="girls">
        select *
        from user2
    </select>
```

### 动态SQL DynamicSQL

#### where

```xml
 <?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
 PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
 "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.atguigu.mybatis.dao.EmployeeMapperDynamicSQL">
	<!-- 
• if:判断
• choose (when, otherwise):分支选择；带了break的swtich-case
	如果带了id就用id查，如果带了lastName就用lastName查;只会进入其中一个
• trim 字符串截取(where(封装查询条件), set(封装修改条件))
• foreach 遍历集合
	 -->
	 <!-- 查询员工，要求，携带了哪个字段查询条件就带上这个字段的值 -->
	 <!-- public List<Employee> getEmpsByConditionIf(Employee employee); -->
	 <select id="getEmpsByConditionIf" resultType="com.atguigu.mybatis.bean.Employee">
	 	select * from tbl_employee
	 	<!-- where -->
	 	<where>
		 	<!-- test：判断表达式（OGNL）
		 	OGNL参照PPT或者官方文档。
		 	  	 c:if  test
		 	从参数中取值进行判断
		 	
		 	遇见特殊符号应该去写转义字符：
		 	&&：
		 	-->
		 	<if test="id!=null">
		 		id=#{id}
		 	</if>
		 	<if test="lastName!=null &amp;&amp; lastName!=&quot;&quot;">
		 		and last_name like #{lastName}
		 	</if>
		 	<if test="email!=null and email.trim()!=&quot;&quot;">
		 		and email=#{email}
		 	</if> 
		 	<!-- ognl会进行字符串与数字的转换判断  "0"==0 -->
		 	<if test="gender==0 or gender==1">
		 	 	and gender=#{gender}
		 	</if>
	 	</where>
	 </select>  
</mapper>
```

#### trim

```xml
 <!--public List<Employee> getEmpsByConditionTrim(Employee employee);  -->
	 <select id="getEmpsByConditionTrim" resultType="com.atguigu.mybatis.bean.Employee">
	 	select * from tbl_employee
	 	<!-- 后面多出的and或者or where标签不能解决 
	 	prefix="":前缀：trim标签体中是整个字符串拼串 后的结果。
	 			prefix给拼串后的整个字符串加一个前缀 
	 	prefixOverrides="":
	 			前缀覆盖： 去掉整个字符串前面多余的字符
	 	suffix="":后缀
	 			suffix给拼串后的整个字符串加一个后缀 
	 	suffixOverrides=""
	 			后缀覆盖：去掉整个字符串后面多余的字符
	 			
	 	-->
	 	<!-- 自定义字符串的截取规则 -->
	 	<trim prefix="where" suffixOverrides="and">
	 		<if test="id!=null">
		 		id=#{id} and
		 	</if>
		 	<if test="lastName!=null &amp;&amp; lastName!=&quot;&quot;">
		 		last_name like #{lastName} and
		 	</if>
		 	<if test="email!=null and email.trim()!=&quot;&quot;">
		 		email=#{email} and
		 	</if> 
		 	<!-- ognl会进行字符串与数字的转换判断  "0"==0 -->
		 	<if test="gender==0 or gender==1">
		 	 	gender=#{gender}
		 	</if>
		 </trim>
	 </select>
```

#### choose

```xml
<!--    若带了id 就按id查 ，若带了lastname 就按 lastname 模糊查询 如果带了email 就按email查 -->
<select id="findUserByConditionChoose" resultType="com.wqm.cn.vo.User" parameterType="com.wqm.cn.vo.User">
    select * from user2 where 1=1
    <choose>
        <when test="id!=null">
            and id=#{id}
        </when>
        <when test="lastName!=null">
            and lastname like #{lastName}
        </when>
    </choose>
</select>
```

#### set

```xml 
<!-- public List<Employee> getEmpsByConditionChoose(Employee employee); -->
	 <select id="getEmpsByConditionChoose" resultType="com.atguigu.mybatis.bean.Employee">
	 	select * from tbl_employee 
	 	<where>
	 		<!-- 如果带了id就用id查，如果带了lastName就用lastName查;只会进入其中一个 -->
	 		<choose>
	 			<when test="id!=null">
	 				id=#{id}
	 			</when>
	 			<when test="lastName!=null">
	 				last_name like #{lastName}
	 			</when>
	 			<when test="email!=null">
	 				email = #{email}
	 			</when>
	 			<otherwise>
	 				gender = 0
	 			</otherwise>
	 		</choose>
	 	</where>
	 </select>
```

#### foreach

```xml
<!--public List<Employee> getEmpsByConditionForeach(List<Integer> ids);  -->
	 <select id="getEmpsByConditionForeach" resultType="com.atguigu.mybatis.bean.Employee">
	 	select * from tbl_employee
	 	<!--
	 		collection：指定要遍历的集合：
	 			list类型的参数会特殊处理封装在map中，map的key就叫list
	 		item：将当前遍历出的元素赋值给指定的变量
	 		separator:每个元素之间的分隔符
	 		open：遍历出所有结果拼接一个开始的字符
	 		close:遍历出所有结果拼接一个结束的字符
	 		index:索引。遍历list的时候是index就是索引，item就是当前值
	 				      遍历map的时候index表示的就是map的key，item就是map的值		 
	 		#{变量名}就能取出变量的值也就是当前遍历出的元素
	 	  -->
	 	<foreach collection="ids" item="item_id" separator=","
	 		open="where id in(" close=")">
	 		#{item_id}
	 	</foreach>
	 </select>
	 <insert id="addEmps" databaseId="oracle">
	 	<!-- oracle第一种批量方式 -->
	 	<!-- <foreach collection="emps" item="emp" open="begin" close="end;">
	 		insert into employees(employee_id,last_name,email) 
			    values(employees_seq.nextval,#{emp.lastName},#{emp.email});
	 	</foreach> -->
	 	
	 	<!-- oracle第二种批量方式  -->
	 	insert into employees(
	 		<!-- 引用外部定义的sql -->
	 		<include refid="insertColumn">
	 			<property name="testColomn" value="abc"/>
	 		</include>
	 	)
	 			<foreach collection="emps" item="emp" separator="union"
	 				open="select employees_seq.nextval,lastName,email from("
	 				close=")">
	 				select #{emp.lastName} lastName,#{emp.email} email from dual
	 			</foreach>
	 </insert>
```

#### set

```xml
 <!--public void updateEmp(Employee employee);  -->
 <update id="updateEmp">
 	<!-- Set标签的使用 -->
 	update tbl_employee 
	<set>
		<if test="lastName!=null">
			last_name=#{lastName},
		</if>
		<if test="email!=null">
			email=#{email},
		</if>
		<if test="gender!=null">
			gender=#{gender}
		</if>
	</set>
	where id=#{id} 
	<!-- 		
		Trim：更新拼串
		update tbl_employee 
		<trim prefix="set" suffixOverrides=",">
			<if test="lastName!=null">
				last_name=#{lastName},
			</if>
			<if test="email!=null">
				email=#{email},
			</if>
			<if test="gender!=null">
				gender=#{gender}
			</if>
		</trim>
		where id=#{id}  -->
	 </update>
	 
```
#### 批量保存

```xml
<!-- 批量保存 -->
	 <!--public void addEmps(@Param("emps")List<Employee> emps);  -->
	 <!--MySQL下批量保存：可以foreach遍历   mysql支持values(),(),()语法-->
	<insert id="addEmps">
	 	insert into tbl_employee(
	 		<include refid="insertColumn"></include>
	 	) 
		values
		<foreach collection="emps" item="emp" separator=",">
			(#{emp.lastName},#{emp.email},#{emp.gender},#{emp.dept.id})
		</foreach>
	 </insert><!--   -->
 <!-- 这种方式需要数据库连接属性allowMultiQueries=true；
 	这种分号分隔多个sql可以用于其他的批量操作（删除，修改） -->
 <!-- <insert id="addEmps">
 	<foreach collection="emps" item="emp" separator=";">
 		insert into tbl_employee(last_name,email,gender,d_id)
 		values(#{emp.lastName},#{emp.email},#{emp.gender},#{emp.dept.id})
 	</foreach>
 </insert> -->
 
 <!-- Oracle数据库批量保存： 
 	Oracle不支持values(),(),()
 	Oracle支持的批量方式
 	1、多个insert放在begin - end里面
 		begin
		    insert into employees(employee_id,last_name,email) 
		    values(employees_seq.nextval,'test_001','test_001@atguigu.com');
		    insert into employees(employee_id,last_name,email) 
		    values(employees_seq.nextval,'test_002','test_002@atguigu.com');
		end;
	2、利用中间表：
		insert into employees(employee_id,last_name,email)
	       select employees_seq.nextval,lastName,email from(
	              select 'test_a_01' lastName,'test_a_e01' email from dual
	              union
	              select 'test_a_02' lastName,'test_a_e02' email from dual
	              union
	              select 'test_a_03' lastName,'test_a_e03' email from dual
	       )	
 -->
```



#### 两个内置参数 

​	 

```xml
 <!-- 两个内置参数：
	 	不只是方法传递过来的参数可以被用来判断，取值。。。
	 	mybatis默认还有两个内置参数：
	 	_parameter:代表整个参数
	 		单个参数：_parameter就是这个参数
	 		多个参数：参数会被封装为一个map；_parameter就是代表这个map
	 	
	 	_databaseId:如果配置了databaseIdProvider标签。
	 		_databaseId就是代表当前数据库的别名oracle
	  -->
	  
	  <!--public List<Employee> getEmpsTestInnerParameter(Employee employee);  -->
	  <select id="getEmpsTestInnerParameter" resultType="com.atguigu.mybatis.bean.Employee">
	  		<!-- bind：可以将OGNL表达式的值绑定到一个变量中，方便后来引用这个变量的值 -->
	  		<bind name="_lastName" value="'%'+lastName+'%'"/>
	  		<if test="_databaseId=='mysql'">
	  			select * from tbl_employee
	  			<if test="_parameter!=null">
	  				where last_name like #{lastName}
	  			</if>
	  		</if>
	  		<if test="_databaseId=='oracle'">
	  			select * from employees
	  			<if test="_parameter!=null">
	  				where last_name like #{_parameter.lastName}
	  			</if>
	  		</if>
	  </select>
```
#### sql重用

```xml
  <!-- 
	  	抽取可重用的sql片段。方便后面引用 
	  	1、sql抽取：经常将要查询的列名，或者插入用的列名抽取出来方便引用
	  	2、include来引用已经抽取的sql：
	  	3、include还可以自定义一些property，sql标签内部就能使用自定义的属性
	  			include-property：取值的正确方式${prop},
	  			#{不能使用这种方式}
	  -->
	  <sql id="insertColumn">
	  		<if test="_databaseId=='oracle'">
	  			employee_id,last_name,email
	  		</if>
	  		<if test="_databaseId=='mysql'">
	  			last_name,email,gender,d_id
	  		</if>
	  </sql>
	  
```

## 缓存机制

### 一级缓存

#### 无效情况

- 同一个会话级别的，查到的直接放到一级缓存中默认开启，会话结束（缓存无效）

- 会话相同，查询条件不同（缓存中不存在，缓存无效）

- 会话相同，执行过程中，有增、删、该(可能会引起数据变化、缓存无效)

- 会话相同，手动清理后缓存无效  sqlSession.clearCache();

#### 二级缓存：（全局缓存）：基于namespace级别的缓存：一个namespace对应一个二级缓存：

	 * 		工作机制：
	 * 		1、一个会话，查询一条数据，这个数据就会被放在当前会话的一级缓存中；
	 * 		2、如果会话关闭；一级缓存中的数据会被保存到二级缓存中；新的会话查询信息，就可以参照二级缓存中的内容；
	 * 3、sqlSession===EmployeeMapper==>Employee
	
	   ​							DepartmentMapper===>Department

​						不同namespace查出的数据会放在自己对应的缓存中（map）

​				效果：数据会从二级缓存中获取 				

​							查出的数据都会被默认先放在一级缓存中。

​				只有会话提交或者关闭以后，一级缓存中的数据才会转移到二级缓存中

##### 		使用：

​				1）、开启全局二级缓存配置：<setting name="cacheEnabled" value="true"/>

​				2）、去mapper.xml中配置使用二级缓存：

​						

```
<mapper namespace="com.wqm.cn.mapper.UserMapper">
    <cache eviction="FIFO" flushInterval="22" readOnly="" type="" size="" blocking=""/>
    evication =
            • LRU – 最近最少使用的：移除最长时间不被使用的对象。
            • FIFO – 先进先出：按对象进入缓存的顺序来移除它们。
            • SOFT – 软引用：移除基于垃圾回收器状态和软引用规则的对象。
            • WEAK – 弱引用：更积极地移除基于垃圾收集器状态和弱引用规则的对象。
            • 默认的是 LRU。 
      flushInterval 时间间隔 毫秒数
      readonly是否只读
      			true：只读；mybatis认为所有从缓存中获取数据的操作都是只读操作，不会修改数据。
				 					mybatis为了加快获取速度，直接就会将数据在缓存中的引用交给用户。不安全，速度快
						false：非只读：mybatis觉得获取的数据可能会被修改。
									mybatis会利用序列化&反序列的技术克隆一份新的数据给你。安全，速度慢
			size：缓存存放多少元素；
			type=""：指定自定义缓存的全类名；
								实现Cache接口即可；
```

​				3）、我们的POJO需要实现序列化接口 

##### **!!**  注意

-  会话关闭后才会进入二级缓存

- 自在使用的《cache》的mapper 的命名空间中 

##### 和缓存有关的设置/属性：

​	1）、cacheEnabled=true：false：关闭缓存（二级缓存关闭）(一级缓存一直可用的)

​	2）、每个select标签都有useCache="true"：

​				**false：不使用缓存（一级缓存依然使用，二级缓存不使用）**

​	3）、【每个增删改标签的：flushCache="true"：（一级二级都会清除）】

​				增删改执行完成后就会清楚缓存；

​				测试：flushCache="true"：一级缓存就清空了；二级也会被清除；

​				查询标签：flushCache="false"：

​				如果flushCache=true;每次查询之后都会清空缓存；缓存是没有被使用的；

​    4）、sqlSession.clearCache();只是清楚当前session的一级缓存；

 	5）、localCacheScope：本地缓存作用域：（一级缓存SESSION）；当前会话的所有数据保存在会话缓存中；

​	STATEMENT：可以禁用一级缓存；		


​	 *第三方缓存整合：

​			1）、导入第三方缓存包即可；

​			2）、导入与第三方缓存整合的适配包；官方有；

​			3）、mapper.xml中使用自定义缓存

​						<cache type="org.mybatis.caches.ehcache.EhcacheCache"></cache>

![image-20201226093143048](https://tva1.sinaimg.cn/large/0081Kckwgy1gm106mpvolj30za0jyqb7.jpg)

![image-20201226094704196](https://tva1.sinaimg.cn/large/0081Kckwgy1gm10mglmrhj30qr0j9dps.jpg)

### Ehcahe





## MYbatis 运行原理

![image-20201226235713677](https://tva1.sinaimg.cn/large/0081Kckwgy1gm1p71afwyj30mc0fljzs.jpg)

![image-20201226230353985](https://tva1.sinaimg.cn/large/0081Kckwgy1gm1nnn7jjdj314l0sdk15.jpg)

流程

![image-20201227011227929](https://tva1.sinaimg.cn/large/0081Kckwgy1gm1rdc3jwfj31hc0u0wrh.jpg)





![image-20201227011333643](https://tva1.sinaimg.cn/large/0081Kckwgy1gm1regcss2j31dc0u0dqi.jpg)

![image-20201227011445866](https://tva1.sinaimg.cn/large/0081Kckwgy1gm1rfqb3vcj31jx0u0aln.jpg)



![image-20201227011101962](https://tva1.sinaimg.cn/large/0081Kckwgy1gm1rbtlf1fj31260sfdnw.jpg)



![image-20201227011545278](https://tva1.sinaimg.cn/large/0081Kckwgy1gm1rgr2v01j31cy0u0q9p.jpg)

## 插件开发

//ssphotos

```
package com.wqm.cn.config;


import org.apache.ibatis.executor.statement.SimpleStatementHandler;
import org.apache.ibatis.plugin.*;

import java.util.Properties;

/**
 * @ProjectName: MBG
 * @Package: com.wqm.cn.config
 * @ClassName: MyFirstPlugIn
 * @Author: WQM
 * @Description: 第一个插件
 * @Date: 2021/1/3 10:30 下午
 * @Version: 1.0
 */
@Intercepts(
        @Signature(type = SimpleStatementHandler.class, method = "query"
                , args = {java.sql.Statement.class,org.apache.ibatis.session.ResultHandler.class})
)
public class MyFirstPlugIn implements Interceptor {
    @Override
    public Object intercept(Invocation invocation) throws Throwable {
        System.out.println("插件执行 invocation = " + invocation);
        return invocation.proceed();
    }

    @Override
    public Object plugin(Object target) {
//        使用当前intercepter 返回代理对象
        System.out.println("包装的对象 target = " + target);
        return Plugin.wrap(target, this);
    }

    @Override
    public void setProperties(Properties properties) {
        System.out.println("插件配置的信息 properties = " + properties);
    }
}
```

```
package com.wqm.cn.config;  
import org.apache.ibatis.executor.statement.RoutingStatementHandler;
import org.apache.ibatis.plugin.*;

import java.util.Properties;

/**
 * @ProjectName: MBG
 * @Package: com.wqm.cn.config
 * @ClassName: MyFirstPlugIn
 * @Author: WQM
 * @Description: 第一个插件
 * @Date: 2021/1/3 10:30 下午
 * @Version: 1.0
 */
@Intercepts(
        @Signature(type = RoutingStatementHandler.class, method = "parameterize"
                , args = {java.sql.Statement.class})
)
public class MySecondPlugIn implements Interceptor {
    @Override
    public Object intercept(Invocation invocation) throws Throwable {
        System.out.println("MySecondPlugIn插件执行 invocation = " + invocation);
        return invocation.proceed();
    }

    @Override
    public Object plugin(Object target) {
//        使用当前intercepter 返回代理对象
        System.out.println("MySecondPlugIn包装的对象 target = " + target);
        return Plugin.wrap(target, this);
    }

    @Override
    public void setProperties(Properties properties) {
        System.out.println("MySecondPlugIn插件配置的信息 properties = " + properties);
    }
}
```

```
//resources/mybatis-config.xml  在全局配置文件注册
<plugins>
    <plugin interceptor="com.wqm.cn.config.MyFirstPlugIn">
        <property name="username" value="wqm"/>
    </plugin>
    <plugin interceptor="com.wqm.cn.config.MySecondPlugIn">
    </plugin>
</plugins>
```

存储过程



## 其他



### 模糊查询like语句该怎么写

（1）’%${question}%’ 可能引起SQL注入，不推荐

（2）"%"#{question}"%" 注意：因为#{…}解析成sql语句时候，会在变量外侧自动加单引号’ '，所以这里 % 需要使用双引号" "，不能使用单引号 ’ '，不然会查不到任何结果。

（3）CONCAT(’%’,#{question},’%’) 使用CONCAT()函数，推荐

（4）使用bind标签

```xml
<select id="listUserLikeUsername" resultType="com.jourwon.pojo.User">
　　<bind name="pattern" value="'%' + username + '%'" />
　　select id,sex,age,username,password from person where username LIKE #{pattern}
</select>
```







