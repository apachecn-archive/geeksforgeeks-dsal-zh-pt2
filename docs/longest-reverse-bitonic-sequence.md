# 最长反向双音素序列

> 原文:[https://www . geesforgeks . org/long-reverse-bitonic-sequence/](https://www.geeksforgeeks.org/longest-reverse-bitonic-sequence/)

给定长度为 **N** 的 **arr[]** ，任务是找到最长的反向[双音素子序列](https://www.geeksforgeeks.org/longest-bitonic-subsequence-dp-15/)的长度。如果一个[子序列](http://en.wikipedia.org/wiki/Subsequence)先递减后递增，则称之为反向双音素。
**示例:**

> **输入:** arr[] = {10，11，2，1，1，5，2，4}
> **输出:** 5
> **解释:**先减后增的最长子序列是{10，2，1，1，2，4}
> **输入:** arr[] = {0，8，4，12，2，10，6，14，1，9，5，13，3，11，7

**方法:**
这个问题是标准[最长递增](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)T5】子序列(LIS)问题的一个变种。使用动态编程构建两个数组**lis【】**和**LDS【】**以分别存储最长的递增和递减子序列，直到数组的每个 i <sup>第</sup>个索引。最后，返回**LDS[I]+lis[I]–1**的最大值，其中 I 的范围从 0 到 N-1。
以下是上述方法的实施:

## C++

```
// C++ program to find the
// longest Reverse bitonic
// Subsequence
#include <bits/stdc++.h>
using namespace std;

// Function to return the length
// of the Longest Reverse Bitonic
// Subsequence in the array
int ReverseBitonic(int arr[], int N)
{
    int i, j;

    // Allocate memory for LIS[] and
    // initialize LIS values as 1 for
    // all indexes
    int lds[N];
    for (i = 0; i < N; i++) {
        lds[i] = 1;
    }

    // Compute LIS values from left
    // to right for every index
    for (i = 1; i < N; i++) {
        for (j = 0; j < i; j++) {
            if (arr[i] < arr[j]
                && lds[i] < lds[j] + 1) {
                lds[i] = lds[j] + 1;
            }
        }
    }

    // Initialize LDS for
    // all indexes as 1
    int lis[N];
    for (i = 0; i < N; i++) {
        lis[i] = 1;
    }

    // Compute LDS values for every
    // index from right to left
    for (i = N - 2; i >= 0; i--) {
        for (j = N - 1; j > i; j--) {
            if (arr[i] < arr[j]
                && lis[i] < lis[j] + 1) {
                lis[i] = lis[j] + 1;
            }
        }
    }

    // Find the maximum value of
    // lis[i] + lds[i] - 1
    // in the array
    int max = lis[0] + lds[0] - 1;
    for (i = 1; i < N; i++) {
        if (lis[i] + lds[i] - 1 > max) {
            max = lis[i] + lds[i] - 1;
        }
    }
    // Return the maximum
    return max;
}

// Driver Program
int main()
{

    int arr[] = { 0, 8, 4, 12, 2, 10, 6,
                  14, 1, 9, 5, 13, 3, 11,
                  7, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);
    printf("Length of LBS is %d\n",
           ReverseBitonic(arr, N));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// longest Reverse bitonic
// Subsequence
import java.io.*;

class GFG{

// Function to return the length
// of the Longest Reverse Bitonic
// Subsequence in the array
static int ReverseBitonic(int arr[], int N)
{
    int i, j;

    // Allocate memory for LIS[] and
    // initialize LIS values as 1 for
    // all indexes
    int[] lds = new int[N];
    for(i = 0; i < N; i++)
    {
        lds[i] = 1;
    }

    // Compute LIS values from left
    // to right for every index
    for(i = 1; i < N; i++)
    {
        for(j = 0; j < i; j++)
        {
            if (arr[i] < arr[j] &&
                lds[i] < lds[j] + 1)
            {
                lds[i] = lds[j] + 1;
            }
        }
    }

    // Initialize LDS for
    // all indexes as 1
    int[] lis = new int[N];
    for(i = 0; i < N; i++)
    {
        lis[i] = 1;
    }

    // Compute LDS values for every
    // index from right to left
    for(i = N - 2; i >= 0; i--)
    {
        for(j = N - 1; j > i; j--)
        {
            if (arr[i] < arr[j] &&
                lis[i] < lis[j] + 1)
            {
                lis[i] = lis[j] + 1;
            }
        }
    }

    // Find the maximum value of
    // lis[i] + lds[i] - 1
    // in the array
    int max = lis[0] + lds[0] - 1;
    for(i = 1; i < N; i++)
    {
        if (lis[i] + lds[i] - 1 > max)
        {
            max = lis[i] + lds[i] - 1;
        }
    }
    // Return the maximum
    return max;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 0, 8, 4, 12,
                  2, 10, 6, 14,
                  1, 9, 5, 13,
                  3, 11, 7, 15 };

    int N = arr.length;

    System.out.println("Length of LBS is " +
                      ReverseBitonic(arr, N));
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program to find the
# longest Reverse bitonic
# Subsequence

# Function to return the length
# of the Longest Reverse Bitonic
# Subsequence in the array
def ReverseBitonic(arr):

    N = len(arr)

    # Allocate memory for LIS[] and
    # initialize LIS values as 1
    # for all indexes
    lds = [1 for i in range(N + 1)]

    # Compute LIS values from left to right
    for i in range(1, N):
        for j in range(0 , i):
            if ((arr[i] < arr[j]) and
                (lds[i] < lds[j] + 1)):
                lds[i] = lds[j] + 1

    # Allocate memory for LDS and
    # initialize LDS values for
    # all indexes
    lis = [1 for i in range(N + 1)]

    # Compute LDS values from right to left
    # Loop from n-2 downto 0
    for i in reversed(range(N - 1)):

        # Loop from n-1 downto i-1
        for j in reversed(range(i - 1, N)):
            if (arr[i] < arr[j] and
                lis[i] < lis[j] + 1):
                lis[i] = lis[j] + 1

    # Return the maximum value of
    # (lis[i] + lds[i] - 1)
    maximum = lis[0] + lds[0] - 1
    for i in range(1, N):
        maximum = max((lis[i] +
                       lds[i] - 1), maximum)

    return maximum

# Driver code
arr = [ 0, 8, 4, 12,
        2, 10, 6, 14,
        1, 9, 5, 13,
        3, 11, 7, 15 ]

print("Length of LBS is", ReverseBitonic(arr))

# This code is contributed by grand_master
```

## C#

```
// C# program to find the
// longest Reverse bitonic
// Subsequence
using System;

class GFG{

// Function to return the length
// of the Longest Reverse Bitonic
// Subsequence in the array
static int ReverseBitonic(int[] arr, int N)
{
    int i, j;

    // Allocate memory for LIS[] and
    // initialize LIS values as 1 for
    // all indexes
    int[] lds = new int[N];
    for(i = 0; i < N; i++)
    {
        lds[i] = 1;
    }

    // Compute LIS values from left
    // to right for every index
    for(i = 1; i < N; i++)
    {
        for(j = 0; j < i; j++)
        {
            if (arr[i] < arr[j] &&
                lds[i] < lds[j] + 1)
            {
                lds[i] = lds[j] + 1;
            }
        }
    }

    // Initialize LDS for
    // all indexes as 1
    int[] lis = new int[N];
    for(i = 0; i < N; i++)
    {
        lis[i] = 1;
    }

    // Compute LDS values for every
    // index from right to left
    for(i = N - 2; i >= 0; i--)
    {
        for(j = N - 1; j > i; j--)
        {
            if (arr[i] < arr[j] &&
                lis[i] < lis[j] + 1)
            {
                lis[i] = lis[j] + 1;
            }
        }
    }

    // Find the maximum value of
    // lis[i] + lds[i] - 1
    // in the array
    int max = lis[0] + lds[0] - 1;
    for(i = 1; i < N; i++)
    {
        if (lis[i] + lds[i] - 1 > max)
        {
            max = lis[i] + lds[i] - 1;
        }
    }

    // Return the maximum
    return max;
}

// Driver code
public static void Main ()
{
    int[] arr = new int[] { 0, 8, 4, 12,
                            2, 10, 6, 14,
                            1, 9, 5, 13,
                            3, 11, 7, 15 };

    int N = arr.Length;

    Console.WriteLine("Length of LBS is " +
                     ReverseBitonic(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to find the
// longest Reverse bitonic
// Subsequence

// Function to return the length
// of the Longest Reverse Bitonic
// Subsequence in the array
function ReverseBitonic(arr, N)
{
    let i, j;

    // Allocate memory for LIS[] and
    // initialize LIS values as 1 for
    // all indexes
    let lds = [];
    for(i = 0; i < N; i++)
    {
        lds[i] = 1;
    }

    // Compute LIS values from left
    // to right for every index
    for(i = 1; i < N; i++)
    {
        for(j = 0; j < i; j++)
        {
            if (arr[i] < arr[j] &&
                lds[i] < lds[j] + 1)
            {
                lds[i] = lds[j] + 1;
            }
        }
    }

    // Initialize LDS for
    // all indexes as 1
    let lis = [];
    for(i = 0; i < N; i++)
    {
        lis[i] = 1;
    }

    // Compute LDS values for every
    // index from right to left
    for(i = N - 2; i >= 0; i--)
    {
        for(j = N - 1; j > i; j--)
        {
            if (arr[i] < arr[j] &&
                lis[i] < lis[j] + 1)
            {
                lis[i] = lis[j] + 1;
            }
        }
    }

    // Find the maximum value of
    // lis[i] + lds[i] - 1
    // in the array
    let max = lis[0] + lds[0] - 1;
    for(i = 1; i < N; i++)
    {
        if (lis[i] + lds[i] - 1 > max)
        {
            max = lis[i] + lds[i] - 1;
        }
    }
    // Return the maximum
    return max;
}

// Driver Code
    let arr = [ 0, 8, 4, 12,
                  2, 10, 6, 14,
                  1, 9, 5, 13,
                  3, 11, 7, 15 ];

    let N = arr.length;

    document.write("Length of LBS is " +
                      ReverseBitonic(arr, N));

// This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
Length of LBS is 7
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*