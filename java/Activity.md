# Activity



**知识基础：**

> activiti是以BPMN规范为基础的，所以需要了解BPMN的基础知识，这里只作简单介绍。

> bpmn通过流程图和用户交互，用工作流自己的表来维护流程数据，其中activiti是28张表，以act_开头，act_hi_是历史记录类表、act_ru_是运行时流程数据维护表。

**BPMN基本对象：**

- 事件event： 代表开始和结束，流程图表示为圆

- 活动Task（activity）：代表处理活动的角色，流程图是一个矩形

- 网关gateway：代表角色的处理选择，决定流程走向，流程图是一个菱形

- 流向flow：代表流程图走向，流程图是一个单方向的箭头线

**活动任务 Task：**

- userTask 人机交互任务，必须有人参与操作的任务

- ServiceTask Task服务任务，机器自动化

- SendTask 发送任务，类似于ServiceTask

- ReceiveTask 状态任务，一般用户表示活动状态，需要singal进行流转

- ManualTask 线下手工执行任务

- BusinessRuleTask 业务规则任务

- ScriptTask 脚本任务

- AbstractTask 抽象任务

**网关 Gateways：**

- parallel Gateway 并行网关 菱形中一个加号，不会解析条件

- Exclusive Gateway 排他网关 菱形或者菱形中一个乘号

- Inclusive Gateway 包容网关 菱形中一个圆，走完所有符合条件的flow



工作流基本表



|         表名          | 概要                     |                         接口 | 作用                             |
| :-------------------: | ------------------------ | ---------------------------: | -------------------------------- |
|   act_ge_bytearray    | 通用----数组             |                              |                                  |
|    act_ge_property    | 通用数据表，参数         |                              |                                  |
|    act_hi_actinst     | 历史----流实例           |               HistoryService |                                  |
|   act_hi_attachment   | 历史----附件             |                              |                                  |
|    act_hi_comment     | 历史----备注             |                              |                                  |
|     act_hi_detail     | 历史----详情             |                              |                                  |
|  act_hi_identitylink  | 历史 ----唯一链接        |                              |                                  |
|    act_hi_procinst    | 历史----运行v信息        |                              |                                  |
|    act_hi_taskinst    | 历史----任务----实例     |                              |                                  |
|    act_hi_varinst     | 历史----变量----实例     |                              |                                  |
|     act_id_group      | 身份认证                 |              IdentityService |                                  |
|   act_procdef_info    | 处理 定义信息            |                              |                                  |
|   act_re_claiminfo    | 流程----请求表           |            RepositoryService | 存储流程部署和流程定义等静态数据 |
|   act_re_deployment   | 流程----部署             |                              |                                  |
|     act_re_model      | 流程----模型             |                              |                                  |
|    act_re_procdef     | 流程----处理定义         |                              |                                  |
| act_ru_deadletter_job | 运行----死信---- 任务    | RuntimeService、 TaskService | 存储流程实例和用户任务等动态数据 |
|  act_ru_event_subscr  | 运行 ----事件 ----子任务 |                              |                                  |
|   act_ru_execution    | 运行 ----执行            |                              |                                  |
|  act_ru_identitylink  | 运行 ----唯一链接        |                              | 主要存储任务节点与参与者相关信息 |
|      act_ru_job       | 运行----任务             |                              |                                  |
| act_ru_suspended_job  | 运行----暂停----任务     |                              |                                  |
|      act_ru_task      | 运行----任务             |                              |                                  |
|   act_ru_timer_job    | 运行----定时任务         |                              |                                  |
|    act_ru_variable    | 运行----变量             |                              |                                  |
|      act_evt_log      |                          |                              |                                  |



![img](https://tva1.sinaimg.cn/large/008eGmZEly1gmwr0f8gnsj30fe06g0t5.jpg)

核心接口

**（一）7大接口**

| 接口              | 功能描述                                                     |      |
| ----------------- | ------------------------------------------------------------ | ---- |
| RuntimeService    | 在流程运行时对流程实例进行管理与控制。                       |      |
| RepositoryService | 提供一系列管理流程部署和流程定义的API。                      |      |
| TaskService       | 对流程任务进行管理，例如任务提醒、任务完成和创建任务等。     |      |
| IdentityService   | 提供对流程角色数据进行管理的API，这些角色数据包括用户组、用户及它们之间的关系。 |      |
| ManagementService | 提供对流程引擎进行管理和维护的服务。                         |      |
| HistoryService    | 对流程的历史数据进行操作，包括查询、删除这些历史数据。       |      |
| FormService       | 表单服务。                                                   |      |

 







Act-get-properties 表不能为空

 



若依数据流



定义模型

![image-20210122193930026](https://tva1.sinaimg.cn/large/008eGmZEly1gmwph7l3zbj325s074q4y.jpg)

新增

![image-20210122194444764](https://tva1.sinaimg.cn/large/008eGmZEly1gmwpmmin50j30lw0gmgmm.jpg)





![image-20210122194513775](https://tva1.sinaimg.cn/large/008eGmZEly1gmwpn4mjbxj30ig03oq2x.jpg)

![image-20210122194533974](https://tva1.sinaimg.cn/large/008eGmZEly1gmwpnhg0llj31kq07i75t.jpg)



各种节点的属性 ==*//TODO*==







# Activiti 实战



![image-20210124194632835](https://tva1.sinaimg.cn/large/008eGmZEgy1gmz0x7zy70j30u00xjnkf.jpg)







![image-20210124200752554](https://tva1.sinaimg.cn/large/008eGmZEgy1gmz1jbq263j312a0potnx.jpg)



![image-20210124200828772](https://tva1.sinaimg.cn/large/008eGmZEgy1gmz1jyat9dj31000i2amr.jpg)





![image-20210124224530499](https://tva1.sinaimg.cn/large/008eGmZEgy1gmz63dxwxmj31840tondx.jpg)

