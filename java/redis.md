# redis

### 基本命令

```
Redis-bechmark   //性能测试
```

```
set							
```

```
get      
```

```
select 0 //库
```

```
Redis-cli //登录客户端
```

```
dbsize //数据库大小
```

```
keys *  //查询所有键
```

```
FLUSHDB  //清库
```

![image-20210101050511826](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7q701xr3j30z80afgpr.jpg)

![image-20210101050557155](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7q7scfcfj30sp09ngo4.jpg)

![image-20210101050934646](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7qbklfqlj313o05rzmd.jpg)

![image-20210101051008206](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7qc59s22j30ow04xq41.jpg)

![image-20210101051050157](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7qcvzzpqj3105071gp6.jpg)

<http://redisdoc.com/>

### 常用key

```
SET +key 
```

```
GET +key
```

```
EXISTS +key 判断是否存在
```

```
MOVE +key +db
```

```
TTL +key      //还剩多少时间过去 -1 永久 -2 不存在(移除了)
```

```
DEL +key
```

```
EXPIRE +key +seconds  //设置过期时间
```

```
TYPE +key           //查看key的数据类型
```

```
LPUSH
```

```
RPUSH
```

```
LRANGE +key +start +end
```

## 基本数据类型

### ￼￼String 

* set/get/del/append/strlen

* Incr/decr/incrby/decrby,一定要是数字才能进行加减

* getrange/setrange

* setex(set with expire)键秒值/      setnx(set if not exist)

* mset/mget/msetnx                //多个 有一个失败 全部失败

* getset(先get再set)

  ![image-20210101055302713](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7rkshdraj30qy0s2do6.jpg)

### LIst

![image-20210101053844130](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7r5wtzz8j30u40u0qe8.jpg)

LPUSH 正着进 反着出

RPUSH 正着进 正着出

 lpush/rpush/lrange

 lpop/rpop

 lindex，按照索引下标获得元素(从上到下)

 llen

 lrem key 删N个value

 ltrim key 开始index 结束index，截取指定范围的值后再赋值给key

 rpoplpush 源列表 目的列表

 lset key index value

 linsert key before/after 值1 值2

性能总结

> 它是一个字符串链表，left、right都可以插入添加； 
>
> 如果键不存在，创建新的链表； 
>
> 如果键已存在，新增内容； 
>
> 如果值全移除，对应的键也就消失了。 
>
> 链表的操作无论是头和尾效率都极高，但假如是对中间元素进行操作，效率就很惨淡了。 

### set

* sadd/smembers/sismember

* scard，获取集合里面的元素个数

*  srem key value 删除集合中元素

*  srandmember key 某个整数(随机出几个数)

* spop key 随机出栈

* move key1 key2 在key1里某个值   作用是将key1里的某个值赋给key2

* 数学集合类

  ​	差集：sdiff

  ​	交集：sinter

  ​	并集：sunion

![image-20210101061151298](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7s4d10uij30jk0s4wmc.jpg)

### HASH

![image-20210101061319750](https://tva1.sinaimg.cn/large/0081Kckwgy1gm7s5wimj8j30gw0p8jy4.jpg)

KV模式不变，但V是一个键值对

* hset/hget/hmset/hmget/hgetall/hdel

* hlen

* hexists key 在key里面的某个值的key

* hkeys/hvals

* hincrby/hincrbyfloat

*  hsetnx

## Redis配置

### 缓存过期策略

#### 1.最近最少是使用LRU（设置了过期时间）

Volatile-lru -> remove the key with an expire set using an LRU algorithm

#### 2.所有最少最少使用

Allkeys-lru -> remove any key according to the LRU algorithm

#### 3.随机（设置了过期时间）

Volatile-random -> remove a random key with an expire set

#### 4.所有随机

Allkeys-random -> remove a random key, any key

#### 5.最接近过期时间

- Volatile-ttl -> remove the key with the nearest expire time (minor TTL)

#### 6. 永不过期

Noeviction -> don't expire at all, just return an error on write operations

### **配置模板**

```
参数说明 
redis.conf 配置项说明如下： 
1. Redis默认不是以守护进程的方式运行，可以通过该配置项修改，使用yes启用守护进程 
  daemonize no 
2. 当Redis以守护进程方式运行时，Redis默认会把pid写入/var/run/redis.pid文件，可以通过pidfile指定 
  pidfile /var/run/redis.pid 
3. 指定Redis监听端口，默认端口为6379，作者在自己的一篇博文中解释了为什么选用6379作为默认端口，因为6379在手机按键上MERZ对应的号码，而MERZ取自意大利歌女Alessia Merz的名字 
  port 6379 
4. 绑定的主机地址 
  bind 127.0.0.1 
5.当 客户端闲置多长时间后关闭连接，如果指定为0，表示关闭该功能 
  timeout 300 
6. 指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为verbose 
  loglevel verbose 
7. 日志记录方式，默认为标准输出，如果配置Redis为守护进程方式运行，而这里又配置为日志记录方式为标准输出，则日志将会发送给/dev/null 
  logfile stdout 
8. 设置数据库的数量，默认数据库为0，可以使用SELECT <dbid>命令在连接上指定数据库id 
  databases 16 
9. 指定在多长时间内，有多少次更新操作，就将数据同步到数据文件，可以多个条件配合 
  save <seconds> <changes> 
  Redis默认配置文件中提供了三个条件： 
  save 900 1 
  save 300 10 
  save 60 10000 
  分别表示900秒（15分钟）内有1个更改，300秒（5分钟）内有10个更改以及60秒内有10000个更改。 
  
10. 指定存储至本地数据库时是否压缩数据，默认为yes，Redis采用LZF压缩，如果为了节省CPU时间，可以关闭该选项，但会导致数据库文件变的巨大 
  rdbcompression yes 
11. 指定本地数据库文件名，默认值为dump.rdb 
  dbfilename dump.rdb 
12. 指定本地数据库存放目录 
  dir ./ 
13. 设置当本机为slav服务时，设置master服务的IP地址及端口，在Redis启动时，它会自动从master进行数据同步 
  slaveof <masterip> <masterport> 
14. 当master服务设置了密码保护时，slav服务连接master的密码 
  masterauth <master-password> 
15. 设置Redis连接密码，如果配置了连接密码，客户端在连接Redis时需要通过AUTH <password>命令提供密码，默认关闭 
  requirepass foobared 
16. 设置同一时间最大客户端连接数，默认无限制，Redis可以同时打开的客户端连接数为Redis进程可以打开的最大文件描述符数，如果设置 maxclients 0，表示不作限制。当客户端连接数到达限制时，Redis会关闭新的连接并向客户端返回max number of clients reached错误信息 
  maxclients 128 
17. 指定Redis最大内存限制，Redis在启动时会把数据加载到内存中，达到最大内存后，Redis会先尝试清除已到期或即将到期的Key，当此方法处理 后，仍然到达最大内存设置，将无法再进行写入操作，但仍然可以进行读取操作。Redis新的vm机制，会把Key存放内存，Value会存放在swap区 
  maxmemory <bytes> 
18. 指定是否在每次更新操作后进行日志记录，Redis在默认情况下是异步的把数据写入磁盘，如果不开启，可能会在断电时导致一段时间内的数据丢失。因为 redis本身同步数据文件是按上面save条件来同步的，所以有的数据会在一段时间内只存在于内存中。默认为no 
  appendonly no 
19. 指定更新日志文件名，默认为appendonly.aof 
   appendfilename appendonly.aof 
20. 指定更新日志条件，共有3个可选值：  
  no：表示等操作系统进行数据缓存同步到磁盘（快）  
  always：表示每次更新操作后手动调用fsync()将数据写到磁盘（慢，安全）  
  everysec：表示每秒同步一次（折衷，默认值） 
  appendfsync everysec 
  
21. 指定是否启用虚拟内存机制，默认值为no，简单的介绍一下，VM机制将数据分页存放，由Redis将访问量较少的页即冷数据swap到磁盘上，访问多的页面由磁盘自动换出到内存中（在后面的文章我会仔细分析Redis的VM机制） 
   vm-enabled no 
22. 虚拟内存文件路径，默认值为/tmp/redis.swap，不可多个Redis实例共享 
   vm-swap-file /tmp/redis.swap 
23. 将所有大于vm-max-memory的数据存入虚拟内存,无论vm-max-memory设置多小,所有索引数据都是内存存储的(Redis的索引数据 就是keys),也就是说,当vm-max-memory设置为0的时候,其实是所有value都存在于磁盘。默认值为0 
   vm-max-memory 0 
24. Redis swap文件分成了很多的page，一个对象可以保存在多个page上面，但一个page上不能被多个对象共享，vm-page-size是要根据存储的 数据大小来设定的，作者建议如果存储很多小对象，page大小最好设置为32或者64bytes；如果存储很大大对象，则可以使用更大的page，如果不 确定，就使用默认值 
   vm-page-size 32 
25. 设置swap文件中的page数量，由于页表（一种表示页面空闲或使用的bitmap）是在放在内存中的，，在磁盘上每8个pages将消耗1byte的内存。 
   vm-pages 134217728 
26. 设置访问swap文件的线程数,最好不要超过机器的核数,如果设置为0,那么所有对swap文件的操作都是串行的，可能会造成比较长时间的延迟。默认值为4 
   vm-max-threads 4 
27. 设置在向客户端应答时，是否把较小的包合并为一个包发送，默认为开启 
  glueoutputbuf yes 
28. 指定在超过一定的数量或者最大的元素超过某一临界值时，采用一种特殊的哈希算法 
  hash-max-zipmap-entries 64 
  hash-max-zipmap-value 512 
29. 指定是否激活重置哈希，默认为开启（后面在介绍Redis的哈希算法时具体介绍） 
  activerehashing yes 
30. 指定包含其它的配置文件，可以在同一主机上多个Redis实例之间使用同一份配置文件，而同时各个实例又拥有自己的特定配置文件 
  include /path/to/local.conf 

```

Aof 开启 dump 和aof 共存 恢复 先找aof 

如果aof 有损坏 使用：redis-check-aof --fix +文件  修复

关机后就会有dump.rdb 



























rediis线程池

```java
import redis.clients.jedis.Jedis;
import redis.clients.jedis.JedisPool;
import redis.clients.jedis.JedisPoolConfig; 
/**
 * @ProjectName: ${PROJECT_NAME}
 * @Package: PACKAGE_NAME
 * @ClassName: Pool
 * @Author: WQM
 * @Description: redis线程池
 * @Date: ${DATE} ${TIME}
 * @Version: 1.0
 */
public class PoolUtil {
    private static JedisPool pool = null; 
    private PoolUtil() {     } 
    public static JedisPool getPool() {
        if (pool == null) {
            synchronized (PoolUtil.class) {
                if (pool == null) {
                    JedisPoolConfig jedisPoolConfig = new JedisPoolConfig();
                    jedisPoolConfig.setMaxIdle(32);
                    jedisPoolConfig.setMaxWaitMillis(100 * 1000);
                    jedisPoolConfig.setTestOnBorrow(true);
                    return new JedisPool(jedisPoolConfig, "111.231.141.151", 6379);
                }
            }
        }
        return pool;
    } 
    //放回池子
    public static void release(JedisPool jedisPool, Jedis jedis) {
        if (null != jedis) {
            jedisPool.returnResourceObject(jedis);
        }
    }
}

```

```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.7.3</version>
</dependency>
```



