# 梳理排序的 C++程序

> 原文:[https://www.geeksforgeeks.org/cpp-program-for-comb-sort/](https://www.geeksforgeeks.org/cpp-program-for-comb-sort/)

梳状排序主要是对冒泡排序的改进。冒泡排序总是比较相邻的值。所以所有的[反演](https://www.geeksforgeeks.org/counting-inversions/)都被一个一个的去掉了。梳状排序通过使用大于 1 的间隙改进了冒泡排序。间隙从一个大值开始，在每次迭代中缩小 1.3 倍，直到达到值 1。因此，梳状排序通过一次交换去除了多个[反转计数](https://www.geeksforgeeks.org/counting-inversions/)，并且性能优于布贝尔排序。

根据经验，收缩因子被发现为 1.3(通过在超过 200，000 个随机列表上测试组合排序)[来源: [Wiki](https://en.wikipedia.org/wiki/Comb_sort) ]

虽然，它的平均效果比冒泡排序好，但最坏的情况仍然是 O(n <sup>2</sup> )。

```
// C++ implementation of Comb Sort
#include <bits/stdc++.h>
using namespace std;

// To find gap between elements
int getNextGap(int gap)
{
    // Shrink gap by Shrink factor
    gap = (gap * 10) / 13;

    if (gap < 1)
        return 1;
    return gap;
}

// Function to sort a[0..n-1] using Comb Sort
void combSort(int a[], int n)
{
    // Initialize gap
    int gap = n;

    // Initialize swapped as true to make sure that
    // loop runs
    bool swapped = true;

    // Keep running while gap is more than 1 and last
    // iteration caused a swap
    while (gap != 1 || swapped == true) {
        // Find next gap
        gap = getNextGap(gap);

        // Initialize swapped as false so that we can
        // check if swap happened or not
        swapped = false;

        // Compare all elements with current gap
        for (int i = 0; i < n - gap; i++) {
            if (a[i] > a[i + gap]) {
                swap(a[i], a[i + gap]);
                swapped = true;
            }
        }
    }
}

// Driver program
int main()
{
    int a[] = { 8, 4, 1, 56, 3, -44, 23, -6, 28, 0 };
    int n = sizeof(a) / sizeof(a[0]);

    combSort(a, n);

    printf("Sorted array: \n");
    for (int i = 0; i < n; i++)
        printf("%d ", a[i]);

    return 0;
}
```

**Output:**

```
Sorted array: 
-44 -6 0 1 3 4 8 23 28 56

```

详情请参考[梳理](https://www.geeksforgeeks.org/comb-sort/)整篇文章！