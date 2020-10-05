> 线程一共有几个状态

创建（new）

运行（runnable）

阻塞（blocked）

等待（waiting）

超时等待（timed-waiting）

终止（terminated）



**业务：普通的线程代码 Thread**

**Runnable 没有返回值、效率相比Callable相对较低！**

Java默认有几个线程：两个，main、GC

Java可以开启线程吗？不可以，需要调用底层C++代码（即本地方法）

>并发、并行

并发编程：并发、并行

并发（多线程操作同一个资源）

- CPU一核，模拟出来多条线程，快速交替

并行（多条线程同时执行）

- CPU多核，多个线程可以同时执行；线程池

并发编程的本质：**充分利用CPU资源**

>wait/sleep 区别

1. 来自不同的类

   wait => Object

   sleep => Thread

2. 关于锁的释放

   wait会释放锁，sleep不会释放锁。

3. 使用的范围不同

   wait：wait必须在同步代码块中

   sleep：可以在任何地方执行

4. 是否需要捕获异常

   wait不需要捕获异常

   sleep必须捕获异常

> Lock锁

> synchronized 和 Lock 的区别

1. Synchronized 内置的Java关键字，Lock是一个Java类
2. synchronized 会自动释放锁，lock必须手动释放锁，不释放锁会造成死锁
3. synchronized 公平锁，Lock不一定，可以通过构造参数配置
4. 都是可重入锁
5. Synchronized适合锁少量的代码，Lock适合锁大量的同步代码

>8锁现象

- synchronized 锁的是创建的对象，同一把锁，先到先得
- 不用锁之间，先到先得
- 静态的同步方法，锁的的Class类模板，静态方法间先到先得