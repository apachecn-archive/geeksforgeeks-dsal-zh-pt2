# 最大化长度为 K 的子序列中连续对的数字和的乘积

> 原文:[https://www . geeksforgeeks . org/最大化长度为 k 的子序列中连续对的数字和乘积/](https://www.geeksforgeeks.org/maximize-product-of-digit-sum-of-consecutive-pairs-in-a-subsequence-of-length-k/)

给定整数数组 **arr[]** ，任务是**最大化**长度子序列 **K** 中每个连续对的数字和的乘积。
**注意:** K 总是偶数，因为会以偶数长度形成对。

**示例:**

> **输入:** arr[] = {2，100，99，3，16}，K = 4
> **输出:** 128
> 长度 4 的最优子序列分别为**【2，100，99，16】**
> 位数之和= 2，2，18，7。
> 所以成对数字和的乘积= 2 * 1 + 18 * 7 = 2 + 126 = **128** ，这是最大值。
> 
> **输入:** arr[] = {10，5，9，101，24，2，20，14}，K = 6
> **输出:** 69
> 长度为 6 的最优子序列=**【10，5，9，24，2，14】**
> 位数之和分别= 1，5，9，6，2，5。
> 所以成对数字和的乘积= 1 * 5+9 * 6+2 * 5 = 5+54+10 =**69**，这是最大值。

**方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。因为我们需要通过包含或排除数组中的一些元素来找到数组中的对，从而形成一个子序列。所以让 **DP[i][j][k]** 成为我们的 **dp 数组**，它存储长度为 **j 的索引 **i** 和**最后一个元素 **K** 的元素的位数之和的最大乘积。

**观测值:**

*   **奇数长度:**在选择偶数长度子序列时，当所选子序列的当前长度为奇数时，则选择最后一个元素的对。因此，我们必须计算**最后一个**和**当前**元素之和的乘积，并且我们通过在下一次调用**甚至**长度时将最后一个保持为 0 来重现。
    ![dp[i][j][k] = max(dp[i][j][k], productDigitSum(arr[k], arr[i]) + solve(i+1, j+1, 0))   ](img/acdeabe4c51f2f6e68ab0ac88e8b8435.png "Rendered by QuickLaTeX.com")
*   **偶数长度:**在选择奇数长度子序列时，当所选子序列的当前长度为偶数时，那么我们只需选择该对的第一个元素。因此，我们只需选择**当前**元素作为下一次递归调用的**最后一个**元素，并在下一次递归调用中搜索该对的**第二个**元素。
    ![dp[i][j][k] = max(dp[i][j][k], solve(i+1, j+1, i))](img/1b1ec6bbdf06ee58c1905f80665591b3.png "Rendered by QuickLaTeX.com")
*   **排除元素:**当前元素的另一个选项是排除当前元素并进一步选择元素。
    T3】

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum product of the digit
// sum of the consecutive pairs of
// the subsequence of the length K

#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;
int dp[1000][MAX][MAX];

// Function to find the product
// of two numbers digit sum
// in the pair
int productDigitSum(int x, int y)
{
    int sumx = 0;

    // Loop to find the digits of
    // the number
    while (x) {
        sumx += (x % 10);
        x /= 10;
    }
    int sumy = 0;

    // Loop to find the digits
    // of other number
    while (y) {
        sumy += (y % 10);
        y /= 10;
    }
    return (sumx * sumy);
}

// Function to find the subsequence
// of the length K
int solve(int arr[], int i, int len,
          int prev, int n, int k)
{
    // Base Case
    if (len == k)
        return 0;

    // Condition when we didn't reach
    // the length K, but ran out of
    // elements of the array
    if (i == n)
        return INT_MIN;

    // Condition if already calculated
    if (dp[i][len][prev])
        return dp[i][len][prev];

    int inc = 0, exc = 0;

    // If length upto this point is odd
    if (len & 1) {

        // If length is odd, it means we need
        // second element of this current pair,
        // calculate the product of digit sum of
        // current and previous element and recur
        // by moving towards next index
        inc = productDigitSum(arr[prev],
                              arr[i])
              + solve(arr, i + 1,
                      len + 1, 0, n, k);
    }

    // If length upto this point is even
    else {
        inc = solve(arr, i + 1, len + 1, i, n, k);
    }

    // Exclude this current element
    // and recur for next elements.
    exc = solve(arr, i + 1, len, prev, n, k);

    // return by memoizing it, by selecting
    // the maximum among two choices.
    return dp[i][len][prev] = max(inc, exc);
}

// Driver Code
int main()
{
    int arr[] = { 10, 5, 9, 101, 24, 2, 20, 14 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 6;
    cout << solve(arr, 0, 0, 0, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum product of the digit
// sum of the consecutive pairs of
// the subsequence of the length K
import java.util.*;

class GFG{

static int MAX = 100;
static int dp[][][] = new int[1000][MAX][MAX];

// Function to find the product
// of two numbers digit sum
// in the pair
static int productDigitSum(int x, int y)
{
    int sumx = 0;

    // Loop to find the digits
    // of the number
    while (x > 0)
    {
        sumx += (x % 10);
        x /= 10;
    }
    int sumy = 0;

    // Loop to find the digits
    // of other number
    while (y > 0)
    {
        sumy += (y % 10);
        y /= 10;
    }
    return (sumx * sumy);
}

// Function to find the subsequence
// of the length K
static int solve(int arr[], int i, int len,
                  int prev, int n, int k)
{

    // Base Case
    if (len == k)
        return 0;

    // Condition when we didn't reach
    // the length K, but ran out of
    // elements of the array
    if (i == n)
        return Integer.MIN_VALUE;

    // Condition if already calculated
    if (dp[i][len][prev] != 0)
        return dp[i][len][prev];

    int inc = 0, exc = 0;

    // If length upto this point is odd
    if ((len & 1) != 0)
    {

        // If length is odd, it means we need
        // second element of this current pair,
        // calculate the product of digit sum of
        // current and previous element and recur
        // by moving towards next index
        inc = (productDigitSum(arr[prev], arr[i]) +
               solve(arr, i + 1, len + 1, 0, n, k));
    }

    // If length upto this point is even
    else
    {
        inc = solve(arr, i + 1, len + 1, i, n, k);
    }

    // Exclude this current element
    // and recur for next elements.
    exc = solve(arr, i + 1, len, prev, n, k);

    // Return by memoizing it, by selecting
    // the maximum among two choices.
    return dp[i][len][prev] = Math.max(inc, exc);
}

// Driver Code
public static void main(String []args)
{
    int arr[] = { 10, 5, 9, 101, 24, 2, 20, 14 };
    int n = arr.length;
    int k = 6;

    System.out.print(solve(arr, 0, 0, 0, n, k));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum product of the digit
# sum of the consecutive pairs of
# the subsequence of the length K
import sys

MAX = 100
dp = []

for i in range(1000):
    temp1 = []
    for j in range(MAX):
        temp2 = []

        for k in range(MAX):
            temp2.append(0)
        temp1.append(temp2)

    dp.append(temp1)

# Function to find the product
# of two numbers digit sum
# in the pair
def productDigitSum(x, y):
    sumx = 0

    # Loop to find the digits of
    # the number
    while x:
        sumx += x % 10
        x = x // 10

    sumy = 0

    # Loop to find the digits
    # of other number
    while y:
        sumy += y % 10
        y = y // 10

    return sumx * sumy

# Function to find the subsequence
# of the length K
def solve(arr, i, len, prev, n, k):

    # Base case
    if len == k:
        return 0

    # Condition when we didn't reach
    # the length K, but ran out of
    # elements of the array
    if i == n:
        return -sys.maxsize - 1

    # Condition if already calculated
    if dp[i][len][prev]:
        return dp[i][len][prev]

    # If length upto this point is odd
    if len & 1:

        # If length is odd, it means we need
        # second element of this current pair,
        # calculate the product of digit sum of
        # current and previous element and recur
        # by moving towards next index
        inc = (productDigitSum(arr[prev], arr[i]) +
               solve(arr, i + 1, len + 1, i, n, k))
    else:

        # If length upto this point is even
        inc = solve(arr, i + 1, len + 1, i, n, k)

    # Exclude this current element
    # and recur for next elements.
    exc = solve(arr, i + 1, len, prev, n, k)

    # Return by memoizing it, by selecting
    # the maximum among two choices.
    dp[i][len][prev] = max(inc, exc)
    return dp[i][len][prev]

# Driver code
arr = [ 10, 5, 9, 101, 24, 2, 20, 14 ]
n = len(arr)
k = 6
print(solve(arr, 0, 0, 0, n, k))

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation to find the
// maximum product of the digit
// sum of the consecutive pairs of
// the subsequence of the length K
using System;
class GFG{

static int MAX = 100;
static int [, ,]dp = new int[1000, MAX, MAX];

// Function to find the product
// of two numbers digit sum
// in the pair
static int productDigitSum(int x, int y)
{
    int sumx = 0;

    // Loop to find the digits
    // of the number
    while (x > 0)
    {
        sumx += (x % 10);
        x /= 10;
    }
    int sumy = 0;

    // Loop to find the digits
    // of other number
    while (y > 0)
    {
        sumy += (y % 10);
        y /= 10;
    }
    return (sumx * sumy);
}

// Function to find the subsequence
// of the length K
static int solve(int []arr, int i, int len,
                 int prev, int n, int k)
{

    // Base Case
    if (len == k)
        return 0;

    // Condition when we didn't reach
    // the length K, but ran out of
    // elements of the array
    if (i == n)
        return Int32.MinValue;

    // Condition if already calculated
    if (dp[i, len, prev] != 0)
        return dp[i, len, prev];

    int inc = 0, exc = 0;

    // If length upto this point is odd
    if ((len & 1) != 0)
    {

        // If length is odd, it means we need
        // second element of this current pair,
        // calculate the product of digit sum of
        // current and previous element and recur
        // by moving towards next index
        inc = (productDigitSum(arr[prev], arr[i]) +
               solve(arr, i + 1, len + 1, 0, n, k));
    }

    // If length upto this point is even
    else
    {
        inc = solve(arr, i + 1, len + 1, i, n, k);
    }

    // Exclude this current element
    // and recur for next elements.
    exc = solve(arr, i + 1, len, prev, n, k);

    // Return by memoizing it, by selecting
    // the maximum among two choices.
    return dp[i, len, prev] = Math.Max(inc, exc);
}

// Driver Code
public static void Main()
{
    int []arr = { 10, 5, 9, 101, 24, 2, 20, 14 };
    int n = arr.Length;
    int k = 6;

    Console.Write(solve(arr, 0, 0, 0, n, k));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// maximum product of the digit
// sum of the consecutive pairs of
// the subsequence of the length K

const MAX = 100;
let dp = []

for (let i = 0; i < 1000; i++) {
    let temp1 = [];
    for (let j = 0; j < MAX; j++) {
        let temp2 = [];
        for (let k = 0; k < MAX; k++) {
            temp2.push(0)
        }
        temp1.push(temp2)
    }
    dp.push(temp1)
}

// Function to find the product
// of two numbers digit sum
// in the pair
function productDigitSum(x, y) {
    let sumx = 0;

    // Loop to find the digits of
    // the number
    while (x) {
        sumx += (x % 10);
        x = Math.floor(x / 10);
    }
    let sumy = 0;

    // Loop to find the digits
    // of other number
    while (y) {
        sumy += (y % 10);
        y = Math.floor(y / 10);
    }
    return (sumx * sumy);
}

// Function to find the subsequence
// of the length K
function solve(arr, i, len, prev, n, k) {
    // Base Case
    if (len == k)
        return 0;

    // Condition when we didn't reach
    // the length K, but ran out of
    // elements of the array
    if (i == n)
        return Number.MIN_SAFE_INTEGER;

    // Condition if already calculated
    if (dp[i][len][prev])
        return dp[i][len][prev];

    let inc = 0, exc = 0;

    // If length upto this point is odd
    if (len & 1) {

        // If length is odd, it means we need
        // second element of this current pair,
        // calculate the product of digit sum of
        // current and previous element and recur
        // by moving towards next index
        inc = productDigitSum(arr[prev],
            arr[i])
            + solve(arr, i + 1,
                len + 1, 0, n, k);
    }

    // If length upto this point is even
    else {
        inc = solve(arr, i + 1, len + 1, i, n, k);
    }

    // Exclude this current element
    // and recur for next elements.
    exc = solve(arr, i + 1, len, prev, n, k);

    // return by memoizing it, by selecting
    // the maximum among two choices.
    return dp[i][len][prev] = Math.max(inc, exc);
}

// Driver Code

let arr = [10, 5, 9, 101, 24, 2, 20, 14];
let n = arr.length;
let k = 6;
document.write(solve(arr, 0, 0, 0, n, k));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
69
```