# 偶数长度的最大和子阵

> 原文:[https://www . geesforgeks . org/最大和偶长度子数组/](https://www.geeksforgeeks.org/maximum-sum-subarray-of-even-length/)

给定一个由 **N** 元素组成的数组 **arr[]** ，任务是找出任意长度子数组 **X** 的最大和，使得 **X > 0** 和 **X % 2 = 0** 。
**举例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 5
> {2，3}为所需子阵。
> **输入:** arr[] = {8，9，-8，9，10}
> **输出:** 20
> {9，-8，9，10}为所需子阵。
> 即使{8，9，-8，9，10}有最大和
> 但长度不均匀。

**方法:**这个问题是[最大子阵和](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)问题的变种，可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法解决。创建一个数组 **dp[]** ，其中 **dp[i]** 将存储偶数长度子阵列的最大和，该子阵列的第一个元素是 **arr[i]** 。现在循环关系为:

> dp[i] = max（（arr[i] + scar[i + 1]）， （scar[i] + scar[i + 1] + dp[i + 2]））

这是因为以元素 **arr[i]** 开始的偶长度子阵列的最大和既可以是 **arr[i]** 和 **arr[i + 1]** 的和，也可以是 **arr[i] + arr[i + 1]** 加上以 **arr[i + 2]** 开始的偶长度子阵列的最大和，即 **dp[i + 2]** 。取这两个的最大值。
最终，来自 **dp[]** 数组的最大值将是所需答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// subarray sum of even length
int maxEvenLenSum(int arr[], int n)
{

    // There has to be at
    // least 2 elements
    if (n < 2)
        return 0;

    // dp[i] will store the maximum
    // subarray sum of even length
    // starting at arr[i]
    int dp[n] = { 0 };

    // Valid subarray cannot start from
    // the last element as its
    // length has to be even
    dp[n - 1] = 0;
    dp[n - 2] = arr[n - 2] + arr[n - 1];

    for (int i = n - 3; i >= 0; i--) {

        // arr[i] and arr[i + 1] can be added
        // to get an even length subarray
        // starting at arr[i]
        dp[i] = arr[i] + arr[i + 1];

        // If the sum of the valid subarray starting
        // from arr[i + 2] is greater than 0 then it
        // can be added with arr[i] and arr[i + 1]
        // to maximize the sum of the subarray
        // starting from arr[i]
        if (dp[i + 2] > 0)
            dp[i] += dp[i + 2];
    }

    // Get the sum of the even length
    // subarray with maximum sum
    int maxSum = *max_element(dp, dp + n);
    return maxSum;
}

// Driver code
int main()
{

    int arr[] = { 8, 9, -8, 9, 10 };
    int n = sizeof(arr) / sizeof(int);

    cout << maxEvenLenSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

// Function to return the maximum
// subarray sum of even length
static int maxEvenLenSum(int arr[], int n)
{

    // There has to be at
    // least 2 elements
    if (n < 2)
        return 0;

    // dp[i] will store the maximum
    // subarray sum of even length
    // starting at arr[i]
    int []dp = new int[n];

    // Valid subarray cannot start from
    // the last element as its
    // length has to be even
    dp[n - 1] = 0;
    dp[n - 2] = arr[n - 2] + arr[n - 1];

    for (int i = n - 3; i >= 0; i--)
    {

        // arr[i] and arr[i + 1] can be added
        // to get an even length subarray
        // starting at arr[i]
        dp[i] = arr[i] + arr[i + 1];

        // If the sum of the valid subarray starting
        // from arr[i + 2] is greater than 0 then it
        // can be added with arr[i] and arr[i + 1]
        // to maximize the sum of the subarray
        // starting from arr[i]
        if (dp[i + 2] > 0)
            dp[i] += dp[i + 2];
    }

    // Get the sum of the even length
    // subarray with maximum sum
    int maxSum = Arrays.stream(dp).max().getAsInt();
    return maxSum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 9, -8, 9, 10 };
    int n = arr.length;

    System.out.println(maxEvenLenSum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# subarray sum of even length
def maxEvenLenSum(arr, n):

    # There has to be at
    # least 2 elements
    if (n < 2):
        return 0

    # dp[i] will store the maximum
    # subarray sum of even length
    # starting at arr[i]
    dp = [0 for i in range(n)]

    # Valid subarray cannot start from
    # the last element as its
    # length has to be even
    dp[n - 1] = 0
    dp[n - 2] = arr[n - 2] + arr[n - 1]

    for i in range(n - 3, -1, -1):

        # arr[i] and arr[i + 1] can be added
        # to get an even length subarray
        # starting at arr[i]
        dp[i] = arr[i] + arr[i + 1]

        # If the sum of the valid subarray
        # starting from arr[i + 2] is
        # greater than 0 then it can be added
        # with arr[i] and arr[i + 1]
        # to maximize the sum of the
        # subarray starting from arr[i]
        if (dp[i + 2] > 0):
            dp[i] += dp[i + 2]

    # Get the sum of the even length
    # subarray with maximum sum
    maxSum = max(dp)
    return maxSum

# Driver code
arr = [8, 9, -8, 9, 10]
n = len(arr)

print(maxEvenLenSum(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MaxSum(int []arr)
    {

        // assigning first element to the array
        int large = arr[0];

        // loop to compare value of large
        // with other elements
        for (int i = 1; i < arr.Length; i++)
        {
            // if large is smaller than other element
            // assig that element to the large
            if (large < arr[i])
                large = arr[i];
        }
        return large;
    }

    // Function to return the maximum
    // subarray sum of even length
    static int maxEvenLenSum(int []arr, int n)
    {

        // There has to be at
        // least 2 elements
        if (n < 2)
            return 0;

        // dp[i] will store the maximum
        // subarray sum of even length
        // starting at arr[i]
        int []dp = new int[n];

        // Valid subarray cannot start from
        // the last element as its
        // length has to be even
        dp[n - 1] = 0;
        dp[n - 2] = arr[n - 2] + arr[n - 1];

        for (int i = n - 3; i >= 0; i--)
        {

            // arr[i] and arr[i + 1] can be added
            // to get an even length subarray
            // starting at arr[i]
            dp[i] = arr[i] + arr[i + 1];

            // If the sum of the valid subarray starting
            // from arr[i + 2] is greater than 0 then it
            // can be added with arr[i] and arr[i + 1]
            // to maximize the sum of the subarray
            // starting from arr[i]
            if (dp[i + 2] > 0)
                dp[i] += dp[i + 2];
        }

        // Get the sum of the even length
        // subarray with maximum sum
        int maxSum = MaxSum(dp);
        return maxSum;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 8, 9, -8, 9, 10 };
        int n = arr.Length;

        Console.WriteLine(maxEvenLenSum(arr, n));
    }
}

// This code is contributed by kanugargng
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the maximum
// subarray sum of even length
function maxEvenLenSum(arr, n) {

    // There has to be at
    // least 2 elements
    if (n < 2)
        return 0;

    // dp[i] will store the maximum
    // subarray sum of even length
    // starting at arr[i]
    let dp = new Array(n).fill(0);

    // Valid subarray cannot start from
    // the last element as its
    // length has to be even
    dp[n - 1] = 0;
    dp[n - 2] = arr[n - 2] + arr[n - 1];

    for (let i = n - 3; i >= 0; i--) {

        // arr[i] and arr[i + 1] can be added
        // to get an even length subarray
        // starting at arr[i]
        dp[i] = arr[i] + arr[i + 1];

        // If the sum of the valid subarray starting
        // from arr[i + 2] is greater than 0 then it
        // can be added with arr[i] and arr[i + 1]
        // to maximize the sum of the subarray
        // starting from arr[i]
        if (dp[i + 2] > 0)
            dp[i] += dp[i + 2];
    }

    // Get the sum of the even length
    // subarray with maximum sum
    let maxSum = dp.sort((a, b) => b - a)[0];
    return maxSum;
}

// Driver code
let arr = [8, 9, -8, 9, 10];
let n = arr.length;

document.write(maxEvenLenSum(arr, n));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
20
```

**时间复杂度:**O(n)
T3】空间复杂度: O(n)