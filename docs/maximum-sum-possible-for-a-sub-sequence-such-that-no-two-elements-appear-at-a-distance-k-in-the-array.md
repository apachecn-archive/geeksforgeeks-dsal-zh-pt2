# 子序列的最大可能和，使得在距离< K 处没有两个元素出现在数组

中

> 原文:[https://www . geeksforgeeks . org/子序列最大可能和-这样-没有两个元素-出现在距离-k-in-array/](https://www.geeksforgeeks.org/maximum-sum-possible-for-a-sub-sequence-such-that-no-two-elements-appear-at-a-distance-k-in-the-array/)

给定一个由 **n** 个整数和一个整数 **k** 组成的数组 **arr[]** ，任务是找到一个子序列的最大可能和，使得子序列中没有两个元素出现在原始数组中的距离 **≤ k** 处。
**举例:**

> **输入:** arr[] = {5，3，4，11，2}，k=1
> **输出:** 16
> 所有可能的子序列为{5，4，2}、{5，11}、{5，2}、{3，11}、{3，2}、{4，2}和{11}
> 其中 5 + 11 = 16 给出最大和。
> **输入:** arr[] = {6，7，1，3，8，2，4}，k = 2
> **输出:** 15

**方法:**在索引 **i** 处选择元素时，我们有两个选项，要么在子序列中包含当前元素，要么不包含。让 **dp[i]** 代表到目前为止到达指数 **i** 元素的最大和。我们可以计算 **dp[i]** 的值如下:

> **DP[I]= max(DP[I –( k+1)]+arr[I]，DP[I–1])**
> **DP[I–(k+1)]+arr[I]**包括索引 **i** 处的元素时的情况。在这种情况下，最大值将是 arr[i] +最大值，直到数组中最后一个包含的元素。
> **DP[I–1]**是不包括当前元素的情况，直到现在的最大值将是直到前一个元素的最大值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum sum possible
int maxSum(int* arr, int k, int n)
{
    if (n == 0)
        return 0;
    if (n == 1)
        return arr[0];
    if (n == 2)
        return max(arr[0], arr[1]);

    // dp[i] represent the maximum sum so far
    // after reaching current position i
    int dp[n];

    // Initialize dp[0]
    dp[0] = arr[0];

    // Initialize the dp values till k since any
    // two elements included in the sub-sequence
    // must be atleast k indices apart, and thus
    // first element and second element
    // will be k indices apart
    for (int i = 1; i <= k; i++)
        dp[i] = max(arr[i], dp[i - 1]);

    // Fill remaining positions
    for (int i = k + 1; i < n; i++)
        dp[i] = max(arr[i], dp[i - (k + 1)] + arr[i]);

    // Return the maximum sum
    int max = *(std::max_element(dp, dp + n));
    return max;
}

// Driver code
int main()
{
    int arr[] = { 6, 7, 1, 3, 8, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << maxSum(arr, k, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum sum possible
static int maxSum(int []arr, int k, int n)
{
    if (n == 0)
        return 0;
    if (n == 1)
        return arr[0];
    if (n == 2)
        return Math.max(arr[0], arr[1]);

    // dp[i] represent the maximum sum so far
    // after reaching current position i
    int[] dp = new int[n];

    // Initialize dp[0]
    dp[0] = arr[0];

    // Initialize the dp values till k since any
    // two elements included in the sub-sequence
    // must be atleast k indices apart, and thus
    // first element and second element
    // will be k indices apart
    for (int i = 1; i <= k; i++)
        dp[i] = Math.max(arr[i], dp[i - 1]);

    // Fill remaining positions
    for (int i = k + 1; i < n; i++)
        dp[i] = Math.max(arr[i], dp[i - (k + 1)] + arr[i]);

    // Return the maximum sum
    return maximum(dp);
}

static int maximum(int[] arr)
{
    int max = Integer.MIN_VALUE;
    for(int i = 0; i < arr.length; i++)
    {
        if(arr[i] > max)
        {
            max = arr[i];
        }
    }
    return max;
}

// Driver code
public static void main (String[] args)
{
    int []arr = { 6, 7, 1, 3, 8, 2, 4 };
    int n = arr.length;
    int k = 2;
    System.out.println(maxSum(arr, k, n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# maximum sum possible
def maxSum(arr, k, n) :

    if (n == 0) :
        return 0;
    if (n == 1) :
        return arr[0];
    if (n == 2) :
        return max(arr[0], arr[1]);

    # dp[i] represent the maximum sum so far
    # after reaching current position i
    dp = [0] * n ;

    # Initialize dp[0]
    dp[0] = arr[0];

    # Initialize the dp values till k since any
    # two elements included in the sub-sequence
    # must be atleast k indices apart, and thus
    # first element and second element
    # will be k indices apart
    for i in range(1, k + 1) :
        dp[i] = max(arr[i], dp[i - 1]);

    # Fill remaining positions
    for i in range(k + 1, n) :
        dp[i] = max(arr[i],
                    dp[i - (k + 1)] + arr[i]);

    # Return the maximum sum
    max_element = max(dp);
    return max_element;

# Driver code
if __name__ == "__main__" :
    arr = [ 6, 7, 1, 3, 8, 2, 4 ];
    n = len(arr);
    k = 2;

    print(maxSum(arr, k, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

// Function to return the maximum sum possible
static int maxSum(int []arr, int k, int n)
{
    if (n == 0)
        return 0;
    if (n == 1)
        return arr[0];
    if (n == 2)
        return Math.Max(arr[0], arr[1]);

    // dp[i] represent the maximum sum so far
    // after reaching current position i
    int[] dp = new int[n];

    // Initialize dp[0]
    dp[0] = arr[0];

    // Initialize the dp values till k since any
    // two elements included in the sub-sequence
    // must be atleast k indices apart, and thus
    // first element and second element
    // will be k indices apart
    for (int i = 1; i <= k; i++)
        dp[i] = Math.Max(arr[i], dp[i - 1]);

    // Fill remaining positions
    for (int i = k + 1; i < n; i++)
        dp[i] = Math.Max(arr[i], dp[i - (k + 1)] + arr[i]);

    // Return the maximum sum
    int max = dp.Max();
    return max;
}

// Driver code
static void Main()
{
    int []arr = { 6, 7, 1, 3, 8, 2, 4 };
    int n = arr.Length;
    int k = 2;
    Console.WriteLine(maxSum(arr, k, n));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the maximum sum possible
    function maxSum(arr, k, n)
    {
        if (n == 0)
            return 0;
        if (n == 1)
            return arr[0];
        if (n == 2)
            return Math.max(arr[0], arr[1]);

        // dp[i] represent the maximum sum so far
        // after reaching current position i
        let dp = new Array(n);

        // Initialize dp[0]
        dp[0] = arr[0];

        // Initialize the dp values till k since any
        // two elements included in the sub-sequence
        // must be atleast k indices apart, and thus
        // first element and second element
        // will be k indices apart
        for (let i = 1; i <= k; i++)
            dp[i] = Math.max(arr[i], dp[i - 1]);

        // Fill remaining positions
        for (let i = k + 1; i < n; i++)
            dp[i] = Math.max(arr[i], dp[i - (k + 1)] + arr[i]);

        // Return the maximum sum
        let max = Number.MIN_VALUE;
        for(let i = 0; i < dp.length; i++)
        {
            max = Math.max(max, dp[i]);
        }
        return max;
    }

    let arr = [ 6, 7, 1, 3, 8, 2, 4 ];
    let n = arr.length;
    let k = 2;
    document.write(maxSum(arr, k, n));

</script>
```

**Output:** 

```
15
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)