## ThreadLocal原理

1. 作用：线程私有，保证多线程是访问安全

2. 应用场景：

   - 线程执行过程中多次引用到同一个变量
   - 多线程隔离

3. 原理：ThreadLocal 作为 每个线程成员变量ThreadLocals(ThreadLocalMap)的key，获取对应的value

   