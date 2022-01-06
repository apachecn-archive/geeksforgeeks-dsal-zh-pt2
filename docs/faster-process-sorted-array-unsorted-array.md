# 为什么处理排序数组比处理未排序数组快？

> 原文:[https://www . geesforgeks . org/fast-process-sorted-array-unsorted-array/](https://www.geeksforgeeks.org/faster-process-sorted-array-unsorted-array/)

下面是一个 C++代码，说明对数据进行排序奇迹般地使代码比未排序的版本更快。让我们尝试一个示例 C++程序，以便更好地理解问题语句。

```
// CPP program to demonstrate processing
// time of sorted and unsorted array
#include <iostream>
#include <algorithm>
#include <ctime>
using namespace std;

const int N = 100001;

int main()
{
    int arr[N];

    // Assign random values to array
    for (int i=0; i<N; i++)
        arr[i] = rand()%N;

    // for loop for unsorted array
    int count = 0;
    double start = clock();
    for (int i=0; i<N; i++)
        if (arr[i] < N/2)
            count++;

    double end = clock();
    cout << "Time for unsorted array :: "
         << ((end - start)/CLOCKS_PER_SEC)
         << endl;
    sort(arr, arr+N);

    // for loop for sorted array
    count = 0;
    start = clock();

    for (int i=0; i<N; i++)
        if (arr[i] < N/2)
            count++;

    end = clock();
    cout << "Time for sorted array :: "
         << ((end - start)/CLOCKS_PER_SEC)
         << endl;

    return 0;
}
```

**输出:**

```
Execution 1:
Time for unsorted array :: 0.00108
Time for sorted array :: 0.00053

Execution 2:
Time for unsorted array :: 0.001101
Time for sorted array :: 0.000593

Execution 3:
Time for unsorted array :: 0.0011
Time for sorted array :: 0.000418

```

请注意，与未排序的数组相比，处理已排序的数组花费的时间更少。排序数组优化的原因是**分支预测。**

**什么是分支预测？**
在计算机体系结构中，分支预测意味着确定程序指令流中的条件分支(跳转)是否可能被采用。
所有流水线处理器都以某种形式进行分支预测，因为它们必须在当前指令被执行之前猜测下一条要提取的指令的地址。

**分支预测如何在上述情况下适用？**

**if** 条件检查**arr【I】<5000**，但是如果您观察到在排序数组的情况下，在传递数字 5000 之后，条件总是假的，并且在此之前它总是真的，编译器在这里优化代码并跳过 if 条件，这被称为分支预测。

**情况 1:排序数组**

```
	T = if condition true
	F = if condition false
	arr[] = {0,1,2,3,4,5,6, .... , 4999,5000,5001, ... , 100000}
            {T,T,T,T,T,T,T, .... , T,    F,   F,   ... ,    F  }	

```

我们可以观察到，预测排序数组中的分支是非常容易的，因为序列是**TTTTTTTTTTTT……fffffffffff**

**情况 2:未排序数组**

```
	T = if condition true
	F = if condition false
	arr[] = {5,0,5000,10000,17,13, ... , 3,21000,10}
	        {T,T,F,     F,   T, T, ... , T, F,    T}

```

很难预测**如果**的陈述是假还是真，因此分支预测在这里没有任何重要作用。

分支预测基于算法遵循的模式，或者基本上是历史，它在前面的步骤中是如何执行的。如果猜测正确，那么 CPU 继续执行，如果出错，那么 CPU 需要刷新流水线，回滚到分支，从头重新开始。

如果编译器不能利用分支预测作为提高性能的工具，程序员可以实现自己的黑客来提高性能。

**参考文献:**

*   [分支预测](https://simple.wikipedia.org/wiki/Branch_prediction)
*   叠置溢出
*   [计算中的流水线操作](https://en.wikipedia.org/wiki/Pipeline_%28computing%29)

本文由 [**曼德普·辛格**](https://github.com/msdeep14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。