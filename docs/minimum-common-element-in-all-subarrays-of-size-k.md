# 大小为 K 的所有子阵列中的最小公共元素

> 原文:[https://www . geeksforgeeks . org/最小公共元素全尺寸子阵列 k/](https://www.geeksforgeeks.org/minimum-common-element-in-all-subarrays-of-size-k/)

给定一个由 **N** 个不同的整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找出所有[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中出现的最小元素，子数组的大小为 **K** 。如果不存在这样的元素，则打印【T12 "-" 1 "。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 4
> **输出:** 2
> **说明:**
> 大小为 4 的子阵为{1，2，3，4}和{2，3，4，5}。上述子阵列中的常见元素是{2，3，4}。
> 上述公共元素的最小值为 2。
> 
> **输入:** arr[] = {1，2，3，4，5}，K = 2
> **输出:** -1
> **解释:**
> 大小为{1，2}、{2，3}、{3，4}、{4，5}的子阵。由于没有公共元素，print -1。

**天真方法:**想法是[生成大小为 **K** 的给定阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有可能的子阵列，并找到所有形成的子阵列中的公共元素。找到公共元素后，打印其中的最小值。如果没有发现元素在所有子阵列中是共同的，那么打印 **"-1"** 。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**想法是首先检查所有子阵列中公共元素的条件，如果存在这样的元素，那么它应该在给定阵列中的范围**【N–K，K】**内。以下是我们可以找到任何此类最小元素的条件:

*   如果 **N** 为奇数， **K ≥ (N + 1)/2** 。
*   如果 **N** 为偶数且 **K ≥ ((N + 1)/2) + 1** 。

如果不满足上述条件，则最小元素位于**【N–K，K】**范围内。因此，[迭代该范围内的给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并打印其中最小元素的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum common
// among all the subarray of size K
// from the given array arr[]
void minCommonElementInSubarrays(
    int arr[], int N, int K)
{
    int c;

    // If N is odd then update
    // C as K >= (N + 1)/2
    if ((N + 1) % 2 == 0) {
        c = (N + 1) / 2;
    }

    // If N is even then update
    // C as K >= (N + 1)/2 + 1
    else {
        c = (N + 1) / 2 + 1;
    }

    // If K < C, return "=1"
    if (K < c) {
        cout << -1;
    }

    // Otherwise
    else {

        // Initialize result variable
        int ar = INT_MAX;

        // Find minimum element
        for (int i = N - K; i < K; i++) {
            ar = min(arr[i], ar);
        }

        // Print the minimum value
        cout << ar;
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5 };

    // Given K
    int K = 4;

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minCommonElementInSubarrays(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum common
// among all the subarray of size K
// from the given array arr[]
static void minCommonElementInSubarrays(int arr[],
                                        int N, int K)
{
    int c;

    // If N is odd then update
    // C as K >= (N + 1)/2
    if ((N + 1) % 2 == 0)
    {
        c = (N + 1) / 2;
    }

    // If N is even then update
    // C as K >= (N + 1)/2 + 1
    else
    {
        c = (N + 1) / 2 + 1;
    }

    // If K < C, return "=1"
    if (K < c)
    {
        System.out.print(-1);
    }

    // Otherwise
    else
    {

        // Initialize result variable
        int ar = Integer.MAX_VALUE;

        // Find minimum element
        for(int i = N - K; i < K; i++)
        {
            ar = Math.min(arr[i], ar);
        }

        // Print the minimum value
        System.out.print(ar);
    }
}

// Driver Code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5 };

    // Given K
    int K = 4;

    int N = arr.length;

    // Function call
    minCommonElementInSubarrays(arr, N, K);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the minimum common
# among all the subarray of size K
# from the given array arr[]
def minCommonElementInSubarrays(arr, N, K):

    c = 0

    # If N is odd then update
    # C as K >= (N + 1)/2
    if ((N + 1) % 2 == 0):
        c = (N + 1) // 2

    # If N is even then update
    # C as K >= (N + 1)/2 + 1
    else:
        c = (N + 1) / 2 + 1

    # If K < C, return "=1"
    if (K < c):
        print(-1)

    # Otherwise
    else:

        # Initialize result variable
        ar = sys.maxsize

        # Find minimum element
        for i in range(N - K, K):
            ar = min(arr[i], ar)

        # Print the minimum value
        print(ar)

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 3, 4, 5 ]

    # Given K
    K = 4

    N = len(arr)

    # Function call
    minCommonElementInSubarrays(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum common
// among all the subarray of size K
// from the given array arr[]
static void minCommonElementInSubarrays(int[] arr,
                                        int N, int K)
{
    int c;

    // If N is odd then update
    // C as K >= (N + 1)/2
    if ((N + 1) % 2 == 0)
    {
        c = (N + 1) / 2;
    }

    // If N is even then update
    // C as K >= (N + 1)/2 + 1
    else
    {
        c = (N + 1) / 2 + 1;
    }

    // If K < C, return "=1"
    if (K < c)
    {
        Console.Write(-1);
    }

    // Otherwise
    else
    {

        // Initialize result variable
        int ar = Int32.MaxValue;

        // Find minimum element
        for(int i = N - K; i < K; i++)
        {
            ar = Math.Min(arr[i], ar);
        }

        // Print the minimum value
        Console.Write(ar);
    }
}

// Driver Code
public static void Main ()
{

    // Given array arr[]
    int[] arr = { 1, 2, 3, 4, 5 };

    // Given K
    int K = 4;

    int N = arr.Length;

    // Function call
    minCommonElementInSubarrays(arr, N, K);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum common
// among all the subarray of size K
// from the given array arr[]
function minCommonElementInSubarrays(arr, N, K)
{
    let c;

    // If N is odd then update
    // C as K >= (N + 1)/2
    if ((N + 1) % 2 == 0) {
        c = parseInt((N + 1) / 2);
    }

    // If N is even then update
    // C as K >= (N + 1)/2 + 1
    else {
        c = parseInt((N + 1) / 2) + 1;
    }

    // If K < C, return "=1"
    if (K < c) {
        document.write(-1);
    }

    // Otherwise
    else {

        // Initialize result variable
        let ar = Number.MAX_VALUE;

        // Find minimum element
        for (let i = N - K; i < K; i++) {
            ar = Math.min(arr[i], ar);
        }

        // Print the minimum value
        document.write(ar);
    }
}

// Driver Code
    // Given array arr[]
    let arr = [ 1, 2, 3, 4, 5 ];

    // Given K
    let K = 4;

    let N = arr.length;

    // Function Call
    minCommonElementInSubarrays(arr, N, K);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)