# Big sur提示您没有权限来打开应用程序的解决办法

您当前位置：[上海润满计算机科技有限公司](http://www.runman.cn/) >> [IT 外包](http://www.runman.cn/it/) >> [知识库](http://www.runman.cn/IT/zsk/) >> [苹果专栏(Mac)](http://www.runman.cn/IT/zsk/apple/) >> 浏览文章

Big sur提示您没有权限来打开应用程序的解决办法

**时间 /** 2021年02月18日 **信息来源 /** 本站原创 **作者 /** 上海 IT 外包 **点击 /** *267*次

 

 

升级到最新的macOS Big Sur后，有一些软件会出现无法打开的情况，比如autocad的激活工具xf-adsk20.app等，会弹出提示：您没有权限来打开应用程序“XXX”。 别着急，安装upx即可解决Big Sur系统提示没有权限的问题。 具体操作步骤如下： 1、下载upx权限修复工具： 链接: https://pan.baidu.com/s/104kHJmsRehxyhB7zqWYtTQ 密码: n5m7 拖入右键应用程序目录进行安装。 2、将打不开的软件拖到应用程序目录，例如x-force，在软件图标上右键，选择“显示包内容”，进入 Contents - MacOS 目录； 3、打开终端，拷贝命令：sudo /Applications/upx -d （注意最后有一个空格）粘贴到终端，然后将第2步的MacOS目录内的图标拖到终端，得到类似命令：sudo /Applications/upx -d /Applications/xf-adsk20.app/Contents/MacOS/x-force，然后按回车键，提示输入密码，这里输入密码不显示，输完密码直接按回车键，返回提示“Unpacked 1 file.”即操作成功。 这时候软件应该可以正常打开了：

