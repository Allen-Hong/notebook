## **HashMap JDK1.8实现原理

#### HashMap概述

- key-value 键值对，key允许null，value允许null。
- 内部结构为 **数据+链表**。
- JDK1.8中 链表长度到达阀值（默认是8），就会将链表转换为红黑二叉树。

#### HashMap数据结构

- hashMap是通过hash值得高16位和低16位异或操作后对capacity（容量）取模得到索引位置，即key.hashcode()^(hashcode>>>16)%capacity，当capacity为2^n时，key.hashcode()^(hashcode>>>16)%capacity值等于key.hashcode()^(hashcode>>>16)&(capacity-1)，因为&运算比%运算效率高，所以采用2的次幂作为capacity的默认值。

- 在**扩容**时，如果length的每次是2^n，那么重新计算出来的索引只有一种是 原索引+16，另一种是索引不变，所以就不需要重新计算索引。

  ![](C:\Users\70790\Pictures\博客\hashMap扩容机制.png)

