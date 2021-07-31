# Jdk8 功能笔记

## lambda

## 排序

- 筛选：

```java
  //方式二 使用java8提供的流api实现 这种叫内部迭代
Map<String, List<Apple>> AppMap2=
    appleList.stream().filter((Apple a)->a.getWeight()>150) //筛选出大于150的
    .collect(groupingBy(Apple::getColor)); //按颜色分组  最后得到map
```



- 分组

```JAVA
  public static void main(String[] args) {
        List<Student> students = Arrays.asList(new Student("广东", 23),
                new Student("广东", 24),
                new Student("广东", 23),
                new Student("北京", 22), 
                new Student("北京", 20), 
                new Student("北京", 20),
                new Student("海南", 25));

        Map<String, List<Student>> listMap = students.stream().collect(Collectors.groupingBy(obj -> obj.getProvince()));
        listMap.forEach((key, value) -> {
            System.out.println("========");
            System.out.println(key);
            value.forEach(obj -> {
                System.out.println(obj.getAge());
            });
        });
 /* 输出结果
      ========
      广东
      23
      24
      23
      ========
      海南
      25
      ========
      北京
      22
      20
      20
 */
```



## 

新建实体类

```java
package com.vvvtimes.vo;
 
import java.math.BigDecimal;
import java.util.Date;
 
public class User {
 
    private Long id;
 
    //姓名
    private String name;
 
    //年龄
    private int age;
 
    //工号
    private String jobNumber;
 
    //性别
    private String sex;
 
    //入职日期
    private Date entryDate;
 
    //家庭成员数量
    private BigDecimal familyMemberQuantity;
 
    public Long getId() {
        return id;
    }
 
    public void setId(Long id) {
        this.id = id;
    }
 
    public String getName() {
        return name;
    }
 
    public void setName(String name) {
        this.name = name;
    }
 
    public int getAge() {
        return age;
    }
 
    public void setAge(int age) {
        this.age = age;
    }
 
    public String getJobNumber() {
        return jobNumber;
    }
 
    public void setJobNumber(String jobNumber) {
        this.jobNumber = jobNumber;
    }
 
    public String getSex() {
        return sex;
    }
 
    public void setSex(String sex) {
        this.sex = sex;
    }
 
    public Date getEntryDate() {
        return entryDate;
    }
 
    public void setEntryDate(Date entryDate) {
        this.entryDate = entryDate;
    }
 
    public BigDecimal getFamilyMemberQuantity() {
        return familyMemberQuantity;
    }
 
    public void setFamilyMemberQuantity(BigDecimal familyMemberQuantity) {
        this.familyMemberQuantity = familyMemberQuantity;
    }
}
1234567891011121314151617181920212223242526272829303132333435363738394041424344454647484950515253545556575859606162636465666768697071727374757677787980818283
```

## 分组

通过groupingBy可以分组指定字段

```java
        //分组
        Map<String, List<User>> groupBySex = userList.stream().collect(Collectors.groupingBy(User::getSex));
        //遍历分组
        for (Map.Entry<String, List<User>> entryUser : groupBySex.entrySet()) {
            String key = entryUser.getKey();
            List<User> entryUserList = entryUser.getValue();
123456
```

## 过滤

通过filter方法可以过滤某些条件

```java
        //过滤
        //排除掉工号为201901的用户
        List<User> userCommonList = userList.stream().filter(a -> !a.getJobNumber().equals("201901")).collect(Collectors.toList());
123
```

## 求和

分基本类型和大数类型求和，基本类型先mapToInt，然后调用sum方法，大数类型使用reduce调用BigDecimal::add方法

```java
        //求和
        //基本类型
        int sumAge = userList.stream().mapToInt(User::getAge).sum();
        //BigDecimal求和
        BigDecimal totalQuantity = userList.stream().map(User::getFamilyMemberQuantity).reduce(BigDecimal.ZERO, BigDecimal::add);
12345
```

上面的求和不能过滤bigDecimal对象为null的情况，可能会报空指针，这种情况，我们可以用filter方法过滤，或者重写求和方法

重写求和方法

```java
package com.vvvtimes.util;
 
import java.math.BigDecimal;
 
public class BigDecimalUtils {
 
    public static BigDecimal ifNullSet0(BigDecimal in) {
        if (in != null) {
            return in;
        }
        return BigDecimal.ZERO;
    }
 
    public static BigDecimal sum(BigDecimal ...in){
        BigDecimal result = BigDecimal.ZERO;
        for (int i = 0; i < in.length; i++){
            result = result.add(ifNullSet0(in[i]));
        }
        return result;
    }
}
123456789101112131415161718192021
```

使用重写的方法

```java
BigDecimal totalQuantity2 = userList.stream().map(User::getFamilyMemberQuantity).reduce(BigDecimal.ZERO, BigDecimalUtils::sum);

12
```

判断对象空

```
stream.filter(x -> x!=null)
 1
stream.filter(Objects::nonNull)
 1
```

判断字段空

```
stream.filter(x -> x.getDateTime()!=null)
 1
```

 

## 最值

求最小与最大，使用min max方法

```java
        //最小
        Date minEntryDate = userList.stream().map(User::getEntryDate).min(Date::compareTo).get();
 
        //最大
        Date maxEntryDate = userList.stream().map(User::getEntryDate).max(Date::compareTo).get();
12345
```

## List 转map

```javascript
         /**
         * List -> Map
         * 需要注意的是：
         * toMap 如果集合对象有重复的key，会报错Duplicate key ....
         *  user1,user2的id都为1。
         *  可以用 (k1,k2)->k1 来设置，如果有重复的key,则保留key1,舍弃key2
         */
        Map<Long, User> userMap = userList.stream().collect(Collectors.toMap(User::getId, a -> a,(k1,k2)->k1));
12345678
```

## 排序

可通过Sort对单字段多字段排序

```java
        //排序
        //单字段排序，根据id排序
        userList.sort(Comparator.comparing(User::getId));
        //多字段排序，根据id，年龄排序
        userList.sort(Comparator.comparing(User::getId).thenComparing(User::getAge));
12345
```

## 去重

可通过distinct方法进行去重

```java
        //去重
        List<Long> idList = new ArrayList<Long>();
        idList.add(1L);
        idList.add(1L);
        idList.add(2L);
        List<Long> distinctIdList = idList.stream().distinct().collect(Collectors.toList());
123456
```

## 获取list某个字段组装新list

```java
        //获取list对象的某个字段组装成新list
        List<Long> userIdList = userList.stream().map(a -> a.getId()).collect(Collectors.toList());
12
```

## 批量设置list列表字段为同一个值

```
addList.stream().forEach(a -> a.setDelFlag("0"));
 1
```
