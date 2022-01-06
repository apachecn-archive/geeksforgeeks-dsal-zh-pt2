# 快速排序的 C++程序

> 原文:[https://www.geeksforgeeks.org/cpp-program-for-quicksort/](https://www.geeksforgeeks.org/cpp-program-for-quicksort/)

像[合并排序](https://www.geeksforgeeks.org/merge-sort/)一样，快速排序是一种分治算法。它选取一个元素作为透视，并围绕选取的透视对给定数组进行分区。快速排序有许多不同的版本，它们以不同的方式选取轴心。

1.  始终选择第一个元素作为轴心。
2.  始终选择最后一个元素作为轴心(在下面实现)
3.  选择一个随机元素作为轴心。
4.  选择中线作为枢轴。

快速排序中的关键过程是分区()。分区的目标是，给定一个数组和数组的元素 x 作为轴心，将 x 放在排序数组中正确的位置，将所有较小的元素(小于 x)放在 x 之前，将所有较大的元素(大于 x)放在 x 之后。所有这些都应该在线性时间内完成。
**递归快速排序函数伪代码:**

```
/* low  --> Starting index,  high  --> Ending index */
quickSort(arr[], low, high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);  // Before pi
        quickSort(arr, pi + 1, high); // After pi
    }
}
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
/* C implementation QuickSort */
#include<stdio.h>

// A utility function to swap two elements
void swap(int* a, int* b)
{
    int t = *a;
    *a = *b;
    *b = t;
}

/* This function takes last element as pivot, places
   the pivot element at its correct position in sorted
    array, and places all smaller (smaller than pivot)
   to left of pivot and all greater elements to right
   of pivot */
int partition (int arr[], int low, int high)
{
    int pivot = arr[high];    // pivot
    int i = (low - 1);  // Index of smaller element

    for (int j = low; j <= high- 1; j++)
    {
        // If current element is smaller than or
        // equal to pivot
        if (arr[j] <= pivot)
        {
            i++;    // increment index of smaller element
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

/* The main function that implements QuickSort
 arr[] --> Array to be sorted,
  low  --> Starting index,
  high  --> Ending index */
void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

/* Function to print an array */
void printArray(int arr[], int size)
{
    int i;
    for (i=0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

// Driver program to test above functions
int main()
{
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    quickSort(arr, 0, n-1);
    printf("Sorted array: \n");
    printArray(arr, n);
    return 0;
}
```

**Output**

```
Sorted array: 
1 5 7 8 9 10 
```

详情请参考[快速排序](https://www.geeksforgeeks.org/quick-sort/)上的完整文章！