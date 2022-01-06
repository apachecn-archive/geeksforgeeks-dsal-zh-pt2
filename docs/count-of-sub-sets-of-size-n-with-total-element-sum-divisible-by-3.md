# 元素总和可被 3 整除的大小为 n 的子集数

> 原文:[https://www . geesforgeks . org/总元素和可被 3 整除的 n 尺寸子集合计数/](https://www.geeksforgeeks.org/count-of-sub-sets-of-size-n-with-total-element-sum-divisible-by-3/)

给定一个整数 **n** 和一个范围**【l，r】**，任务是用给定范围内的整数找到总大小子集 **n** 的计数，使得其元素的总和可被 **3** 整除。
**举例:**

> **输入:** n = 2，l = 1，r = 5
> **输出:** 9
> 可能的子集有{1，2}、{2，1}、{3，3}、{5，1}、{1，5}、{4，2}、{2，4}、{5，4}和{4，5}
> **输入:** n = 3，l = 9，r = 9
> **输出:**

**方法:**因为我们需要子集元素的和能被 3 整除。因此，我们不再关心这些数字，而是对这些数字进行计数，这样它们在与 **3** 分开时会给出余数 **0** 、 **1** 和 **2** ，分别用下面给出的公式:

> 例如，一个元素 **k** 使得 **k % 3 = 2** 对于某个整数 **x** 可以被发现为 **k = 3 * x + 2** 。
> 然后我们有**l≤(3 * x)+2≤r**
> **l–2≤(3 * x)≤r–2**
> **天花板((l–2)/3)≤x≤地板((r–2)/3)**

现在，通过动态编程 **dp[i][j]** 我们可以检查有多少元素会给出一个可被 **3** 整除的和。这里 **dp[i][j]** 代表第一个 **i** 元素的和，这些元素在除以 **3** 时给出余数 **j** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define MOD 1000000007
#define ll long long int
using namespace std;

// Function to return the total number of
// required sub-sets
int totalSubSets(ll n, ll l, ll r)
{

    // Variable to store total elements
    // which on dividing by 3  give
    // remainder 0, 1 and 2 respectively
    ll zero = floor((double)r / 3)
              - ceil((double)l / 3) + 1;
    ll one = floor((double)(r - 1) / 3)
             - ceil((double)(l - 1) / 3) + 1;
    ll two = floor((double)(r - 2) / 3)
             - ceil((double)(l - 2) / 3) + 1;

    // Create a dp table
    ll dp[n][3];
    memset(dp, 0, sizeof(dp));
    dp[0][0] = zero;
    dp[0][1] = one;
    dp[0][2] = two;

    // Process for n states and store
    // the sum (mod 3) for 0, 1 and 2
    for (ll i = 1; i < n; ++i) {

        // Use of MOD for large numbers
        dp[i][0] = ((dp[i - 1][0] * zero)
                    + (dp[i - 1][1] * two)
                    + (dp[i - 1][2] * one))
                   % MOD;
        dp[i][1] = ((dp[i - 1][0] * one)
                    + (dp[i - 1][1] * zero)
                    + (dp[i - 1][2] * two))
                   % MOD;
        dp[i][2] = ((dp[i - 1][0] * two)
                    + (dp[i - 1][1] * one)
                    + (dp[i - 1][2] * zero))
                   % MOD;
    }

    // Final answer store at dp[n - 1][0]
    return dp[n - 1][0];
}

// Driver Program
int main()
{
    ll n = 5;
    ll l = 10;
    ll r = 100;
    cout << totalSubSets(n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    static int MOD = 1000000007;

    // Function to return the total number of
    // required sub-sets
    static int totalSubSets(int n, int l, int r)
    {

        // Variable to store total elements
        // which on dividing by 3 give
        // remainder 0, 1 and 2 respectively
        int zero = (int)Math.floor((double)r / 3)
                - (int)Math.ceil((double)l / 3) + 1;
        int one = (int)Math.floor((double)(r - 1) / 3)
                - (int)Math.ceil((double)(l - 1) / 3) + 1;
        int two = (int)Math.floor((double)(r - 2) / 3)
                - (int)Math.ceil((double)(l - 2) / 3) + 1;

        // Create a dp table
        int [][] dp = new int[n][3];

        dp[0][0] = zero;
        dp[0][1] = one;
        dp[0][2] = two;

        // Process for n states and store
        // the sum (mod 3) for 0, 1 and 2
        for (int i = 1; i < n; ++i)
        {

            // Use of MOD for large numbers
            dp[i][0] = ((dp[i - 1][0] * zero)
                        + (dp[i - 1][1] * two)
                        + (dp[i - 1][2] * one))
                    % MOD;
            dp[i][1] = ((dp[i - 1][0] * one)
                        + (dp[i - 1][1] * zero)
                        + (dp[i - 1][2] * two))
                    % MOD;
            dp[i][2] = ((dp[i - 1][0] * two)
                        + (dp[i - 1][1] * one)
                        + (dp[i - 1][2] * zero))
                    % MOD;
        }

        // Final answer store at dp[n - 1][0]
        return dp[n - 1][0];
    }

    // Driver Program
    public static void main(String []args)
    {
        int n = 5;
        int l = 10;
        int r = 100;
        System.out.println(totalSubSets(n, l, r));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to return the total
# number of required sub-sets
def totalSubSets(n, l, r):

    MOD = 1000000007 ;

    # Variable to store total elements
    # which on dividing by 3 give
    # remainder 0, 1 and 2 respectively
    zero = (math.floor(r / 3) -
            math.ceil(l / 3) + 1);
    one = (math.floor((r - 1) / 3) -
           math.ceil((l - 1) / 3) + 1);
    two = (math.floor((r - 2) / 3) -
           math.ceil((l - 2) / 3) + 1);

    # Create a dp table
    dp = [[0 for x in range(3)]
             for y in range(n)]

    dp[0][0] = zero;
    dp[0][1] = one;
    dp[0][2] = two;

    # Process for n states and store
    # the sum (mod 3) for 0, 1 and 2
    for i in range(1, n):

        # Use of MOD for large numbers
        dp[i][0] = ((dp[i - 1][0] * zero) +
                    (dp[i - 1][1] * two) +
                    (dp[i - 1][2] * one)) % MOD;
        dp[i][1] = ((dp[i - 1][0] * one) +
                    (dp[i - 1][1] * zero) +
                    (dp[i - 1][2] * two)) % MOD;
        dp[i][2] = ((dp[i - 1][0] * two)+
                    (dp[i - 1][1] * one) +
                    (dp[i - 1][2] * zero)) % MOD;

    # Final answer store at dp[n - 1][0]
    return dp[n - 1][0];

# Driver Code
n = 5;
l = 10;
r = 100;
print(totalSubSets(n, l, r));

# This code is contributed
# by chandan_jnu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MOD = 1000000007;

    // Function to return the total number of
    // required sub-sets
    static int totalSubSets(int n, int l, int r)
    {

        // Variable to store total elements
        // which on dividing by 3 give
        // remainder 0, 1 and 2 respectively
        int zero = (int)Math.Floor((double)r / 3)
                - (int)Math.Ceiling((double)l / 3) + 1;
        int one = (int)Math.Floor((double)(r - 1) / 3)
                - (int)Math.Ceiling((double)(l - 1) / 3) + 1;
        int two = (int)Math.Floor((double)(r - 2) / 3)
                - (int)Math.Ceiling((double)(l - 2) / 3) + 1;

        // Create a dp table
        int [, ] dp = new int[n, 3];

        dp[0,0] = zero;
        dp[0,1] = one;
        dp[0,2] = two;

        // Process for n states and store
        // the sum (mod 3) for 0, 1 and 2
        for (int i = 1; i < n; ++i)
        {

            // Use of MOD for large numbers
            dp[i,0] = ((dp[i - 1, 0] * zero)
                        + (dp[i - 1, 1] * two)
                        + (dp[i - 1, 2] * one))
                    % MOD;
            dp[i,1] = ((dp[i - 1, 0] * one)
                        + (dp[i - 1, 1] * zero)
                        + (dp[i - 1, 2] * two))
                    % MOD;
            dp[i,2] = ((dp[i - 1, 0] * two)
                        + (dp[i - 1, 1] * one)
                        + (dp[i - 1, 2] * zero))
                    % MOD;
        }

        // Final answer store at dp[n - 1,0]
        return dp[n - 1, 0];
    }

    // Driver Program
    public static void Main()
    {
        int n = 5;
        int l = 10;
        int r = 100;
        Console.WriteLine(totalSubSets(n, l, r));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
# Php implementation of the approach

# Function to return the total number of
# required sub-sets
function totalSubSets($n, $l, $r)
{

    $MOD = 1000000007 ;
    // Variable to store total elements
    // which on dividing by 3 give
    // remainder 0, 1 and 2 respectively
    $zero = floor($r / 3)
            - ceil($l / 3) + 1;
    $one = floor(($r - 1) / 3)
            - ceil(($l - 1) / 3) + 1;
    $two = floor(($r - 2) / 3)
            - ceil(($l - 2) / 3) + 1;

    // Create a dp table
    $dp = array() ;
    for($i = 0; $i < $n; $i++)
        for($j = 0; $j < 3; $j++)
            $dp[$i][$j] = 0 ;

    $dp[0][0] = $zero;
    $dp[0][1] = $one;
    $dp[0][2] = $two;

    // Process for n states and store
    // the sum (mod 3) for 0, 1 and 2
    for ($i = 1; $i < $n; ++$i)
    {

        // Use of MOD for large numbers
        $dp[$i][0] = (($dp[$i - 1][0] * $zero)
                    + ($dp[$i - 1][1] * $two)
                    + ($dp[$i - 1][2] * $one))
                % $MOD;
        $dp[$i][1] = (($dp[$i - 1][0] * $one)
                    + ($dp[$i - 1][1] * $zero)
                    + ($dp[$i - 1][2] * $two))
                % $MOD;
        $dp[$i][2] = (($dp[$i - 1][0] * $two)
                    + ($dp[$i - 1][1] * $one)
                    + ($dp[$i - 1][2] * $zero))
                % $MOD;
    }

    // Final answer store at dp[n - 1][0]
    return $dp[$n - 1][0];
}

// Driver Program
$n = 5;
$l = 10;
$r = 100;
echo totalSubSets($n, $l, $r);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let MOD = 1000000007;

    // Function to return the total number of
    // required sub-sets
    function totalSubSets(n, l, r)
    {

        // Variable to store total elements
        // which on dividing by 3 give
        // remainder 0, 1 and 2 respectively
        let zero = Math.floor(r / 3)
                - Math.ceil(l / 3) + 1;
        let one = Math.floor((r - 1) / 3)
                - Math.ceil((l - 1) / 3) + 1;
        let two = Math.floor((r - 2) / 3)
                - Math.ceil((l - 2) / 3) + 1;

        // Create a dp table
        let dp = new Array(n);
        for(let i = 0; i < n; i++)
        {
            dp[i] = new Array(3);
            for(let j = 0; j < 3; j++)
            {
                dp[i][j] = 0;
            }
        }

        dp[0][0] = zero;
        dp[0][1] = one;
        dp[0][2] = two;

        // Process for n states and store
        // the sum (mod 3) for 0, 1 and 2
        for (let i = 1; i < n; ++i)
        {

            // Use of MOD for large numbers
            dp[i][0] = ((dp[i - 1][0] * zero)
                        + (dp[i - 1][1] * two)
                        + (dp[i - 1][2] * one))
                    % MOD;
            dp[i][1] = ((dp[i - 1][0] * one)
                        + (dp[i - 1][1] * zero)
                        + (dp[i - 1][2] * two))
                    % MOD;
            dp[i][2] = ((dp[i - 1][0] * two)
                        + (dp[i - 1][1] * one)
                        + (dp[i - 1][2] * zero))
                    % MOD;
        }

        // Final answer store at dp[n - 1][0]
        return dp[n - 1][0];
    }

    let n = 5;
    let l = 10;
    let r = 100;
    document.write(totalSubSets(n, l, r));

</script>
```

**Output:** 

```
80107136
```