# 德格|第 1 集(简介及应用)

> 原文:[https://www . geesforgeks . org/deque-set-1-introduction-applications/](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)

[去重或双端队列](http://en.wikipedia.org/wiki/Double-ended_queue)是[队列数据结构](https://www.geeksforgeeks.org/queue-set-1introduction-and-array-implementation/)的一般化版本，允许在两端插入和删除。

**对德客的操作:**
主要对队列进行以下四种基本操作:

***【插入前置】(*** :在德清前面增加一项。
***【插入最后一个】(*** ):在得球后方增加一个物品。
***【删除前置】(*** ):从德格的前置删除一个项目。
***删除最后一个()*** :从德格后方删除一个项目。

除以上操作外，还支持以下操作:
***【getFront()***:从队列中获取前置项。
***getRear()*** :从队列中获取最后一个项目。
***isEmpty()***:检查德格是否为空。
***is full()***:检查德格是否已满。

**得克的应用:**
由于得克同时支持堆栈和队列操作，所以可以兼而有之。Deque 数据结构支持 O(1)时间内的顺时针和逆时针旋转，这在某些应用中非常有用。
此外，需要在两端移除和/或添加元素的问题可以使用德克尔有效地解决。例如参见[大小为 k 的所有子阵列的最大值问题。](https://www.geeksforgeeks.org/maximum-of-all-subarrays-of-size-k/)、 [0-1 BFS](https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/) 、[找到第一个参观所有汽油泵](https://www.geeksforgeeks.org/find-a-tour-that-visits-all-stations/)的循环游。

参见 [wiki 页面](http://en.wikipedia.org/wiki/Double-ended_queue#Applications)的另一个 A-steak 作业调度算法的例子，其中使用了 Deque，因为两端都需要删除操作。

**语言支持:**
C++ STL 提供了德客作为 [std::德客](https://www.geeksforgeeks.org/deque-cpp-stl/)的实现，Java 提供了[德客接口](https://www.geeksforgeeks.org/deque-interface-java-example/)。详见[本](http://en.wikipedia.org/wiki/Double-ended_queue#Language_support)。
Java 中的[德格](https://www.geeksforgeeks.org/deque-interface-java-example/)
Python 中的[德格](https://www.geeksforgeeks.org/deque-in-python/)

**实现:**
可以使用[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)或者圆形数组来实现一个德格。在这两种实现中，我们都可以在 O(1)时间内实现所有操作。我们将很快讨论德奎数据结构的 C/C++实现。

 **[使用圆形数组](https://www.geeksforgeeks.org/implementation-deque-using-circular-array/)** 
实现德清如果发现以上代码/算法不正确，请写评论，或者找其他方法解决同样的问题。