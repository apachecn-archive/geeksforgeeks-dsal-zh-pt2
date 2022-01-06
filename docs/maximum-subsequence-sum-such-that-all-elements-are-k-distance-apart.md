# 最大子序列和，使得所有元素相距 K 距离

> 原文:[https://www . geesforgeks . org/maximum-subsequer-sum-so-all-elements-k-distance/](https://www.geeksforgeeks.org/maximum-subsequence-sum-such-that-all-elements-are-k-distance-apart/)

给定一个由 **N** 个整数和另一个整数 **K** 组成的数组 **arr[]** 。任务是找到一个子序列的最大和，使得原始数组中子序列中所有连续元素的索引之差正好是 **K** 。例如，如果 **arr[i]** 是子序列的第一个元素，那么下一个元素必须是 **arr[i + k]** ，然后是 **arr[i + 2k]** 等等。
**举例:**

> **输入:** arr[] = {2，-3，-1，-1，2}，K = 2
> **输出:** 3
> **输入:** arr[] = {2，3，-1，-1，2}，K = 3
> **输出:** 5

**方法:**可能存在 **K** 序列，其中元素相距 K 距离，这些元素可以是:
的形式

> 0，0 + k，0 + 2k，…，0 + n*k
> 1，1 + k，1 + 2k，…，1 + n*k
> 2，2 + k，2 + 2k，…，2 + n*k
> k-1，k-1 + k，k-1 + 2k，…，k-1 + n*k

现在，序列的任何子阵列都是原始阵列的子序列，其中元素彼此相距 K 个距离。
因此，任务现在简化为寻找这些序列的最大子阵和，这可以通过[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)找到。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum subarray sum
// for the array {a[i], a[i + k], a[i + 2k], ...}
int maxSubArraySum(int a[], int n, int k, int i)
{
    int max_so_far = INT_MIN, max_ending_here = 0;

    while (i < n) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;

        i += k;
    }
    return max_so_far;
}

// Function to return the sum of
// the maximum required subsequence
int find(int arr[], int n, int k)
{
    // To store the result
    int maxSum = 0;

    // Run a loop from 0 to k
    for (int i = 0; i <= min(n, k); i++) {
        int sum = 0;

        // Find the maximum subarray sum for the
        // array {a[i], a[i + k], a[i + 2k], ...}
        maxSum = max(maxSum,
                     maxSubArraySum(arr, n, k, i));
    }

    // Return the maximum value
    return maxSum;
}

// Driver code
int main()
{
    int arr[] = { 2, -3, -1, -1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    cout << find(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the maximum subarray sum
// for the array {a[i], a[i + k], a[i + 2k], ...}
static int maxSubArraySum(int a[], int n,
                          int k, int i)
{
    int max_so_far = Integer.MIN_VALUE,
        max_ending_here = 0;

    while (i < n)
    {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;

        i += k;
    }
    return max_so_far;
}

// Function to return the sum of
// the maximum required subsequence
static int find(int arr[], int n, int k)
{
    // To store the result
    int maxSum = 0;

    // Run a loop from 0 to k
    for (int i = 0; i <= Math.min(n, k); i++)
    {
        int sum = 0;

        // Find the maximum subarray sum for the
        // array {a[i], a[i + k], a[i + 2k], ...}
        maxSum = Math.max(maxSum,
                      maxSubArraySum(arr, n, k, i));
    }

    // Return the maximum value
    return maxSum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {2, -3, -1, -1, 2};
    int n = arr.length;
    int k = 2;

    System.out.println(find(arr, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to return the maximum subarray sum
# for the array {a[i], a[i + k], a[i + 2k], ...}
import sys
def maxSubArraySum(a, n, k, i):

    max_so_far = -sys.maxsize;
    max_ending_here = 0;

    while (i < n):
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here):
            max_so_far = max_ending_here;

        if (max_ending_here < 0):
            max_ending_here = 0;

        i += k;

    return max_so_far;

# Function to return the sum of
# the maximum required subsequence
def find(arr, n, k):

    # To store the result
    maxSum = 0;

    # Run a loop from 0 to k
    for i in range(0, min(n, k) + 1):
        sum = 0;

        # Find the maximum subarray sum for the
        # array {a[i], a[i + k], a[i + 2k], ...}
        maxSum = max(maxSum,
                     maxSubArraySum(arr, n, k, i));

    # Return the maximum value
    return maxSum;

# Driver code
if __name__ == '__main__':
    arr = [ 2, -3, -1, -1, 2 ];
    n = len(arr);
    k = 2;

    print(find(arr, n, k));

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum subarray sum
    // for the array {a[i], a[i + k], a[i + 2k], ...}
    static int maxSubArraySum(int []a, int n,
                              int k, int i)
    {
        int max_so_far = int.MinValue,
            max_ending_here = 0;

        while (i < n)
        {
            max_ending_here = max_ending_here + a[i];
            if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;

            if (max_ending_here < 0)
                max_ending_here = 0;

            i += k;
        }
        return max_so_far;
    }

    // Function to return the sum of
    // the maximum required subsequence
    static int find(int []arr, int n, int k)
    {
        // To store the result
        int maxSum = 0;

        // Run a loop from 0 to k
        for (int i = 0; i <= Math.Min(n, k); i++)
        {

            // Find the maximum subarray sum for the
            // array {a[i], a[i + k], a[i + 2k], ...}
            maxSum = Math.Max(maxSum,
                              maxSubArraySum(arr, n, k, i));
        }

        // Return the maximum value
        return maxSum;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {2, -3, -1, -1, 2};
        int n = arr.Length;
        int k = 2;

        Console.WriteLine(find(arr, n, k));
    }   
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum subarray sum
// for the array {a[i], a[i + k], a[i + 2k], ...}
function maxSubArraySum(a, n, k, i)
{
    let max_so_far = Number.MIN_VALUE,
        max_ending_here = 0;

    while (i < n) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;

        i += k;
    }
    return max_so_far;
}

// Function to return the sum of
// the maximum required subsequence
function find(arr, n, k)
{
    // To store the result
    let maxSum = 0;

    // Run a loop from 0 to k
    for (let i = 0; i <= Math.min(n, k); i++) {
        let sum = 0;

        // Find the maximum subarray sum for the
        // array {a[i], a[i + k], a[i + 2k], ...}
        maxSum = Math.max(maxSum,
                     maxSubArraySum(arr, n, k, i));
    }

    // Return the maximum value
    return maxSum;
}

// Driver code
    let arr = [ 2, -3, -1, -1, 2 ];
    let n = arr.length;
    let k = 2;

    document.write(find(arr, n, k));

</script>
```

**Output:** 

```
3
```