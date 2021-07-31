# iso 开发

可删除部分

```undefined
Xcode.app/Contents/Developer/Platforms/WatchOS.platform/Library/Developer/CoreSimulator/Profiles/Runtimes/watchOS.simruntime

Xcode.app/Contents/Developer/Platforms/AppleTVOS.platform/Library/Developer/CoreSimulator/Profiles/Runtimes/tvOS.simruntime
```



## 基本数据类型

![截屏2021-07-14 上午12.44.00](https://i.loli.net/2021/07/14/92l4LBi3VXNsh6d.png)

### 布尔

```swift
var b:Bool = true
```



### 常量

```swift
let a:Int = 3
let a = 9
```

### 变量

```swift
var b = 9
var f = true
var z:String = "z"
```

### 整型

```swift
var z:Int = 90
```

### 浮点

```swift
var Double = 3.0
```

### 字符串

```swift
var s:String = "zsdfs"
```

### 字符

```swift
var c:Character="c"
```



### 类型判断

```swift

var greeting = "Hello, playground"
var d:Double = 9.0
print(c)
print(b)
let g = 9
var t = type(of: c)
print(t)
print("c \(b)")//字符串拼接
// 单行注释
/*
 多行注释
 */
```

### 类型别名

![截屏2021-07-14 上午1.04.03](https://i.loli.net/2021/07/14/JBWXiK2hC4eRESP.png)

```swift
//别名语法 typealias
typealias S = String
var james:S="javames"
print(james)
print("它的名字是\(james)")
```

### ？？ 语法

```swift
// ?? 语法

var ten:S="100"
var v:Int = Int(ten) ?? 0
print(Int(ten)!)
```

### 可选类型

```swift
//可选类型
var a:Int?=100
print(a!)
if(a==nil){
    print("a 的值为空")
}else{
    print("a的值为 \(a!)")// 将a的值解析出来
}
```

## 元组

```swift
//元组类型
//不同类型数据的封装

//存值
y.3=true



```

### 声明

```swift
var y = (1,2.0,"yuanzu",false)
var y1:(Int,String) = (3,"指定类型的元组定义")
var y2 = (1)
var y3:(Double)=(3.0)
```

### 取值

```swift
print(y)
print(y1)
print(y.0)
// 取值
print(y.2)
```

### 复制，修改

```swift
// 复制，传值
var temp = y.3
print(temp)
var yname = (name1:3,name2:"元组健值",name3:false)
print(yname.name3)//元组按名称取值
var yn:(name:Int,name1:String,name3:Double) = (3,"元组声明时指定名称和类型",3.3)
print(yn.name3)
```

### 解构

```swift
//元组解构
let (n1,m1)=("james","Kottlin")
print(n1)
print(m1)
```

### 忽略 -

```swift
// 解构忽略
let(n2,_,m2) = ("张三","李四","王五")
print(n2,m2)
```

## 基础运算符

![image-20210715214607115](https://i.loli.net/2021/07/15/FL7tUKp6sazegkN.png)

```swift
```

### 比较运算符

![image-20210715214713738](https://i.loli.net/2021/07/15/6Xl4ONZm9faRLYs.png)

```swift
```

### 逻辑运算符

![image-20210715214823613](https://i.loli.net/2021/07/15/We5xmNFtVUlgDfj.png)

```swift
```
### 三元运算符

![image-20210715214856262](https://i.loli.net/2021/07/15/SGDACabLKcZifrI.png)

```swift
```
### 合并空值运算符

![image-20210715214933911](https://i.loli.net/2021/07/15/Lb12gXQv5PFzNwr.png)

### 区间是运算符

![image-20210715215209894](https://i.loli.net/2021/07/15/cwb6iFUq3O9LA1f.png)

运算符的一些说明

![image-20210715215308615](https://i.loli.net/2021/07/15/PKGJ2rv3a4MdcUX.png)

![image-20210715215436891](https://i.loli.net/2021/07/15/SiXNg8nLqRMVc75.png)

```swift
```
## 程序控制

### if

```swift
if y.1 < 10 {
    print("temp < 10")
}else if(y.1 > 10){
    print("temp > 10")
}else{
    print("print jj")
}

if g > 5 {
    //TODO
}else if g > 20{
    print("g>20")
}else{
    print("sdfs")
}
if "hell" == "hello"{
    print(a)
}
```
可选绑定

```swift
//可选绑定
var value:Int? = 9
if let v = value{
    print("value 的值是\(v)")
}else{
    print("value的值为空")
}
```
隐式展开

```swift
//隐式展开
var yy:Int! = 100
var b:Int = yy  //接收的地方要指定数据类型
print(b)
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```
```swift
```

