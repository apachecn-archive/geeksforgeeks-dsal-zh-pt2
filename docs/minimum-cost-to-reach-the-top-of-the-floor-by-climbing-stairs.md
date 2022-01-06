# 爬楼梯到达楼层顶部的最小成本

> 原文:[https://www . geesforgeks . org/爬楼梯到达楼层顶部的最低成本/](https://www.geeksforgeeks.org/minimum-cost-to-reach-the-top-of-the-floor-by-climbing-stairs/)

给定 N 个非负整数，表示从每个楼梯移动的成本。第一步付费，你可以爬一两步。假设可以从 0 步或 1 步开始，任务是通过爬 N 级楼梯找到到达楼层顶部(N+1)的最小成本。

**示例:**

```
Input: a[] = { 16, 19, 10, 12, 18 }
Output: 31
Start from 19 and then move to 12\. 

Input: a[] = {2, 5, 3, 1, 7, 3, 4}
Output: 9 
2->3->1->3
```

**方法:**设 dp[i]为从第 0 步或第 1 步爬第 I 级楼梯的费用。因此 ***dp[i] =成本[i] +最低(dp[i-1]，dp[i-2])*** 。由于需要 dp[i-1]和 dp[i-2]来计算从第 I 步开始的旅行成本，因此可以使用自下而上的方法来解决这个问题。答案将是到达 n-1 <sup>第</sup>级楼梯和 n-2 <sup>第</sup>级楼梯的最低成本。以自下而上的方式计算 dp[]数组。

下面是上述方法的实现。

## C++

```
// C++ program to find the minimum
// cost required to reach the n-th floor
#include <bits/stdc++.h>
using namespace std;

// function to find the minimum cost
// to reach N-th floor
int minimumCost(int cost[], int n)
{
    // declare an array
    int dp[n];

    // base case
    if (n == 1)
        return cost[0];

    // initially to climb till 0-th
    // or 1th stair
    dp[0] = cost[0];
    dp[1] = cost[1];

    // iterate for finding the cost
    for (int i = 2; i < n; i++) {
        dp[i] = min(dp[i - 1], dp[i - 2]) + cost[i];
    }

    // return the minimum
    return min(dp[n - 2], dp[n - 1]);
}

// Driver Code
int main()
{
    int a[] = { 16, 19, 10, 12, 18 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << minimumCost(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// minimum cost required to
// reach the n-th floor
import java.io.*;
import java.util.*;

class GFG
{
// function to find
// the minimum cost
// to reach N-th floor
static int minimumCost(int cost[],
                       int n)
{
    // declare an array
    int dp[] = new int[n];

    // base case
    if (n == 1)
        return cost[0];

    // initially to
    // climb till 0-th
    // or 1th stair
    dp[0] = cost[0];
    dp[1] = cost[1];

    // iterate for finding the cost
    for (int i = 2; i < n; i++)
    {
        dp[i] = Math.min(dp[i - 1],
                         dp[i - 2]) + cost[i];
    }

    // return the minimum
    return Math.min(dp[n - 2],
                    dp[n - 1]);
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 16, 19, 10, 12, 18 };
    int n = a.length;
    System.out.print(minimumCost(a, n));
}
}
```

## 蟒蛇 3

```
# Python3 program to find
# the minimum cost required
# to reach the n-th floor

# function to find the minimum
# cost to reach N-th floor
def minimumCost(cost, n):

    # declare an array
    dp = [None]*n

    # base case
    if n == 1:
        return cost[0]

    # initially to climb
    # till 0-th or 1th stair
    dp[0] = cost[0]
    dp[1] = cost[1]

    # iterate for finding the cost
    for i in range(2, n):
        dp[i] = min(dp[i - 1],
                    dp[i - 2]) + cost[i]

    # return the minimum
    return min(dp[n - 2], dp[n - 1])

# Driver Code
if __name__ == "__main__":
    a = [16, 19, 10, 12, 18 ]
    n = len(a)
    print(minimumCost(a, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the
// minimum cost required to
// reach the n-th floor
using System;

class GFG
{
// function to find
// the minimum cost
// to reach N-th floor
static int minimumCost(int[] cost,
                       int n)
{
    // declare an array
    int []dp = new int[n];

    // base case
    if (n == 1)
        return cost[0];

    // initially to
    // climb till 0-th
    // or 1th stair
    dp[0] = cost[0];
    dp[1] = cost[1];

    // iterate for finding the cost
    for (int i = 2; i < n; i++)
    {
        dp[i] = Math.Min(dp[i - 1],
                         dp[i - 2]) + cost[i];
    }

    // return the minimum
    return Math.Min(dp[n - 2],
                    dp[n - 1]);
}

// Driver Code
public static void Main()
{
    int []a = { 16, 19, 10, 12, 18 };
    int n = a.Length;
    Console.WriteLine(minimumCost(a, n));
}
}

// This code is contributed
// by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// minimum cost required
// to reach the n-th floor

// function to find the minimum
// cost to reach N-th floor
function minimumCost(&$cost, $n)
{
    // declare an array

    // base case
    if ($n == 1)
        return $cost[0];

    // initially to climb
    // till 0-th or 1th stair
    $dp[0] = $cost[0];
    $dp[1] = $cost[1];

    // iterate for finding
    // the cost
    for ($i = 2; $i < $n; $i++)
    {
        $dp[$i] = min($dp[$i - 1],
                      $dp[$i - 2]) +
                      $cost[$i];
    }

    // return the minimum
    return min($dp[$n - 2],
               $dp[$n - 1]);
}

// Driver Code
$a = array(16, 19, 10, 12, 18);
$n = sizeof($a);
echo(minimumCost($a, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// minimum cost required to
// reach the n-th floor

    // function to find
// the minimum cost
// to reach N-th floor   
    function minimumCost(cost,n)
    {
        // declare an array
    let dp = new Array(n);

    // base case
    if (n == 1)
        return cost[0];

    // initially to
    // climb till 0-th
    // or 1th stair
    dp[0] = cost[0];
    dp[1] = cost[1];

    // iterate for finding the cost
    for (let i = 2; i < n; i++)
    {
        dp[i] = Math.min(dp[i - 1],
                         dp[i - 2]) + cost[i];
    }

    // return the minimum
    return Math.min(dp[n - 2],
                    dp[n - 1]);
    }

    // Driver Code
    let a=[16, 19, 10, 12, 18 ];
    let n = a.length;
    document.write(minimumCost(a, n));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
31
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)

**空间优化方法:**使用双变量 dp1 和 dp2，而不是使用 dp[]数组来计算成本。因为到达最后两个楼梯的成本是必需的，所以使用两个变量，并在爬一个楼梯时通过交换来更新它们。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum
// cost required to reach the n-th floor
// space-optimized solution
#include <bits/stdc++.h>
using namespace std;

// function to find the minimum cost
// to reach N-th floor
int minimumCost(int cost[], int n)
{
    int dp1 = 0, dp2 = 0;

    // traverse till N-th stair
    for (int i = 0; i < n; i++) {
        int dp0 = cost[i] + min(dp1, dp2);

        // update the last two stairs value
        dp2 = dp1;
        dp1 = dp0;
    }
    return min(dp1, dp2);
}
// Driver Code
int main()
{
    int a[] = { 2, 5, 3, 1, 7, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << minimumCost(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// minimum cost required to
// reach the n-th floor
// space-optimized solution
import java.io.*;
import java.util.*;

class GFG
{
// function to find
// the minimum cost
// to reach N-th floor
static int minimumCost(int cost[], int n)
{
    int dp1 = 0, dp2 = 0;

    // traverse till N-th stair
    for (int i = 0; i < n; i++)
    {
        int dp0 = cost[i] +
                  Math.min(dp1, dp2);

        // update the last
        // two stairs value
        dp2 = dp1;
        dp1 = dp0;
    }
    return Math.min(dp1, dp2);
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 2, 5, 3, 1, 7, 3, 4 };
    int n = a.length;
    System.out.print(minimumCost(a, n));
}
}
```

## 蟒蛇 3

```
# Python3 program to find
# the minimum cost required
# to reach the n-th floor
# space-optimized solution

# function to find the minimum
# cost to reach N-th floor
def minimumCost(cost, n):

    dp1 = 0
    dp2 = 0

    # traverse till N-th stair
    for i in range(n):
        dp0 = cost[i] + min(dp1, dp2)

        # update the last
        # two stairs value
        dp2 = dp1
        dp1 = dp0
    return min(dp1, dp2)

# Driver Code
if __name__ == "__main__":
    a = [ 2, 5, 3, 1, 7, 3, 4 ]
    n = len(a)
    print(minimumCost(a, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the
// minimum cost required to
// reach the n-th floor
// space-optimized solution
using System;

class GFG
{
// function to find
// the minimum cost
// to reach N-th floor
static int minimumCost(int[] cost,
                       int n)
{
    int dp1 = 0, dp2 = 0;

    // traverse till N-th stair
    for (int i = 0; i < n; i++)
    {
        int dp0 = cost[i] +
                  Math.Min(dp1, dp2);

        // update the last
        // two stairs value
        dp2 = dp1;
        dp1 = dp0;
    }
    return Math.Min(dp1, dp2);
}

// Driver Code
public static void Main()
{
    int[] a = { 2, 5, 3, 1, 7, 3, 4 };
    int n = a.Length;
    Console.Write(minimumCost(a, n));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// minimum cost required to
// reach the n-th floor
// space-optimized solution

// function to find the minimum
// cost to reach N-th floor
function minimumCost(&$cost, $n)
{
    $dp1 = 0;
    $dp2 = 0;

    // traverse till N-th stair
    for ($i = 0; $i < $n; $i++)
    {
        $dp0 = $cost[$i] +
               min($dp1, $dp2);

        // update the last
        // two stairs value
        $dp2 = $dp1;
        $dp1 = $dp0;
    }
    return min($dp1, $dp2);
}
// Driver Code
$a = array(2, 5, 3, 1, 7, 3, 4);
$n = sizeof($a);
echo (minimumCost($a, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to find the
// minimum cost required to
// reach the n-th floor
// space-optimized solution

    // function to find
// the minimum cost
// to reach N-th floor
    function minimumCost(cost,n)
    {
        let dp1 = 0, dp2 = 0;

    // traverse till N-th stair
    for (let i = 0; i < n; i++)
    {
        let dp0 = cost[i] +
                  Math.min(dp1, dp2);

        // update the last
        // two stairs value
        dp2 = dp1;
        dp1 = dp0;
    }
    return Math.min(dp1, dp2);
    }

    // Driver Code
    let a=[2, 5, 3, 1, 7, 3, 4 ];
    let n = a.length;
    document.write(minimumCost(a, n));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
9
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)

使用自顶向下的方法可以解决以下问题。在这种情况下，重复次数将为 **dp[i] =成本[i] +分钟(dp[i+1]，dp[i+2])。**