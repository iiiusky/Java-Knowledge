---
description: Root Branch Leaf （ 根 枝 叶）
---

# Tree

## Binary Tree

* **描述**
  * **每个节点最多两个叶子**
* **特点**
  * **当数据量大时，树高high 会比较大，且查询会比较慢**
  * **在查询时会产生很多磁盘IO，因为遍历次数过多**
* **图示**

![](../../../.gitbook/assets/image-7.png)

* **B Tree**
* **特点**
  * 每个节点最多可以有M个叉
  * 所有节点都存储数据
* **局部性原理**
  * 当查询到一页数据，大概率会使用其附近的数据，这样**磁盘预读**能充分提高磁盘IO，避免未来磁盘IO，从而提高效率
* **如何做索引**
  * \*\*\*\*
* **图示**

![](../../../.gitbook/assets/image-26.png)

### B+ Tree

* **特点**
  * 与B Tree区别在于叶子之间增加了链表
  * 根到所有叶子的高度一样
  * 适合范围查询
* **图示**

![](../../../.gitbook/assets/image-30.png)

### 总结

* 数据库索引用于加速查询
* 虽然哈希索引是O\(1\)，树索引是O\(log\(n\)\)，但SQL有很多“有序”需求，故数据库使用树型索引
* InnoDB不支持哈希索引
* **数据预读**的思路是：磁盘读写并不是按需读取，而是按页预读，一次会读一页的数据，每次加载更多的数据，以便未来减少磁盘IO
* **局部性原理**：软件设计要尽量遵循“数据读取集中”与“使用到一个数据，大概率会使用其附近的数据”，这样磁盘预读能充分提高磁盘IO
* 数据库的索引最常用B+树：

\(1\)很适合磁盘存储，能够充分利用局部性原理，磁盘预读；

\(2\)很低的树高度，能够存储大量数据；

\(3\)索引本身占用的内存很小；

\(4\)能够很好的支持单点查询，范围查询，有序性查询；

> 参考文献
>
> [https://mp.weixin.qq.com/s/YMbRJwyjutGMD1KpI\_fS0A](https://mp.weixin.qq.com/s/YMbRJwyjutGMD1KpI_fS0A)

