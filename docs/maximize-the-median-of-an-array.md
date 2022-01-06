# 最大化数组的中值

> 原文:[https://www . geeksforgeeks . org/最大化数组中值/](https://www.geeksforgeeks.org/maximize-the-median-of-an-array/)

给定 n 个元素的数组。任务是打印数组，使数组的中值最大。

**示例:**

```
Input: arr[] = {3, 1, 2, 3, 8}
Output: 3 1 8 2 3

Input: arr[] = {9, 8, 7, 6, 5, 4}
Output: 7 6 9 8 5 4
```

**方法:**任何序列的中值都是给定数组的最中间元素。因此，如果数组有奇数个元素，则第 n/2 个元素是数组的中值，在这种情况下，如果数组有偶数个元素，则第 n/2 个和第 n/2–1 个元素是中值。
要最大化任何数组的中值，首先，根据数组的大小检查其大小是偶数还是奇数，执行以下步骤。

1.  **如果大小是奇数:**从数组中找出最大的元素，用第 n/2 个元素交换。
2.  **如果大小是偶数:**找到前两个最大元素，用第 n/2 和第 n/2-1 个元素交换。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print array with maximum median
void printMaxMedian(int arr[], int n)
{
    // case when size of array is odd
    if (n % 2) {
        int* maxElement = max_element(arr, arr + n);
        swap(*maxElement, arr[n / 2]);
    }

    // when the size of the array is even
    else {
        // find 1st maximum element
        int* maxElement1 = max_element(arr, arr + n);

        // find 2nd maximum element
        int* maxElement2 = max_element(arr, maxElement1);
        maxElement2 = max(maxElement2,
                          max_element(maxElement1 + 1, arr + n));

        // swap position for median
        swap(*maxElement1, arr[n / 2]);
        swap(*maxElement2, arr[n / 2 - 1]);
    }

    // print resultant array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 4, 8, 3, 1, 3, 7, 0, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printMaxMedian(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

public static int getIndexOfLargest(int[] array,
                                    int st,
                                    int n)
{
    if (array == null || array.length == 0)

        // null or empty
        return -1;

    int largest = st;
    for(int i = st + 1; i < n; i++)
    {
        if (array[i] > array[largest])
            largest = i;
    }

    // Position of the first largest
    // found
    return largest;
}

public static void swap(int a, int b, int[] arr)
{
    int temp = arr[a];
    arr[a] = arr[b];
    arr[b] = temp;
}

// Function to print array with maximum median
public static void printMaxMedian(int[] arr, int n)
{

    // Case when size of array is odd
    if (n % 2 != 0)
    {
        int maxElement = getIndexOfLargest(
            arr, 0, arr.length);

        swap(maxElement, n / 2, arr);
    }

    // When the size of the array is even
    else
    {

        // Find 1st maximum element
        int maxElement1 = getIndexOfLargest(
            arr, 0, arr.length);

        // Find 2nd maximum element
        int maxElement2 = getIndexOfLargest(
            arr, 0, maxElement1);

        maxElement2 = Math.max(
            arr[maxElement2],
            getIndexOfLargest(arr, maxElement1 + 1,
                              arr.length));

        // Swap position for median
        swap(maxElement1, n / 2, arr);
        swap(maxElement2, n / 2 - 1, arr);
    }

    // Print resultant array
    for(int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Driver Code
public static void main(String[] args)
    throws java.lang.Exception
{
    int arr[] = { 4, 8, 3, 1, 3, 7, 0, 4 };

    printMaxMedian(arr, arr.length);
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to print the array with
# maximum median
def printMaxMedian(arr, n):

    # case when size of the array is odd
    if n % 2 != 0:
        maxElement = arr.index(max(arr))
        (arr[maxElement],
         arr[n // 2]) = (arr[n // 2],
                         arr[maxElement])

    # when size of array is even
    else:

        # find 1st maximum element
        maxElement1 = arr.index(max(arr))

        # find 2nd maximum element
        maxElement2 = arr.index(max(arr[0 : maxElement1]))
        maxElement2 = arr.index(max(arr[maxElement2],
                                max(arr[maxElement1 + 1:])))

        # swap position for median
        (arr[maxElement1],
         arr[n // 2]) = (arr[n // 2],
                         arr[maxElement1])
        (arr[maxElement2],
         arr[n // 2 - 1]) = (arr[n // 2 - 1],
                             arr[maxElement2])

    # print the resultant array
    for i in range(0, n):
        print(arr[i], end = " ")

# Driver code
if __name__ == "__main__":

    arr = [4, 8, 3, 1, 3, 7, 0, 4]
    n = len(arr)
    printMaxMedian(arr, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

static int getIndexOfLargest(int[] array,
                             int st, int n)
{
    if (array == null || array.Length == 0)

        // Null or empty
        return -1;

    int largest = st;
    for(int i = st + 1; i < n; i++)
    {
        if (array[i] > array[largest])
            largest = i;
    }

    // Position of the first largest
    // found
    return largest;
}

static void swap(int a, int b, int[] arr)
{
    int temp = arr[a];
    arr[a] = arr[b];
    arr[b] = temp;
}

// Function to print array with maximum median
static void printMaxMedian(int[] arr, int n)
{

    // Case when size of array is odd
    if (n % 2 != 0)
    {
        int maxElement = getIndexOfLargest(
            arr, 0, arr.Length);

        swap(maxElement, n / 2, arr);
    }

    // When the size of the array is even
    else
    {

        // Find 1st maximum element
        int maxElement1 = getIndexOfLargest(
            arr, 0, arr.Length);

        // Find 2nd maximum element
        int maxElement2 = getIndexOfLargest(
            arr, 0, maxElement1);

        maxElement2 = Math.Max(
            arr[maxElement2],
            getIndexOfLargest(arr, maxElement1 + 1,
                              arr.Length));

        // Swap position for median
        swap(maxElement1, n / 2, arr);
        swap(maxElement2, n / 2 - 1, arr);
    }

    // Print resultant array
    for(int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Driver Code
static void Main()
{
    int[] arr = { 4, 8, 3, 1, 3, 7, 0, 4 };

    printMaxMedian(arr, arr.Length);
}
}

// This code is contributed by divyeshrabadiya07
```

**Output:** 

```
4 3 3 7 8 1 0 4
```