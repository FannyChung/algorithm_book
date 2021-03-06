# 哈希

先介绍两个概念：

**hash函数**：hash函数具有以下几个特点：

1. 把无限的输入映射到有限的输出域上
2. 输入同则输出同
3. 多个不同输入可能输出同
4. 离散型，均匀分布

**hash表**：数组+链表的实现。

key--hash函数--&gt; hashcode--%size--&gt;p\(在数组中的位置\)

因为hash函数是均匀分布的，所以每个链表几乎一样长。

扩容：当链表长超过某个阈值后，需要扩容数组。每次扩容的代价为$$log_{d}N$$，其中N是样本大小，d是每次扩容的倍数。

总体来说，认为对hashset、hashmap的增删时间复杂度为O\(1\)。因为就算有扩容，也可以利用离线扩容的方式，调用者感知不到这个时间。

Java中hash表是用的数组+红黑树的方法。

