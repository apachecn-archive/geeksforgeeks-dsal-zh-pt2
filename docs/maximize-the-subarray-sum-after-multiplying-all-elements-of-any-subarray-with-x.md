# 将任意子阵列的所有元素乘以 X 后最大化子阵列和

> 原文:[https://www . geeksforgeeks . org/将任何子阵列的所有元素乘以 x 后的子阵列总和最大化/](https://www.geeksforgeeks.org/maximize-the-subarray-sum-after-multiplying-all-elements-of-any-subarray-with-x/)

给定一个由 **N** 个整数和一个整数 **X** 组成的数组 **arr[]** 。我们可以选择任意一个子数组，将其所有元素乘以 **X** 。乘法后，找到和最大的子阵列。任务是以最终子阵列总和最大化的方式将子阵列相乘。
**举例:**

> **输入:** arr[] = { -3，8，-2，1，-6}，X = -1
> **输出:** 15
> 选择带有{-2，1，-6 }的子数组，乘以 X。
> 现在新数组是{ -3，8，2，-1，6 }，其最大子数组和为 15。
> **输入:** arr[] = {1，2，4，-10}，X = 2
> **输出:** 14

**方法:**不能用贪婪的方法解决问题。贪婪的方法在很多情况下都会失败，其中之一就是 *a[] = { -3，8，-2，1，6 }和 x = -1* 。我们将使用动态规划来解决上述问题。让**DP【ind】【state】**，其中 **ind** 是数组中的当前索引，有 3 种状态。

*   第一种状态定义了在索引**找到要与 **X** 相乘的**之前，没有选择子阵列。
*   第二种状态定义了索引 **ind** 处的当前元素在子数组中，子数组乘以 **X** 。
*   第三种状态定义子阵列已经被选择。

[卡丹的](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)算法和 DP 一起使用，同时得到最大子阵和。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 5

// Function to return the maximum sum
int func(int idx, int cur, int a[], int dp[N][3], int n, int x)
{

    // Base case
    if (idx == n)
        return 0;

    // If already calculated
    if (dp[idx][cur] != -1)
        return dp[idx][cur];

    int ans = 0;

    // If no elements have been chosen
    if (cur == 0) {

        // Do not choose any element and use
        // Kadane's algorithm by taking max
        ans = max(ans, a[idx] + func(idx + 1, 0, a, dp, n, x));

        // Choose the sub-array and multiply x
        ans = max(ans, x * a[idx] + func(idx + 1, 1, a, dp, n, x));
    }
    else if (cur == 1) {

        // Choose the sub-array and multiply x
        ans = max(ans, x * a[idx] + func(idx + 1, 1, a, dp, n, x));

        // End the sub-array multiplication
        ans = max(ans, a[idx] + func(idx + 1, 2, a, dp, n, x));
    }
    else

        // No more multiplication
        ans = max(ans, a[idx] + func(idx + 1, 2, a, dp, n, x));

    // Memoize and return the answer
    return dp[idx][cur] = ans;
}

// Function to get the maximum sum
int getMaximumSum(int a[], int n, int x)
{

    // Initialize dp with -1
    int dp[n][3];
    memset(dp, -1, sizeof dp);

    // Iterate from every position and find the
    // maximum sum which is possible
    int maxi = 0;
    for (int i = 0; i < n; i++)
        maxi = max(maxi, func(i, 0, a, dp, n, x));

    return maxi;
}

// Driver code
int main()
{
    int a[] = { -3, 8, -2, 1, -6 };
    int n = sizeof(a) / sizeof(a[0]);
    int x = -1;

    cout << getMaximumSum(a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int N = 5;

// Function to return the maximum sum
static int func(int idx, int cur, int a[],
                int dp[][], int n, int x)
{

    // Base case
    if (idx == n)
    {
        return 0;
    }

    // If already calculated
    if (dp[idx][cur] != -1)
    {
        return dp[idx][cur];
    }

    int ans = 0;

    // If no elements have been chosen
    if (cur == 0)
    {

        // Do not choose any element and use
        // Kadane's algorithm by taking max
        ans = Math.max(ans, a[idx] +
                func(idx + 1, 0, a, dp, n, x));

        // Choose the sub-array and multiply x
        ans = Math.max(ans, x * a[idx] +
                func(idx + 1, 1, a, dp, n, x));
    }
    else if (cur == 1)
    {

        // Choose the sub-array and multiply x
        ans = Math.max(ans, x * a[idx] +
                func(idx + 1, 1, a, dp, n, x));

        // End the sub-array multiplication
        ans = Math.max(ans, a[idx] +
                func(idx + 1, 2, a, dp, n, x));
    }
    else // No more multiplication
    {
        ans = Math.max(ans, a[idx] +
                func(idx + 1, 2, a, dp, n, x));
    }

    // Memoize and return the answer
    return dp[idx][cur] = ans;
}

// Function to get the maximum sum
static int getMaximumSum(int a[], int n, int x)
{

    // Initialize dp with -1
    int dp[][] = new int[n][3];
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Iterate from every position and find the
    // maximum sum which is possible
    int maxi = 0;
    for (int i = 0; i < n; i++)
    {
        maxi = Math.max(maxi, func(i, 0, a, dp, n, x));
    }

    return maxi;
}

// Driver code
public static void main(String[] args)
{
    int a[] = {-3, 8, -2, 1, -6};
    int n = a.length;
    int x = -1;
    System.out.println(getMaximumSum(a, n, x));

}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

N = 5

# Function to return the maximum sum
def func(idx, cur, a, dp, n, x) :

    # Base case
    if (idx == n) :
        return 0

    # If already calculated
    if (dp[idx][cur] != -1):
        return dp[idx][cur]

    ans = 0

    # If no elements have been chosen
    if (cur == 0) :

        # Do not choose any element and use
        # Kadane's algorithm by taking max
        ans = max(ans, a[idx] + func(idx + 1, 0, a, dp, n, x))

        # Choose the sub-array and multiply x
        ans = max(ans, x * a[idx] + func(idx + 1, 1, a, dp, n, x))

    elif (cur == 1) :

        # Choose the sub-array and multiply x
        ans = max(ans, x * a[idx] + func(idx + 1, 1, a, dp, n, x))

        # End the sub-array multiplication
        ans = max(ans, a[idx] + func(idx + 1, 2, a, dp, n, x))

    else :

        # No more multiplication
        ans = max(ans, a[idx] + func(idx + 1, 2, a, dp, n, x))

    # Memoize and return the answer
    dp[idx][cur] = ans

    return dp[idx][cur]

# Function to get the maximum sum
def getMaximumSum(a, n, x) :

    # Initialize dp with -1
    dp = [[-1 for i in range(3)] for j in range(n)]

    # Iterate from every position and find the
    # maximum sum which is possible
    maxi = 0
    for i in range (0, n) :
        maxi = max(maxi, func(i, 0, a, dp, n, x))

    return maxi

# Driver code

a =  [ -3, 8, -2, 1, -6 ]  
n = len(a)
x = -1

print(getMaximumSum(a, n, x))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int N = 5;

// Function to return the maximum sum
static int func(int idx, int cur, int []a,
                int [,]dp, int n, int x)
{

    // Base case
    if (idx == n)
    {
        return 0;
    }

    // If already calculated
    if (dp[idx,cur] != -1)
    {
        return dp[idx,cur];
    }

    int ans = 0;

    // If no elements have been chosen
    if (cur == 0)
    {

        // Do not choose any element and use
        // Kadane's algorithm by taking max
        ans = Math.Max(ans, a[idx] +
                func(idx + 1, 0, a, dp, n, x));

        // Choose the sub-array and multiply x
        ans = Math.Max(ans, x * a[idx] +
                func(idx + 1, 1, a, dp, n, x));
    }
    else if (cur == 1)
    {

        // Choose the sub-array and multiply x
        ans = Math.Max(ans, x * a[idx] +
                func(idx + 1, 1, a, dp, n, x));

        // End the sub-array multiplication
        ans = Math.Max(ans, a[idx] +
                func(idx + 1, 2, a, dp, n, x));
    }
    else // No more multiplication
    {
        ans = Math.Max(ans, a[idx] +
                func(idx + 1, 2, a, dp, n, x));
    }

    // Memoize and return the answer
    return dp[idx,cur] = ans;
}

// Function to get the maximum sum
static int getMaximumSum(int []a, int n, int x)
{

    // Initialize dp with -1
    int [,]dp = new int[n,3];
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            dp[i,j] = -1;
        }
    }

    // Iterate from every position and find the
    // maximum sum which is possible
    int maxi = 0;
    for (int i = 0; i < n; i++)
    {
        maxi = Math.Max(maxi, func(i, 0, a, dp, n, x));
    }

    return maxi;
}

// Driver code
public static void Main(String[] args)
{
    int []a = {-3, 8, -2, 1, -6};
    int n = a.Length;
    int x = -1;
    Console.WriteLine(getMaximumSum(a, n, x));

}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$N = 5;

// Function to return the maximum sum
function func($idx, $cur, $a, $dp, $n, $x)
{

    // Base case
    if ($idx == $n)
        return 0;

    // If already calculated
    if ($dp[$idx][$cur] != -1)
        return $dp[$idx][$cur];

    $ans = 0;

    // If no elements have been chosen
    if ($cur == 0)
    {

        // Do not choose any element and use
        // Kadane's algorithm by taking max
        $ans = max($ans, $a[$idx] +
                func($idx + 1, 0, $a, $dp, $n, $x));

        // Choose the sub-array and multiply x
        $ans = max($ans, $x * $a[$idx] +
                func($idx + 1, 1, $a, $dp, $n, $x));
    }
    else if ($cur == 1)
    {

        // Choose the sub-array and multiply x
        $ans = max($ans, $x * $a[$idx] +
                func($idx + 1, 1, $a, $dp, $n, $x));

        // End the sub-array multiplication
        $ans = max($ans, $a[$idx] +
                func($idx + 1, 2, $a, $dp, $n, $x));
    }
    else

        // No more multiplication
        $ans = max($ans, $a[$idx] +
                func($idx + 1, 2, $a, $dp,$n, $x));

    // Memoize and return the answer
    return $dp[$idx][$cur] = $ans;
}

// Function to get the maximum sum
function getMaximumSum($a, $n, $x)
{

    // Initialize dp with -1
    $dp = array(array()) ;

    for($i = 0; $i < $n; $i++)
    {
        for($j = 0; $j < 3; $j++)
        {
            $dp[$i][$j] = -1;
        }
    }

    // Iterate from every position and find the
    // maximum sum which is possible
    $maxi = 0;
    for ($i = 0; $i < $n; $i++)
        $maxi = max($maxi, func($i, 0, $a, $dp, $n, $x));

    return $maxi;
}

    // Driver code
    $a = array( -3, 8, -2, 1, -6 );
    $n = count($a) ;
    $x = -1;

    echo getMaximumSum($a, $n, $x);

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach   
var N = 5;

    // Function to return the maximum sum
    function func(idx , cur , a , dp , n , x) {

        // Base case
        if (idx == n) {
            return 0;
        }

        // If already calculated
        if (dp[idx][cur] != -1) {
            return dp[idx][cur];
        }

        var ans = 0;

        // If no elements have been chosen
        if (cur == 0) {

            // Do not choose any element and use
            // Kadane's algorithm by taking max
            ans = Math.max(ans, a[idx] +
            func(idx + 1, 0, a, dp, n, x));

            // Choose the sub-array and multiply x
            ans = Math.max(ans, x * a[idx] +
            func(idx + 1, 1, a, dp, n, x));
        } else if (cur == 1) {

            // Choose the sub-array and multiply x
            ans = Math.max(ans, x * a[idx] +
            func(idx + 1, 1, a, dp, n, x));

            // End the sub-array multiplication
            ans = Math.max(ans, a[idx] +
            func(idx + 1, 2, a, dp, n, x));
        } else // No more multiplication
        {
            ans = Math.max(ans, a[idx] +
            func(idx + 1, 2, a, dp, n, x));
        }

        // Memoize and return the answer
        return dp[idx][cur] = ans;
    }

    // Function to get the maximum sum
    function getMaximumSum(a , n , x) {

        // Initialize dp with -1
        var dp = Array(n).fill().map(()=>Array(3).fill(0));
        for (i = 0; i < n; i++) {
            for (j = 0; j < 3; j++) {
                dp[i][j] = -1;
            }
        }

        // Iterate from every position and find the
        // maximum sum which is possible
        var maxi = 0;
        for (i = 0; i < n; i++) {
            maxi = Math.max(maxi, func(i, 0, a, dp, n, x));
        }

        return maxi;
    }

    // Driver code

        var a = [ -3, 8, -2, 1, -6 ];
        var n = a.length;
        var x = -1;
        document.write(getMaximumSum(a, n, x));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
15
```

**时间复杂度:**O(N * 3)
T3】辅助空间: O(N * 3)