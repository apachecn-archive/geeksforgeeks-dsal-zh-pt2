# 使用大于或等于 m 的数字对 n 求和的不同方式

> 原文:[https://www . geesforgeks . org/different-way-sum-n-using-numbers-great-equal-m/](https://www.geeksforgeeks.org/different-ways-sum-n-using-numbers-greater-equal-m/)

给定两个自然数 **n** 和 **m** 。任务是找出大于或等于 m 的数相加得到总和 n 的方法数
**例:**

```
Input : n = 3, m = 1
Output : 3
Following are three different ways
to get sum n such that each term is
greater than or equal to m
1 + 1 + 1, 1 + 2, 3 

Input : n = 2, m = 1
Output : 2
Two ways are 1 + 1 and 2
```

想法是通过定义 2D 矩阵来使用动态规划，比如 dp[][]。 **dp[i][j]** 定义用大于或等于 j 的数得到和 I 的方法数，因此 dp[i][j]可以定义为:

> **如果 i < j，dp[i][j] = 0** ，因为我们无法使用大于或等于 j 的数字来实现 I 的较小和
> **如果 i = j，dp[i][j] = 1** ，因为只有一种方法可以使用等于 j 的数字 I 来显示和 I，否则 DP[I][j]= DP[I][j+1]+DP[I-j][j]， 因为使用大于或等于 j 的数获得 I 的和等于使用大于或等于 j+1 的数获得 I 的和以及使用大于或等于 j 的数获得 i-j 的和的和。

以下是该方法的实现:

## C++

```
// CPP Program to find number of ways to
// which numbers that are greater than
// given number can be added to get sum.
#include <bits/stdc++.h>
#define MAX 100
using namespace std;

// Return number of ways to which numbers
// that are greater than given number can
// be added to get sum.
int numberofways(int n, int m)
{
    int dp[n+2][n+2];
    memset(dp, 0, sizeof(dp));

    dp[0][n + 1] = 1;

    // Filling the table. k is for numbers
    // greater than or equal that are allowed.
    for (int k = n; k >= m; k--) {

        // i is for sum
        for (int i = 0; i <= n; i++) {

            // initializing dp[i][k] to number
            // ways to get sum using numbers
            // greater than or equal k+1
            dp[i][k] = dp[i][k + 1];

            // if i > k
            if (i - k >= 0)
                dp[i][k] = (dp[i][k] + dp[i - k][k]);
        }
    }

    return dp[n][m];
}

// Driver Program
int main()
{
    int n = 3, m = 1;
    cout << numberofways(n, m) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find number of ways to
// which numbers that are greater than
// given number can be added to get sum.
import java.io.*;

class GFG {

    // Return number of ways to which numbers
    // that are greater than given number can
    // be added to get sum.
    static int numberofways(int n, int m)
    {
        int dp[][]=new int[n+2][n+2];

        dp[0][n + 1] = 1;

        // Filling the table. k is for numbers
        // greater than or equal that are allowed.
        for (int k = n; k >= m; k--) {

            // i is for sum
            for (int i = 0; i <= n; i++) {

                // initializing dp[i][k] to number
                // ways to get sum using numbers
                // greater than or equal k+1
                dp[i][k] = dp[i][k + 1];

                // if i > k
                if (i - k >= 0)
                    dp[i][k] = (dp[i][k] + dp[i - k][k]);
            }
        }

        return dp[n][m];
    }

    // Driver Program
    public static void main(String args[])
    {
        int n = 3, m = 1;
        System.out.println(numberofways(n, m));
    }
}

/*This code is contributed by Nikita tiwari.*/
```

## 蟒蛇 3

```
# Python3 Program to find number of ways to
# which numbers that are greater than
# given number can be added to get sum.
MAX = 100
import numpy as np

# Return number of ways to which numbers
# that are greater than given number can
# be added to get sum.

def numberofways(n, m) :

    dp = np.zeros((n + 2, n + 2))

    dp[0][n + 1] = 1

    # Filling the table. k is for numbers
    # greater than or equal that are allowed.
    for k in range(n, m - 1, -1) :

        # i is for sum
        for i in range(n + 1) :

            # initializing dp[i][k] to number
            # ways to get sum using numbers
            # greater than or equal k+1
            dp[i][k] = dp[i][k + 1]

            # if i > k
            if (i - k >= 0) :
                dp[i][k] = (dp[i][k] + dp[i - k][k])

    return dp[n][m]

# Driver Code
if __name__ == "__main__" :

    n, m = 3, 1
    print(numberofways(n, m))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find number of ways to
// which numbers that are greater than
// given number can be added to get sum.
using System;

class GFG {

    // Return number of ways to which numbers
    // that are greater than given number can
    // be added to get sum.
    static int numberofways(int n, int m)
    {
        int[, ] dp = new int[n + 2, n + 2];

        dp[0, n + 1] = 1;

        // Filling the table. k is for numbers
        // greater than or equal that are allowed.
        for (int k = n; k >= m; k--) {

            // i is for sum
            for (int i = 0; i <= n; i++) {

                // initializing dp[i][k] to number
                // ways to get sum using numbers
                // greater than or equal k+1
                dp[i, k] = dp[i, k + 1];

                // if i > k
                if (i - k >= 0)
                    dp[i, k] = (dp[i, k] + dp[i - k, k]);
            }
        }

        return dp[n, m];
    }

    // Driver Program
    public static void Main()
    {
        int n = 3, m = 1;
        Console.WriteLine(numberofways(n, m));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP Program to find number of ways to
// which numbers that are greater than
// given number can be added to get sum.

$MAX = 100;

// Return number of ways to which numbers
// that are greater than given number can
// be added to get sum.
function numberofways($n, $m)
{
    global $MAX;
    $dp = array_fill(0, $n + 2, array_fill(0, $n+2, NULL));

    $dp[0][$n + 1] = 1;

    // Filling the table. k is for numbers
    // greater than or equal that are allowed.
    for ($k = $n; $k >= $m; $k--)
    {

        // i is for sum
        for ($i = 0; $i <= $n; $i++)
        {

            // initializing dp[i][k] to number
            // ways to get sum using numbers
            // greater than or equal k+1
            $dp[$i][$k] = $dp[$i][$k + 1];

            // if i > k
            if ($i - $k >= 0)
                $dp[$i][$k] = ($dp[$i][$k] + $dp[$i - $k][$k]);
        }
    }

    return $dp[$n][$m];
}

    // Driver Program
    $n = 3;
    $m = 1;
    echo numberofways($n, $m) ;
    return 0;

    // This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript Program to find number of ways to
// which numbers that are greater than
// given number can be added to get sum.

    // Return number of ways to which numbers
    // that are greater than given number can
    // be added to get sum.
    function numberofways(n,m)
    {
        let dp=new Array(n+2);
        for(let i=0;i<dp.length;i++)
        {
            dp[i]=new Array(n+2);
            for(let j=0;j<dp[i].length;j++)
            {
                dp[i][j]=0;
            }
        }

        dp[0][n + 1] = 1;

        // Filling the table. k is for numbers
        // greater than or equal that are allowed.
        for (let k = n; k >= m; k--) {

            // i is for sum
            for (let i = 0; i <= n; i++) {

                // initializing dp[i][k] to number
                // ways to get sum using numbers
                // greater than or equal k+1
                dp[i][k] = dp[i][k + 1];

                // if i > k
                if (i - k >= 0)
                    dp[i][k] = (dp[i][k] + dp[i - k][k]);
            }
        }

        return dp[n][m];
    }

    // Driver Program
    let n = 3, m = 1;
    document.write(numberofways(n, m));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
3
```