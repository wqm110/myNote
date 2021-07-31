MBG



pom

```xml
<dependency>
    <groupId>org.mybatis.generator</groupId>
    <artifactId>mybatis-generator-core</artifactId>
    <version>1.4.0</version>
</dependency>
<dependency>
    <groupId>org.mybatis.generator</groupId>
    <artifactId>mybatis-generator-maven-plugin</artifactId>
    <version>1.4.0</version>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.22</version>
</dependency>
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.6</version>
</dependency>
```

```xml
<!DOCTYPE generatorConfiguration PUBLIC
        "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <context id="simple" targetRuntime="MyBatis3">
        <jdbcConnection driverClass="com.mysql.cj.jdbc.Driver"
                        password="123456"
                        userId="root"
                        connectionURL="jdbc:mysql://111.231.141.151:3306/myemployees" />

        <javaModelGenerator targetPackage="com.wqm.cn.vo" targetProject="src/main/java"/>

        <sqlMapGenerator targetPackage="com.wqm.cn.mapper" targetProject="src/main/resources"/>

        <javaClientGenerator type="XMLMAPPER" targetPackage="com.wqm.cn.mapper" targetProject="src/main/java"/>

        <table tableName="employees" />
    </context>
</generatorConfiguration>
```

```java
 package com.wqm.cn.util;

import org.mybatis.generator.api.MyBatisGenerator;
import org.mybatis.generator.config.Configuration;
import org.mybatis.generator.config.xml.ConfigurationParser;
import org.mybatis.generator.exception.InvalidConfigurationException;
import org.mybatis.generator.exception.XMLParserException;
import org.mybatis.generator.internal.DefaultShellCallback;

import java.io.File;
import java.io.IOException;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

/**
 * @ProjectName: MBG
 * @Package: com.wqm.cn.util
 * @ClassName: MBG
 * @Author: WQM
 * @Description:
 * @Date: 2021/1/3 9:55 上午
 * @Version: 1.0
 */
public class MBG {
    public static void main(String[] args) throws IOException, XMLParserException, InvalidConfigurationException, SQLException, InterruptedException {
        List<String> warnings = new ArrayList<String>();
        File f = new File("");
        String currenturl = MBG.class.getPackage().toString().replace("package ","")
                .replace(".",File.separator);
        String dir = "/src/main/java/"+currenturl+"/mybatis-config.xml";
        dir = f.getAbsolutePath() + dir;
        System.out.println("dir = " + dir);
        boolean overwrite = true;
        File configFile = new File(dir);
        ConfigurationParser cp = new ConfigurationParser(warnings);
        Configuration config = cp.parseConfiguration(configFile);
        DefaultShellCallback callback = new DefaultShellCallback(overwrite);
        MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, callback, warnings);
        myBatisGenerator.generate(null);
    }
}

```

分页插件

```
新版不逊要
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>最新版本</version>
</dependency>
新版不逊要

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

https://github.com/pagehelper/Mybatis-PageHelper/blob/master/wikis/zh/HowToUse.md

```
<plugins>
    <!-- com.github.pagehelper为PageHelper类所在包名 -->
    <plugin interceptor="com.github.pagehelper.PageInterceptor">
        <!-- 使用下面的方式配置参数，后面会有所有的参数介绍 -->
        <property name="supportMethodsArguments" value="true"/>
        <!--<property name="params" value="pageNum=pageNumKey;pageSize=pageSizeKey;"/>-->
	</plugin>
</plugins>
```