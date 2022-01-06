# 如何让 Mergesort 在最佳情况下进行 O(n)比较？

> 原文:[https://www . geesforgeks . org/make-merge sort-perform-comparison-best-case/](https://www.geeksforgeeks.org/make-mergesort-perform-comparisons-best-case/)

正如我们所知， [Mergesort](https://www.geeksforgeeks.org/merge-sort/) 是一种[分治算法](https://www.geeksforgeeks.org/divide-and-conquer-introduction/)，它递归地将数组分成两半，直到它达到 1 大小的数组，然后它合并排序后的子数组，直到原始数组完全排序。[合并排序的典型实现](https://www.geeksforgeeks.org/merge-sort/)在所有三种情况下(最佳、平均和最差)都在 O(n Log n)时间内工作。

我们需要将最佳案例性能从 O(n log n)降低到 O(n)。

想法是考虑数组已经排序的情况。在合并之前，只需检查 arr[mid] > arr[mid+1]，因为我们处理的是已排序的子数组。这就引出了递归关系 T(n) = 2*T(n/2) + 1，可以用[大师定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)求解，所以 T(n) = n。

示例:

```
Input : 1 2 3 4
Subarrays with size of 1:|1||2| |3||4|
Subarrays with size of 2: |1 2| |3 4|
Output : 1 2 3 4

Input : 1 2 3 4 5 6 7 8 
        Subarrays with size of 1: |1||2| |3||4| |5||6| |7||8|
        Subarrays with size of 2: |1 2| |3 4| |5 6| |7 8|
        Subarrays with size of 4: |1 2 3 4| |5 6 7 8|
Output : 1 2 3 4 5 6 7 8 

```

```
// C program to implement merge sort that works
// in O(n) time in best case.
#include <stdio.h>
#include <stdlib.h>

void merge(int* arr, int low, int mid, int high);

void mergesort(int* arr, int low, int high)
{
    if (low < high) {
        int mid = (low + high) / 2;
        mergesort(arr, low, mid);
        mergesort(arr, mid + 1, high);

        // This is where we optimize for best
        // case.
        if (arr[mid] > arr[mid + 1])
            merge(arr, low, mid, high);
    }
}

void merge(int* arr, int low, int mid, int high)
{
    int i = low, j = mid + 1, k = 0;
    int* temp = (int*)calloc(high - low + 1, sizeof(int));
    while ((i <= mid) && (j <= high))
        if (arr[i] < arr[j])
            temp[k++] = arr[i++];
        else
            temp[k++] = arr[j++];
    while (j <= high) // if( i>mid )
        temp[k++] = arr[j++];
    while (i <= mid) // j>high
        temp[k++] = arr[i++];

    // copy temp[] to arr[]
    for (i = low, k = 0; i <= high; i++, k++)
        arr[i] = temp[k];
    free(temp);
}

int main()
{
    int a[] = { 1, 2, 3, 4, 5, 6, 7, 8 };
    mergesort(a, 0, 7);
    for (int i = 0; i < 8; i++)
        printf("%d ", a[i]);
    return 0;
}
```

输出:

```
 1 2 3 4 5 6 7 8

```

本文由 **[什洛米·埃尔海亚尼](https://www.facebook.com/shlomi.elhaiani)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。