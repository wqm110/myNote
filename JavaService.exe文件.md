## 下载JavaService.exe文件

下载地址:http://pan.baidu.com/s/1boWk1uJ（支持Windows 7 64位）

 

## 创建server文件目录

在D盘新建一个文件夹如：D:\server

将要发布的jar文件和JavaService.exe拷贝到新建的server目录下面

 

## 安装服务

1 用cmd命令进到server文件目录里

2 执行如下命令

```
./JavaService.exe -install TESTSERVER "%JAVA_HOME%/jre/bin/server/jvm.dll" -Djava.class.path="%JAVA_HOME%/lib/tools.jar;c:/service/oa.jar" -Xms500m -Xmx500m -start com.ruoyi.RuoYiApplication  -out "c:/service/out.log" -err "c:/service/err.log"
```

3 安装成功后，显示如下信息

```
The TESTSERVER automatic service was successfully installed　　
```

4 启动服务

```
net start TESTSERVER
```

也可以在Windows服务里启动服务

![img](https://i.loli.net/2021/06/29/YaOe3C5qgjVhXRL.jpg)　 

5 停止服务

```
net stop TESTSERVER
```

 

## 卸载服务

执行如下命令

```
./JavaService.exe -uninstall TESTSERVER 
```

还可以使用如下命令

```
sc delete TESTSERVER
```

卸载成功后，显示如下信息

```
Successfully uninstalled service TESTSERVER
```

也可以看到此时Windows服务里TESTSERVER服务已卸载。　

　