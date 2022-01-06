# C 程序在 O(n)时间和 O(1)额外空间重新排列正负数

> 原文:[https://www . geesforgeks . org/c-program-to-重排-正负数-on-time-and-O1-extra-space/](https://www.geeksforgeeks.org/c-program-to-rearrange-positive-and-negative-numbers-in-on-time-and-o1-extra-space/)

数组包含随机顺序的正数和负数。重新排列数组元素，使正数和负数交替出现。正数和负数的数量不必相等。如果有更多的正数，它们会出现在数组的末尾。如果有更多的负数，它们也会出现在数组的末尾。
例如，如果输入数组是[-1，2，-3，4，5，6，-7，8，9]，那么输出应该是[9，-7，8，-3，5，-1，2，4，6]
**注:**划分过程改变元素的相对顺序。也就是说，用这种方法不能保持元素出现的顺序。[维护本问题中元素的出现顺序见本](https://www.geeksforgeeks.org/rearrange-array-alternating-positive-negative-items-o1-extra-space/)。
解决方法是先用 QuickSort 的划分过程将正数和负数分开。在划分过程中，将 0 视为透视元素的值，以便所有负数都放在正数之前。一旦负数和正数被分开，我们从第一个负数和第一个正数开始，用下一个正数交换每个交替的负数。

## C

```
// A C++ program to put positive numbers at even indexes (0, 
// 2, 4,..) and negative numbers at odd indexes (1, 3, 5, ..)
#include <stdio.h>

// prototype for swap
void swap(int *a, int *b);

// The main function that rearranges elements of given array. 
// It puts  positive elements at even indexes (0, 2, ..) and 
// negative numbers at odd indexes (1, 3, ..).
void rearrange(int arr[], int n)
{
    // The following few lines are similar to partition process
    // of QuickSort.  The idea is to consider 0 as pivot and
    // divide the array around it.
    int i = -1;
    for (int j = 0; j < n; j++)
    {
        if (arr[j] < 0)
        {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }

    // Now all positive numbers are at end and negative numbers
    // at the beginning of array. Initialize indexes for starting
    // point of positive and negative numbers to be swapped
    int pos = i+1, neg = 0;

    // Increment the negative index by 2 and positive index by 1,
    // i.e., swap every alternate negative number with next 
    // positive number
    while (pos < n && neg < pos && arr[neg] < 0)
    {
        swap(&arr[neg], &arr[pos]);
        pos++;
        neg += 2;
    }
}

// A utility function to swap two elements
void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// A utility function to print an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%4d ", arr[i]);
}

// Driver program to test above functions
int main()
{
    int arr[] = {-1, 2, -3, 4, 5, 6, -7, 8, 9};
    int n = sizeof(arr)/sizeof(arr[0]);
    rearrange(arr, n);
    printArray(arr, n);
    return 0;
}
```

**输出:**

```
    4   -3    5   -1    6   -7    2    8    9
```

**时间复杂度:** O(n)，其中 n 为给定数组中的元素个数。
**辅助空间:** O(1)

更多详情请参考[整篇文章在 O(n)时间和 O(1)额外空间](https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers-publish/)重新排列正负数！