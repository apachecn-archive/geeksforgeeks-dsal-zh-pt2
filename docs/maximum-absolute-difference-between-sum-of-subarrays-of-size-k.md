# 大小为 K 的子阵列之和的最大绝对差

> 原文:[https://www . geeksforgeeks . org/大小为 k 的子阵之和的最大绝对差值/](https://www.geeksforgeeks.org/maximum-absolute-difference-between-sum-of-subarrays-of-size-k/)

给定一个大小为 **N** 的数组**arr【】**和一个整数 **K** ，任务是找出大小为 **K** 的子数组之和之间的最大绝对差。
**举例:**

> **输入:** arr[] = {-2，-3，4，-1，-2，1，5，-3}，K = 3
> **输出:** 6
> **解释:** :
> 子阵之和(-2，-3，4) = -1
> 子阵之和(-3，4，-1)=-0
> 子阵之和(4，-1，-2) = 1
> 子阵之和(-1，-2，1) = -2 【T12
> **输入:** arr [ ] = {2，5，-1，7，-3，-1，-2}，K = 4
> **输出:** 12

**天真法**
最简单的方法是生成所有大小的子阵 **K** 并找出其中的最小和与最大和。最后，返回最大值和最小值之间的绝对差值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O (1)*
**高效进场**
思路是使用[滑动窗口手法](https://www.geeksforgeeks.org/window-sliding-technique/)。按照以下步骤解决问题:

1.  检查 **K** 是否大于 **N** ，然后返回-1。

3.  计算第一个 **K** 大小子阵的和，更新 **maxSum** 和 **minSum** ，将**和**减**arr【start】**，将 **start** 加 1。
4.  遍历**从 **K** 到 **N** 止**，进行以下操作:
    *   将总和增加**arr【I】**。
    *   更新 **maxSum** 和 **minSum** 。
    *   将**和**减**等于【开始】**。
    *   将**增加 1，开始**。
5.  返回 **maxSum** 和 **minSum** 的绝对差值。

以下是上述方法的实现:

## C++

```
// C++ program to find the
// maximum absolute difference
// between the sum of all
// subarrays of size K
#include <bits/stdc++.h>
using namespace std;

// Return absolute difference
// between sum of all subarrays
// of size k
int MaxAbsSumOfKsubArray(int arr[],
                         int K, int N)
{

    // Stores maximum sum of
    // all K size subarrays
    int maxSum = INT_MIN;

    // Stores minimum sum of
    // all K size subarray
    int minSum = INT_MAX;

    // Stores the sum of current
    // subarray of size K
    int sum = 0;

    // Starting index of the
    // current subarray
    int start = 0;

    int i = 0;

    if (N < K)
        return -1;

    // Calculate the sum of
    // first K elements
    while (i < K)
    {
        sum += arr[i];
        i++;
    }

    // Update maxSum and minSum
    maxSum = max(maxSum, sum);
    minSum = min(minSum, sum);

    // Decrement sum by arr[start]
    // and increment start by 1
    sum -= arr[start++];

    // Traverse arr for the
    // remaining subarrays
    while (i < N)
    {

        // Increment sum by arr[i]
        sum += arr[i];

        // Increment i
        i++;

        // Update maxSum and minSum
        maxSum = max(maxSum, sum);
        minSum = min(minSum, sum);

        // Decrement sum by arr[start]
        // and increment start by 1
        sum -= arr[start++];
    }

    // Return absolute difference
    // between maxSum and minSum
    return abs(maxSum - minSum);
}

// Driver code
int main()
{
    int arr[] = { -2, -3, 4, -1,
                  -2, 1, 5, -3 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << MaxAbsSumOfKsubArray(arr, K, N)
         << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// maximum absolute difference
// between the sum of all
// subarrays of size K

import java.util.*;

class GFG {

    // Return absolute difference
    // between sum of all subarrays
    // of size k
    static int MaxAbsSumOfKsubArray(
        int[] arr,
        int K, int N)
    {
        // Stores maximum sum of
        // all K size subarrays
        int maxSum = Integer.MIN_VALUE;

        // Stores minimum sum of
        // all K size subarray
        int minSum = Integer.MAX_VALUE;

        // Stores the sum of current
        // subarray of size K
        int sum = 0;

        // Starting index of the
        // current subarray
        int start = 0;

        int i = 0;

        if (N < K)
            return -1;

        // Calculate the sum of
        // first K elements
        while (i < K) {
            sum += arr[i];
            i++;
        }

        // Update maxSum and minSum
        maxSum = Math.max(maxSum, sum);
        minSum = Math.min(minSum, sum);

        // Decrement sum by arr[start]
        // and increment start by 1
        sum -= arr[start++];

        // Traverse arr for the
        // remaining subarrays
        while (i < N) {

            // Increment sum by arr[i]
            sum += arr[i];

            // Increment i
            i++;

            // Update maxSum and minSum
            maxSum = Math.max(maxSum, sum);
            minSum = Math.min(minSum, sum);

            // Decrement sum by arr[start]
            // and increment start by 1
            sum -= arr[start++];
        }

        // Return absolute difference
        // between maxSum and minSum
        return Math.abs(maxSum - minSum);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { -2, -3, 4, -1,
                      -2, 1, 5, -3 };
        int K = 3;
        int N = arr.length;
        System.out.println(
            MaxAbsSumOfKsubArray(
                arr, K, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the
# maximum absolute difference
# between the sum of all
# subarrays of size K
import sys

# Return absolute difference
# between sum of all subarrays
# of size k
def MaxAbsSumOfKsubArray(arr, K, N):

    # Stores maximum sum of
    # all K size subarrays
    maxSum = - sys.maxsize - 1

    # Stores minimum sum of
    # all K size subarray
    minSum = sys.maxsize

    # Stores the sum of current
    # subarray of size K
    sum = 0

    # Starting index of the
    # current subarray
    start = 0

    i = 0

    if (N < K):
        return -1

    # Calculate the sum of
    # first K elements
    while (i < K):
        sum += arr[i]
        i += 1

    # Update maxSum and minSum
    maxSum = max(maxSum, sum)
    minSum = min(minSum, sum)

    # Decrement sum by arr[start]
    # and increment start by 1
    sum -= arr[start]
    start += 1

    # Traverse arr for the
    # remaining subarrays
    while (i < N):

        # Increment sum by arr[i]
        sum += arr[i]

        # Increment i
        i += 1

        # Update maxSum and minSum
        maxSum = max(maxSum, sum)
        minSum = min(minSum, sum)

        # Decrement sum by arr[start]
        # and increment start by 1
        sum -= arr[start]
        start += 1

    # Return absolute difference
    # between maxSum and minSum
    return abs(maxSum - minSum)

# Driver code
arr = [ -2, -3, 4, -1,
        -2, 1, 5, -3 ]
K = 3
N = len(arr)

print(MaxAbsSumOfKsubArray(arr, K, N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to find the
// maximum absolute difference
// between the sum of all
// subarrays of size K
using System;
class GFG{

// Return absolute difference
// between sum of all subarrays
// of size k
static int MaxAbsSumOfKsubArray(
       int[] arr,
       int K, int N)
{
    // Stores maximum sum of
    // all K size subarrays
    int MaxSum = Int32.MinValue;

    // Stores minimum sum of
    // all K size subarray
    int MinSum = Int32.MaxValue;

    // Stores the sum of current
    // subarray of size K
    int sum = 0;

    // Starting index of the
    // current subarray
    int start = 0;

    int i = 0;

    if (N < K)
        return -1;

    // Calculate the sum of
    // first K elements
    while (i < K)
    {
        sum += arr[i];
        i++;
    }

    // Update maxSum and minSum
    MaxSum = Math.Max(MaxSum, sum);
    MinSum = Math.Min(MinSum, sum);

    // Decrement sum by arr[start]
    // and increment start by 1
    sum -= arr[start++];

    // Traverse arr for the
    // remaining subarrays
    while (i < N)
    {

        // Increment sum by arr[i]
        sum += arr[i];

        // Increment i
        i++;

        // Update maxSum and minSum
        MaxSum = Math.Max(MaxSum, sum);
        MinSum = Math.Min(MinSum, sum);

        // Decrement sum by arr[start]
        // and increment start by 1
        sum -= arr[start++];
    }

    // Return absolute difference
    // between maxSum and minSum
    return Math.Abs(MaxSum - MinSum);
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { -2, -3, 4, -1,
                  -2, 1, 5, -3 };
    int K = 3;
    int N = arr.Length;
    Console.Write(MaxAbsSumOfKsubArray(arr, K, N));
}
}

// This code is contributed
// by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program to find the 
    // maximum absolute difference 
    // between the sum of all 
    // subarrays of size K 

    // Return absolute difference 
    // between sum of all subarrays 
    // of size k 
    function MaxAbsSumOfKsubArray(arr, K, N) 
    { 

        // Stores maximum sum of 
        // all K size subarrays 
        let maxSum = Number.MIN_VALUE;

        // Stores minimum sum of 
        // all K size subarray 
        let minSum = Number.MAX_VALUE; 

        // Stores the sum of current 
        // subarray of size K 
        let sum = 0; 

        // Starting index of the 
        // current subarray 
        let start = 0; 

        let i = 0; 

        if (N < K) 
            return -1; 

        // Calculate the sum of 
        // first K elements 
        while (i < K)
        { 
            sum += arr[i]; 
            i++; 
        } 

        // Update maxSum and minSum 
        maxSum = Math.max(maxSum, sum); 
        minSum = Math.min(minSum, sum); 

        // Decrement sum by arr[start] 
        // and increment start by 1 
        sum -= arr[start++]; 

        // Traverse arr for the 
        // remaining subarrays 
        while (i < N) 
        { 

            // Increment sum by arr[i] 
            sum += arr[i]; 

            // Increment i 
            i++; 

            // Update maxSum and minSum 
            maxSum = Math.max(maxSum, sum); 
            minSum = Math.min(minSum, sum); 

            // Decrement sum by arr[start] 
            // and increment start by 1 
            sum -= arr[start++]; 
        } 

        // Return absolute difference 
        // between maxSum and minSum 
        return Math.abs(maxSum - minSum); 
    } 

    let arr = [ -2, -3, 4, -1, -2, 1, 5, -3 ]; 
    let K = 3; 
    let N = arr.length; 

    document.write(MaxAbsSumOfKsubArray(arr, K, N));

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O (N)*
***辅助空间:** O (1)*