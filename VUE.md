# VUE

[BILBLI教程](https://www.bilibili.com/video/BV15741177Eh?p=3&spm_id_from=pageDriver)

## 初识

- 渐进式

  ![image-20210718000229092](https://i.loli.net/2021/07/18/SmDOPfHzVWnRpYC.png)

- 高级功能

  ![image-20210718000249790](https://i.loli.net/2021/07/18/FbzXkYLtsyR51uT.png)

### 安装

![image-20210718001042870](https://i.loli.net/2021/07/18/r2c5fV9GkijIF87.png)

### ES6

#### let

![image-20210718084718756](https://i.loli.net/2021/07/18/lwBqEncM51AXDi6.png)

If 和 for 没有作用域

![image-20210718090341375](https://i.loli.net/2021/07/18/8WwvUfnZzaMNOCx.png)



新方式

![image-20210718091159059](https://i.loli.net/2021/07/18/OpqFg9PRIk2HDYd.png)

#### const

![image-20210718092223344](https://i.loli.net/2021/07/18/SVycOK14lG2fRId.png)

- Const 的对象不能修改

- const 定义的时候必须有初始值

- const的对象不能再修改，内部属性可以修改

#### 对象增强写法

##### 属性增强写法

  ![image-20210718093409501](https://i.loli.net/2021/07/18/NuTwS3kq9ebJyt1.png)

##### 方法的增强写法

![image-20210718093551103](https://i.loli.net/2021/07/18/eujC3RhKsU4z68y.png)

### 响应式

##### MVVM

##### 声明周期

![image-20210718003000892](https://i.loli.net/2021/07/18/1wxELoAh6md5N7R.png)

![image-20210718004040242](https://i.loli.net/2021/07/18/u2TkAdsORzqfjaI.png)

![image-20210718005200984](https://i.loli.net/2021/07/18/QxAnbFJSzm4NhV2.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <h1>{{message}}</h1>
    <!--    <h1>{{animals}}</h1>-->
    <ul>
        <li v-for="an in animals"><h3 style="color:#5ca014">{{an}}</h3></li>
    </ul>
        <div>进度条:{{percent}}</div>
    <dev id="counter">
        <h2>计数器</h2>
        <button v-on:click="increament">点击停止</button>
        <!--    <button @click="subment">点击开始</button>-->
        <div>当前计数:{{counter}}</div>
    </dev>
</div>
</body>
<script src="./vue.js"></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: 90,
            animals: [
                'dog', 'cat', 'elephant'
            ],
            percent:'',
            counter: 0
        }, mounted() {
            setInterval(() => {
                this.counter++
                if (this.counter > 500) {
                    this.counter = 0
                    this.percent += "🐦\t"
                }

            }, 1)
        }, methods: {
            increament() {
                setInterval(() => {
                    if (this.counter !== 0) this.counter--
                }, 1)
            },
            device() {
            }
        }
    })

</script>
</html>

```



![image-20210718010816146](https://i.loli.net/2021/07/18/PwC5GgLJjSoWeql.png)

方法：method（在对象内部的）

函数：function（独立的）



#### 差值操作：

##### mustouch

![image-20210718013854051](https://i.loli.net/2021/07/18/YmsGalwOeK1AZIW.png)

```html
{{firstName + \t + lastName}}
{{firstName}} {{lastName}}
{{counter * 2}}
```

##### v-once 

```vue
<h2 v-once>
  {{name}}
</h2>
```

![image-20210718014508618](https://i.loli.net/2021/07/18/8zbwlSZPnGpv61I.png)

##### v-html

```<a href="http://www.baidu.com"> 解析```

##### v-text

##### v-pre {{message}}  不对mustouch 进行解析

##### v-cloak 斗篷

##### v-bind

  ![image-20210718020357892](https://i.loli.net/2021/07/18/5qAXt6saUlZcCfp.png)


```html
    <img  v-bind:src="img.url" alt="tupain">
    <img  :src="img.url" alt="tupain"> 语法糖
```

###### 动态绑定class

![image-20210718021747034](https://i.loli.net/2021/07/18/w6FWJj5QiA1eZRh.png)

###### 对象语法

###### 数组语法

![image-20210718023543443](https://i.loli.net/2021/07/18/596wI72kFHCzlb4.png)

### 计算属性：computed：

computed 方法使用名词名字

![image-20210718074855262](https://i.loli.net/2021/07/18/iO4dZfvluobCR6A.png)

![image-20210718075536509](https://i.loli.net/2021/07/18/ekwTFczUrnJY4sD.png)

#### 计算属性完整写法

![image-20210718083352956](https://i.loli.net/2021/07/18/7GLQoeTAH3xbltu.png)

#### 计算属性缓存

![image-20210718084350127](https://i.loli.net/2021/07/18/rhFujIC7bQRxdz6.png)

### 事件监听：v-on

![image-20210718084439379](https://i.loli.net/2021/07/18/VF5Rr2cwsmtCGHb.png)

#### 语法糖

![image-20210718094533803](https://i.loli.net/2021/07/18/M8XByv5hzZiJdfu.png)

![image-20210718095626830](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/plD3MrUdYshHRXx.png)

```html
<button v-on:click="getss()"></button>
<button v-on:click="getss"></button>
<button @:click="getss()"></button>
<button @:click="getss"></button>
<script>
getss(event){
  //
}
</script>
```

![image-20210718100037133](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/JeH4aBhxuONb8Rf.png)

#### 修饰符

![image-20210718100234310](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/3eH1jrSN9VJEXDY.png)

### 条件判断：v-if

![image-20210718100948778](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/JvnD2LPRbyUw516.png)

![image-20210718101050421](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/QlzMUochjuEIwtg.png)

![image-20210718102229793](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/9p5nseKNTSDtQ3f.png)

vm 复用问题的解决

![image-20210718102525045](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718102525045.png)

### 条件显示：v-show

![image-20210718102919432](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718102919432.png)

### 循环：v-for

![image-20210718142622658](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718142622658.png)

![image-20210718150055657](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718150055657.png)

![image-20210718151014807](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718151014807.png)

![image-20210718151256644](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718151256644.png)

![image-20210718151627004](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718151627004.png)

练习

```html
<!DOCTYPE html>
<html lang="en" xmlns:>
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <div v-if="books.length>0">
        <table>
            <thead>
            <tr>
                <th></th>
                <th>书籍名称</th>
                <th>出版日期</th>
                <th>价格</th>
                <th>购买数量</th>
                <th>操作</th>
                <th></th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(book,index) in books">

                <td>{{book.name}}</td>
                <td>{{book.publishDate}}</td>
                <td>{{book.price | showPrice}}</td>
                <td>
                    <button @click="sub(index)" :disabled="book.amount <= 1">-</button>
                    {{book.amount}}
                    <button @click="add(index)">+</button>
                </td>
                <td>
                    <button @click="remove(index)">移除</button>
                </td>
            </tr>
            <tr>
                <td>总价:{{totalPrice | showPrice}}</td>
            </tr>
            </tbody>

        </table>
    </div>
</div>
</body>
<script src="./vue.js"></script>
<script>
    const v = new Vue({
        el: '#app',
        data: {
            currentIndex: 0,
            books: [
                {
                    name: '算法导论',
                    publishDate: '2021-07-18',
                    price: 90,
                    amount: 1,
                    opt: '添加'
                }
            ],
            // totalPrice: 0,

        }, mounted: {},
        methods: {
            add(index) {
                this.books[index].amount += 1
            },
            sub(index) {
                this.books[index].amount -= 1
                let book = this.books[index].amount

                if (this.books[index].amount < 1)
                    this.books.slice(1, index - 1)
            },
            remove(index) {
                this.books.slice(index, 1)
            }
        }, computed: {
            totalPrice() {
                let tp = 0
                for (let i = 0; i < this.books.length; i++) {
                    tp += this.books[i].amount * this.books[i].price
                }
                return tp
            }
        }, filters: {
            showPrice(p) {
                return '￥' + p + '.00'
            }
        }
    })
</script>
<style>
    table thead {
        color: #5ca014;
    }

    table tbody {
        padding-left: 150px;
        background-color: #bcb8c1;
    }
</style>
</html>

```

高阶函数

- filter
- map
- reduce

```js
totalPrice() {
    return this.books.reduce((preValue, book) => {
    		return preValue + book.amount * book.price
  	}, 0)
}
```

### 表单双向绑定：v-model

手动双向绑定1

![image-20210718172933105](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718172933105.png)

手动双向绑定2

![image-20210718173135496](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718173135496.png)

原理

![image-20210718173259813](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718173259813.png)

### v-radio

### v-checkbox

![image-20210718174323829](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718174323829.png)

### v-select

![image-20210718174727131](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718174727131.png)

值绑定

![image-20210718175113133](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718175113133.png)

![image-20210718175217348](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718175217348.png)

### 修饰符

![image-20210718175719549](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718175719549.png)

## 组件化

![image-20210718180227802](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718180227802.png)

![image-20210718180850463](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718180850463.png)

![image-20210718180930248](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718180930248.png)

![image-20210718181636496](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718181636496.png)

![image-20210718181656363](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718181656363.png)

![image-20210718182102164](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718182102164.png)

### 全局组件和局部组件

![image-20210718182226847](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718182226847.png)

### 父组件和子组件



![image-20210718182818932](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718182818932.png)

### 组件分离

![image-20210718183649267](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718183649267.png)

![image-20210718183752480](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718183752480.png)

![image-20210718184249441](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718184249441.png)

### 组件数据的存放

![image-20210718184527951](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718184527951.png)

### 父子组件的通信

![image-20210718191136406](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718191136406.png)

### 父组件给子组件传值：props

![image-20210718192923500](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718192923500.png)

### 驼峰传值

![image-20210718194710791](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718194710791.png)

### 子传父 三部曲

![image-20210718200158842](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718200158842.png)

![image-20210718195705962](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718195705962.png)

![image-20210718195804387](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718195804387.png)

![image-20210718195940651](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718195940651.png)

### 父子组件的访问方式

![image-20210720222327728](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210720222327728.png)

#### children

![image-20210721010650807](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210721010650807.png)

#### ref

![image-20210721011202286](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210721011202286.png)

![image-20210721011516120](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210721011516120.png)



###  slot

![image-20210718200859739](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210718200859739.png)

#### 具名插槽

![image-20210723193938138](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723193938138.png)

![image-20210723195133419](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723195133419.png)

#### 作用域插槽

![image-20210723202859422](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723202859422.png)

![image-20210723202819931](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723202819931.png)



## 前端模块化开发

![image-20210723203058439](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723203058439.png)



![image-20210723205349075](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723205349075.png)



![image-20210723214945475](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723214945475.png)

### comonJs

![image-20210723215549040](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723215549040.png)







### ES6

导入、导出

![image-20210723220743071](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723220743071.png)

![image-20210723220802063](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723220802063.png)

![image-20210723220828861](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723220828861.png)

![image-20210723220904330](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723220904330.png)

![image-20210723221020709](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723221020709.png)

![image-20210723221457723](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723221457723.png)

![image-20210723221858490](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723221858490.png)





![image-20210723222006389](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723222006389.png)



## webpack

### [中文档](https://www.webpackjs.com/concepts/)

![image-20210723222242288](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723222242288.png)

![image-20210723222310092](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723222310092.png)



![image-20210723222555975](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723222555975.png)

![image-20210723222826448](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723222826448.png)



![image-20210723222941649](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723222941649.png)

![image-20210723223137766](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723223137766.png)





![image-20210723223601970](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723223601970.png)



![image-20210723223931790](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723223931790.png)

```js
webpack ./main.js ./bundle.js
```

![image-20210723225136665](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723225136665.png)

![image-20210723225240575](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723225240575.png)

### 配置 webpack.config.js

生成package.json

```shell
npm init
```

![image-20210723225927216](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723225927216.png)



![image-20210723230630867](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723230630867.png)

![image-20210723230658963](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723230658963.png)

### loader

![image-20210723230908042](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723230908042.png)



![image-20210723232332896](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723232332896.png)

![image-20210723232538679](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723232538679.png)



![image-20210723232648782](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723232648782.png)

![image-20210723232715869](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723232715869.png)



### Less 

![image-20210723233445608](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723233445608.png)

![image-20210723233554879](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723233554879.png)

![image-20210723234042802](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723234042802.png)

![image-20210723234307829](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210723234307829.png)





### 图片处理



![image-20210724000044123](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724000044123.png)



![image-20210724000203557](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724000203557.png)

![image-20210724000317766](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724000317766.png)

###  es6

![image-20210724005452661](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724005452661.png)

![image-20210724010757073](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724010757073.png)



![image-20210724013727615](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724013727615.png)

![image-20210724014451109](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724014451109.png)



![image-20210724015813600](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724015813600.png)

![image-20210724015914272](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724015914272.png)





### plugin

![image-20210724020747752](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724020747752.png)

#### 版权

![image-20210724075151560](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724075151560.png)

#### html

![image-20210724081641373](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724081641373.png)

#### js 压缩

![image-20210724091051524](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724091051524.png)

#### 本地服务器

![image-20210724091548381](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724091548381.png)





#### 配置分离

![image-20210724094357041](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724094357041.png)



![image-20210724094511855](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724094511855.png)



![image-20210724094546456](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724094546456.png)

## vue CLI

![image-20210724094922030](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724094922030.png)

### 准备

![image-20210724095256560](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724095256560.png)

![image-20210724095335002](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724095335002.png)

###  cli2 使用

![image-20210724100028527](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724100028527.png)

![image-20210724101454673](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724101454673.png)

![image-20210724102252693](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724102252693.png)

![image-20210724103538647](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724103538647.png)

#### 目录结构

![image-20210724103830917](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724103830917.png)

### CLI3 使用





![image-20210724110253730](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724110253730.png)



![image-20210724112156319](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724112156319.png)









## VUE-ROUTER

![image-20210724120638634](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724120638634.png)

![image-20210724120602980](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724120602980.png)



![image-20210724122034989](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724122034989.png)





![image-20210724122518469](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724122518469.png)

![image-20210724122802630](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724122802630.png)



### location

#### Location.hash

#### location.href

![image-20210724124740073](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724124740073.png)

### History

#### historyt.pushState

![image-20210724124758406](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724124758406.png)

#### history.replaceState

History.back() 回退

![image-20210724125324967](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724125324967.png)

#### go()

![image-20210724125400636](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724125400636.png)

### 使用

![image-20210724125649771](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724125649771.png)

![image-20210724130759721](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210724130759721.png)



![image-20210731000218569](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731000218569.png)



![image-20210731000413026](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731000413026.png)

![image-20210731000355465](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731000355465.png)

链接不可反回

![image-20210731000707730](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731000707730.png)



![image-20210731001347537](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731001347537.png)

![image-20210731001421173](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731001421173.png)

![image-20210731002110219](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731002110219.png)

$rout 当前活跃的路由

$router 全局路由对象

![image-20210731004811939](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731004811939.png)

![image-20210731004842309](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731004842309.png)

​					![image-20210731011501682](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731011501682.png)

​	

![image-20210731011712519](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731011712519.png)



![image-20210731012624543](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731012624543.png)

​	

![image-20210731012602350](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731012602350.png)

参数传递

![image-20210731012913884](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731012913884.png)

![image-20210731013203961](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731013203961.png)



![image-20210731013506803](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731013506803.png)

![image-20210731014637726](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731014637726.png)

![image-20210731014558717](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731014558717.png)

![image-20210731014735082](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210731014735082.png)









## VUEX







## AXIOS（请求封装）

