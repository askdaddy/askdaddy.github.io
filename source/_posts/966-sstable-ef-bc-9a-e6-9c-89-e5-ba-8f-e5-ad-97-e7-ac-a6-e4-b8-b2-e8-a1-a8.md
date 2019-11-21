---
title: SSTable：有序字符串表
url: 966.html
id: 966
categories:
  - 大数据
date: 2016-04-01 14:22:33
tags:
---

假设我们有一大批数据（GB或TB量级）需要处理，处理过程可能分为好几个步骤，每个步骤必须由不同的二进制文件(程序)来处理 - 或者可以假设我们正在执行一系列的map-reduce任务！由于输入数据量很大，读取和写入数据的效率决定了运行时间。因此，不会使用随机读写，而是对数据进行流式读取，一旦处理完成，再通过流式写入将数据刷新到磁盘。通过这种方式，我们可以[分摊磁盘I / O成本](http://www.google.com/url?q=http%3A%2F%2Fwww.igvita.com%2F2009%2F06%2F23%2Fmeasuring-optimizing-io-performance%2F&sa=D&sntz=1&usg=AFQjCNGd3z4bwQu2deoTpE_5MLNGXi2XAA) 。不需要磁盘寻道，直接连续的向前写入。 有序字符串表(Sorted String Table)是包含一组任意有序键 - 值对的文件，可以很好的处理重复键，不需要额外的空间来填充(padding)键或值，并且键值可以是任意的东西。顺序的读取整个文件，就可以获得一个有序的索引。如果文件非常大，可以在前面追加或创建独立的`key:offset`索引来加速访问。这就是SSTable，一个非常简单却非常有用的交换大量有序数据片段的方式。 来源： _[图灵社区 : 阅读 : SSTable和日志结构化存储：LevelDB](http://www.ituring.com.cn/article/19383)_