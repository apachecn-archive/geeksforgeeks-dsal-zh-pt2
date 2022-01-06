# 三个数组的最大和，不允许从其中连续拾取元素

> 原文:[https://www . geeksforgeeks . org/三个数组的最大和-这样就不允许从同一个数组中连续选取元素/](https://www.geeksforgeeks.org/maximum-sum-from-three-arrays-such-that-picking-elements-consecutively-from-same-is-not-allowed/)

给定 **N** 整数的三个数组 **A[]** 、 **B[]** 和 **C[]** 。我们可以从这个数组中选择 **N** 个元素，使得对于每个索引 **i** 只能从这些数组中选择一个元素，即**A【I】**、**B【I】**或**C【I】**，并且不能从同一个数组中选择两个连续的元素。任务是通过从这些数组中选择元素来打印我们能得到的最大数字总和。

**示例:**

> **输入:** a[] = {10，20，30}，b[] = {40，50，60}，c[] = {70，80，90}
> **输出:** 210
> 70 + 50 + 90 = 210
> 
> **输入:** a[] = {6，8，2，7，4，2，7}，b[] = {7，8，5，8，6，3，5}，c[] = {8，3，2，6，8，4，1}
> **输出:** 46
> 从 C，A，B，A，C，B，A 中选择元素

**方法:**上述问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。让 **dp[i][j]** 被认为是最大和，直到选择了来自第 j 个数组的 i if 元素。我们可以从任何数组中为第一个索引选择一个元素，但是稍后我们可以递归地只从剩下的两个数组中为下一步选择一个元素。所有组合返回的最大和将是我们的答案。使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)避免重复和多次相同的函数调用。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int N = 3;

// Function to return the maximum sum
int FindMaximumSum(int ind, int kon, int a[], int b[],
                   int c[], int n, int dp[][N])
{

    // Base case
    if (ind == n)
        return 0;

    // Already visited
    if (dp[ind][kon] != -1)
        return dp[ind][kon];
    int ans = -1e9 + 5;

    // If the element has been taken
    // from first array in previous step
    if (kon == 0) {
        ans = max(ans, b[ind] + FindMaximumSum(ind + 1,
                                               1, a, b,
                                               c, n, dp));
        ans = max(ans, c[ind] + FindMaximumSum(ind + 1,
                                               2, a, b,
                                               c, n, dp));
    }

    // If the element has been taken
    // from second array in previous step
    else if (kon == 1) {
        ans = max(ans, a[ind] + FindMaximumSum(ind + 1,
                                               0, a, b,
                                               c, n, dp));
        ans = max(ans, c[ind] + FindMaximumSum(ind + 1,
                                               2, a, b,
                                               c, n, dp));
    }

    // If the element has been taken
    // from third array in previous step
    else if (kon == 2) {
        ans = max(ans, a[ind] + FindMaximumSum(ind + 1,
                                               1, a, b,
                                               c, n, dp));
        ans = max(ans, b[ind] + FindMaximumSum(ind + 1,
                                               0, a, b,
                                               c, n, dp));
    }

    return dp[ind][kon] = ans;
}

// Driver code
int main()
{
    int a[] = { 6, 8, 2, 7, 4, 2, 7 };
    int b[] = { 7, 8, 5, 8, 6, 3, 5 };
    int c[] = { 8, 3, 2, 6, 8, 4, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    int dp[n][N];
    memset(dp, -1, sizeof dp);

    // Pick element from first array
    int x = FindMaximumSum(0, 0, a, b, c, n, dp);

    // Pick element from second array
    int y = FindMaximumSum(0, 1, a, b, c, n, dp);

    // Pick element from third array
    int z = FindMaximumSum(0, 2, a, b, c, n, dp);

    // Print the maximum of them
    cout << max(x, max(y, z));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

static int N = 3;

// Function to return the maximum sum
static int FindMaximumSum(int ind, int kon, int a[],
               int b[], int c[], int n, int dp[][])

{
    // Base case
    if (ind == n)
        return 0;

    // Already visited
    if (dp[ind][kon] != -1)
        return dp[ind][kon];
    int ans = (int) (-1e9 + 5);

    // If the element has been taken
    // from first array in previous step
    if (kon == 0) {
        ans = Math.max(ans, b[ind] +
              FindMaximumSum(ind + 1,
                  1, a, b,c, n, dp));

        ans = Math.max(ans, c[ind] +
              FindMaximumSum(ind + 1,
                 2, a, b,c, n, dp));

    }

    // If the element has been taken
    // from second array in previous step
    else if (kon == 1) {
        ans = Math.max(ans, a[ind] +
              FindMaximumSum(ind + 1,
                 0, a, b, c, n, dp));

        ans = Math.max(ans, c[ind] +
              FindMaximumSum(ind + 1,
                 2, a, b, c, n, dp));

    }

    // If the element has been taken
    // from third array in previous step
    else if (kon == 2) {
        ans = Math.max(ans, a[ind] +
              FindMaximumSum(ind + 1,
                 1, a, b, c, n, dp));

        ans = Math.max(ans, b[ind] +
              FindMaximumSum(ind + 1,
                 0, a, b, c, n, dp));

    }

    return dp[ind][kon] = ans;
}

// Driver code
public static void main(String[] args) {

    int a[] = { 6, 8, 2, 7, 4, 2, 7 };
    int b[] = { 7, 8, 5, 8, 6, 3, 5 };
    int c[] = { 8, 3, 2, 6, 8, 4, 1 };
    int n = a.length;
    int dp[][] = new int[n][N];

    for(int i = 0; i < n; i++) {

        for(int j = 0; j < N; j++) {
            dp[i][j] =- 1;
        }
    }

    // Pick element from first array
    int x = FindMaximumSum(0, 0, a, b, c, n, dp);

    // Pick element from second array
    int y = FindMaximumSum(0, 1, a, b, c, n, dp);

    // Pick element from third array
    int z = FindMaximumSum(0, 2, a, b, c, n, dp);

    // Print the maximum of them
    System.out.println(Math.max(x, Math.max(y, z)));

    }
}
// This code has been contributed
// by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum sum
def FindMaximumSum(ind, kon, a, b, c, n, dp):

    # Base case
    if ind == n:
        return 0

    # Already visited
    if dp[ind][kon] != -1:
        return dp[ind][kon]

    ans = -10 ** 9 + 5

    # If the element has been taken
    # from first array in previous step
    if kon == 0:
        ans = max(ans, b[ind] +
                  FindMaximumSum(ind + 1, 1,
                                 a, b, c, n, dp))
        ans = max(ans, c[ind] +
                  FindMaximumSum(ind + 1, 2,
                                 a, b, c, n, dp))

    # If the element has been taken
    # from second array in previous step
    elif kon == 1:
        ans = max(ans, a[ind] +
                  FindMaximumSum(ind + 1, 0,
                                 a, b, c, n, dp))
        ans = max(ans, c[ind] +
                  FindMaximumSum(ind + 1, 2,
                                 a, b, c, n, dp))

    # If the element has been taken
    # from third array in previous step
    elif kon == 2:
        ans = max(ans, a[ind] +
                  FindMaximumSum(ind + 1, 1,
                                 a, b, c, n, dp))
        ans = max(ans, b[ind] +
                  FindMaximumSum(ind + 1, 0,
                                 a, b, c, n, dp))

    dp[ind][kon] = ans
    return ans

# Driver code
if __name__ == "__main__":

    N = 3
    a = [6, 8, 2, 7, 4, 2, 7]
    b = [7, 8, 5, 8, 6, 3, 5]
    c = [8, 3, 2, 6, 8, 4, 1]
    n = len(a)

    dp = [[-1 for i in range(N)]
              for j in range(n)]

    # Pick element from first array
    x = FindMaximumSum(0, 0, a, b, c, n, dp)

    # Pick element from second array
    y = FindMaximumSum(0, 1, a, b, c, n, dp)

    # Pick element from third array
    z = FindMaximumSum(0, 2, a, b, c, n, dp)

    # Print the maximum of them
    print(max(x, y, z))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    static int N = 3;

    // Function to return the maximum sum
    static int FindMaximumSum(int ind, int kon, int []a,
                int []b, int []c, int n, int [,]dp)

    {
        // Base case
        if (ind == n)
            return 0;

        // Already visited
        if (dp[ind,kon] != -1)
            return dp[ind,kon];
        int ans = (int) (-1e9 + 5);

        // If the element has been taken
        // from first array in previous step
        if (kon == 0)
        {
            ans = Math.Max(ans, b[ind] +
                FindMaximumSum(ind + 1,
                    1, a, b,c, n, dp));

            ans = Math.Max(ans, c[ind] +
                FindMaximumSum(ind + 1,
                    2, a, b,c, n, dp));

        }

        // If the element has been taken
        // from second array in previous step
        else if (kon == 1)
        {
            ans = Math.Max(ans, a[ind] +
                FindMaximumSum(ind + 1,
                    0, a, b, c, n, dp));

            ans = Math.Max(ans, c[ind] +
                FindMaximumSum(ind + 1,
                    2, a, b, c, n, dp));

        }

        // If the element has been taken
        // from third array in previous step
        else if (kon == 2)
        {
            ans = Math.Max(ans, a[ind] +
                FindMaximumSum(ind + 1,
                    1, a, b, c, n, dp));

            ans = Math.Max(ans, b[ind] +
                FindMaximumSum(ind + 1,
                    0, a, b, c, n, dp));

        }

        return dp[ind,kon] = ans;
    }

    // Driver code
    public static void Main()
    {

        int []a = { 6, 8, 2, 7, 4, 2, 7 };
        int []b = { 7, 8, 5, 8, 6, 3, 5 };
        int []c = { 8, 3, 2, 6, 8, 4, 1 };
        int n = a.Length;
        int [,]dp = new int[n,N];

        for(int i = 0; i < n; i++)
        {

            for(int j = 0; j < N; j++)
            {
                dp[i,j] =- 1;
            }
        }

        // Pick element from first array
        int x = FindMaximumSum(0, 0, a, b, c, n, dp);

        // Pick element from second array
        int y = FindMaximumSum(0, 1, a, b, c, n, dp);

        // Pick element from third array
        int z = FindMaximumSum(0, 2, a, b, c, n, dp);

        // Print the maximum of them
        Console.WriteLine(Math.Max(x, Math.Max(y, z)));

        }
}

// This code has been contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$N = 3;

// Function to return the maximum sum
function FindMaximumSum($ind, $kon, $a,
                        $b, $c, $n, $dp)
{
    global $N;

    // Base case
    if ($ind == $n)
        return 0;

    // Already visited
    if ($dp[$ind][$kon] != -1)
        return $dp[$ind][$kon];
    $ans = -1e9 + 5;

    // If the element has been taken
    // from first array in previous step
    if ($kon == 0)
    {
        $ans = max($ans, $b[$ind] +
                   FindMaximumSum($ind + 1, 1, $a,
                                  $b, $c, $n, $dp));
        $ans = max($ans, $c[$ind] +
                   FindMaximumSum($ind + 1, 2, $a,
                                  $b, $c, $n, $dp));
    }

    // If the element has been taken
    // from second array in previous step
    else if ($kon == 1)
    {
        $ans = max($ans, $a[$ind] +
                   FindMaximumSum($ind + 1, 0,
                                  $a, $b, $c, $n, $dp));
        $ans = max($ans, $c[$ind] +
                   FindMaximumSum($ind + 1, 2,
                                  $a, $b, $c, $n, $dp));
    }

    // If the element has been taken
    // from third array in previous step
    else if ($kon == 2)
    {
        $ans = max($ans, $a[$ind] +
                   FindMaximumSum($ind + 1, 1,
                                  $a, $b, $c, $n, $dp));
        $ans = max($ans, $b[$ind] +
                   FindMaximumSum($ind + 1, 0,
                                  $a, $b, $c, $n, $dp));
    }

    return $dp[$ind][$kon] = $ans;
}

// Driver code
$a = array( 6, 8, 2, 7, 4, 2, 7 );
$b = array( 7, 8, 5, 8, 6, 3, 5 );
$c = array( 8, 3, 2, 6, 8, 4, 1 );
$n = count($a);
$dp = array_fill(0, $n,
      array_fill(0, $N, -1));

// Pick element from first array
$x = FindMaximumSum(0, 0, $a, $b,
                      $c, $n, $dp);

// Pick element from second array
$y = FindMaximumSum(0, 1, $a, $b,
                      $c, $n, $dp);

// Pick element from third array
$z = FindMaximumSum(0, 2, $a, $b,
                      $c, $n, $dp);

// Print the maximum of them
print(max($x, max($y, $z)));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
var N = 3;

// Function to return the maximum sum
function FindMaximumSum(ind, kon, a, b, c, n, dp)
{

    // Base case
    if (ind == n)
        return 0;

    // Already visited
    if (dp[ind][kon] != -1)
        return dp[ind][kon];
    var ans = -1000000005;

    // If the element has been taken
    // from first array in previous step
    if (kon == 0) {
        ans = Math.max(ans, b[ind] + FindMaximumSum(ind + 1,
                                               1, a, b,
                                               c, n, dp));
        ans = Math.max(ans, c[ind] + FindMaximumSum(ind + 1,
                                               2, a, b,
                                               c, n, dp));
    }

    // If the element has been taken
    // from second array in previous step
    else if (kon == 1) {
        ans = Math.max(ans, a[ind] + FindMaximumSum(ind + 1,
                                               0, a, b,
                                               c, n, dp));
        ans = Math.max(ans, c[ind] + FindMaximumSum(ind + 1,
                                               2, a, b,
                                               c, n, dp));
    }

    // If the element has been taken
    // from third array in previous step
    else if (kon == 2) {
        ans = Math.max(ans, a[ind] + FindMaximumSum(ind + 1,
                                               1, a, b,
                                               c, n, dp));
        ans = Math.max(ans, b[ind] + FindMaximumSum(ind + 1,
                                               0, a, b,
                                               c, n, dp));
    }

    return dp[ind][kon] = ans;
}

// Driver code
var a = [ 6, 8, 2, 7, 4, 2, 7 ];
var b = [ 7, 8, 5, 8, 6, 3, 5 ];
var c = [ 8, 3, 2, 6, 8, 4, 1 ];
var n = a.length;
var dp = Array.from(Array(n), ()=> Array(n).fill(-1));
// Pick element from first array
var x = FindMaximumSum(0, 0, a, b, c, n, dp);
// Pick element from second array
var y = FindMaximumSum(0, 1, a, b, c, n, dp);
// Pick element from third array
var z = FindMaximumSum(0, 2, a, b, c, n, dp);
// Print the maximum of them
document.write( Math.max(x, Math.max(y, z)));

</script>
```

**Output:** 

```
45
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)