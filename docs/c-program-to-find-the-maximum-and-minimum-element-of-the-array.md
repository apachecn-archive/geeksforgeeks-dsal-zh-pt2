# C 程序求数组的最大和最小元素

> 原文:[https://www . geesforgeks . org/c-program-to-find-最大和最小数组元素/](https://www.geeksforgeeks.org/c-program-to-find-the-maximum-and-minimum-element-of-the-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是编写 [C 程序](https://www.geeksforgeeks.org/c-programming-language/)迭代递归寻找给定数组的[个最大和最小元素。](https://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)

**示例:**

> **输入:** arr[] = {1，2，4，-1}
> **输出:**
> 最小元素为-1
> 最大元素为 4
> 
> **输入:** arr[] = {-1，-1，-1，-1}
> **输出:**
> 最小元素为-1
> 最大元素为-1

**进场:**

1.  让 **maxE** 和 **minE** 成为存储数组最小和最大元素的变量。
2.  将 **minE** 初始化为 [INT_MAX](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) ，将 **maxE** 初始化为 [INT_MIN](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 。
3.  遍历给定的数组 arr[]。
4.  如果当前元素小于 **minE** ，则更新 **minE** 为当前元素。
5.  如果当前元素大于 **maxE** ，则更新 **maxE** 为当前元素。
6.  对数组中的元素重复上述两个步骤。

下面是上述方法的实现:

## 迭代方法

```
// C program for the above approach
#include <limits.h>
#include <stdio.h>

// Function to find the minimum and
// maximum element of the array
void findMinimumMaximum(int arr[], int N)
{
    int i;

    // variable to store the minimum
    // and maximum element
    int minE = INT_MAX, maxE = INT_MIN;

    // Traverse the given array
    for (i = 0; i < N; i++) {

        // If current element is smaller
        // than minE then update it
        if (arr[i] < minE) {
            minE = arr[i];
        }

        // If current element is greater
        // than maxE then update it
        if (arr[i] > maxE) {
            maxE = arr[i];
        }
    }

    // Print the minimum and maximum element
    printf("The minimum element is %d", minE);
    printf("\n");
    printf("The maximum element is %d", maxE);

    return;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 2, 4, -1 };

    // length of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    findMinimumMaximum(arr, N);

    return 0;
}
```

## 递归方法

```
// C program for the above approach
#include <limits.h>
#include <stdio.h>

// Recursive function to find the minimum
// and the maximum element of the array
void recursiveMinMax(int arr[], int N,
                     int* minE, int* maxE)
{
    // Base Case
    if (N < 0) {
        return;
    }

    // If current element is smaller
    // than minE then update it
    if (arr[N] < *minE) {
        *minE = arr[N];
    }

    // If current element is greater
    // than maxE then update it
    if (arr[N] > *maxE) {
        *maxE = arr[N];
    }

    // Recursive call for next iteration
    recursiveMinMax(arr, N - 1, minE, maxE);
}

// Function to find the minimum and
// maximum element of the array
void findMinimumMaximum(int arr[], int N)
{
    int i;

    // variable to store the minimum
    // and maximum element
    int minE = INT_MAX, maxE = INT_MIN;

    // Recursive Function to find
    // minimum & maximum element
    recursiveMinMax(arr, N - 1, &minE, &maxE);

    // Print the minimum and maximum element
    printf("The minimum element is %d", minE);
    printf("\n");
    printf("The maximum element is %d", maxE);

    return;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 2, 4, -1 };

    // length of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    findMinimumMaximum(arr, N);
    return 0;
}
```

**Output:**

```
The minimum element is -1
The maximum element is 4

```

**时间复杂度:** *O(N)* ，其中 N 是给定数组中元素的个数。