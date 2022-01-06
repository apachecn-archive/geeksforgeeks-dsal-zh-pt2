# 二进制插入排序的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-for-binary-insert-sort/](https://www.geeksforgeeks.org/c-program-for-binary-insertion-sort/)

我们可以使用二分搜索法减少[正常插入排序](https://www.geeksforgeeks.org/insertion-sort/)中的比较次数。二进制插入排序查找使用二分搜索法查找在每次迭代中插入所选项目的正确位置。
在正常插入中，排序在最坏的情况下需要 O(i)(第一次迭代)。我们可以通过使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)将其减少到 0(logi)。

## C/C++

## C

```
// C program for implementation of binary insertion sort
#include <stdio.h>

// A binary search based function to find the position
// where item should be inserted in a[low..high]
int binarySearch(int a[], int item, int low, int high)
{
    if (high <= low)
        return (item > a[low])?  (low + 1): low;

    int mid = (low + high)/2;

    if(item == a[mid])
        return mid+1;

    if(item > a[mid])
        return binarySearch(a, item, mid+1, high);
    return binarySearch(a, item, low, mid-1);
}

// Function to sort an array a[] of size \'n\'
void insertionSort(int a[], int n)
{
    int i, loc, j, k, selected;

    for (i = 1; i < n; ++i)
    {
        j = i - 1;
        selected = a[i];

        // find location where selected should be inserted
        loc = binarySearch(a, selected, 0, j);

        // Move all elements after location to create space
        while (j >= loc)
        {
            a[j+1] = a[j];
            j--;
        }
        a[j+1] = selected;
    }
}

// Driver program to test above function
int main()
{
    int a[] = {37, 23, 0, 17, 12, 72, 31,
              46, 100, 88, 54};
    int n = sizeof(a)/sizeof(a[0]), i;

    insertionSort(a, n);

    printf("Sorted array: \n");
    for (i = 0; i < n; i++)
        printf("%d ",a[i]);

    return 0;
}
```

更多详情请参考[二进制插入排序](https://www.geeksforgeeks.org/binary-insertion-sort/)整篇文章！