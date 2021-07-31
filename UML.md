

# UML

## 概述

![image-20201229204711721](https://tva1.sinaimg.cn/large/0081Kckwgy1gm50kg1fk7j31130lhati.jpg)



案例![image-20201229204759060](https://tva1.sinaimg.cn/large/0081Kckwgy1gm50lel7lnj312h0nyqla.jpg)

用例：怎么用怎么交互

领域模型：业务模型 Component Diagram

![image-20201229205344842](https://tva1.sinaimg.cn/large/0081Kckwgy1gm50r5mjy5j311b0j2dl4.jpg)

 动态建模 Sequence Diagram

![image-20201229205726229](https://tva1.sinaimg.cn/large/0081Kckwgy1gm50uyuo1hj30wm0n3wo7.jpg)



![image-20201229204634478](https://tva1.sinaimg.cn/large/0081Kckwgy1gm50jscfhcj311c0gldnm.jpg)

### UML定义![image-20201229210256670](https://tva1.sinaimg.cn/large/0081Kckwgy1gm510puojgj311q0m6wqv.jpg)



![image-20201229211727975](https://tva1.sinaimg.cn/large/0081Kckwgy1gm51frrajyj30lm0bfgt5.jpg)



![image-20201229211815275](https://tva1.sinaimg.cn/large/0081Kckwgy1gm51gl7l6cj30lt0e8doc.jpg)



![image-20201229213302526](https://tva1.sinaimg.cn/large/0081Kckwgy1gm51w16mfgj30kk0d0af4.jpg)

> (1) 用例图(Use Case Diagram)，描述系统功能；

> (2) 类图(Class Diagram)，描述系统的静态结构；

> (3) 对象图(Object Diagram)，描述系统在某个时刻的静态结构；

> (4) 组件图(Component Diagram)，描述了实现系统的元素的组织；

> (5) 配置图(Deployment Diagram)，描述了环境元素的配置，并把实现系统的元素映射到配置上；

> (6) 状态图(State Diagram)，描述了系统元素的状态条件和响应；

> (7) 时序图(Sequence Diagram)，按时间顺序描述系统元素间的交互；

> (8) 协作图(Collaboration Diagram)，按照时间和空间顺序描述系统元素间的交互和它们之间的关系；

> (9) 活动图(Activity Diagram)，描述了系统元素的活动；

### 初步接触

#### 类图

![image-20201229220154021](https://tva1.sinaimg.cn/large/0081Kckwgy1gm52q03zu3j310j0pqwt5.jpg)

![image-20201229220610095](https://tva1.sinaimg.cn/large/0081Kckwgy1gm52uhpsz9j311g0na49e.jpg)

![image-20201229220843379](https://tva1.sinaimg.cn/large/0081Kckwgy1gm52x6kz5wj31040j2gwz.jpg)

![StarUML 类图](https://gblobscdn.gitbook.com/assets%2F-L9shwSMiocGHpSKcbss%2F-MICRkvtgCev38ZdEOzz%2F-MICXxhUZPR6Q1UWMdUN%2FClass Diagram!UML Property_6.png?alt=media&token=cc7829d2-8dac-45fa-a4c9-00745fd212f8)

##### 名词

composition：组合

multiplicity：多样性；多重性

Association：联合

aggregation：聚合

Qualifler：修饰语

Classifier：分类器

stereotype：模式化形象（图形样式）

Parameter：参数

alignment ：队列：线形：排列方式

Substitution：替换

##### 类图详细说明 

###### 基本操作

- **Visibility** : Change visibility property.

  可见性: 更改可见性属性。

- **Add Note** : Add a linked note.

  加注: 添加一个链接注释。

- **Add Constraint** : Add a constraint.

  添加约束: 添加约束。

- **Add Attribute** (`Ctrl+Enter`) : Add an attribute.

  添加属性(Ctrl + Enter) : 添加属性。

- **Add Operation** (`Ctrl+Shift+Enter`) : Add an operation.

  添加操作(Ctrl + Shift + Enter) : 添加操作。

- **Add Template Parameter** : Add a template parameter.

  添加模板参数: 添加模板参数。

- **Add Reception** : Add a reception.

  添加接待: 添加一个接待。

- **Add Sub-Class** : Add a sub-class.

  添加子类: 添加子类。

- **Add Super-Class** : Add a super class.

  添加超类: 添加一个超类。

- **Add Provided Interface** : Add a provided interface.

  添加提供的接口: 添加提供的接口。

- **Add Required Interface** : Add a required interface.

  添加必需的接口: 添加必需的接口。

- **Add Associated Class** : Add an associated class.

  添加关联类: 添加关联类。

- **Add Aggregated Class** : Add an aggregated class.

  添加聚合类: 添加聚合类。

- **Add Composited Class** : Add a composited class.

  添加组合类: 添加组合类。

- **Add Port** : Add a port.

  添加端口: 添加一个端口。

- **Add Part** : Add a part.

  添加部分: 添加一个部分。

###### 属性

- **Visibility** : Change visibility property.

  可见性: 更改可见性属性。

- **Add** (`Ctrl+Enter`) : Add one more attribute in the below.

  添加(Ctrl + Enter) : 在下面添加一个属性。

- **Delete** (`Ctrl+Delete`) : Delete the attribute

  Delete (Ctrl + Delete) : 删除属性

- **Move Up** (`Ctrl+Up`) : Move the attribute up.

  向上移动(Ctrl + Up) : 向上移动属性。

- **Move Down** (`Ctrl+Down`) : Move the attribute down.

  向下移动(Ctrl + Down) : 向下移动属性。

###### 操作

1. Select a Classifier.

   选择一个分类器。

2. Select **Model | Add | Operation** in Menu Bar or **Add | Operation** in Context Menu.

   在菜单栏中选择模型 | 添加 | 操作或在关联菜单中选择添加 | 操作。

   您可以使用 QuickEdit 进行操作，方法是在选定的 Operation 上双击或按 Enter 键。

   - **Operation Expression** : Edit Operation expression.

     操作表达式: 编辑操作表达式。

     *Syntax of Operation Expression*

     操作表达式的语法

     

     ```
     operation ::= [ '<<' stereotype `>>` ] [ visibility ] name [ '(' parameter-list ')' ] [ ':' return-type ]
     stereotype ::= (identifier)
     visibility ::= '+' | '#' | '-' | '~'
     name ::= (identifier)
     parameter-list ::= parameter [ ',' parameter ]*
     parameter ::= (identifier)
     return-type ::= (identifier)
     ```

   - 

**Visibility** : Change visibility property.

可见性: 更改可见性属性。

- **Add** (`Ctrl+Enter`) : Add one more operation in the below.

  添加(Ctrl + Enter) : 在下面添加一个操作。

- **Delete** (`Ctrl+Delete`) : Delete the operation

  Delete (Ctrl + Delete) : 删除操作

- **Move Up** (`Ctrl+Up`) : Move the operation up.

  向上(Ctrl + Up) : 向上移动操作。

- **Move Down** (`Ctrl+Down`) : Move the operation down.

  向下移动(Ctrl + Down) : 向下移动操作。

To add a Parameter, see [Parameter](https://docs.staruml.io/working-with-uml-diagrams/class-diagram#parameter).
###### 参数
To add a Parameter:

添加参数:

1. Select an Operation.

   选择一个操作。

2. Select **Model | Add | Parameter** in Menu Bar or **Add | Parameter** in Context Menu.

   在菜单栏中选择模型 | 添加 | 参数或在关联菜单中选择添加 | 参数。

###### 模板参数

To add a Template Parameter:

添加模板参数:

1. Select an Element.

   选择一个元素。

2. Select **Model | Add | Template Parameter** in Menu Bar or **Add | Template Parameter** in Context Menu.

   在菜单栏中选择模型 | 添加 | 模板参数或在上下文菜单中选择添加 | 模板参数。

You can use **QuickEdit** for Template Parameter by double-click or press `Enter` on a selected Template Parameter.

您可以使用 QuickEdit 作为模板参数，方法是双击或按下所选模板参数的回车键。

- **Template Parameter Expression** : Edit Template Parameter expression.

  模板参数表达式: 编辑模板参数表达式。

  *Syntax of Template Parameter Expression*

  模板参数表达式的语法

  

  ```
  template-parameter ::= [ '<<' stereotype `>>` ] [ visibility ] name [':' type ] [ '=' defaut-value ]
  stereotype ::= (identifier)
  visibility ::= '+' | '#' | '-' | '~'
  name ::= (identifier)
  type ::= (identifier)
  default-value ::= (string)
  ```

- **Visibility** : Change visibility property.

  可见性: 更改可见性属性。

- **Add** (`Ctrl+Enter`) : Add one more template parameter in the below.

  添加(Ctrl + Enter) : 在下面添加一个模板参数。

- **Delete** (`Ctrl+Delete`) : Delete the template parameter.

  Delete (Ctrl + Delete) : 删除模板参数。

- **Move Up** (`Ctrl+Up`) : Move the template parameter up.

  向上移动(Ctrl + Up) : 向上移动模板参数。

- **Move Down** (`Ctrl+Down`) : Move the template parameter down.

  向下移动(Ctrl + Down) : 向下移动模板参数。

####  接口

To create an Interface:

创建一个界面:

1. Select **Interface** in **Toolbox**.

   在“工具箱”中选择“接口”。

2. Drag on the diagram as the size of Interface.

   拖到图表上，显示为接口的大小。

To create an Interface (model element only) by Menu:

通过 Menu 创建一个接口(仅限于模型元素) :

1. Select an Element where a new Interface to be contained.

   选择要包含新接口的元素。

2. Select **Model | Add | Interface** in Menu Bar or **Add | Interface** in Context Menu.

   在菜单栏中选择模型 | 添加 | 界面或在关联菜单中选择添加 | 界面。

You can use **QuickEdit** for Interface by double-click or press `Enter` on a selected Interface.

您可以通过在选定的接口上双击或按 Enter 键使用 QuickEdit for Interface。

- **Name Expression** : Edit name expression.

  名称表达式: 编辑名称表达式。

  *Syntax of Name Expression*

  名称表达式的语法

  

  ```
  expression ::= [ '<<' stereotype `>>` ] [ visibility ] name
  stereotype ::= (identifier)
  visibility ::= '+' | '#' | '-' | '~'
  name ::= (identifier)
  ```

- **Visibility** : Change visibility property.

  可见性: 更改可见性属性。

- **Add Note** : Add a linked note.

  加注: 添加一个链接注释。

- **Add Constraint** : Add a constraint.

  添加约束: 添加约束。

- **Add Attribute** (`Ctrl+Enter`) : Add an attribute.

  添加属性(Ctrl + Enter) : 添加属性。

- **Add Operation** (`Ctrl+Shift+Enter`) : Add an operation.

  添加操作(Ctrl + Shift + Enter) : 添加操作。

- **Add Reception** : Add a reception.

  添加接待: 添加一个接待。

- **Add Sub-Interface** : Add a sub-interface.

  添加子接口: 添加子接口。

- **Add Super-Interface** : Add a super interface.

  添加超级界面: 添加一个超级界面。

- **Add Realizing Class** : Add an realizing class.

  添加实现类: 添加一个实现类。

To show an Interface as Lollipop notation, Interface should be realized (See [Interface Realization](https://docs.staruml.io/working-with-uml-diagrams/class-diagram#interface-realization)) and then change Stereotype Display to Icon or Icon with Label (See [Stereotype Display](https://docs.staruml.io/user-guide/formatting-diagram#stereotype-display)).

要将一个接口显示为棒棒糖符号，接口应该被实现(参见接口实现) ，然后将 Stereotype Display 更改为带有标签的图标或图标(参见 Stereotype Display)。

To show an Interface as Socket notation, Interface should have dependants (See [Dependency](https://docs.staruml.io/working-with-uml-diagrams/class-diagram#dependency)) and then change Stereotype Display to Icon or Icon with Label (See [Stereotype Display](https://docs.staruml.io/user-guide/formatting-diagram#stereotype-display)).

为了显示一个作为 Socket 符号的接口，接口应该有受抚养人(见依赖项) ，然后改变 Stereotype 显示为图标或带有标签的图标(见 Stereotype 显示)。

To suppress Attributes, see [Suppress Attributes](https://docs.staruml.io/user-guide/formatting-diagram#suppress-attributes).

若要取消属性，请参见取消属性。

To suppress Operations, see [Suppress Operations](https://docs.staruml.io/user-guide/formatting-diagram#suppress-operations).

若要取消“操作”，请参阅取消“操作”。

To suppress Receptions, see [Suppress Receptions](https://docs.staruml.io/user-guide/formatting-diagram#suppress-receptions).

要抑制接受，请参阅抑制接受。

To show or hide Operation Signatures, see [Show Operation Signature](https://docs.staruml.io/user-guide/formatting-diagram#show-operation-signature).

若要显示或隐藏操作签名，请参阅显示操作签名。



![image-20201229223602902](https://tva1.sinaimg.cn/large/0081Kckwgy1gm53pieuvwj30s40q6mz2.jpg)

#### 依赖：（使用的别人） 

一个事物的变化会影响到另外一个

![image-20201229223545912](https://tva1.sinaimg.cn/large/0081Kckwgy1gm53p7vm81j30o20et0zb.jpg)



![image-20201229223617711](https://tva1.sinaimg.cn/large/0081Kckwgy1gm53prtvtjj30zl0n3qfx.jpg)

#### 关联  

![image-20201229232755249](https://tva1.sinaimg.cn/large/0081Kckwgy1gm557htx1zj30mn0eg10z.jpg)

引用

##### 导航

![image-20201230001940238](https://tva1.sinaimg.cn/large/0081Kckwgy1gm56pc3mesj30gw0ej41q.jpg)



导航性

多重性

# ![image-20210505222541916](https://i.loli.net/2021/05/05/e3pLRXAmD6w7n4T.png)

##### 聚合和组合

![image-20201230003241115](https://tva1.sinaimg.cn/large/0081Kckwgy1gm572vo3mfj30h40b7mza.jpg)









![image-20201230005031360](https://tva1.sinaimg.cn/large/0081Kckwgy1gm58v2vr0jj30my0g910m.jpg)

![image-20201230012439534](https://tva1.sinaimg.cn/large/0081Kckwgy1gm58kwxt75j30l80a8tcu.jpg)

![image-20201230013416503](https://tva1.sinaimg.cn/large/0081Kckwgy1gm58uxyz92j30hk0ca0uh.jpg)

![image-20201230013503875](https://tva1.sinaimg.cn/large/0081Kckwgy1gm58vqpd76j30me0d3jwq.jpg)

![image-20201230022428276](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5ab5dnojj30me0cwqaj.jpg)



![image-20201230054508823](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5g3yfaauj31700u0jx5.jpg)



![image-20201230054727131](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5g6d1bl5j30pl0i8n5r.jpg)

#### 用例图

![image-20201230055153069](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5gayo1eej30ec0d4n01.jpg)

#### 用例 use case（文本）



![image-20201230055047205](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5g9u23f1j30mo0dhdp7.jpg)

![image-20201230061229427](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5gwer24nj30n90frn4t.jpg)

![image-20201230061552993](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5gzxq6acj30o70gijvs.jpg)

![image-20201230061621018](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5h0evmd9j30pa0jjgsz.jpg)

![image-20201230062146806](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5h62lypej30ml0e97b8.jpg)

![image-20201230063149741](https://tva1.sinaimg.cn/large/0081Kckwgy1gm5hgj7urxj30n20bvdor.jpg)