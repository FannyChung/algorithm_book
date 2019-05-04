# 大数据与hash

大规模数据处理问题，可以用hash来进行分流。

## 查重

一个大文件，每行是字符串，无序，打印出所有重复的元素。

方法：用分布式读取并计算hashcode，然后根据hashcode%M（M为机器数量）的值来进行分流，分给不同的机器来处理。如果分给每台机器的数量仍然很多，则再次分流，在机器内进行并行处理。

## 布隆过滤器

用途：查找一个值是否在超大规模的词典中出现过。

考虑用布隆过滤器，原理是用bitmap表示词典里的所有单词，

设bitmap有m位，建立词典的bitmap：对词典里的每个元素v，根据k个hash函数得到k个hashcode，k个hashcode对m取模得到k个位置i。把bitmap这k个第i位置1。

判断目标字符串是否在词典中，方法是：同样根据k个hash找到对应的k个i，对比bitmap的这k个i位置是否都为1，如果是，则认为是在词典里。

> bitmap的实现：
>
> 可以用int数组a，一个int有32b，Int\[1000\]可以表示32000位的bitmap。而第i位的位置在a\[i/32\]的第i%32位。

当然，根据这种判断方法，可能会有误判：就算判断在词典中，实际上也可能不在词典中。

> 例子：
>
> 对于100亿的字符串词典，假设每个字符串是64B，则占用的空间为64B\*100,0000,0000=640GB。如果直接用hashset，则至少需要640G的内存。不太现实。
>
> 用布隆过滤器，如果限定失误率为0.0001，则需要的m为，内存为22.3G.

### 参数确定

主要有三个参数，err限定的误差，m是bitmap的位数，k是hash函数个数。

$$m=-\frac{n-ln{err}}{{ln2}^2}$$

$$k=ln2*\frac{m}{n}$$

$$err={\(1-e^{-\frac{n\*k}{m}}\)^k}$$
