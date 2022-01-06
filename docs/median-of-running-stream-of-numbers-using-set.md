# 连续数字流的中位数–(使用集合)

> 原文:[https://www . geeksforgeeks . org/使用集合的运行数字流中位数/](https://www.geeksforgeeks.org/median-of-running-stream-of-numbers-using-set/)

假设从数据流中读取整数。求从第一个整数开始到最后一个整数为止读取的所有元素的中值。这也被称为运行整数的中位数。
给定的[链接](https://www.geeksforgeeks.org/median-of-stream-of-running-integers-using-stl/)已经包含了使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)解决此问题的方案。
然而，下面的解决方案使用了相同的概念，但是实现是通过使用集合。
在这个解决方案中，我们将打印偶数长度情况下较小的中间值，而不是取它们的平均值。

**示例:**

> **输入:** arr[] = {-10，14，11，-5，7}
> **输出:** -10 -10 11 -5 7
> 
> **输入:** arr[] = {2，-5，14 }
> T3】输出: 2 -5 2

**进场:**

*   按升序创建两个多集 **g** ，将存储上半部分，按降序创建两个多集 **s** ，将存储数组的下半部分 **arr[]** 。
*   将第一个元素插入 **s** 。并用这个值初始化中位数。
*   对于数组的每隔一个元素 **x** 。检查两组的尺寸:
    *   当**尺寸>尺寸(g)** 时:如果 **x >中值**那么将 **s** 的第一个元素插入 **g** 和**从 **s** 中移除**那个元素，将 **x** 插入 **s** 中。否则将 **x** 插入 **g** 。
    *   当**尺寸<尺寸(g)** 时:如果 **x <中值**，则将 **g** 的第一个元素插入 **s** 和**中，从 **g** 中移除**那个元素，将 **x** 插入 **g** 中。否则将 **x** 插入 **s** 。
    *   当**尺寸(s) =尺寸(g)** 时:如果 **x >中间值**。将 **x** 插入 **s** 。否则将 **x** 插入 **g** 。

下面是上述方法的实现:

```
// C++ program to find running median for 
// a stream of integers using Set
#include <bits/stdc++.h>
using namespace std;

// Function to print the running median 
// for the array arr[]
void printRunningMedian(int arr[], int n)
{
    // Multiset is used to handle duplicates
    // Multiset g for storing upper half 
    // (ascending order)
    // The first element will be the smallest)
    multiset<int> g;

    // Multiset s for storing lower half 
    // (descending order). The first element 
    // will be the largest
    multiset<int, greater<int> > s;

    s.insert(arr[0]);

    // Initialise median with the first element
    int med = arr[0];
    printf("%d ", med);

    for (int i = 1; i < n; i++) {

        // Only add elements to upper half if 
        // its size less then the size of the
        // lower half (maintain only difference
        // of 1)
        if (s.size() > g.size()) {
            if (arr[i] < med) {
                int temp = *s.begin();
                s.erase(s.begin());
                g.insert(temp);
                s.insert(arr[i]);
            }
            else
                g.insert(arr[i]);

            med = *s.begin() > *g.begin() ?
                   *g.begin() : *s.begin();
        }

        // Only add elements to lower half if 
        // it's size less then the size of the 
        // upper half (maintain only difference
        // of 1)
        else if (s.size() < g.size()) {
            if (arr[i] > med) {
                int temp = *g.begin();
                g.erase(g.begin());
                s.insert(temp);
                g.insert(arr[i]);
            }
            else
                s.insert(arr[i]);

            med = *s.begin() > *g.begin() ? 
                   *g.begin() : *s.begin();
        }

        // If sizes are same
        else {
            if (arr[i] > med) {
                g.insert(arr[i]);
                med = *g.begin();
            }
            else {
                s.insert(arr[i]);
                med = *s.begin();
            }
        }

        printf("%d ", med);
    }

    printf("\n");
}

// Driver code
int main()
{
    int arr[] = { -10, 14, 11, -5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printRunningMedian(arr, n);
    return 0;
}
```

**Output:**

```
-10 -10 11 -5 7

```