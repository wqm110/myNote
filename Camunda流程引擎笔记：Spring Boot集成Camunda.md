# [Camunda流程引擎笔记(一)：Spring Boot集成Camunda](https://segmentfault.com/a/1190000022127867)

[![img](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/150537686-5d0b224ef0acf_huge128.jpeg)**悠然自得**](https://segmentfault.com/u/vulgar_cd)发布于 2020-03-24

> 开发工具：IDEA 2019.3.1
>
> 框架版本：Spring Boot 2.2.5.RELEASE
>
> Camunda版本：3.4.1
>
> Camunda modeler: 3.7.1
>
> 数据库：H2

## 一、创建maven工程

### 引入依赖

```
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>2.2.5.RELEASE</version>
</parent>

<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
  </dependency>
    <!-- camunda依赖 -->
  <dependency>
    <groupId>org.camunda.bpm.springboot</groupId>
    <artifactId>camunda-bpm-spring-boot-starter-webapp</artifactId>
    <version>3.4.1</version>
  </dependency>

  <dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
  </dependency>
</dependencies>
```

### 创建Spring Boot引导类

```
@SpringBootApplication
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}
```

### 启动应用

应用启动后访问`http://localhost:8080/`，可以看到下面的页面：

![image-20200319162625820.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0BX.png)

## 二、自定义配置应用

在`application.yml`中添加以下配置：

```
camunda:
  bpm:
    admin-user:
      id: kermit
      password: superSecret
      first-name: kermit
    filter:
      create: All tasks
```

再次启动应用，可以看到以下页面：

![image-20200319163107281.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0BT.png)

这时候流程引擎不再要求你注册，可以使用在`application.yml`中配置的`用户名(kermit)`和`密码(superSecret)`登录。



# [Camunda流程引擎笔记(二)：Service Task](https://segmentfault.com/a/1190000022128011)

[![img](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/150537686-5d0b224ef0acf_huge128-20210722014738439.jpeg)**悠然自得**](https://segmentfault.com/u/vulgar_cd)发布于 2020-03-24

> `Service Task`即服务任务，就是由系统驱动的任务。

## 一、下载安装camunda-modeler

### 下载

点击`https://camunda.com/download/modeler/`下载`camunda-modeler`流程绘制工具。

![image-20200319164508351.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0DB.png)

### 安装

安装camunda-modeler流程绘制工具后打开可以看到以下界面：

![image-20200319165751555.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0DE.png)

## 二、绘制一个简单的流程

### 新建一个BPMN文档

双击圆圈添加注释`审核流程开始`。

![image-20200319173424673.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0DV.png)

### 创建一个 SERVICE TASK

点击图中圆圈选择圆角方框。添加注释`审核`，然后点击`小扳手`选择`Service Task`。

![image-20200319173517768.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0D9.png)

### 配置 SERVICE TASK

![image-20200320093146005.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Eb.png)

`Implementation`有多个类型，这里只演示Java Class，其他类型可以自行试试。

### 绘制流程结束节点

点击`审核`圆角方框，选择黑色圆圈，添加注释`审核流程结束`。

![image-20200320094431120.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Ed.png)

### 保存

将上面绘制的流程保存为`audit.bpmn`。

## 三、配置应用

### 配置

- 在`src/main/resources`目录下创建`META-INF`文件夹，创建一个空的`processes.xml`文件。

- 将上面绘制

  ```
  audit.bpmn
  ```

  拷贝到

  ```
  src/main/resources
  ```

  下。

  ![image-20200320094936627.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Ee.png)

- 在应用引导类上添加`@EnableProcessApplication`注解，开启camunda自动配置。

  ```
  @EnableProcessApplication
  @SpringBootApplication
  public class App {
      public static void main(String[] args) {
          SpringApplication.run(App.class, args);
      }
  }
  ```

### 编写回调代码

要实现流程回调Java代码，Java类必须实现`org.camunda.bpm.engine.delegate.JavaDelegate`接口。

```
public class AuditDelegate implements JavaDelegate {

    @Override
    public void execute(DelegateExecution execution) throws Exception {
        System.out.println("审核流程 - SERVICE TASK - 回调");
    }
}
```

### 测试

- 启动应用

- 开启一个流程实例

  访问`http://localhost:8080/app/tasklist/default/#/`开启流程实例。

  ![image-20200320093914245.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0EL.png)

  ![image-20200320093948176.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0EO.png)

  ![image-20200320094014221.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0EQ.png)

  回到应用控制台可以看到Java回调类打印的字符串：

  ![image-20200320094119393.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0EX.png)

  流程结束。







# [Camunda流程引擎笔记(三)：User Task](https://segmentfault.com/a/1190000022128159)

[![img](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/150537686-5d0b224ef0acf_huge128-20210722014808398.jpeg)**悠然自得**](https://segmentfault.com/u/vulgar_cd)发布于 2020-03-24

> `User Task`即用户任务，就是由用户驱动的任务。

## 一、绘制流程

在`audit.bpmn`流程中的`审核流程开始节点`和`审核节点`之间添加一个圆角方框并添加注释为`审批`。同样点击小扳手选择`User Task`将该节点设置为用户任务（User Task）。

![image-20200320100136417.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Gx.png)

![image-20200320100335740.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0GO.png)

## 二、测试

1、更新应用中的bpmn流程文件。

2、启动应用。

3、启动一个流程实例。

4、查看任务列表。

![image-20200320100809413.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Hb.png)

刷新一下页面。

![image-20200320100832249.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Hy.png)

点击`审批`，再点击`Diagram`。可以看到流程到了`User Task`-用户审批节点。

![image-20200320101036283.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0HB-20210722014811380.png)

再点击`Form`，这里可以看到一些属性值和`Complete`按钮。因为我们没有配置属性变量，所以直接点击`Complete`按钮通过审批。

![image-20200320101255945.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0HC.png)

通过审批之后，便到了`Service Task`节点，所以回到控制台可以看到回调信息：

![image-20200320101358764.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0HO.png)

流程结束。



# [Camunda流程引擎笔记(四)：Send Task，Receive Task](https://segmentfault.com/a/1190000022128311)

[![img](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/150537686-5d0b224ef0acf_huge128-20210722014839589.jpeg)**悠然自得**](https://segmentfault.com/u/vulgar_cd)发布于 2020-03-24

> 流程引擎中`Send Task`和`Service Task`拥有相同的行为，都是通过回调Java代码完成相应逻辑。通常`Send Task`和`Receive Task`配合使用。

## 一、Send Task

绘制一个`Send Task`流程，配置过程和`Service Task`一样。

![image-20200320112548056.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0IQ.png)

## 二、Receive Task

> A Receive Task is a simple task that waits for the arrival of a certain message. When the process execution arrives at a Receive Task, the process state is committed to the persistence storage. This means that the process will stay in this wait state until a specific message is received by the engine, which triggers continuation of the process beyond the Receive Task.
>
> 翻译：接收任务是一个简单的任务，它等待特定消息的到来。当流程执行到达接收任务时，流程状态被提交到持久性存储。这意味着流程将保持这种等待状态，直到引擎接收到特定的消息，这将触发Receive任务之外的流程继续。
>
> 简单来说就是流程到达`Receive Task`节点后将持久化这个状态直到接收到一个特定的消息，才会继续往下走。

绘制一个`Receive Task`流程。

![image-20200320113242502.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0IZ.png)

## 三、测试

- 编写Java回调类。

  这里的`.createMessageCorrelation("message")`中配置了上面流程图中的`Message Name`填写字符串。

  而`.processInstanceBusinessKey("messageBusinessKey")`中填写了一个特定的业务key，方便找到特定的`Receive Task`流程。

  ```
  public class SendTaskDelegate implements JavaDelegate {
      @Override
      public void execute(DelegateExecution execution) throws Exception {
          execution.getProcessEngineServices()
                  .getRuntimeService()
                  .createMessageCorrelation("message")
                  .processInstanceBusinessKey("messageBusinessKey")
                  .correlate();
      }
  }
  ```

- 启动流程。

  首先启动`Send Task`流程可以看到以下错误：

  ![image-20200320113637028.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Jo.png)

  很明显，这是提示我们需要首先启动一个`Receive Task`流程实例以接收`Send Task`流程实例发送的消息。

  启动`Send Task`流程实例。

  ![image-20200320113836231.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Jq.png)

  这里`Business Key`填写了上面代码中配置的`messageBusinessKey`。

  访问`http://localhost:8080/app/cockpit/default/#/dashboard`，可以看到有一个活动中的流程：

  ![image-20200320114058415.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0JD.png)

  点击`Running Process Instances`：

  ![image-20200320114128639.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0JF.png)

  这里显示`Receive Task`流程停止在了`receive message`节点上。

  接下来启动一个`Send Task`流程实例：

  ![image-20200320114332673.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0JH.png)

  再次访问`http://localhost:8080/app/cockpit/default/#/dashboard`，可以看到已经没有执行中的流程了：

  ![image-20200320114419936.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0JT.png)

  说明`Receive Task`流程已经接受到了`Send Task`流程发送的`message`消息，所以流程继续执行直到结束。



# [Camunda流程引擎笔记(五)：Gateway](https://segmentfault.com/a/1190000022128396)

[![img](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/150537686-5d0b224ef0acf_huge128-20210722014918161.jpeg)**悠然自得**](https://segmentfault.com/u/vulgar_cd)发布于 2020-03-24

> `Gateway`即任务网关，控制任务的走向。

## 一、绘制流程

在前面绘制的审核流程图上的`User Task`节点和`Service Task`节点之间添加一个`Gateway`组件。

![image-20200323102557785.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0KY.png)

然后从`Gateway`组件拉一条单向箭头至`审核流程结束`节点。

![image-20200323102827876.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0K5.png)

修改`User Task`节点，添加一个`Boolean`变量`approve`。

![image-20200323103223460.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0K8.png)

修改`Gateway`组件分支属性。

![image-20200323103341226.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Le.png)

![image-20200323103419766.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Lm.png)

## 二、测试

1、更新应用中的bpmn流程文件。

2、启动应用。

3、启动一个流程实例。

![image-20200323103538519.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0Lz.png)

4、访问`http://localhost:8080/app/tasklist/default/#/`查看任务列表，可以看到我们在`User Task`节点上增加的变量`approve`，点击`Complete`。

![image-20200323103617019.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0LD.png)

5、查看日志，可以看到`Service Task`已经回调了Java代理类，结束流程。

![image-20200323103911279.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0LJ.png)

6、再次启动一个审批流程实例，这次我们将`approve`变量值置为`false`。可以看到流程直接走向了`拒绝`分支，结束了流程。



# [Camunda流程引擎笔记(六)：Business Rule Task](https://segmentfault.com/a/1190000022129549)

[![img](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/150537686-5d0b224ef0acf_huge128-20210722015030793.jpeg)**悠然自得**](https://segmentfault.com/u/vulgar_cd)发布于 2020-03-24

> `Business Rule Task`即`业务规则任务`，就是可以针对一个任务流程定义多个规则，打个比方就是一个流程能通过的情况可能有多种，这里的很多种就可以抽象成业务规则。所以配置好业务规则可以使一个流程变得更加灵活。

为了说明`Business Rule Task`以及总结之前说明的各种任务组件，这里将绘制一个稍微复杂点的流程。

## 一、绘制流程图

流程图最终效果。

> 当审批金额小于1万元时，不问原因直接由财务审批，财务审批后回调Java代码执行回调逻辑。
>
> 当审批金额大于等于1万元时，经由审批决策判断该审批申请是否通过。
>
> - 通过，由财务审批。
> - 不通过，回调Java代码，执行回调逻辑。

![image-20200323144237357.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0ML.png)

- 在

  ```
  财务审批
  ```

  节点添加变量

  ```
  passed
  ```

  供

  ```
  gateway
  ```

  节点使用。

  ![image-20200323145012578.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0MR.png)

- 配置

  ```
  审批决策
  ```

  节点

  ![image-20200324161208168.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE03O.png)

## 二、决策配置

- 新建一个决策配置页（DMN）。

  ![image-20200323145420417.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0ZR.png)

- 配置决策名和id。

  ![image-20200323145604266.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE0ZW.png)

- 配置决策内容。

  > 这里配置了两个输入项，一个返回项。
  >
  > - Role，角色 - 申请人角色
  > - UseFor，资金用处，这里定义了两种可以被通过的用处：文具，电脑。一种不能被通过的用处：食物。
  > - Passed，决策是否通过。

  ![image-20200323145701019.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00c.png)

  ![image-20200323145729452.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00k.png)

  最终决策配置。

  ![image-20200323150044366.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00l.png)

## 三、配置回调类

```
/**
 * 审批同意委托类
 */
public class AgreeDelegate implements JavaDelegate {
    @Override
    public void execute(DelegateExecution execution) throws Exception {
        System.out.println("审批【金额：" 
                           + execution.getVariablesLocal().get("amount") + "】已被同意。");
    }
}
/**
 * 审批拒绝委托类
 */
public class RejectDelegate implements JavaDelegate {
    @Override
    public void execute(DelegateExecution execution) throws Exception {
        System.out.println("审批【金额：" + execution.getVariables().get("amount")
                + ", 角色：" + execution.getVariables().get("role")
                + ", 资金方向：" + execution.getVariables().get("userFor") + "】已被拒绝。");
    }
}
```

## 四、测试

### 场景一：金额小于1万元，审核通过

![image-20200323150424215.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00q.png)

访问`http://localhost:8080/app/tasklist/default/#/`查看任务列表。

![image-20200323150524080.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00x.png)

可以看到流程已经到了`财务审批`节点。

点击页面上的`Form`table，将`passed`勾选上。

![image-20200323150649178.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00z.png)

点击`Complete`，查看系统日志。

![image-20200323150805802.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00A.png)

### 场景二：金额小于1万元，审核拒绝

访问`http://localhost:8080/app/tasklist/default/#/`，点击页面上的`Form`table，将`passed`勾选取消。

![image-20200323151252661.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00B.png)

### 场景三：金额大于1万元，决策拒绝

![image-20200323151424793.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00C-20210722015038322.png)

访问`http://localhost:8080/app/cockpit/default/#/decisions`查看决策列表。

![image-20200323151556889.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00D.png)

点击`Approve Decision`，查看决策详情。

![image-20200323151636467.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00P.png)

点击下方的`ID`，查看决策结果。

可以看到流程走到了编号为4的业务规则，下方的`Inputs`table中是我们启动流程实例时传入的决策变量值。
![image-20200323151728692.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE00U.png)

查看系统日志。
可以看到资金方向为`null`，所以系统获取到的`UseFor`是业务规则里配置的值。

![image-20200323151906940.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE000.png)

### 场景四：金额大于1万元，决策通过

![image-20200323152442288.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE007.png)

访问`http://localhost:8080/app/tasklist/default/#/`查看任务列表，可以看到任务已经到了`财务审批`节点。

![image-20200323152548364.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE009.png)
再次访问`http://localhost:8080/app/cockpit/default/#/decisions`查看决策详情。

可以看到这次走到了业务规则2，返回结果为`true`。

![image-20200323152858743.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE01g.png)

![image-20200323152830768.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE01k.png)
回到任务列表勾选`passed`。

![image-20200323153001375.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE01s.png)

查看系统日志。

![image-20200323153028502.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE01u.png)





# [Camunda流程引擎笔记(七)：自定义流程](https://segmentfault.com/a/1190000022137289)

[![img](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/150537686-5d0b224ef0acf_huge128-20210722015130097.jpeg)**悠然自得**](https://segmentfault.com/u/vulgar_cd)发布于 2020-03-25

> 之前的笔记中使用的流程功能都是基于
>
> ```
> Camunda
> ```
>
> 官方提供的内置功能，这里简单讲述一下使用
>
> ```
> Camunda
> ```
>
> 提供的API实现自定义流程。
>
> 实现自定义流程，那么我们就可以重新实现符合自己需求的流程前端页面，但是这里我们依然使用官方提供的前端页面，但是只是作为任务查看（当然也可不用，直接看json数据）。

这里还是使用上篇用到的审批流程图，然后我们使用官方提供的API实现`启动流程`、`审批流程`等功能。

![image-20200323160935084.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE06i.png)

## 一、修改流程图

将`财务审批`节点中的`Assignee`输入框中的值删除。

![image-20200323171958501.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE06v.png)

## 二、编写代码

### 1、启动流程实例

- service

```
@Autowired
private RuntimeService runtimeService;

/**
 * 开启流程实例
 *
 * @param amount 申请金额
 * @param role 角色
 * @param useFor 资金方向
 * @return java.lang.String
 */
 public String startProcess(long amount, String role, String useFor) {
    Map<String, Object> initialVariables = new HashMap<>(1);
    initialVariables.put("amount", amount);
    if (amount >= 10000) {
      initialVariables.put("role", role);
      initialVariables.put("useFor", useFor);
    }
    Execution execution = runtimeService.startProcessInstanceByKey("approve_process", initialVariables);
    return "实例启动成功，实例ID：" + execution.getProcessInstanceId();
  }
```

- controller

```
@ApiOperation("启动实例")
@PostMapping("/start")
public String startProcess(@RequestParam long amount,
                         @RequestParam(required = false) String role,
                         @RequestParam(required = false) String useFor) {
return processService.startProcess(amount, role, useFor);
}
```

### 2、任务认领

- service

```
@Autowired
private TaskService taskService;

/**
 * 任务认领
 *
 * @param processInstanceId 流程实例ID
 * @return java.lang.String
 */
 public String assignTask(String processInstanceId) {
    List<Task> tasks = taskService.createTaskQuery().processInstanceId(processInstanceId).active().list();
    if (!CollectionUtils.isEmpty(tasks)) {
      taskService.claim(tasks.get(0).getId(), "admin");
      return "任务认领成功，任务ID：" + tasks.get(0).getId() + "，认领人：admin";
    }
    return "无任务可认领";
  }
```

- controller

```
@ApiOperation("任务认领")
@PostMapping("/assign")
public String assignTask(@RequestParam String processInstanceId) {
return processService.assignTask(processInstanceId);
}
```

### 3、任务审核

- service

```
@Autowired
private TaskService taskService;

/**
* 任务审核
*
* @param taskId 任务ID
* @return java.lang.String
*/
public String approveTask(String taskId, boolean passed) {
List<Task> tasks = taskService.createTaskQuery().taskId(taskId).taskAssignee("admin").list();
if (!CollectionUtils.isEmpty(tasks)) {
  Map<String, Object> approveVariables = new HashMap<>(1);
  approveVariables.put("passed", passed);
  taskService.complete(taskId, approveVariables);
  return "任务审核完成，审核"
    + (passed ? "通过" : "拒绝");
}
return "无任务可审核";
}
```

- controller

```
@ApiOperation("任务审核")
@PostMapping("/approve")
public String approveTask(@RequestParam String taskId, @RequestParam boolean passed) {
return processService.approveTask(taskId, passed);
}
```

## 三、测试

### 1、金额小于1万元，审核通过

![image-20200323172841234.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE1h7.png)

访问`http://localhost:8080/app/cockpit/default/#/`查看流程详情。

可以看到这里的`Process Instances ID`与刚刚通过自定义API请求返回的实例ID是一致的。

![image-20200323173308607.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE1ie.png)

访问`http://localhost:8080/app/tasklist/default/#/`查看任务列表。

可以看到右上角显示该任务还未被认领，因为我们上面将`Assignee`的值置为了空，然后右下角的操作按钮是无法操作的。

![image-20200323173010049.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE1ij.png)

接下来认领任务。

将上面请求到的流程实例ID作为任务认领的参数。

![image-20200323173513757.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE1jm.png)

再次访问`http://localhost:8080/app/tasklist/default/#/`查看任务列表。

可以看到右上角已经显示该任务已被`admin`认领了，并且右下角的操作按钮也已经可以操作了。

![image-20200323173642490.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE1jp.png)

访问`http://localhost:8080/app/cockpit/default/#/`查看任务详情。

可以看到这里的任务ID和我们请求返回的任务ID是一致的。

最后审核任务。

将上面请求到的任务ID作为任务审核的参数。

![image-20200323174046101.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE1jW.png)

访问`http://localhost:8080/app/tasklist/default/#/`查看任务列表。

可以看到已经没有等待执行的任务了。

![image-20200323174130243.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24o.png)

再访问`http://localhost:8080/app/cockpit/default/#/`查看实例看板。

已经没有允许中的实例了。

![image-20200323174222632.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24r.png)

### 2、金额大于1万元，决策通过

![image-20200323174423101.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24J.png)

访问`http://localhost:8080/app/cockpit/default/#/`查看决策详情。

![image-20200323174517116.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24L.png)

![image-20200323174529108.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24M.png)

再访问`查看任务列表`。

可以看到又到了任务认领环节了。

![image-20200323174604380.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24O-20210722015136562.png)

![image-20200323174700963.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24Q.png)
最后任务审批。

![image-20200323174733402.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24S.png)

再一次访问`http://localhost:8080/app/cockpit/default/#/`查看实例看板。

![image-20200323174829910.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE24U.png)

已无运行中的流程实例。

更多信息访问[Camunda官网](https://link.segmentfault.com/?url=https%3A%2F%2Fdocs.camunda.org%2F)。





# [Camunda流程引擎笔记(八)：运行时发布流程](https://segmentfault.com/a/1190000022137547)

[![img](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/150537686-5d0b224ef0acf_huge128-20210722015218091.jpeg)**悠然自得**](https://segmentfault.com/u/vulgar_cd)发布于 2020-03-25

## 前言

可以看到前面我们所演示的示例都是经过了`绘制流程图` -> `将流程图复制到项目中` -> `打包应用` -> `运行应用` -> `使用流程`一系列流程。

其实，`Camnuda`流程引擎是从`Activiti`分裂而来，具体信息可以参考：

- [Camunda/Flowable/Activiti技术发展史](https://link.segmentfault.com/?url=https%3A%2F%2Fblog.csdn.net%2Fqq_30739519%2Farticle%2Fdetails%2F86583765%3Fdepth_1-utm_source%3Ddistribute.pc_relevant.none-task%26amp%3Butm_source%3Ddistribute.pc_relevant.none-task)
- [从Activiti分裂而来的camunda BPM](https://link.segmentfault.com/?url=http%3A%2F%2Fblog.sina.com.cn%2Fs%2Fblog_a19742b10101bkz1.html)

`Camunda BPM`轻巧且开发人员友好。

- Camunda BPM既可以用作独立的流程引擎服务器，也可以用在自定义Java应用程序中。
- Camunda BPM还提供REST API，以便非Java开发人员可以构建连接到远程流程引擎的应用程序。

这里主要演示一下`Camunda BPM`提供的REST API实现运行时发布流程定义。

## 一、启动应用

首先需要引入一个REST API的依赖。

```
<dependency>
  <groupId>org.camunda.bpm.springboot</groupId>
  <artifactId>camunda-bpm-spring-boot-starter-rest</artifactId>
  <version>3.4.1</version>
</dependency>
```

![image-20200324101205163.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE25H.png)

可以看到这里初始化了4个流程，这4个流程都是应用中绑定的流程定义。

访问`http://localhost:8080/app/cockpit/default/#/processes`查看流程看板。

![image-20200324101453250.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE25K.png)

正如上面所说，这里也只有绑定在应用中的4个流程。

## 二、绘制流程

接下来，使用`Camunda modeler`绘制一个简单的流程图。

![image-20200324101545433.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE25P.png)

然后点击工具栏的发布按钮。

可以看到提示我们已经连上了服务器，并通过`http://localhost:8080/rest`接口发布我们新定义的流程。

![image-20200324101630805.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE25S.png)

最后点击`Deploy`。

提示发布成功。

![image-20200324101740979.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE25V.png)

再回到`http://localhost:8080/app/cockpit/default/#/processes`查看流程看板。

![image-20200324101831558.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE253.png)

![image.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE29f.png)

管理端已经可以看到我们刚发布的流程定义了。

## 三、测试

接下来，简单启动一个流程实例。

![image-20200324102003161.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE26H.png)

![image-20200324102021343.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE26N.png)

![image-20200324102031183.png](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/bVbE26U.png)

最后可以发现，该流程是可以正常使用的，和应用中绑定的流程并无区别，当使用`MySql`等数据库时，运行时发布的流程会直接存库，所以再次重启应用时，不用担心运行时发布的流程消失。

这样开发人员就可以更专注于业务逻辑开发，而业务流程控制则可以交给更专业的产品来绘制流程图。

## 四、总结

`Camunda BPM`流程引擎笔记到此告一段落，流程引擎作为一门学科，不是几篇笔记就说的清楚的，更多信息访问[Camunda官网](https://link.segmentfault.com/?url=https%3A%2F%2Fdocs.camunda.org%2F)。

