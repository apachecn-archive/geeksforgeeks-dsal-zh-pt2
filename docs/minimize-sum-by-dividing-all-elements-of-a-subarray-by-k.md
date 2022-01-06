# 通过将子阵列的所有元素除以 K 来最小化总和

> 原文:[https://www . geeksforgeeks . org/通过将子数组的所有元素除以 k 来最小化总和/](https://www.geeksforgeeks.org/minimize-sum-by-dividing-all-elements-of-a-subarray-by-k/)

给定一个由 **N** 整数和一个正整数 **K** 组成的数组 **arr[]** ，任务是在执行一次给定操作**Atmos**后最小化数组元素的总和。操作是选择一个子阵列，将子阵列的所有元素除以 **K** 。找到并打印最小可能的总和。
**举例:**

> **输入:** arr[] = {1，-2，3}，K = 2
> **输出:** 0.5
> 选择子阵列{3}并除以 K
> 数组变为{1，-2，1.5}，其中 1–2+1.5 = 0.5
> **输入:** arr[] = {-1，-2，-3，-5}，K = 4
> **输出:** -11

**进场:**

*   使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)找到最大和子阵列，说**最大和**，因为它将是有助于最大化阵列和的子阵列。
*   现在有两种情况:
    1.  **maxSum > 0:** 用 **K** 除找到的子阵列的每个元素，得到的阵列的和将尽可能最小。
    2.  **maxSum ≤ 0:** 因为数组的和已经是最小值，所以不需要进行运算。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum subarray sum
int maxSubArraySum(int a[], int size)
{
    int max_so_far = INT_MIN, max_ending_here = 0;

    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to return the minimized sum
// of the array elements after performing
// the given operation
double minimizedSum(int a[], int n, int K)
{

    // Find maximum subarray sum
    int sum = maxSubArraySum(a, n);
    double totalSum = 0;

    // Find total sum of the array
    for (int i = 0; i < n; i++)
        totalSum += a[i];

    // Maximum subarray sum is already negative
    if (sum < 0)
        return totalSum;

    // Choose the subarray whose sum is
    // maximum and divide all elements by K
    totalSum = totalSum - sum + (double)sum / (double)K;
    return totalSum;
}

// Driver code
int main()
{

    int a[] = { 1, -2, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    int K = 2;

    cout << minimizedSum(a, n, K);

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
static int maxSubArraySum(int a[], int size)
{
    int max_so_far = Integer.MIN_VALUE,
        max_ending_here = 0;

    for (int i = 0; i < size; i++)
    {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to return the minimized sum
// of the array elements after performing
// the given operation
static double minimizedSum(int a[], int n, int K)
{

    // Find maximum subarray sum
    int sum = maxSubArraySum(a, n);
    double totalSum = 0;

    // Find total sum of the array
    for (int i = 0; i < n; i++)
        totalSum += a[i];

    // Maximum subarray sum is already negative
    if (sum < 0)
        return totalSum;

    // Choose the subarray whose sum is
    // maximum and divide all elements by K
    totalSum = totalSum - sum + (double)sum /
                                (double)K;
    return totalSum;
}

// Driver code
public static void main(String []args)
{
    int a[] = { 1, -2, 3 };
    int n = a.length;
    int K = 2;

    System.out.println(minimizedSum(a, n, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to return the maximum subarray sum
def maxSubArraySum(a, size) :

    max_so_far = -(sys.maxsize - 1);
    max_ending_here = 0;

    for i in range(size) :

        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here) :
            max_so_far = max_ending_here;

        if (max_ending_here < 0) :
            max_ending_here = 0;

    return max_so_far;

# Function to return the minimized sum
# of the array elements after performing
# the given operation
def minimizedSum(a, n, K) :

    # Find maximum subarray sum
    sum = maxSubArraySum(a, n);
    totalSum = 0;

    # Find total sum of the array
    for i in range(n) :
        totalSum += a[i];

    # Maximum subarray sum is already negative
    if (sum < 0) :
        return totalSum;

    # Choose the subarray whose sum is
    # maximum and divide all elements by K
    totalSum = totalSum - sum + sum / K;

    return totalSum;

# Driver code
if __name__ == "__main__" :

    a = [ 1, -2, 3 ];
    n = len(a);
    K = 2;

    print(minimizedSum(a, n, K));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum subarray sum
static int maxSubArraySum(int []a, int size)
{
    int max_so_far = int.MinValue,
        max_ending_here = 0;

    for (int i = 0; i < size; i++)
    {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to return the minimized sum
// of the array elements after performing
// the given operation
static double minimizedSum(int []a, int n, int K)
{

    // Find maximum subarray sum
    int sum = maxSubArraySum(a, n);
    double totalSum = 0;

    // Find total sum of the array
    for (int i = 0; i < n; i++)
        totalSum += a[i];

    // Maximum subarray sum is already negative
    if (sum < 0)
        return totalSum;

    // Choose the subarray whose sum is
    // maximum and divide all elements by K
    totalSum = totalSum - sum + (double)sum /
                                (double)K;
    return totalSum;
}

// Driver code
public static void Main(String []args)
{
    int []a = { 1, -2, 3 };
    int n = a.Length;
    int K = 2;

    Console.WriteLine(minimizedSum(a, n, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum subarray sum
function maxSubArraySum(a, size)
{
    var max_so_far = -1000000000, max_ending_here = 0;

    for (var i = 0; i < size; i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to return the minimized sum
// of the array elements after performing
// the given operation
function minimizedSum(a, n, K)
{

    // Find maximum subarray sum
    var sum = maxSubArraySum(a, n);
    var totalSum = 0;

    // Find total sum of the array
    for (var i = 0; i < n; i++)
        totalSum += a[i];

    // Maximum subarray sum is already negative
    if (sum < 0)
        return totalSum;

    // Choose the subarray whose sum is
    // maximum and divide all elements by K
    totalSum = totalSum - sum + sum / K;
    return totalSum;
}

// Driver code
var a = [1, -2, 3];
var n = a.length;
var K = 2;
document.write( minimizedSum(a, n, K));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
0.5
```

**时间复杂度:** O(N)