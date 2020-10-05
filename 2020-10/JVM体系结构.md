1. **JVM体系结构**

![image-20200313104338985](C:\Users\70790\AppData\Roaming\Typora\typora-user-images\image-20200313104338985.png)

![image-20200313104554468](C:\Users\70790\AppData\Roaming\Typora\typora-user-images\image-20200313104554468.png)

**2.Native 、方法区**

- Native调用底层C语言的库，调用本地方法接口（JNI）

- **方法区**

  方法区被所有线程共享，所有字段和方法字节码，以及一些特殊方法，如构造函数，接口代码也在此定义，简单说，所有定义的方法的信息都保存在该区域，此区域属于共享空间。

  静态变量、常量、类信息（构造方法、接口定义）、运行时的常量池存在方法区中，但是实例变量存在堆内存中，和方法区无关。

![image-20200313110113446](C:\Users\70790\AppData\Roaming\Typora\typora-user-images\image-20200313110113446.png)

3. **深入理解 栈**

   ​    栈：栈内存，主管程序的运行，生命周期和线程同步，线程结束，栈内存也就释放，对于栈来说，不存在垃圾回收的问题。

   ​	栈：8大基本类型+对象引用+实例的方法

4. 堆

   一个JVM只有一个堆。

   ![image-20200313112935764](C:\Users\70790\AppData\Roaming\Typora\typora-user-images\image-20200313112935764.png)

5. GC回收算法

   - 复制算法：适用于对象存活度较低的场景
   - 标记清除算法：两次扫描，存在碎片
   - 标记压缩算法：多了一次移动，没有内存碎片





- jvm虚拟机是什么   .java=>.class=>
- 双亲委派机制：类加载 application class loader => extensions class loader bootstrapclassloader  如果已经加载过，则不需要重新加载。作用：保护java本身的类对象不被修改
- 沙箱安全机制：代码安全检查
- JVM内存模型
- 新生代
- 幸存区01
- 幸存区02
- 老年代
- 永久区（元空间）
- GC回收策略
- 引用计数法
- 复制算法
- 标记压缩清除算法