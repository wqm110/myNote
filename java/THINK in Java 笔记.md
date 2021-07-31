# THINK in Java 笔记



![image-20210115131556064](https://tva1.sinaimg.cn/large/008eGmZEgy1gmob1y1xobj313r0mk1eb.jpg)

bigInteger

bigDECIMAL

### 第二章

数组  确保数组初始化 

​		 下标检查

​		 创建数组对象时 实际上是创建了一个引用数组，每个引用默认初始化为特定的值，该值拥有自己的关键字null

​		基本对象的数组 初始值默认0

![image-20210115132717082](https://tva1.sinaimg.cn/large/008eGmZEgy1gmobdquee1j30mp0jckb1.jpg)

类的属性 声明时 不回默认初始化 class A{ int x; x++}  会报错

static 关键字 为特定域分配丹玉存储空间 1、不与具体对象绑定  2、不要创建对象

### 第三章

​	同名现象

​	算数运算符 去掉小数 10/4=2

```java
Random rand = new Random(47);
int k = rand.nextInt(100);//rand.nextFloat(),rand.nextDouble()
```

一元加减

```java
x=-a;
```

自动递增和递减

```java
++2;
--2;
i--;

```

equals

```java
 a.equals()比较内容  == 比较引用（直接值）
```

短路

```java

```

直接常量

```java
int  i=0x2f;double b=3D;float c=4f;
System.out.println(Integer.toBaneryString(i));
```

按位操作符

|  &   | 都是1才为1 |  &=  |      |
| :--: | :--------: | :--: | ---- |
|  \|  |            | \|=  |      |
|  ~   |            |      |      |
|  ^   |            |  ^=  |      |

结尾和舍入    

```java
Math.rand(8.6) =9
 

```



```java
Character.isLowerCase(c)
```

return 标签机制

```java

```




```java

```



```java
 
```



```java

```




```java

```



```java

```



```java

```



```java

```




```java

```




```java

```



```java

```



```java

```




```java

```



```java

```




```java

```



```java

```