# 用于分类排序的 C++程序

> 原文:[https://www . geeksforgeeks . org/CPP-program-for-pigon hole-sort/](https://www.geeksforgeeks.org/cpp-program-for-pigeonhole-sort/)

[鸽子洞排序](https://en.wikipedia.org/wiki/Pigeonhole_sort)是一种排序算法，适用于元素数量和可能键值数量大致相同的元素列表排序。
需要 O( *n* + *Range* )时间，其中 n 为输入数组中的元素个数，【Range】为数组中可能的值个数。

**算法工作:**

1.  在数组中查找最小值和最大值。让最小值和最大值分别为“最小值”和“最大值”。还可以找到“最大-最小-1”的范围。
2.  建立一个与范围大小相同的初始空“文件箱”数组。
3.  访问数组中的每个元素，然后将每个元素放入它的文件夹中。元素 arr[i]被放入索引 arr[I]–min 处的孔中。
4.  按顺序在鸽子洞数组上开始循环，并将非空洞的元素放回原始数组中。

```
/* C program to implement Pigeonhole Sort */
#include <bits/stdc++.h>
using namespace std;

/* Sorts the array using pigeonhole algorithm */
void pigeonholeSort(int arr[], int n)
{
    // Find minimum and maximum values in arr[]
    int min = arr[0], max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] < min)
            min = arr[i];
        if (arr[i] > max)
            max = arr[i];
    }
    int range = max - min + 1; // Find range

    // Create an array of vectors. Size of array
    // range. Each vector represents a hole that
    // is going to contain matching elements.
    vector<int> holes[range];

    // Traverse through input array and put every
    // element in its respective hole
    for (int i = 0; i < n; i++)
        holes[arr[i] - min].push_back(arr[i]);

    // Traverse through all holes one by one. For
    // every hole, take its elements and put in
    // array.
    int index = 0; // index in sorted array
    for (int i = 0; i < range; i++) {
        vector<int>::iterator it;
        for (it = holes[i].begin(); it != holes[i].end(); ++it)
            arr[index++] = *it;
    }
}

// Driver program to test the above function
int main()
{
    int arr[] = { 8, 3, 2, 7, 4, 6, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    pigeonholeSort(arr, n);

    printf("Sorted order is : ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

**Output:**

```
Sorted order is : 2 3 4 6 7 8 8

```

详情请参考[整理](https://www.geeksforgeeks.org/pigeonhole-sort/)整篇文章！