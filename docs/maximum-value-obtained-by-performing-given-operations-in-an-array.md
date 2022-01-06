# 通过在数组中执行给定操作获得的最大值

> 原文:[https://www . geesforgeks . org/通过在阵列中执行给定操作获得的最大值/](https://www.geeksforgeeks.org/maximum-value-obtained-by-performing-given-operations-in-an-array/)

给定一个数组 **arr[]** ，任务是找出最大可获得值。允许用户将两个连续的元素相加或相乘。但是，两次乘法运算之间必须至少有一次加法运算(即不允许两次连续的乘法运算)。
假设数组元素为 **1，2，3，4** ，则 **1 * 2 + 3 + 4** 是有效运算，而 **1 + 2 * 3 * 4** 不是有效运算，因为有连续的乘法运算。
**举例:**

```
Input : 5 -1 -5 -3 2 9 -4
Output : 33
Explanation:
The maximum value obtained by following the above conditions is 33\. 
The sequence of operations are given as:
5 + (-1) + (-5) * (-3) + 2 * 9 + (-4) = 33

Input : 5 -3 -5 2 3 9 4
Output : 62
```

**方法:**
这个问题可以用动态规划来解决。

1.  假设 2D 数组 dp[][]的维数为 n * 2。
2.  dp[i][0]表示如果最后一个操作是加法，则直到第 I 个位置的数组的最大值。
3.  dp[i][1]表示如果最后一个操作是乘法，则直到第 I 个位置的数组的最大值。

现在，由于不允许连续乘法运算，所以递推关系可以认为是:

```
dp[i][0] = max(dp[ i - 1][0], dp[ i - 1][1]) + a[ i + 1];
dp[i][1] = dp[i - 1][0] - a[i] + a[i] * a[i + 1];
```

基本情况是:

```
dp[0][0] = a[0] + a[1];
dp[0][1] = a[0] * a[1];
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// A function to calculate the maximum value
void findMax(int a[], int n)
{
    int dp[n][2];
    memset(dp, 0, sizeof(dp));

    // basecases
    dp[0][0] = a[0] + a[1];
    dp[0][1] = a[0] * a[1];

    //Loop to iterate and add the max value in the dp array
    for (int i = 1; i <= n - 2; i++) {
        dp[i][0] = max(dp[i - 1][0], dp[i - 1][1]) + a[i + 1];
        dp[i][1] = dp[i - 1][0] - a[i] + a[i] * a[i + 1];
    }

    cout << max(dp[n - 2][0], dp[n - 2][1]);
}

// Driver Code
int main()
{
    int arr[] = { 5, -1, -5, -3, 2, 9, -4 };
    findMax(arr, 7);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // A function to calculate the maximum value
    static void findMax(int []a, int n)
    {
        int dp[][] = new int[n][2];
        int i, j;

        for (i = 0; i < n ; i++)
            for(j = 0; j < 2; j++)
                dp[i][j] = 0;

        // basecases
        dp[0][0] = a[0] + a[1];
        dp[0][1] = a[0] * a[1];

        // Loop to iterate and add the
        // max value in the dp array
        for (i = 1; i <= n - 2; i++)
        {
            dp[i][0] = Math.max(dp[i - 1][0],
                                dp[i - 1][1]) + a[i + 1];
            dp[i][1] = dp[i - 1][0] - a[i] +
                        a[i] * a[i + 1];
        }

        System.out.println(Math.max(dp[n - 2][0],
                                    dp[n - 2][1]));
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 5, -1, -5, -3, 2, 9, -4 };
        findMax(arr, 7);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import numpy as np

# A function to calculate the maximum value
def findMax(a, n) :

    dp = np.zeros((n, 2));

    # basecases
    dp[0][0] = a[0] + a[1];
    dp[0][1] = a[0] * a[1];

    # Loop to iterate and add the max value in the dp array
    for i in range(1, n - 1) :
        dp[i][0] = max(dp[i - 1][0], dp[i - 1][1]) + a[i + 1];
        dp[i][1] = dp[i - 1][0] - a[i] + a[i] * a[i + 1];

    print(max(dp[n - 2][0], dp[n - 2][1]), end ="");

# Driver Code
if __name__ == "__main__" :

    arr = [ 5, -1, -5, -3, 2, 9, -4 ];
    findMax(arr, 7);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // A function to calculate the maximum value
    static void findMax(int []a, int n)
    {
        int [,]dp = new int[n, 2];
        int i, j;

        for (i = 0; i < n ; i++)
            for(j = 0; j < 2; j++)
                dp[i, j] = 0;

        // basecases
        dp[0, 0] = a[0] + a[1];
        dp[0, 1] = a[0] * a[1];

        // Loop to iterate and add the
        // max value in the dp array
        for (i = 1; i <= n - 2; i++)
        {
            dp[i, 0] = Math.Max(dp[i - 1, 0], dp[i - 1, 1]) + a[i + 1];

            dp[i, 1] = dp[i - 1, 0] - a[i] + a[i] * a[i + 1];
        }

        Console.WriteLine(Math.Max(dp[n - 2, 0], dp[n - 2, 1]));
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 5, -1, -5, -3, 2, 9, -4 };
        findMax(arr, 7);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the above approach
// A function to calculate the maximum value
    function findMax(a , n) {
        var dp = Array(n).fill().map(()=>Array(2).fill(0));
        var i, j;

        for (i = 0; i < n; i++)
            for (j = 0; j < 2; j++)
                dp[i][j] = 0;

        // basecases
        dp[0][0] = a[0] + a[1];
        dp[0][1] = a[0] * a[1];

        // Loop to iterate and add the
        // max value in the dp array
        for (i = 1; i <= n - 2; i++) {
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1]) + a[i + 1];
            dp[i][1] = dp[i - 1][0] - a[i] + a[i] * a[i + 1];
        }

        document.write(Math.max(dp[n - 2][0], dp[n - 2][1]));
    }

    // Driver Code

        var arr = [ 5, -1, -5, -3, 2, 9, -4 ];
        findMax(arr, 7);

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
33
```