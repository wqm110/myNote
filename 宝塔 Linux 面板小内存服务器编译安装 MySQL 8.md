# 宝塔 Linux 面板小内存服务器编译安装 MySQL 8

2019-01-02 

 4119 

 [运维笔记](https://docs.euyyue.com/category/note/)

宝塔面板在编译安装 MySQL 8 时，要求 3700M 内存，如果内存不足，我们可以选择极速安装，或者，如果一定要自己编译的话，可以使用命令行来跳过配置检测。

实际上，MySQL 8 编译过程中，需要 6G 以上的内存。如果我们的内存实在不够，可以创建 swap 虚拟内存。

以一台 2G 内存的服务器为例，我们新增 4G 的 swap，安装 Linux 工具箱，设置 swap 虚拟内存，输入

```
4096
```

点击确定。

如果设置 swap 以后，数据盘空间过小，那 Linux 工具箱目前并不适合我们。把上面的数字改回0，然后手动设置 swap 到系统盘：

```
fallocate -l 4G /swap
chown root:root /swap 
chmod 0600 /swap
mkswap /swap
swapon /swap
echo '/swap    swap    swap    defaults    0 0' >> /etc/fstab
```

查看一下 swap 是否开启成功：

```
swapon -s

Filename                                Type            Size    Used    Priority
/swap                                   file    4194300 9480    -2
```

现在内存应该够了，我们还要检查一下，/www 所在的磁盘够不够。编译 MySQL 8 占用的空间巨大，需要约 13G。如果不够，把不需要的文件删一下，或者扩容磁盘，这里不赘述。

检查一下各路径的大小：

```
df -h

Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        858M     0  858M   0% /dev
tmpfs           868M  588K  867M   1% /dev/shm
tmpfs           868M  576K  867M   1% /run
tmpfs           868M     0  868M   0% /sys/fs/cgroup
/dev/vda1        20G  7.5G   12G  41% /
/dev/vdb1        20G  4.4G   15G  22% /www
tmpfs           174M     0  174M   0% /run/user/1003
tmpfs           174M     0  174M   0% /run/user/0
```

这回肯定够用了。如果不够的话建议先清理磁盘，推荐安装系统后首先编译 MySQL 8，待完成后再编译其他软件 。

由于服务器配置较低，编译过程耗时可能超过 2 小时。在 CentOS 8 系统中，耗时超过 4 小时。为了防止意外断网停止编译，建议使用宝塔终端安装。

运行以下命令，编译安装 MySQL 8.0：

```
cd /www/server/panel/install
rm -rf mysql.sh
wget http://download.bt.cn/install/0/mysql.sh
bash mysql.sh install 8.0
```

以后有新版本时，更新命令也是类似的，只要把最后一句改为

```
bash mysql.sh update 8.0
```

注意：编译到 67% 和 75% 的时候，会卡在 Linking CXX executable 这个地方，假死好一会儿，原因是 ld.gold 占用了全部内存。编译完成后，安装过程中会将文件从 src 目录复制到上层目录，会多占用一半空间。在编译完成之前尽量清理磁盘空间，务必把数据盘空间留足。

------

写在最后：

编译安装非常费时费力，但是宝塔现在的极速安装包更新不及时，且有一些比较影响使用的问题。因此暂时还是只能推荐编译。Linux 原本就有非常完善的软件包管理方式，如果以后宝塔能够建立自己的软件安装源，参考成熟的软件源打包分发，那么就可以推荐使用极速安装了。

国内建立安装源的面板，也是有的，比如 AppNode，据称其软件源参考了 Remi。但 AppNode 是一个跟 AMH 类似的，模块中心化的面板，并且，免费版只能建立 3 个站点，且不支持子站。这就注定了 AppNode 不适用于大多数“暂时不赚钱”的站长。而宝塔是不从这些站长身上赚钱的，因此这种盈利模式可以算是“业界良心”。