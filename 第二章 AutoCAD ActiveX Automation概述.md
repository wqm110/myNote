第二章 AutoCAD ActiveX Automation概述

李济雄 2020-10-09 15:53:38  707  收藏 7
分类专栏： python for AutoCAD
版权

python for AutoCAD
专栏收录该内容
9 篇文章5 订阅
订阅专栏
AutoCAD的ActiveX自动操作的英文全称是AutoCAD ActiveX Automation，ActiveX是微软制定的一种实现程序间通信、调用的软件复用规范，它提供了一种控制AutoCAD的机制。
Automation技术允许一个应用程序操纵在另一个应用程序中实现的对象。从而可以被操纵。操纵程序被称为客户，而被操纵程序称为服务器，被操纵的对象是ActiveX对象

什么是AutoCAD ActiveX
AutoCAD ActiveX，即是AutoCAD ActiveX Automation，提供了一种程序化的机制来操纵AutoCAD，这种操作既可以是在AutoCAD内部，也可以是来自AutoCAD外部的。因此，当提及AutoCAD ActiveX的时候，不是一种特定的语言，而是一种方法，一种操作。

![image-20210726003048252](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210726003048252.png)

执行一个AutoCAD ActiveX接口有两个优点：

程序化地访问AutoCAD图形，对于更多的编程环境是开放的，在ActiveX自动化之前，不受开发语言的限制；
与其他Windows应用程序共享数据，变得非常简单；
AutoCAD ActiveX Automation
AutoCAD ActiveX基本特点
AutoCAD的二次开发途径主要有两个

文件开发
文件开发是指根据用户的具体开发需要，按照AutoCAD提供的方法和文件格式，通过编辑AutoCAD系统所支持的文本文件，或建立同种类型新的文本文件，来开发AutoCAD；
程序开发
AutoCAD API，通过编写程序来实现对AutoCAD开发的方法；
AutoCAD ActiveX命令
命令的用户化
程序参数文件（ACAD.PGP）的结构与功能。AutoCAD程序参数文件（ACAD.PGP）是一个文本文件，用于存放AutoCAD定义的命令。这个文件分为两个部分：

第一部分定义外部命令；
第二部分定义命令别名；

![image-20210726003104512](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210726003104512.png)

“;”引导注释；

![image-20210726003124991](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210726003124991.png)



在ACAD.PGP中定义AutoCAD的外部命令

外部命令的具体格式：


定义命令别名和缩写
命令别名向的定义格式如下：

![image-20210726003138809](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210726003138809.png)

AutoCAD ActiveX AutoMation开发技术基础
一个应用程序支持的对象、方法和属性通常在应用的类型库中定义。类型库是一个文件或文件的一部分，它描述一个或多个对象，但不存储对象，而是存储对象的接口描述。
AutoCAD的所有对象组成一个层状结构。最高层是Application对象，其他对象都是Application对象的子类。为了得到一个特定的对象，必须从Application对象对子对象遍历，直到找到该特定的对象。在AutoCAD ActiveX界面中有许多不同类型的对象：

图形对象，如线、弧、文本和标注都是对象；
样式设置，如线性和标注样式均为对象；
组织结构，如图层、组合和图块也是对象；
图形显示，如视图和视口都是对象；
图形和AutoCAD应用程序本身也是对象；

![image-20210726003249182](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210726003249182.png)

Application对象
Application对象，即应用程序对象，是AutoCAD ActiveX自动操作对象模型的根对象。Application对象也有许多属性和方法：



ActiveDocument属性，返回当前AutoCAD正在进行编辑的图形；
Preferences属性，返回Preferences对象，用于AutoCAD的设置；



![image-20210726003310108](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210726003310108.png)

Document对象
Document对象，即文档对象，是AutoCAD当前编辑的图形，它可以存取所有的AutoCAD图形与非图形对象。ModelSpace和PaperSpace属性可存取图形对象，而非图形对象可以通过DimStyles、Layers、LineTypes、TestStyles、ViewPorts和Views等存取。

![image-20210726003323111](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210726003323111.png)


Collection对象
AutoCAD组合大部分的对象在集合中，尽管这些集合包含不同类型的数据；

图形对象和非图形对象
图形对象
也被称为实体，是图形的可见对象。可以使用ModelSpace和PaperSpace的Add[EntityName]方法产生一个新的图形对象，如AddLine。图形对象的编辑可以通过图形对象自身的方法实现，如Offset、Copy等；
非图形对象
非图形对象是指图形中的不可见对象，包括DimStyles、Layers、LineTypes、TestStyles、ViewPorts和Views和SelectionSet等。
Preferences、Plot和Utility对象
参数选择：Preferences
打印出图：Plot
实用工具：Utility



![image-20210726003346141](https://pic-wqm.oss-cn-beijing.aliyuncs.com/uPic/image-20210726003346141.png)


访问对象层次
使用python访问AutoCAD的内部对象时，需要通过对应用程序的链接；

import win32com.client
AcadApp = win32com.client.Dispatch("AutoCAD.Application.19")
1
上面的代码就创建了外部程序与AutoCAD的链接，在链接到AutoCAD的应用程序之后，返回一个Application对象，可以通过下面的这行代码指向AutoCAD中的活动文档；

ActiveDocument = AcadApp.ActiveDocument
如果我们想要在模型空间绘制一个实体，则需要获得AutoCAD的模型空间；

ModelSpace = ActiveDocument.ModelSpace
下面我们实现在模型空间中绘制一条直线：

import win32com.client
AcadApp = win32com.client.Dispatch("AutoCAD.Application.19")
ActiveDocument = AcadApp.ActiveDocument
ModelSpace = ActiveDocument.ModelSpace

line = ModelSpace.AddLine(startpoint, endpoint)

```shell
import win32com.client
AcadApp = win32com.client.Dispatch("AutoCAD.Application.19")
ActiveDocument = AcadApp.ActiveDocument
ModelSpace = ActiveDocument.ModelSpace

line = ModelSpace.AddLine(startpoint, endpoint)
```

上面的这段代码展示了一个应用层次：
Application>>>ActiveDocument>>>ModelSpace>>>AddLine

|      |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |

集合对象操作
|   名称   |   含义   |
| ---- | ---- | 
|      |      | 
| 文档  （Documents）|  集合	包含所有在当前AutoCAD进程打开的文档
|模型空间（ModelSpace）| 集合	包含在模型空间中的所有图形对象（图元）
|图纸空间（PaperSpace）| 集合	包含在活动图纸空间布局中的所有图形对象（图元）
|图块（Block）|集合	包含在指定图块定义中的所有图元
|图块（Blocks）|集合	包含在图形中的所有图块
|字典（Dictionaries）|集合	包含在图形中的所有字典
|标注样式（DimStyles）|集合	包含在图形中的所有标注样式
|组合（Groups）|集合	包含在图形中的所有组合
|超级链接（Hyperlinks）|集合	包含提供图元的所有超级链接
|图层（Layers）|集合	包含在图形中的所有图层
|布局（Layouts）|集合	包含在图形中的所有布局
|线型（LineTypes）|集合	包含在图形中的所有线型
|菜单条（MenuBar）|集合	包含当前显示于AutoCAD的所有菜单
|菜单组（MenuGroups）|集合	包含当前装载到AutoCAD中的所有菜单和工具拦
|注册应用程序（RegisteredApplication）|集合	包含在图形中的所有注册的应用程序
|选择集（SelectionSets）|集合	包含在图形中的所有选择集
|字型（TextStyles）|集合	包含在图形中的所有文字样式
|UCSs集合	|包含在图形中的所有用户坐标系统（UCS）
|视图（Views）|集合	包含在图形中所有的视图
|视口（Viewports）|集合	包含在图形中的所有视口
|访问集合
大多数集合对象是通过文档对象来访问的。文档对象包含每个集合对象的属性。下面以创建一个图层集合为例

import win32com.client
AcadApp = win32com.client.Dispatch("AutoCAD.Application.19")
ActiveDocument = AcadApp.ActiveDocument
layer = ActiveDocument.Layers
1
2
3
上面代码获得了当前的图层集合，并将图层集合命名为“layer”，我们想要在图层集合中，添加一个新的图层，需要使用Add方法：

new_layer = layer.Add("HIT_Layer")
在集合对象中循环
选择集合对象中的一个指定成员，使用Item（项目）方法。Item方法需要一个标识符。

删除集合对象中的成员
删除指定的成员，可使用所找到成员对象的Delete方法。

acad.ActiveDocument.SelectionSets.Item("SS1").Delete()
————————————————
版权声明：本文为CSDN博主「李济雄」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_43496130/article/details/108973656