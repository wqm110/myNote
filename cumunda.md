# cumunda 学习笔记

## cumunda rest api

1. 教程地址[bili](https://www.bilibili.com/video/BV1yo4y1C7yP/)
2. 服务器地址 111.231.141.151:80

+ 使用moduleer 绘制流程图
+ 下载postman

### 使用postman部署流程

- docs.cumunda.org->reference[链接](https://docs.camunda.org/manual/7.7/reference/rest/deployment/)

![image-20210622002853895](https://i.loli.net/2021/06/22/m2E4gTxU8IqjJX9.png)

```
/deployment/create
```

![image-20210622003622010](https://i.loli.net/2021/06/22/9uVW4cGjlJgOMQw.png)

![image-20210622003857658](https://i.loli.net/2021/06/22/85wXg3bDqEpfFv9.png)

点击send

![image-20210622004215998](https://i.loli.net/2021/06/22/1YqSVvDlXrCFM3R.png)

去控制面板[查看结果](http://111.231.141.151/camunda/app/cockpit/default/#/dashboard)

![image-20210622004609147](https://i.loli.net/2021/06/22/6dMgnqPbCLGr8Bt.png)

![image-20210622004647980](https://i.loli.net/2021/06/22/S8tU4kRbrV9JOmv.png)

![image-20210622004727142](https://i.loli.net/2021/06/22/RNUvJpQjOe8bYnL.png)

### 启动流程

![image-20210622005041611](https://i.loli.net/2021/06/22/SYp9z14srQ2UdHK.png)

参数样例：

```json
{"variables":
    {"aVariable" : {"value" : "aStringValue", "type": "String"},
     "anotherVariable" : {"value" : true, "type": "Boolean"}},
     "businessKey" : "myBusinessKey"
    }
```

​	两种启动方式

```http
POST /process-definition/aProcessDefinitionId/start

POST /process-definition/key/aProcessDefinitionKey/start
```

样例

```jso
{"variables":
    {"aProcessVariable" : {"value" : "aStringValue", "type": "String"}},
      "businessKey" : "myBusinessKey",
"skipCustomListeners" : true,
"startInstructions" :
  [
  {
    "type": "startBeforeActivity",
    "activityId": "activityId",
    "variables":
      {"var": {
        "value": "aVariableValue",
        "local": false,
        "type": "String"}
      }
  },
  {
    "type": "startAfterActivity",
    "activityId": "anotherActivityId",
    "variables":
      {"varLocal": {
        "value": "anotherVariableValue",
        "local": true,
        "type": "String"}
      }
  }]
      }
```

设置路径及请求头

![image-20210622005926745](https://i.loli.net/2021/06/22/EWXuoh9ai2yTeqb.png)

![image-20210622010051105](https://i.loli.net/2021/06/22/LfbYVMFQ6KHBmst.png)

