# 子集的最大大小，使得所有子集元素的乘积是 N 的因子

> 原文:[https://www . geeksforgeeks . org/子集元素的最大大小是 n 的倍数/](https://www.geeksforgeeks.org/maximum-size-of-subset-such-that-product-of-all-subset-elements-is-a-factor-of-n/)

给定一个整数 **N** 和一个具有 **M** 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到子集的最大大小，使得子集的所有元素的[乘积是 **N**](https://www.geeksforgeeks.org/sum-products-possible-subsets/) 的[因子。](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)

**示例:**

> **输入:** N = 12，arr[] = {2，3，4}
> **输出:** 2
> **解释:**给定数组 5 个子集，使得子集所有元素的乘积是 12 的因子。它们是{2}、{3}、{4}、{2，3} as (2 * 3) = 6，以及{3，4} as (3 * 4) = 12。因此，有效子集的最大大小是 2。
> 
> **输入:** N = 64，arr[] = {1，2，4，8，16，32}
> **输出:** 4

**方法:**通过遍历给定数组的所有子集**arr【】**并跟踪子集的大小使得 **N %(子集元素的乘积)= 0** ，可以使用[递归](https://www.geeksforgeeks.org/recursion/)来解决给定的问题。同样，为了使子集元素的乘积成为 **N** 的因子，数组**arr【】**的所有单个元素也必须是 **N** 的因子。因此，上述问题可以通过以下步骤解决:

*   创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **maximizeSubset()** ，计算所需子集的最大大小。
*   如果给定数组 **arr[]** 的所有元素都已遍历，则返回 0，这是基本情况。
*   迭代数组的所有元素 **arr[]** ，如果 **N % arr[i] = 0** ，在一个子集中包含 **arr[i]** ，并递归调用剩余数组元素的 **N = N/arr[i]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum size of
// the subset such that the product of
// subset elements is a factor of N
int maximizeSubset(int N, int arr[],
                   int M, int x = 0)
{
    // Base Case
    if (x == M) {
        return 0;
    }

    // Stores maximum size of valid subset
    int ans = 0;

    // Traverse the given array
    for (int i = x; i < M; i++) {

        // If N % arr[i] = 0, include arr[i]
        // in a subset and recursively call
        // for the remaining array integers
        if (N % arr[i] == 0) {
            ans = max(
                ans, maximizeSubset(
                         N / arr[i], arr,
                         M, x + 1)
                         + 1);
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int N = 64;
    int arr[] = { 1, 2, 4, 8, 16, 32 };
    int M = sizeof(arr) / sizeof(arr[0]);

    cout << maximizeSubset(N, arr, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the maximum size of
    // the subset such that the product of
    // subset elements is a factor of N
    static int maximizeSubset(int N, int[] arr, int M,
                              int x)
    {
        // Base Case
        if (x == M) {
            return 0;
        }

        // Stores maximum size of valid subset
        int ans = 0;

        // Traverse the given array
        for (int i = x; i < M; i++) {

            // If N % arr[i] = 0, include arr[i]
            // in a subset and recursively call
            // for the remaining array integers
            if (N % arr[i] == 0) {
                ans = Math.max(ans,
                               maximizeSubset(N / arr[i],
                                              arr, M, x + 1)
                                   + 1);
            }
        }

        // Return Answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 64;
        int[] arr = { 1, 2, 4, 8, 16, 32 };
        int M = arr.length;

        System.out.println(maximizeSubset(N, arr, M, 0));
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the maximum size of
# the subset such that the product of
# subset elements is a factor of N
def maximizeSubset(N, arr, M, x=0):

    # Base Case
    if (x == M):
        return 0

    # Stores maximum size of valid subset
    ans = 0

    # Traverse the given array
    for i in range(x, M):

        # If N % arr[i] = 0, include arr[i]
        # in a subset and recursively call
        # for the remaining array integers
        if (N % arr[i] == 0):
            ans = max(
                ans, maximizeSubset(
                    N // arr[i], arr,
                    M, x + 1)
                + 1)

    # Return Answer
    return ans

# Driver Code
N = 64
arr = [1, 2, 4, 8, 16, 32]
M = len(arr)

print(maximizeSubset(N, arr, M))

# This code is contributed by Saurabh jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum size of
// the subset such that the product of
// subset elements is a factor of N
static int maximizeSubset(int N, int []arr,
                   int M, int x)
{
    // Base Case
    if (x == M) {
        return 0;
    }

    // Stores maximum size of valid subset
    int ans = 0;

    // Traverse the given array
    for (int i = x; i < M; i++) {

        // If N % arr[i] = 0, include arr[i]
        // in a subset and recursively call
        // for the remaining array integers
        if (N % arr[i] == 0) {
            ans = Math.Max(
                ans, maximizeSubset(
                         N / arr[i], arr,
                         M, x + 1)
                         + 1);
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void Main()
{
    int N = 64;
    int []arr = { 1, 2, 4, 8, 16, 32 };
    int M = arr.Length;

    Console.Write(maximizeSubset(N, arr, M,0));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the maximum size of
       // the subset such that the product of
       // subset elements is a factor of N
       function maximizeSubset(N, arr,
           M, x = 0)
       {

           // Base Case
           if (x == M) {
               return 0;
           }

           // Stores maximum size of valid subset
           let ans = 0;

           // Traverse the given array
           for (let i = x; i < M; i++) {

               // If N % arr[i] = 0, include arr[i]
               // in a subset and recursively call
               // for the remaining array integers
               if (N % arr[i] == 0) {
                   ans = Math.max(
                       ans, maximizeSubset(
                           Math.floor(N / arr[i]), arr,
                           M, x + 1)
                   + 1);
               }
           }

           // Return Answer
           return ans;
       }

       // Driver Code
       let N = 64;
       let arr = [1, 2, 4, 8, 16, 32];
       let M = arr.length;

       document.write(maximizeSubset(N, arr, M));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
4
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*