# Java面试题笔记

## JAVASE

### 类初始

####  类初始化过程

![image-20201224181745405](https://tva1.sinaimg.cn/large/0081Kckwgy1glz459cg96j311x0l1ah3.jpg)

1. 父类  静态变量 --静态代码块 子类 静态变量 -- 静态代码块

2. 子类实例化   <init> 生成几个对象就执行几次

   父类先实例化  

   ​       		super（）

   ​				静态显示 赋值

   ​				父类非静态代码块

   ​				父类无参构造

   子类 显示变量赋值    

   ​        非静态代码块

   ​		无参构造  最后

   ​		

   ![image-20201224185810607](https://tva1.sinaimg.cn/large/0081Kckwgy1glz5c5eepyj316z0gt13i.jpg)

   ​		

3. 

![image-20201224182226095](https://tva1.sinaimg.cn/large/0081Kckwgy1glz4a2ieo5j315b0jx44r.jpg)

![image-20201224183608735](https://tva1.sinaimg.cn/large/0081Kckwgy1glz4ofa2ysj31c00q5jz0.jpg)



![image-20201224183836037](https://tva1.sinaimg.cn/large/0081Kckwgy1glz4qvs45tj31270jogop.jpg)

![image-20201224191407541](https://tva1.sinaimg.cn/large/0081Kckwgy1glz5rz0k9pj310u0kojx3.jpg)

![image-20201224192832023](https://tva1.sinaimg.cn/large/0081Kckwgy1glz66uqx60j311k0i2dk6.jpg)

![image-20201224193308017](https://tva1.sinaimg.cn/large/0081Kckwgy1glz6bn9uorj311u0ejn17.jpg)

![image-20201224192910061](https://tva1.sinaimg.cn/large/0081Kckwgy1glz67jalahj30ml0dfn1d.jpg)

![image-20201224192924103](https://tva1.sinaimg.cn/large/0081Kckwgy1glz67sdtntj30tj0f1tfu.jpg)



![image-20201224194510554](https://tva1.sinaimg.cn/large/0081Kckwgy1glz6o71yg0j312v0fmq9h.jpg)







































## java 虚拟机

### JMM -- volatile

#### 1. 可见性（保证）

![image-20201222083308018](https://tva1.sinaimg.cn/large/0081Kckwgy1glwcm18mn4j31d10jwdkj.jpg)

- 一个线程 {   1拷贝走 ——>2 修改——>3写回主内存 }  就要通知其他线程

- 主内存共享 不能操作，各自线程在自己的内存中修改赋值
- 线程间不能直接通信，必须通过主内存来完成

![image-20201222085542899](https://tva1.sinaimg.cn/large/0081Kckwgy1glwcnsqd0rj31bx0i54e8.jpg)

#### 2.原子性 (不保证)

![image-20201222090704750](https://tva1.sinaimg.cn/large/0081Kckwgy1glwczlgo2gj30w102xq50.jpg)

![image-20201222091758635](https://tva1.sinaimg.cn/large/0081Kckwgy1glwdaxq9bnj30sd0eejua.jpg)

![image-20201222091458881](https://tva1.sinaimg.cn/large/0081Kckwgy1glwd7u9ubbj315a0kwwms.jpg)

![image-20201222092413141](https://tva1.sinaimg.cn/large/0081Kckwgy1glwdhfoe3fj318s0g70ul.jpg)

![image-20201222092916804](https://tva1.sinaimg.cn/large/0081Kckwgy1glwdmq219tj315e0hen5o.jpg)

#### 3.指令重排

![image-20201222094910869](https://tva1.sinaimg.cn/large/0081Kckwgy1glwe7f3tm6j319t0g8ajn.jpg)

![image-20201222095719951](https://tva1.sinaimg.cn/large/0081Kckwgy1glwefw3i0xj30m60hg41k.jpg)

不行，先考虑依赖

![image-20201222100301916](https://tva1.sinaimg.cn/large/0081Kckwgy1glweltkz39j30qi0jd77l.jpg)

![image-20201222172450877](https://tva1.sinaimg.cn/large/0081Kckwgy1glwrdlthbmj30xt0f8k0r.jpg)

![image-20201222172539736](https://tva1.sinaimg.cn/large/0081Kckwgy1glwredoc9cj30z303iq5r.jpg)

### CAS

- 是什么 比较交换

```java
AtomicInteger atomicInteger = new AtomicInteger(5);
System.out.println(atomicInteger.compareAndSet(5, 2019)+"\t var"+atomicInteger.toString());
```

Atomic 原理

![image-20201222191002995](https://tva1.sinaimg.cn/large/0081Kckwgy1glwuf1j0q5j31ba0kw4ep.jpg)



#### 什么是CAS

##### 定义

![image-20201222191045398](https://tva1.sinaimg.cn/large/0081Kckwgy1glwufrvtiwj31bb0lmnd9.jpg)

![image-20201222191353026](https://tva1.sinaimg.cn/large/0081Kckwgy1glwv11a2xoj30vw0cxwg2.jpg)

##### 底层汇编

![image-20201222193339648](https://tva1.sinaimg.cn/large/0081Kckwgy1glwv3kd0b7j31b80cbn6o.jpg)

##### CAS总结

![image-20201222193544417](https://tva1.sinaimg.cn/large/0081Kckwgy1glwv5qtsupj315p0ghtjd.jpg)

##### ABA

![image-20201222195354956](https://tva1.sinaimg.cn/large/0081Kckwgy1glwvomzljcj31a30d3qcp.jpg)

### 集合线程不安全

#### ArrayList、Map、Set

![image-20201223035709423](https://tva1.sinaimg.cn/large/0081Kckwgy1glx9ngb3vyj30kq0cy426.jpg)

![image-20201223040902549](https://tva1.sinaimg.cn/large/0081Kckwgy1glx9zsowmuj30hf02paap.jpg)

##### 解决

- new Vctor（）
- Collections.synchronizedList()

- 写时复制  CopyOnWriteArrayList (写时)
- ![image-20201223042421761](https://tva1.sinaimg.cn/large/0081Kckwgy1glxafqohroj30lp0dudg1.jpg)

hasSet() 底层  hashMap() key恒定RECENT

HashMap 

concurentHashMap()

### 锁

#### 公平锁

![image-20201223050421512](https://tva1.sinaimg.cn/large/0081Kckwgy1glxbld0kkqj30m601gwf9.jpg)

#### 非公平锁

![image-20201223050444902](https://tva1.sinaimg.cn/large/0081Kckwgy1glxblr96o2j30uz03040l.jpg)

#### 重入锁

![image-20201223051217470](https://tva1.sinaimg.cn/large/0081Kckwgy1glxbtlvgm4j30le06sn02.jpg)

#### 自旋锁

![image-20201223054143321](https://tva1.sinaimg.cn/large/0081Kckwgy1glxco8ft6gj318l06ogp0.jpg)

不用一直等，可以去做别的，循环探查

```java
package atomic.lock;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicReference;

/**
 * @ProjectName: JUC
 * @Package: atomic.lock
 * @ClassName: SpinLockDemo
 * @Author: WQM
 * @Description: 自旋锁
 * @Date: 2021/1/4 7:23 上午
 * @Version: 1.0
 */
public class SpinLockDemo {
    public static void main(String[] args) {
        SpLock lock = new SpLock();
        lock.myllock();
        try {
            TimeUnit.SECONDS.sleep(5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        lock.myUnlock();
    }
}

class SpLock implements Runnable {
    AtomicReference<Thread> atomicReference = new AtomicReference<>();

    //zi选方法
    public void myllock() {
        Thread thread = Thread.currentThread();
        System.out.println("thread.getName() = " + thread.getName() + "\t comin (*￣︶￣)");
        while (!atomicReference.compareAndSet(null, thread)) {
            System.out.print(".." );
        }
    }

    public void myUnlock() {
        Thread thread = Thread.currentThread();
        atomicReference.compareAndSet(thread, null);
        System.out.println("thread = " + thread.getName() + "\t unlock");
    }

    @Override
    public void run() {

    }
}
```



#### 读写锁

```java
package Lock; 
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.locks.ReentrantReadWriteLock; 
public class ReadWriteLock { 
    public static void main(String[] args) { 
        ReentrantReadWriteLock rlock = new ReentrantReadWriteLock();
        Mycache mycache = new Mycache();
        for (int i = 0; i < 50; i++) {
            rlock.writeLock().lock();
            try {
                mycache.put(String.valueOf(i), i); } catch (Exception e) {
                e.printStackTrace();
                rlock.writeLock().unlock();  }
        }
        for (int i = 0; i < 50; i++) {
            rlock.readLock().lock();
            try {
                mycache.get(String.valueOf(i));
            } catch (Exception e) {
                e.printStackTrace();
                rlock.readLock().unlock();
            }
        } 
    } 
}

class Mycache {
    private volatile Map<String, Object> map = new HashMap<String, Object>(); 
    public void put(String key, Object o) throws InterruptedException {
        System.out.println(key + "  ：正在写入");
        map.put(key, o);
        this.wait(1000);
        System.out.println(key + "  ：写入完成"); 
    } 
    public void get(String key) {
        System.out.println(key + "  ：正在读取");
        map.get(key);
        System.out.println(key + "  ：读取完成");  
    } 
}
```

#### 死锁

![image-20201223213202230](https://tva1.sinaimg.cn/large/0081Kckwgy1gly451elwhj30z60dite9.jpg)



##### 原因

![image-20201223213303842](https://tva1.sinaimg.cn/large/0081Kckwgy1gly463k0jgj30oa082t9s.jpg)

##### 排查

- jps 得到pid

- jstack  + pid

  



#### CurrentDownLanth 倒计时

![image-20201223073111714](https://tva1.sinaimg.cn/large/0081Kckwgy1glxfu5nvvhj31be06tgpx.jpg)

#### CyclicBarria  等到齐

![image-20201223073358576](https://tva1.sinaimg.cn/large/0081Kckwgy1glxfx1hc10j314603yju6.jpg)

```java
package aboutThread.Lock;

import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

/**
 * @ProjectName: java_basic
 * @Package: aboutThread.Lock
 * @ClassName: CyclicBarriaTest
 * @Author: WQM
 * @Description:
 * @Date: 2020/12/23 7:36 上午
 * @Version: 1.0
 */
public class CyclicBarriaTest {
    public static void main(String[] args) {
        CyclicBarrier cyclicBarrier = new CyclicBarrier(50, () -> {
            System.out.println("集齐了。。。。50个");
        });

        for (int i = 0; i < 50; i++) {
            new Thread(() -> {
                try {
                    cyclicBarrier.await();
                    System.out.println(Thread.currentThread().getId());
                } catch (InterruptedException | BrokenBarrierException e) {
                    e.printStackTrace();
                }
            }, String.valueOf(i)).start();
        }

    }
}
```

#### Semaphore 抢车位

```java 
package aboutThread.Lock;

import java.util.concurrent.Semaphore;
import java.util.concurrent.TimeUnit;

/**
 * @ProjectName: java_basic
 * @Package: aboutThread.Lock
 * @ClassName: SemaphoreDemo
 * @Author: WQM
 * @Description: 抢车位
 * @Date: 2020/12/23 7:50 上午
 * @Version: 1.0
 */
public class SemaphoreDemo {
    public static void main(String[] args) {
        Semaphore semaphore = new Semaphore(4);
        for (int i = 0; i < 50; i++) {
            new Thread(()->{

                try {
                    semaphore.acquire();
                    System.out.println(Thread.currentThread().getId()+ "抢到车位");
                    TimeUnit.SECONDS.sleep(3);
                    System.out.println(Thread.currentThread().getId()+ "\t 开走了");
                } catch (Exception e) {
                    e.printStackTrace();
                }finally {
                    semaphore.release();
                }
            },String.valueOf(i)).start();
         }
    }
}
```

### 队列

#### 1 阻塞队列

![image-20201223080434608](https://tva1.sinaimg.cn/large/0081Kckwgy1glxgsx5u8kj316g0jraij.jpg)

![image-20201223080704822](https://tva1.sinaimg.cn/large/0081Kckwgy1glxgvir44cj318y0bjgvd.jpg)

![image-20201223081512861](https://tva1.sinaimg.cn/large/0081Kckwgy1glxh3ylc9jj31b10ghgvj.jpg)

##### 用法

![image-20201223082325705](https://tva1.sinaimg.cn/large/0081Kckwgy1glxhci6hb6j31au0kyk5m.jpg)

- 1异常

```java
       BlockingQueue<Integer> blockingQueue = new ArrayBlockingQueue<>(10);
        for (int i = 0; i < 30; i++) {
            new Thread(()->{
                //方法调用
                blockingQueue.add(new Random().nextInt(10));  //添加
                System.out.println(blockingQueue.element());  //检查
                try {
                    sleep(3);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                blockingQueue.remove();                      //移除
//                blockingQueue.remove();
            },"t1").start();
        }
```



- 2 布尔

![image-20201223083622873](https://tva1.sinaimg.cn/large/0081Kckwgy1glxhpz96lpj30yv0fy12t.jpg)

**多线程 安全情况下 并发 操作资源类**

**判断干活唤醒通知**

**严防虚假唤醒**

##### 生产消费 1 传统版

- 资源类

```java
package aboutThread.productCustom;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * @ProjectName: java_basic
 * @Package: aboutThread.productCustom
 * @ClassName: Resource
 * @Author: WQM
 * @Description: 资源类
 * @Date: 2020/12/23 9:02 上午
 * @Version: 1.0
 */
public class Resource {
    //多线程的的资源类
    private volatile int num = 0;
    private Lock lock = new ReentrantLock();
    private Condition condition = lock.newCondition();

    //生产
    public void incressment() throws Exception {
        lock.lock();
        try {
            //判断
            while (num != 0) {
                condition.await();
                System.out.println("等待不能生产");
            }
            num++;
            System.out.println(Thread.currentThread().getName() + "生产了\t " + num);
            condition.signalAll();
        } catch (Exception e) {
            e.printStackTrace();
        }
            lock.unlock();
    }

    //消费
    public void decressment() throws Exception {
        lock.lock();
        try {
            //判断
            while (num == 0) {
                condition.await();
                System.out.println("空等待不能消费");
            }
            num--;
            System.out.println(Thread.currentThread().getName() + "消费\t " + num);
            condition.signalAll();
        } catch (Exception e) {
            e.printStackTrace();
        }
        finally {
            lock.unlock();
        }
    }
}
```

- 消费

```java
package aboutThread.productCustom;

/**
 * @ProjectName: java_basic
 * @Package: aboutThread.productCustom
 * @ClassName: PrpductCustomerD
 * @Author: WQM
 * @Description: 生产者消费者
 * @Date: 2020/12/23 9:02 上午
 * @Version: 1.0
 */
public class PrpductCustomerD {
    public static void main(String[] args) {
        Resource resource = new Resource();
        //生产
        new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                try {
                    resource.incressment();
                    Thread.sleep(5000);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }, "a").start();
        //消费
        new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                try {
                    resource.decressment();
                    Thread.sleep(6000);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }, "b").start();
    }
}
```



##### Syncized ReentantLock 区别

- 原理

  + s 关键字 底层是monitor

  + Lock 具体类 api层面的锁

- 使用方法

  - s 不用手动释放锁
  - ReentantLock 需要手动去释放锁 若没有释放可能会出现死锁现象 

- 是否可中断

  - s 不可中断 异常 程序正常完成
  - 可中断 1 设置超时 2 lockinterruptly（）

- 加锁是否公平

  - s 是非公平锁
  - ReentantLock 可以是公平锁，默认是非公平锁，

- 锁绑定

  - s 模糊唤醒
  - ReentantLock 精确唤醒 多重Condition

##### 面试题

![image-20201223162732931](https://tva1.sinaimg.cn/large/0081Kckwgy1glxvcanmfij30rz061wh6.jpg)

##### 

###### 实现方式1

```java
package aboutThread.productCustom;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;
/**
 * @ProjectName: java_basic
 * @Package: aboutThread.productCustom
 * @ClassName: Print5
 * @Author: WQM
 * @Description: 面试题
 * @Date: 2020/12/23 4:12 下午
 * @Version: 1.0
 */
public class Print5 {
    public static void main(String[] args) {
        Resouce1 re = new Resouce1();

        for (int i = 0; i < 10; i++) {
            new Thread(() -> {
                try {
                    re.print5();
                    re.print10();
                    re.print15();
                    System.out.println(Thread.currentThread().getName() + "\t");
                } catch (Exception e) {
                    e.printStackTrace();
                } finally {
                }
            }, "第" + String.valueOf(i) + "次：").start();
        }
    }


}
//资源类
class Resouce1 {
    private volatile int num = 1;//A1 B2 C3 标志位
    ReentrantLock lock = new ReentrantLock();
    private Condition c1 = lock.newCondition();
    private Condition c2 = lock.newCondition();
    private Condition c3 = lock.newCondition();

    public void print5() {
        lock.lock();
        try {
            //判断
            while (!(num == 1)) {//1 干活
                c1.await();
            }
            print(5, "AA");
            //通知
            num = 2;
            c2.signal(); //唤醒2
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    public void print10() throws InterruptedException {
        lock.lock();
        try {
            //判断
            while (!(num == 2)) {
                c2.await();
            }
            //干活
            print(10, "BB");
            //通知
            num = 3;
            c3.signal();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    void print15() {
        lock.lock();
        try {
            while (!(num == 3)) {
                c3.await();
            }
            //干活
            print(15, "CC");
            System.out.println();
            //通知
            num = 1;
            c1.signal();//再通知1
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    void print(int times, String content) {
        for (int i = 0; i < times; i++) {
            System.out.print(content+"\t");
        }
    }


}
```

###### 实现方式2 

```java
package aboutThread.productCustom;

import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicInteger;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

/**
 * @ProjectName: java_basic
 * @Package: aboutThread.productCustom
 * @ClassName: Print5
 * @Author: WQM
 * @Description: 面试题
 * @Date: 2020/12/23 4:12 下午
 * @Version: 1.0
 */
public class Print5 {
    public static void main(String[] args) throws InterruptedException {
        v2();
    }

    static void v2() throws InterruptedException {

        Myresource re = new Myresource(new ArrayBlockingQueue<>(10));
        //生产

        new Thread(() -> {
            try {
                re.myProdt();
            } catch (Exception e) {
                e.printStackTrace();
            } finally {

            }
        }, "生产者").start();

        //消费

        new Thread(() -> {
            try {
                re.myCostommer();
            } catch (Exception e) {
                e.printStackTrace();
            } finally {

            }
        }, "消费者").start();
        TimeUnit.SECONDS.sleep(150);
        re.stops();

    }

    static void v1() {
        Resouce1 re = new Resouce1();
        for (int i = 0; i < 10; i++) {
            new Thread(() -> {
                try {
                    re.print5();
                    re.print10();
                    re.print15();
                    System.out.println(Thread.currentThread().getName() + "\t");
                } catch (Exception e) {
                    e.printStackTrace();
                } finally {
                }
            }, "第" + String.valueOf(i) + "次：").start();
        }
    }
}

//队列型
class Myresource {

    private volatile boolean FLAG = true;//默认开启队列
    private AtomicInteger atomicInteger = new AtomicInteger(); //状态值
    BlockingQueue blockingQueue = null;

    public Myresource(BlockingQueue<String> blockingQueue) {
        this.blockingQueue = blockingQueue;
        System.out.println("blockingQueue.getClass().getName() = " +
                blockingQueue.getClass().getName());
    }

    public void myProdt() throws InterruptedException {
        String data = null;
        boolean retValue;//
        while (FLAG) {
            Thread.sleep(2000);
            data = atomicInteger.incrementAndGet() + "";
            retValue = blockingQueue.offer(data, 2L, TimeUnit.SECONDS);//等待两秒 等不到失败
            if (retValue) {
                System.out.println(Thread.currentThread().getName() + "\t 插入队列" + data + "成功");
            } else {
                System.out.println(Thread.currentThread().getName() + "\t 插入队列" + data + "失败");
            }
        }
        System.out.println(Thread.currentThread().getName() + "\t 被老板叫停了");
    }

    public void myCostommer() throws InterruptedException {
        String result = null;
        while (FLAG) {
            Thread.sleep(5000);
            result = (String) blockingQueue.poll(2L, TimeUnit.SECONDS);
            if (null == result || result.equalsIgnoreCase("")) {
                FLAG = false;
                System.out.println(Thread.currentThread().getName() + "\t 超过两秒没取到蛋糕 结束");
                return;
            }
            System.out.println(Thread.currentThread().getName() + "\t 成功取到消费队列蛋糕" + result);

        }
    }

    public void stops() {
        FLAG = false;
    }

}

//普通型
class Resouce1 {
    private volatile int num = 1;//A1 B2 C3 标志位
    ReentrantLock lock = new ReentrantLock();
    private Condition c1 = lock.newCondition();
    private Condition c2 = lock.newCondition();
    private Condition c3 = lock.newCondition();

    public void print5() {
        lock.lock();
        try {
            //判断
            while (!(num == 1)) {//1 干活
                c1.await();
            }
            print(5, "AA");
            //通知
            num = 2;
            c2.signal(); //唤醒2
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    public void print10() throws InterruptedException {
        lock.lock();
        try {
            //判断
            while (!(num == 2)) {
                c2.await();
            }
            //干活
            print(10, "BB");
            //通知
            num = 3;
            c3.signal();
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    }

    void print15() {
        lock.lock();
        try {
            while (!(num == 3)) {
                c3.await();
            }
            //干活
            print(15, "CC");
            System.out.println();
            //通知
            num = 1;
            c1.signal();//再通知1
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            lock.unlock();
        }
    } 
    void print(int times, String content) {
        for (int i = 0; i < times; i++) {
            System.out.print(content + "\t");
        }
    }


}
```

### 线程池

#### 为什么用

![image-20201223192134802](https://tva1.sinaimg.cn/large/0081Kckwgy1gly0dcmuizj31dd0bpgyx.jpg)

![image-20201223192357057](https://tva1.sinaimg.cn/large/0081Kckwgy1gly0fsbco9j30wf0hqdj3.jpg)

Exectors ThreadPoolExecutor

实现多线程的方法

- 实现runable 接口
- 继承Thread 类
- 线程池
- CallAble 有返回值 Feature



##### ThreadPoolExecutor 七大参数

![image-20201223194324332](https://tva1.sinaimg.cn/large/0081Kckwgy1gly1011kbdj31540egdnx.jpg)

![image-20201223194655752](https://tva1.sinaimg.cn/large/0081Kckwgy1gly13oiuipj30sz0edwlz.jpg)

![image-20201223201253406](https://tva1.sinaimg.cn/large/0081Kckwgy1gly1upcy8vj31eu0gnguk.jpg)

![image-20201223202055536](https://tva1.sinaimg.cn/large/0081Kckwgy1gly231oxfvj31fs0kjafl.jpg)

##### 线程池的底层原理

![image-20201223203421008](https://tva1.sinaimg.cn/large/0081Kckwgy1gly2h1jc5xj31do0l4wvg.jpg)



![image-20201223204817786](https://tva1.sinaimg.cn/large/0081Kckwgy1gly2vipzjjj30lt0grdiv.jpg)

##### 拒绝策略

![image-20201223205117221](https://tva1.sinaimg.cn/large/0081Kckwgy1gly2yn4idfj30q00agaes.jpg)

- 分类

  ![image-20201223205157263](https://tva1.sinaimg.cn/large/0081Kckwgy1gly2zc28x6j312806s77v.jpg)

##### 手写线程池 AbortPolicy 默认策略

```java
package ThreadPool;

import java.util.concurrent.Executors;
import java.util.concurrent.LinkedBlockingDeque;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

/**
 * @ProjectName: java_basic
 * @Package: ThreadPool
 * @ClassName: Pool1
 * @Author: WQM
 * @Description: 手写线程池
 * @Date: 2020/12/23 9:07 下午
 * @Version: 1.0
 */
public class Pool1 {
    public static void main(String[] args) {

        ThreadPoolExecutor pool = new ThreadPoolExecutor(10,
                20,
                30,
                TimeUnit.SECONDS,
                new LinkedBlockingDeque<>(3),
                Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.AbortPolicy());
        try {
            for (int i = 0; i < 10; i++) {

                pool.execute(() -> {
                    System.out.println("Thread.currentThread().getName() = " +
                            Thread.currentThread().getName() + "\t 来办理业务");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            pool.shutdown();
        }


    }
}
```

###### 调用者 CallerRunsPolicy

```java
package ThreadPool; 
import java.util.concurrent.Executors;
import java.util.concurrent.LinkedBlockingDeque;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

/**
 * @ProjectName: java_basic
 * @Package: ThreadPool
 * @ClassName: Pool1
 * @Author: WQM
 * @Description: 手写线程池
 * @Date: 2020/12/23 9:07 下午
 * @Version: 1.0
 */
public class Pool1 {
    public static void main(String[] args) { 
        ThreadPoolExecutor pool = new ThreadPoolExecutor(10,
                20,
                30,
                TimeUnit.SECONDS,
                new LinkedBlockingDeque<>(3),
                Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.CallerRunsPolicy());
        try {
            for (int i = 0; i < 50; i++) {

                pool.execute(() -> {
                    System.out.println("当前线程 = " +
                            Thread.currentThread().getName() + "\t 来办理业务");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            pool.shutdown();
        } 
    }
}
```

2

```java
package ThreadPool;
import java.util.concurrent.Executors;
import java.util.concurrent.LinkedBlockingDeque;
import java.util.concurrent.ThreadPoolExecutor;
import java.util.concurrent.TimeUnit;

/**
 * @ProjectName: java_basic
 * @Package: ThreadPool
 * @ClassName: Pool1
 * @Author: WQM
 * @Description: 手写线程池
 * @Date: 2020/12/23 9:07 下午
 * @Version: 1.0
 */
public class Pool1 {
    public static void main(String[] args) {
        ThreadPoolExecutor pool = new ThreadPoolExecutor(5,
                9,
                30,
                TimeUnit.SECONDS,
                new LinkedBlockingDeque<>(3),
                Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.CallerRunsPolicy());
        try {
            for (int i = 0; i < 10; i++) {

                pool.execute(() -> {
                    System.out.println("当前线程 = " +
                            Thread.currentThread().getName() + "\t 来办理业务");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            pool.shutdown();
        }
    }
}
```

###### 配置

- io密集型 
- ![image-20201223212617899](https://tva1.sinaimg.cn/large/0081Kckwgy1gly3z2c8foj313r03rq4z.jpg)

![image-20201223212726898](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6q6sllvj31b50e8mzb.jpg)

### JVM GC

![image-20201223225428727](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6iszucsj30t80fpwhq.jpg)

![image-20201223225444907](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6j3hbuwj30vn0fz46q.jpg)

![image-20201223225602506](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6kff4ysj30iq0c6whm.jpg)

#### gc 算法

![image-20201223225628087](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6kw0siwj309z08hgm9.jpg)

##### 算法概述

![image-20201224041951617](https://tva1.sinaimg.cn/large/0081Kckwgy1glyfxds3x6j314a0koq88.jpg)

##### 引用计数 不用

![image-20201223225940829](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6o89xuej30o70bcn0k.jpg)

![image-20201223231101752](https://tva1.sinaimg.cn/large/0081Kckwgy1gly7016v8dj318a0lbamp.jpg)

###### 枚举根节点可达性分析

![image-20201223231243425](https://tva1.sinaimg.cn/large/0081Kckwgy1gly71tvne8j31bd0lch2l.jpg)

###### GCROOT

![image-20201223231547730](https://tva1.sinaimg.cn/large/0081Kckwgy1gly750e72bj317o0m1qje.jpg)

###### 四种gcroot

![image-20201223231956220](https://tva1.sinaimg.cn/large/0081Kckwgy1gly79av726j30zr09ago2.jpg)

##### 复制 新生代

![image-20201223230209959](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6qubl2wj30u80fkzsi.jpg)

##### 标记清除

![image-20201223230403880](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6ssclrmj30wu0gi42h.jpg)

##### 标记整理

![image-20201223230457121](https://tva1.sinaimg.cn/large/0081Kckwgy1gly6tpir1dj30zc0fjn14.jpg)

gcroot

#### JVM 参数例子

```shell
(base) admin:java_basic/ (master*) $ jinfo -flags 8105                                                                          [0:04:42]
VM Flags:
-XX:-AlwaysTenure 
-XX:CICompilerCount=4 
-XX:ConcGCThreads=2 
-XX:G1ConcRefinementThreads=8  
-XX:G1HeapRegionSize=1048576 
-XX:GCDrainStackTargetSize=64 
-XX:InitialHeapSize=268435456 //初始堆内存
-XX:MarkStackSize=4194304     //占内存
-XX:MaxHeapSize=4294967296    //堆内存
-XX:MaxNewSize=2576351232    //新生代
-XX:MaxTenuringThreshold=15   //专老年代的年龄
-XX:MetaspaceSize=4096 
-XX:MinHeapDeltaBytes=1048576 
-XX:MinHeapSize=8388608 
-XX:-NeverTenure 
-XX:NonNMethodCodeHeapSize=5839372 
-XX:NonProfiledCodeHeapSize=122909434 
-XX:+PrintGCDetails 
-XX:ProfiledCodeHeapSize=122909434 
-XX:ReservedCodeCacheSize=251658240 
-XX:+SegmentedCodeCache 
-XX:SoftMaxHeapSize=4294967296 
-XX:+UseCompressedClassPointers 
-XX:+UseCompressedOops 
-XX:+UseG1GC            //gc回收器 
-XX:+PrintFlagsInitial   //打印初始值
```

##### 全部参数

```shell
[Global flags]
      int ActiveProcessorCount                     = -1                                        
    uintx AdaptiveSizeDecrementScaleFactor         = 4                                         
    uintx AdaptiveSizeMajorGCDecayTimeScale        = 10                                        
    uintx AdaptiveSizePolicyCollectionCostMargin   = 50                                        
    uintx AdaptiveSizePolicyInitializingSteps      = 20                                        
    uintx AdaptiveSizePolicyOutputInterval         = 0                                         
    uintx AdaptiveSizePolicyWeight                 = 10                                        
    uintx AdaptiveSizeThroughPutPolicy             = 0                                         
    uintx AdaptiveTimeWeight                       = 25                                        
     bool AggressiveHeap                           = false                                     
     intx AliasLevel                               = 3                                      {C2 
     bool AlignVector                              = true                                   {C2 
    ccstr AllocateHeapAt                           =                                           
     intx AllocateInstancePrefetchLines            = 1                                         
     intx AllocatePrefetchDistance                 = -1                                        
     intx AllocatePrefetchInstr                    = 0                                         
     intx AllocatePrefetchLines                    = 3                                         
     intx AllocatePrefetchStepSize                 = 16                                        
     intx AllocatePrefetchStyle                    = 1                                         
     bool AllowParallelDefineClass                 = false                                     
     bool AllowRedefinitionToAddDeleteMethods      = false                                     
     bool AllowUserSignalHandlers                  = false                                     
     bool AllowVectorizeOnDemand                   = true                                   {C2 
     bool AlwaysActAsServerClassMachine            = false                                     
     bool AlwaysCompileLoopMethods                 = false                                     
     bool AlwaysLockClassLoader                    = false                                     
     bool AlwaysPreTouch                           = false                                     
     bool AlwaysRestoreFPU                         = false                                     
     bool AlwaysTenure                             = false                                     
    ccstr ArchiveClassesAtExit                     =                                           
     intx ArrayCopyLoadStoreMaxElem                = 8                                      {C2 
     bool AssertOnSuspendWaitFailure               = false                                     
     intx AutoBoxCacheMax                          = 128                                    {C2 
     intx BCEATraceLevel                           = 0                                         
     bool BackgroundCompilation                    = true                                   {pd 
   size_t BaseFootPrintEstimate                    = 268435456                                 
     intx BiasedLockingBulkRebiasThreshold         = 20                                        
     intx BiasedLockingBulkRevokeThreshold         = 40                                        
     intx BiasedLockingDecayTime                   = 25000                                     
     intx BiasedLockingStartupDelay                = 0                                         
     bool BlockLayoutByFrequency                   = true                                   {C2 
     intx BlockLayoutMinDiamondPercentage          = 20                                     {C2 
     bool BlockLayoutRotateLoops                   = true                                   {C2 
     bool BranchOnRegister                         = false                                  {C2 
     bool C1OptimizeVirtualCallProfiling           = true                                   {C1 
     bool C1ProfileBranches                        = true                                   {C1 
     bool C1ProfileCalls                           = true                                   {C1 
     bool C1ProfileCheckcasts                      = true                                   {C1 
     bool C1ProfileInlinedCalls                    = true                                   {C1 
     bool C1ProfileVirtualCalls                    = true                                   {C1 
     bool C1UpdateMethodData                       = true                                   {C1 
     intx CICompilerCount                          = 2                                         
     bool CICompilerCountPerCPU                    = false                                     
     bool CITime                                   = false                                     
     bool CalculateClassFingerprint                = false                                     
     bool CheckJNICalls                            = false                                     
     bool ClassUnloading                           = true                                      
     bool ClassUnloadingWithConcurrentMark         = true                                      
     bool ClipInlining                             = true                                      
    uintx CodeCacheExpansionSize                   = 65536                                  {pd 
     bool CompactFields                            = true                                      
     bool CompactStrings                           = true                                   {pd 
    ccstr CompilationMode                          = default                                   
ccstrlist CompileCommand                           =                                           
    ccstr CompileCommandFile                       =                                           
ccstrlist CompileOnly                              =                                           
     intx CompileThreshold                         = 10000                                  {pd 
   double CompileThresholdScaling                  = 1.000000                                  
     intx CompilerThreadPriority                   = -1                                        
     intx CompilerThreadStackSize                  = 1024                                   {pd 
   size_t CompressedClassSpaceSize                 = 1073741824                                
     uint ConcGCThreads                            = 0                                         
     intx ConditionalMoveLimit                     = 3                                   {C2 pd 
     intx ContendedPaddingWidth                    = 128                                       
     bool CrashOnOutOfMemoryError                  = false                                     
     bool CreateCoredumpOnCrash                    = true                                      
     bool CriticalJNINatives                       = true                                      
     bool DTraceAllocProbes                        = false                                     
     bool DTraceMethodProbes                       = false                                     
     bool DTraceMonitorProbes                      = false                                     
     bool Debugging                                = false                                     
     bool DisableAttachMechanism                   = false                                     
     bool DisableExplicitGC                        = false                                     
     bool DisplayVMOutputToStderr                  = false                                     
     bool DisplayVMOutputToStdout                  = false                                     
     bool DoEscapeAnalysis                         = true                                   {C2 
     bool DoReserveCopyInSuperWord                 = true                                   {C2 
     bool DontCompileHugeMethods                   = true                                      
     bool DontYieldALot                            = false                                  {pd 
    ccstr DumpLoadedClassList                      =                                           
     bool DumpReplayDataOnError                    = true                                      
     bool DumpSharedSpaces                         = false                                     
     bool DynamicDumpSharedSpaces                  = false                                     
     bool EagerXrunInit                            = false                                     
     intx EliminateAllocationArraySizeLimit        = 64                                     {C2 
     bool EliminateAllocations                     = true                                   {C2 
     bool EliminateAutoBox                         = true                                   {C2 
     bool EliminateLocks                           = true                                   {C2 
     bool EliminateNestedLocks                     = true                                   {C2 
     bool EnableContended                          = true                                      
     bool EnableDynamicAgentLoading                = true                                      
   size_t ErgoHeapSizeLimit                        = 0                                         
    ccstr ErrorFile                                =                                           
     bool ErrorFileToStderr                        = false                                     
     bool ErrorFileToStdout                        = false                                     
 uint64_t ErrorLogTimeout                          = 120                                       
   double EscapeAnalysisTimeout                    = 20.000000                              {C2 
     bool EstimateArgEscape                        = true                                      
     bool ExecutingUnitTests                       = false                                     
     bool ExitOnOutOfMemoryError                   = false                                     
     bool ExplicitGCInvokesConcurrent              = false                                     
     bool ExtendedDTraceProbes                     = false                                     
     bool ExtensiveErrorReports                    = false                                     
    ccstr ExtraSharedClassListFile                 =                                           
     intx FieldsAllocationStyle                    = 1                                         
     bool FilterSpuriousWakeups                    = true                                      
     bool FlightRecorder                           = false                                     
    ccstr FlightRecorderOptions                    =                                           
     bool ForceNUMA                                = false                                     
     bool ForceTimeHighResolution                  = false                                     
     intx FreqInlineSize                           = 325                                    {pd 
   double G1ConcMarkStepDurationMillis             = 10.000000                                 
    uintx G1ConcRSHotCardLimit                     = 4                                         
   size_t G1ConcRSLogCacheSize                     = 10                                        
   size_t G1ConcRefinementGreenZone                = 0                                         
   size_t G1ConcRefinementRedZone                  = 0                                         
    uintx G1ConcRefinementServiceIntervalMillis    = 300                                       
     uint G1ConcRefinementThreads                  = 0                                         
   size_t G1ConcRefinementThresholdStep            = 2                                         
   size_t G1ConcRefinementYellowZone               = 0                                         
    uintx G1ConfidencePercent                      = 50                                        
   size_t G1HeapRegionSize                         = 0                                         
    uintx G1HeapWastePercent                       = 5                                         
    uintx G1MixedGCCountTarget                     = 8                                         
    uintx G1PeriodicGCInterval                     = 0                                      {manageable}  
     bool G1PeriodicGCInvokesConcurrent            = true                                      
   double G1PeriodicGCSystemLoadThreshold          = 0.000000                               {manageable}   
     intx G1RSetRegionEntries                      = 0                                         
   size_t G1RSetScanBlockSize                      = 64                                        
     intx G1RSetSparseRegionEntries                = 0                                         
     intx G1RSetUpdatingPauseTimePercent           = 10                                        
     uint G1RefProcDrainInterval                   = 1000                                      
    uintx G1ReservePercent                         = 10                                        
    uintx G1SATBBufferEnqueueingThresholdPercent   = 60                                        
   size_t G1SATBBufferSize                         = 1024                                      
   size_t G1UpdateBufferSize                       = 256                                       
     bool G1UseAdaptiveConcRefinement              = true                                      
     bool G1UseAdaptiveIHOP                        = true                                      
    uintx GCDrainStackTargetSize                   = 64                                        
    uintx GCHeapFreeLimit                          = 2                                         
    uintx GCLockerEdenExpansionPercent             = 5                                         
    uintx GCPauseIntervalMillis                    = 0                                         
    uintx GCTimeLimit                              = 98                                        
    uintx GCTimeRatio                              = 99                                        
   size_t HeapBaseMinAddress                       = 2147483648                             {pd 
     bool HeapDumpAfterFullGC                      = false                                  {manageable}  
     bool HeapDumpBeforeFullGC                     = false                                  {manageable}  
     bool HeapDumpOnOutOfMemoryError               = false                                  {manageable}  
    ccstr HeapDumpPath                             =                                        {manageable}  
    uintx HeapFirstMaximumCompactionCount          = 3                                         
    uintx HeapMaximumCompactionInterval            = 20                                        
    uintx HeapSearchSteps                          = 3                                         
   size_t HeapSizePerGCThread                      = 43620760                                  
     bool IgnoreEmptyClassPaths                    = false                                     
     bool IgnoreUnrecognizedVMOptions              = false                                     
    uintx IncreaseFirstTierCompileThresholdAt      = 50                                        
     bool IncrementalInline                        = true                                   {C2 
   size_t InitialBootClassLoaderMetaspaceSize      = 4194304                                   
    uintx InitialCodeCacheSize                     = 2555904                                {pd 
   size_t InitialHeapSize                          = 0                                         
    uintx InitialRAMFraction                       = 64                                        
   double InitialRAMPercentage                     = 1.562500                                  
    uintx InitialSurvivorRatio                     = 8                                         
    uintx InitialTenuringThreshold                 = 7                                         
    uintx InitiatingHeapOccupancyPercent           = 45                                        
     bool Inline                                   = true                                      
    ccstr InlineDataFile                           =                                           
     intx InlineSmallCode                          = 1000                                   {pd 
     bool InlineSynchronizedMethods                = true                                   {C1 
     bool InsertMemBarAfterArraycopy               = true                                   {C2 
     intx InteriorEntryAlignment                   = 16                                  {C2 pd 
     intx InterpreterProfilePercentage             = 33                                        
     bool JavaMonitorsInStackTrace                 = true                                      
     intx JavaPriority10_To_OSPriority             = -1                                        
     intx JavaPriority1_To_OSPriority              = -1                                        
     intx JavaPriority2_To_OSPriority              = -1                                        
     intx JavaPriority3_To_OSPriority              = -1                                        
     intx JavaPriority4_To_OSPriority              = -1                                        
     intx JavaPriority5_To_OSPriority              = -1                                        
     intx JavaPriority6_To_OSPriority              = -1                                        
     intx JavaPriority7_To_OSPriority              = -1                                        
     intx JavaPriority8_To_OSPriority              = -1                                        
     intx JavaPriority9_To_OSPriority              = -1                                        
     bool LIRFillDelaySlots                        = false                               {C1 pd 
   size_t LargePageHeapSizeThreshold               = 134217728                                 
   size_t LargePageSizeInBytes                     = 0                                         
     intx LiveNodeCountInliningCutoff              = 40000                                  {C2 
     intx LoopMaxUnroll                            = 16                                     {C2 
     intx LoopOptsCount                            = 43                                     {C2 
     intx LoopPercentProfileLimit                  = 30                                  {C2 pd 
    uintx LoopStripMiningIter                      = 0                                      {C2 
    uintx LoopStripMiningIterShortLoop             = 0                                      {C2 
     intx LoopUnrollLimit                          = 60                                  {C2 pd 
     intx LoopUnrollMin                            = 4                                      {C2 
     bool LoopUnswitching                          = true                                   {C2 
     bool ManagementServer                         = false                                     
   size_t MarkStackSize                            = 4194304                                   
   size_t MarkStackSizeMax                         = 536870912                                 
     uint MarkSweepAlwaysCompactCount              = 4                                         
    uintx MarkSweepDeadRatio                       = 5                                         
     intx MaxBCEAEstimateLevel                     = 5                                         
     intx MaxBCEAEstimateSize                      = 150                                       
 uint64_t MaxDirectMemorySize                      = 0                                         
     bool MaxFDLimit                               = true                                      
    uintx MaxGCMinorPauseMillis                    = 18446744073709551615                      
    uintx MaxGCPauseMillis                         = 18446744073709551614                      
    uintx MaxHeapFreeRatio                         = 70                                     {manageable}  
   size_t MaxHeapSize                              = 130862280                                 
     intx MaxInlineLevel                           = 15                                        
     intx MaxInlineSize                            = 35                                        
     intx MaxJNILocalCapacity                      = 65536                                     
     intx MaxJavaStackTraceDepth                   = 1024                                      
     intx MaxJumpTableSize                         = 65000                                  {C2 
     intx MaxJumpTableSparseness                   = 5                                      {C2 
     intx MaxLabelRootDepth                        = 1100                                   {C2 
     intx MaxLoopPad                               = 15                                     {C2 
   size_t MaxMetaspaceExpansion                    = 5452592                                   
    uintx MaxMetaspaceFreeRatio                    = 70                                        
   size_t MaxMetaspaceSize                         = 18446744073709551615                      
   size_t MaxNewSize                               = 18446744073709551615                      
     intx MaxNodeLimit                             = 80000                                  {C2 
 uint64_t MaxRAM                                   = 137438953472                           {pd 
    uintx MaxRAMFraction                           = 4                                         
   double MaxRAMPercentage                         = 25.000000                                 
     intx MaxRecursiveInlineLevel                  = 1                                         
    uintx MaxTenuringThreshold                     = 15                                        
     intx MaxTrivialSize                           = 6                                         
     intx MaxVectorSize                            = 64                                     {C2 
   size_t MetaspaceSize                            = 21810376                               {pd 
     bool MethodFlushing                           = true                                      
   size_t MinHeapDeltaBytes                        = 170392                                    
    uintx MinHeapFreeRatio                         = 40                                     {manageable}  
   size_t MinHeapSize                              = 0                                         
     intx MinInliningThreshold                     = 250                                       
     intx MinJumpTableSize                         = 10                                  {C2 pd 
   size_t MinMetaspaceExpansion                    = 340784                                    
    uintx MinMetaspaceFreeRatio                    = 40                                        
    uintx MinRAMFraction                           = 2                                         
   double MinRAMPercentage                         = 50.000000                                 
    uintx MinSurvivorRatio                         = 3                                         
   size_t MinTLABSize                              = 2048                                      
     intx MonitorBound                             = 0                                         
     intx MultiArrayExpandLimit                    = 6                                      {C2 
    uintx NUMAChunkResizeWeight                    = 20                                        
   size_t NUMAInterleaveGranularity                = 2097152                                   
    uintx NUMAPageScanRate                         = 256                                       
   size_t NUMASpaceResizeRate                      = 1073741824                                
     bool NUMAStats                                = false                                     
    ccstr NativeMemoryTracking                     = off                                       
     bool NeverActAsServerClassMachine             = false                                  {pd 
     bool NeverTenure                              = false                                     
    uintx NewRatio                                 = 2                                         
   size_t NewSize                                  = 1363144                                   
   size_t NewSizeThreadIncrease                    = 5320                                   {pd 
     intx NmethodSweepActivity                     = 10                                        
     intx NodeLimitFudgeFactor                     = 2000                                   {C2 
    uintx NonNMethodCodeHeapSize                   = 5242880                                {pd 
    uintx NonProfiledCodeHeapSize                  = 22020096                               {pd 
     intx NumberOfLoopInstrToAlign                 = 4                                      {C2 
     intx ObjectAlignmentInBytes                   = 8                                    {lp64_
   size_t OldPLABSize                              = 1024                                      
   size_t OldSize                                  = 5452592                                   
     bool OmitStackTraceInFastThrow                = true                                      
ccstrlist OnError                                  =                                           
ccstrlist OnOutOfMemoryError                       =                                           
     intx OnStackReplacePercentage                 = 140                                    {pd 
     bool OptimizeFill                             = true                                   {C2 
     bool OptimizePtrCompare                       = true                                   {C2 
     bool OptimizeStringConcat                     = true                                   {C2 
     bool OptoBundling                             = false                               {C2 pd 
     intx OptoLoopAlignment                        = 16                                     {pd 
     bool OptoRegScheduling                        = true                                {C2 pd 
     bool OptoScheduling                           = false                               {C2 pd 
    uintx PLABWeight                               = 75                                        
     bool PSChunkLargeArrays                       = true                                      
      int ParGCArrayScanChunk                      = 50                                        
    uintx ParallelGCBufferWastePct                 = 10                                        
     uint ParallelGCThreads                        = 0                                         
   size_t ParallelOldDeadWoodLimiterMean           = 50                                        
   size_t ParallelOldDeadWoodLimiterStdDev         = 80                                        
     bool ParallelRefProcBalancingEnabled          = true                                      
     bool ParallelRefProcEnabled                   = false                                     
     bool PartialPeelAtUnsignedTests               = true                                   {C2 
     bool PartialPeelLoop                          = true                                   {C2 
     intx PartialPeelNewPhiDelta                   = 0                                      {C2 
    uintx PausePadding                             = 1                                         
     intx PerBytecodeRecompilationCutoff           = 200                                       
     intx PerBytecodeTrapLimit                     = 4                                         
     intx PerMethodRecompilationCutoff             = 400                                       
     intx PerMethodTrapLimit                       = 100                                       
     bool PerfAllowAtExitRegistration              = false                                     
     bool PerfBypassFileSystemCheck                = false                                     
     intx PerfDataMemorySize                       = 32768                                     
     intx PerfDataSamplingInterval                 = 50                                        
    ccstr PerfDataSaveFile                         =                                           
     bool PerfDataSaveToFile                       = false                                     
     bool PerfDisableSharedMem                     = false                                     
     intx PerfMaxStringConstLength                 = 1024                                      
   size_t PreTouchParallelChunkSize                = 1073741824                                
     bool PreferInterpreterNativeStubs             = false                                  {pd 
     intx PrefetchCopyIntervalInBytes              = -1                                        
     intx PrefetchFieldsAhead                      = -1                                        
     intx PrefetchScanIntervalInBytes              = -1                                        
     bool PreserveAllAnnotations                   = false                                     
     bool PreserveFramePointer                     = false                                  {pd 
   size_t PretenureSizeThreshold                   = 0                                         
     bool PrintClassHistogram                      = false                                  {manageable}  
     bool PrintCodeCache                           = false                                     
     bool PrintCodeCacheOnCompilation              = false                                     
     bool PrintCommandLineFlags                    = false     //打印 命令号参数  
     bool PrintCompilation                         = false                                     
     bool PrintConcurrentLocks                     = false                                  {manageable}  
     bool PrintExtendedThreadInfo                  = false                                     
     bool PrintFlagsFinal                          = false                                     
     bool PrintFlagsInitial                        = false                                     
     bool PrintFlagsRanges                         = false                                     
     bool PrintGC                                  = false                                     
     bool PrintGCDetails                           = false                                     
     bool PrintHeapAtSIGBREAK                      = true                                      
     bool PrintSharedArchiveAndExit                = false                                     
     bool PrintSharedDictionary                    = false                                     
     bool PrintStringTableStatistics               = false                                     
     bool PrintTieredEvents                        = false                                     
     bool PrintVMOptions                           = false                                     
     bool PrintVMQWaitTime                         = false                                     
     bool PrintWarnings                            = true                                      
    uintx ProcessDistributionStride                = 4                                         
     bool ProfileInterpreter                       = true                                   {pd 
     intx ProfileMaturityPercentage                = 20                                        
    uintx ProfiledCodeHeapSize                     = 23068672                               {pd 
    uintx PromotedPadding                          = 3                                         
    uintx QueuedAllocationWarningCount             = 0                                         
      int RTMRetryCount                            = 5                                    {ARCH 
     bool RangeCheckElimination                    = true                                      
     bool ReassociateInvariants                    = true                                   {C2 
     bool ReduceBulkZeroing                        = true                                   {C2 
     bool ReduceFieldZeroing                       = true                                   {C2 
     bool ReduceInitialCardMarks                   = true                                   {C2 
     bool ReduceSignalUsage                        = false                                     
     intx RefDiscoveryPolicy                       = 0                                         
     bool RegisterFinalizersAtInit                 = true                                      
     bool RelaxAccessControlCheck                  = false                                     
    ccstr ReplayDataFile                           =                                           
     bool RequireSharedSpaces                      = false                                     
    uintx ReservedCodeCacheSize                    = 50331648                               {pd 
     bool ResizePLAB                               = true                                      
     bool ResizeTLAB                               = true                                   {pd 
     bool RestoreMXCSROnJNICalls                   = false                                     
     bool RestrictContended                        = true                                      
     bool RestrictReservedStack                    = true                                      
     bool RewriteBytecodes                         = true                                   {pd 
     bool RewriteFrequentPairs                     = true                                   {pd 
     bool SafepointTimeout                         = false                                     
     intx SafepointTimeoutDelay                    = 10000                                     
     bool ScavengeBeforeFullGC                     = true                                      
     bool SegmentedCodeCache                       = false                                     
     intx SelfDestructTimer                        = 0                                         
    ccstr SharedArchiveConfigFile                  =                                           
    ccstr SharedArchiveFile                        =                                           
   size_t SharedBaseAddress                        = 34359738368                               
    ccstr SharedClassListFile                      =                                           
    uintx SharedSymbolTableBucketSize              = 4                                         
     bool ShowCodeDetailsInExceptionMessages       = false                                  {manageable}  
     bool ShowMessageBoxOnError                    = false                                     
     bool ShrinkHeapInSteps                        = true                                      
   size_t SoftMaxHeapSize                          = 0                                      {manageable}  
     intx SoftRefLRUPolicyMSPerMB                  = 1000                                      
     bool SplitIfBlocks                            = true                                   {C2 
     intx StackRedPages                            = 1                                      {pd 
     intx StackReservedPages                       = 1                                      {pd 
     intx StackShadowPages                         = 20                                     {pd 
     bool StackTraceInThrowable                    = true                                      
     intx StackYellowPages                         = 2                                      {pd 
    uintx StartAggressiveSweepingAt                = 10                                        
     bool StartAttachListener                      = false                                     
    ccstr StartFlightRecording                     =                                           
     bool StressLdcRewrite                         = false                                     
    uintx StringDeduplicationAgeThreshold          = 3                                         
    uintx StringTableSize                          = 65536                                     
     bool SuperWordLoopUnrollAnalysis              = true                                {C2 pd 
     bool SuperWordReductions                      = true                                   {C2 
     bool SuppressFatalErrorMessage                = false                                     
    uintx SurvivorPadding                          = 3                                         
    uintx SurvivorRatio                            = 8                                         
     intx SuspendRetryCount                        = 50                                        
     intx SuspendRetryDelay                        = 5                                         
    uintx TLABAllocationWeight                     = 35                                        
    uintx TLABRefillWasteFraction                  = 64                                        
   size_t TLABSize                                 = 0                                         
     bool TLABStats                                = true                                      
    uintx TLABWasteIncrement                       = 4                                         
    uintx TLABWasteTargetPercent                   = 1                                         
    uintx TargetPLABWastePct                       = 10                                        
    uintx TargetSurvivorRatio                      = 50                                        
    uintx TenuredGenerationSizeIncrement           = 20                                        
    uintx TenuredGenerationSizeSupplement          = 80                                        
    uintx TenuredGenerationSizeSupplementDecay     = 2                                         
     intx ThreadPriorityPolicy                     = 0                                         
     bool ThreadPriorityVerbose                    = false                                     
     intx ThreadStackSize                          = 1024                                   {pd 
    uintx ThresholdTolerance                       = 10                                        
     intx Tier0BackedgeNotifyFreqLog               = 10                                        
     intx Tier0InvokeNotifyFreqLog                 = 7                                         
     intx Tier0ProfilingStartPercentage            = 200                                       
     intx Tier23InlineeNotifyFreqLog               = 20                                        
     intx Tier2BackEdgeThreshold                   = 0                                         
     intx Tier2BackedgeNotifyFreqLog               = 14                                        
     intx Tier2CompileThreshold                    = 0                                         
     intx Tier2InvokeNotifyFreqLog                 = 11                                        
     intx Tier3AOTBackEdgeThreshold                = 120000                                    
     intx Tier3AOTCompileThreshold                 = 15000                                     
     intx Tier3AOTInvocationThreshold              = 10000                                     
     intx Tier3AOTMinInvocationThreshold           = 1000                                      
     intx Tier3BackEdgeThreshold                   = 60000                                     
     intx Tier3BackedgeNotifyFreqLog               = 13                                        
     intx Tier3CompileThreshold                    = 2000                                      
     intx Tier3DelayOff                            = 2                                         
     intx Tier3DelayOn                             = 5                                         
     intx Tier3InvocationThreshold                 = 200                                       
     intx Tier3InvokeNotifyFreqLog                 = 10                                        
     intx Tier3LoadFeedback                        = 5                                         
     intx Tier3MinInvocationThreshold              = 100                                       
     intx Tier4BackEdgeThreshold                   = 40000                                     
     intx Tier4CompileThreshold                    = 15000                                     
     intx Tier4InvocationThreshold                 = 5000                                      
     intx Tier4LoadFeedback                        = 3                                         
     intx Tier4MinInvocationThreshold              = 600                                       
     bool TieredCompilation                        = true                                   {pd 
     intx TieredCompileTaskTimeout                 = 50                                        
     intx TieredRateUpdateMaxTime                  = 25                                        
     intx TieredRateUpdateMinTime                  = 1                                         
     intx TieredStopAtLevel                        = 4                                         
     bool TimeLinearScan                           = false                                  {C1 
    ccstr TraceJVMTI                               =                                           
     bool TraceSuspendWaitFailures                 = false                                     
     intx TrackedInitializationLimit               = 50                                     {C2 
     bool TrapBasedNullChecks                      = false                                  {pd 
     bool TrapBasedRangeChecks                     = false                               {C2 pd 
     intx TypeProfileArgsLimit                     = 2                                         
    uintx TypeProfileLevel                         = 111                                    {pd 
     intx TypeProfileMajorReceiverPercent          = 90                                     {C2 
     intx TypeProfileParmsLimit                    = 2                                         
     intx TypeProfileWidth                         = 2                                         
     intx UnguardOnExecutionViolation              = 0                                         
     bool UseAES                                   = false                                     
     intx UseAVX                                   = 3                                    {ARCH 
     bool UseAdaptiveGCBoundary                    = false                                     
     bool UseAdaptiveGenerationSizePolicyAtMajorCollection  = true                             
     bool UseAdaptiveGenerationSizePolicyAtMinorCollection  = true                             
     bool UseAdaptiveNUMAChunkSizing               = true                                      
     bool UseAdaptiveSizeDecayMajorGCCost          = true                                      
     bool UseAdaptiveSizePolicy                    = true                                      
     bool UseAdaptiveSizePolicyFootprintGoal       = true                                      
     bool UseAdaptiveSizePolicyWithSystemGC        = false                                     
     bool UseAddressNop                            = false                                {ARCH 
     bool UseBASE64Intrinsics                      = false                                     
     bool UseBMI1Instructions                      = false                                {ARCH 
     bool UseBMI2Instructions                      = false                                {ARCH 
     bool UseBiasedLocking                         = true                                      
     bool UseBimorphicInlining                     = true                                   {C2 
     bool UseBsdPosixThreadCPUClocks               = true                                      
     bool UseCLMUL                                 = false                                {ARCH 
     bool UseCMoveUnconditionally                  = false                                  {C2 
     bool UseCodeAging                             = true                                      
     bool UseCodeCacheFlushing                     = true                                      
     bool UseCompiler                              = true                                      
     bool UseCompressedClassPointers               = false                                {lp64_
     bool UseCompressedOops                        = false                                {lp64_
     bool UseCondCardMark                          = false                                     
     bool UseCountLeadingZerosInstruction          = false                                {ARCH 
     bool UseCountTrailingZerosInstruction         = false                                {ARCH 
     bool UseCountedLoopSafepoints                 = false                                  {C2 
     bool UseCounterDecay                          = true                                      
     bool UseDivMod                                = true                                   {C2 
     bool UseDynamicNumberOfCompilerThreads        = true                                      
     bool UseDynamicNumberOfGCThreads              = true                                      
     bool UseFMA                                   = false                                     
     bool UseFPUForSpilling                        = false                                  {C2 
     bool UseFastJNIAccessors                      = true                                      
     bool UseFastStosb                             = false                                {ARCH 
     bool UseG1GC                                  = false                                     
     bool UseGCOverheadLimit                       = true                                      
     bool UseHeavyMonitors                         = false                                     
     bool UseInlineCaches                          = true                                      
     bool UseInterpreter                           = true                                      
     bool UseJumpTables                            = true                                   {C2 
     bool UseLWPSynchronization                    = true                                      
     bool UseLargePages                            = false                                  {pd 
     bool UseLargePagesInMetaspace                 = false                                     
     bool UseLargePagesIndividualAllocation        = false                                  {pd 
     bool UseLoopCounter                           = true                                      
     bool UseLoopInvariantCodeMotion               = true                                   {C1 
     bool UseLoopPredicate                         = true                                   {C2 
     bool UseMaximumCompactionOnSystemGC           = true                                      
     bool UseNUMA                                  = false                                     
     bool UseNUMAInterleaving                      = false                                     
     bool UseNewLongLShift                         = false                                {ARCH 
     bool UseNotificationThread                    = true                                      
     bool UseOSErrorReporting                      = false                                  {pd 
     bool UseOnStackReplacement                    = true                                   {pd 
     bool UseOnlyInlinedBimorphic                  = true                                   {C2 
     bool UseOprofile                              = false                                     
     bool UseOptoBiasInlining                      = true                                   {C2 
     bool UsePSAdaptiveSurvivorSizePolicy          = true                                      
     bool UseParallelGC                            = false                                     
     bool UseParallelOldGC                         = false                                     
     bool UsePerfData                              = true                                      
     bool UsePopCountInstruction                   = false                                     
     bool UseProfiledLoopPredicate                 = true                                   {C2 
     bool UseRDPCForConstantTableBase              = false                                  {C2 
     bool UseRTMDeopt                              = false                                {ARCH 
     bool UseRTMLocking                            = false                                {ARCH 
     bool UseSHA                                   = false                                     
     intx UseSSE                                   = 99                                        
     bool UseSSE42Intrinsics                       = false                                {ARCH 
     bool UseSerialGC                              = false                                     
     bool UseSharedSpaces                          = true                                      
     bool UseSignalChaining                        = true                                      
     bool UseStoreImmI16                           = true                                 {ARCH 
     bool UseStringDeduplication                   = false                                     
     bool UseSubwordForMaxVector                   = true                                   {C2 
     bool UseSuperWord                             = true                                   {C2 
     bool UseTLAB                                  = true   // 是否使用本地线程分配缓冲（Thread Local Allocation Buffer, TLAB）           
     {pd 
     bool UseThreadPriorities                      = true                                   {pd 
     bool UseTypeProfile                           = true                                      
     bool UseTypeSpeculation                       = true                                   {C2 
     bool UseUnalignedLoadStores                   = false                                {ARCH 
     bool UseVectorCmov                            = false                                  {C2 
     bool UseXMMForArrayCopy                       = false                                     
     bool UseXMMForObjInit                         = false                                {ARCH 
     bool UseXmmI2D                                = false                                {ARCH 
     bool UseXmmI2F                                = false                                {ARCH 
     bool UseXmmLoadAndClearUpper                  = true                                 {ARCH 
     bool UseXmmRegToRegMoveAll                    = false                                {ARCH 
     intx VMThreadPriority                         = -1                                        
     intx VMThreadStackSize                        = 1024                                   {pd 
     intx ValueMapInitialSize                      = 11                                     {C1 
     intx ValueMapMaxLoopSize                      = 8                                      {C1 
     intx ValueSearchLimit                         = 1000                                   {C2 
     bool VerifyMergedCPBytecodes                  = true                                      
     bool VerifySharedSpaces                       = false                                     
    uintx YoungGenerationSizeIncrement             = 20                                        
    uintx YoungGenerationSizeSupplement            = 80                                        
    uintx YoungGenerationSizeSupplementDecay       = 8                                         
   size_t YoungPLABSize                            = 4096                                      
     bool ZeroTLAB                 
```

##### 常用参数

![image-20201224003806123](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd5dheicj31b90l9n9r.jpg)

###### 元空间

![image-20201224005802737](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd5531oaj30rv05ztbi.jpg)



##### 垃圾回收日志

###### GC

![image-20201224011314901](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd53i1lej31e30e3qic.jpg)



###### FULL GC

![image-20201224011734242](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd51zyqaj31e30e3qic.jpg)



![image-20201224011857436](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd4vzxioj30h306wtac.jpg)



##### <b>**垃圾回收器分类** <b>

![image-20201224035726419](https://tva1.sinaimg.cn/large/0081Kckwgy1glyfa2lklhj31790kqqd0.jpg)

- ###### 串行(新生代) 效率高

![image-20201224040708476](https://tva1.sinaimg.cn/large/0081Kckwgy1glyfk4w3g2j31an01zt9s.jpg)

![image-20201224045158198](https://tva1.sinaimg.cn/large/0081Kckwgy1glygutevbaj31bx0izalc.jpg)

- 并行

多个垃圾回收器，也会暂停用户服务，停顿短，适合交互小的环境

- CMS

![image-20201224041423726](https://tva1.sinaimg.cn/large/0081Kckwgy1glyfrp0p05j319y0j4n4c.jpg)

![image-20201224063001840](https://tva1.sinaimg.cn/large/0081Kckwgy1glyjouw4ztj311g0hcgvk.jpg)

四部

![image-20201224063532622](https://tva1.sinaimg.cn/large/0081Kckwgy1glyjuk3nndj30oj09aacf.jpg)

![image-20201224064004987](https://tva1.sinaimg.cn/large/0081Kckwgy1glyjz9pqvvj30qw03smye.jpg)

![image-20201224063933096](https://tva1.sinaimg.cn/large/0081Kckwgy1glyjypsnldj30x6042myq.jpg)

![image-20201224063911568](https://tva1.sinaimg.cn/large/0081Kckwgy1glyjycp8sgj313d05wn05.jpg)

![image-20201224064153702](https://tva1.sinaimg.cn/large/0081Kckwgy1glyk187548j30vo076ae5.jpg)

![image-20201224064127697](https://tva1.sinaimg.cn/large/0081Kckwgy1glyk0quxwvj31380hiwvf.jpg)

![image-20201224064318903](https://tva1.sinaimg.cn/large/0081Kckwgy1glyk2n5mptj30sy060gnj.jpg)

![image-20201224064343708](https://tva1.sinaimg.cn/large/0081Kckwgy1glyk3383qvj314u06ljww.jpg)

![image-20201224064515859](https://tva1.sinaimg.cn/large/0081Kckwgy1glyk4ofnrsj3152050gqi.jpg)



- G1 -XX:+UserG1GC

![image-20201224053441589](https://tva1.sinaimg.cn/large/0081Kckwgy1glyi3a7zqvj31bv0lnk75.jpg)

![image-20201224053525931](https://tva1.sinaimg.cn/large/0081Kckwgy1glyi42a4hqj311r0blth6.jpg)

![image-20201224053903624](https://tva1.sinaimg.cn/large/0081Kckwgy1glyi7v0q1rj31dh0boqgq.jpg)

###### G1 特点

![image-20201224054135894](https://tva1.sinaimg.cn/large/0081Kckwgy1glyiah3rotj31dx0b1nce.jpg)

![image-20201224054957061](https://tva1.sinaimg.cn/large/0081Kckwgy1glyij5b090j31d808ewqg.jpg)

![image-20201224055038133](https://tva1.sinaimg.cn/large/0081Kckwgy1glyijw41n9j31c10le18v.jpg)

![image-20201224055446740](https://tva1.sinaimg.cn/large/0081Kckwgy1glyio6qc7dj30oc0a77fv.jpg)

回收步骤

![image-20201224055619889](https://tva1.sinaimg.cn/large/0081Kckwgy1glyipt06nvj31850kvk85.jpg)

 ![image-20201224055903722](https://tva1.sinaimg.cn/large/0081Kckwgy1glyismwt3wj30xs0h3akt.jpg)

G1参数

![image-20201224060405908](https://tva1.sinaimg.cn/large/0081Kckwgy1glyixu091wj316y09d795.jpg)

![image-20201224060437893](https://tva1.sinaimg.cn/large/0081Kckwgy1glyiye8gzgj317c09oq86.jpg)

G1和CMS相比的优势

![image-20201224060734257](https://tva1.sinaimg.cn/large/0081Kckwgy1glyj1ghm5fj30zf096jvb.jpg)

- ZMS



![image-20201224043936479](https://tva1.sinaimg.cn/large/0081Kckwgy1glyghxb6yhj30vj0bqwkq.jpg)

![image-20201224044339243](https://tva1.sinaimg.cn/large/0081Kckwgy1glygm4s5hhj30pp0edwkp.jpg)



![image-20201224044909558](https://tva1.sinaimg.cn/large/0081Kckwgy1glygrv0etaj30we07ntcp.jpg)

![image-20201224050020026](https://tva1.sinaimg.cn/large/0081Kckwgy1glyh3i1bh7j317t0a2jxv.jpg)

##### 选用

![image-20201224052137957](https://tva1.sinaimg.cn/large/0081Kckwgy1glyhpnmwwoj30pb0c2wjl.jpg)

![image-20201224052154761](https://tva1.sinaimg.cn/large/0081Kckwgy1glyhpyko42j31cv0b9n5x.jpg)

#### 引用

![image-20201224014806843](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd4soa5tj30nw0bt0ui.jpg)



##### 强引用

![image-20201224015013914](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd4mp6ryj31df0erdud.jpg)

![image-20201224015217047](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd4gywluj30fn07waci.jpg)

##### 软引用

 

![image-20201224015906836](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd4dsig1j30py0eun2l.jpg)

弱引用

![image-20201224020232955](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd4afes9j317s087jve.jpg)

应用场景

![image-20201224021353127](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd47093vj31bz0jwgxw.jpg)

##### 虚引用

![image-20201224023036081](https://tva1.sinaimg.cn/large/0081Kckwgy1glycrrhby8j31dh0kmwxn.jpg)

对象回收监控

![image-20201224023612720](https://tva1.sinaimg.cn/large/0081Kckwgy1glycxjd2tdj30za0jfak0.jpg)

![image-20201224024054975](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd2gbhp1j311k0lsk29.jpg)



### GC Root 四大引用总结

![image-20201224024450710](https://tva1.sinaimg.cn/large/0081Kckwgy1glyd6ikejxj31170kon2j.jpg)

### OOM  outOfMemery

#### 1 java.lang.StackOverflowError

![image-20201224025125632](https://tva1.sinaimg.cn/large/0081Kckwgy1glyddd1h3qj30je0hatda.jpg)

深度加载 栈内存溢出



![image-20201224025510031](https://tva1.sinaimg.cn/large/0081Kckwgy1glydh8sw0qj30m20dgq4o.jpg)

#### 2 堆错误

![image-20201224025644594](https://tva1.sinaimg.cn/large/0081Kckwgy1glydiw0bkfj316c0clado.jpg)

#### 3 垃圾回收 error

![image-20201224030134685](https://tva1.sinaimg.cn/large/0081Kckwgy1glydo7wqj1j30zi0ien5c.jpg)

![image-20201224030601214](https://tva1.sinaimg.cn/large/0081Kckwgy1glydsjz0o7j30l60dvae2.jpg)

#### 4 java.lang.OutofMemmoryError：Ditect buffer memory

![image-20201224031308267](/Users/admin/Library/Application Support/typora-user-images/image-20201224031308267.png)

![image-20201224031818967](https://tva1.sinaimg.cn/large/0081Kckwgy1glye5c3n4lj31a206vtb7.jpg)

![image-20201224032030352](https://tva1.sinaimg.cn/large/0081Kckwgy1glye7mljbcj30yu0i943m.jpg)

#### 5. java.lang.OutofMemmoryError：unable to create new native thread

一个应用 默认最大 1024个线程

![image-20201224032928573](https://tva1.sinaimg.cn/large/0081Kckwgy1glyegyqkpoj31780d87fo.jpg)

6 java.lang.OutofMemmoryError：Metaspace

![image-20201224034554199](https://tva1.sinaimg.cn/large/0081Kckwgy1glyey2tgixj31540hywpv.jpg)



### 系统变慢

1. top cup
2. uptime
3. vmstat -n 2 3 

![image-20201224065302142](https://tva1.sinaimg.cn/large/0081Kckwgy1glykcrblvdj31bg0kodj7.jpg)

![image-20201224065512670](https://tva1.sinaimg.cn/large/0081Kckwgy1glykf47vewj31b90jr18y.jpg)

## JAVASE

### enum

```java 
package testenum;

import lombok.Getter;

/**
 * @ProjectName: java_basic
 * @Package: testenum
 * @ClassName: Enum
 * @Author: WQM
 * @Description: 枚举
 * @Date: 2020/12/23 7:16 上午
 * @Version: 1.0
 */
public enum EnumTest {
    ONE(1, "齐国"), TWO(1, "赵国"), THREE(3, "楚国");

    @Getter
    private Integer retCoder;
    @Getter
    private Integer retMessage;
    @Getter
    private Integer retMessage2;


    EnumTest(Integer retCoder, String retMessage) {
    }

    public static EnumTest forEach(int index) {
        EnumTest[] lists = EnumTest.values();
        for (EnumTest e : lists) {
            if (index == e.retCoder) {
                return e;
            }
        }
        return null;
    }

}
```

根据id或名字获取版

```java
package sigleton;

import lombok.Getter;

/**
 * @ProjectName: java_basic
 * @Package: sigleton
 * @ClassName: Singleton_Enmu
 * @Author: WQM
 * @Description: 枚举单例
 * @Date: 2020/12/24 4:14 下午
 * @Version: 1.0
 */
public enum Singleton_Enum {
    QI(1, "齐国"), CHU(2, "楚国"), YAN(3, "燕国"), HAN(4, "韩国"),
    ZHAO(5, "赵国"), WEI(6, "魏国"), QIN(7, "秦国");
    @Getter
    private Integer id; 
    @Getter
    private String name; 
    //枚举构造
    Singleton_Enum(Integer id, String name) {
    }

    @Override
    public String toString() {
        return super.toString();
    } 
    //遍历获取
    public static Singleton_Enum get(Object id) {
        Singleton_Enum[] list = Singleton_Enum.values();
        Boolean Flag = false;//默认根据 名字查找
        //System.out.println(id.getClass().getName());
        if (id.getClass().getName() == "java.lang.Integer") {
            Flag = true;
        }
        for (Singleton_Enum e : list
        ) {
            //编号查找
            if (Flag && e.ordinal() == (Integer) id) {
                return e;
            } //名字查找
            else if (!Flag && !(id == null) && e.name().equals(id)) {
                return e;
            }
        }
        return null;//没有找到
    }

}
```