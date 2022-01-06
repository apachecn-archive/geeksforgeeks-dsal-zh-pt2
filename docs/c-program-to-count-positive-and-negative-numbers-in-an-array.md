# 计算数组中正数和负数的程序

> 原文:[https://www . geesforgeks . org/c-程序对数组中的正负数进行计数/](https://www.geeksforgeeks.org/c-program-to-count-positive-and-negative-numbers-in-an-array/)

给定一个大小为 **N** 的整数数组 **arr** ，任务是找出数组中正数和负数的计数

**示例:**

> **输入:** arr[] = {2，-1，5，6，0，-3}
> **输出:**
> 正元素= 3
> 负元素= 2
> 有 3 个正，2 个负，1 个零。
> 
> **输入:** arr[] = {4，0，-2，-9，-7，1}
> **输出:**
> 正元素= 2
> 负元素= 3
> 有 2 个正，3 个负，1 个零。

**进场:**

1.  逐个遍历数组中的元素。
2.  对于每个元素，检查该元素是否小于 0。如果是，则增加负元素的计数。
3.  对于每个元素，检查该元素是否大于 0。如果是，则增加正元素的计数。
4.  打印正负元素的计数。

下面是上述方法的实现:

```
// C program to find the count of positive
// and negative integers in an array

#include <stdio.h>

// Function to find the count of
// positive integers in an array
int countPositiveNumbers(int* arr, int n)
{
    int pos_count = 0;
    int i;
    for (i = 0; i < n; i++) {
        if (arr[i] > 0)
            pos_count++;
    }
    return pos_count;
}

// Function to find the count of
// negative integers in an array
int countNegativeNumbers(int* arr, int n)
{
    int neg_count = 0;
    int i;
    for (i = 0; i < n; i++) {
        if (arr[i] < 0)
            neg_count++;
    }
    return neg_count;
}

// Function to print the array
void printArray(int* arr, int n)
{
    int i;

    printf("Array: ");
    for (i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

// Driver program
int main()
{
    int arr[] = { 2, -1, 5, 6, 0, -3 };
    int n;
    n = sizeof(arr) / sizeof(arr[0]);

    printArray(arr, n);

    printf("Count of Positive elements = %d\n",
           countPositiveNumbers(arr, n));
    printf("Count of Negative elements = %d\n",
           countNegativeNumbers(arr, n));

    return 0;
}
```

**Output:**

```
Array: 2 -1 5 6 0 -3 
Count of Positive elements = 3
Count of Negative elements = 2

```