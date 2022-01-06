# 执行给定操作后的最大可能数组和

> 原文:[https://www . geesforgeks . org/执行给定操作后的最大可能数组和/](https://www.geeksforgeeks.org/maximum-possible-array-sum-after-performing-the-given-operation/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是在多次应用给定操作后，找到数组元素的最大和。在单次操作中，选择一个索引 **1 ≤ i < N** ，并将**arr【I】**和**arr【I–1】**乘以 **-1** 。
**示例:**

> **输入:** arr[] = {-10，5，-4}
> **输出:** 19
> 执行 i = 1 和
> 的运算数组变成{10，-5，-4}
> 执行 i = 2 和
> 的运算数组变成{10，5，4}
> 10 + 5 + 4 = 19
> **输入:** arr[] = {10，-4，-8，-11，3 }

****方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。由于选择并翻转同一个**arr【I】**是没有用的，我们将考虑从左到右的顺序对数组的每个元素最多翻转一次。让 **dp[i][0]** 代表第 **i <sup>第</sup>** 指数的最大可能总和，而不翻转第 **i <sup>第</sup>** 指数。 **dp[i][1]** 表示通过翻转 **i <sup>th</sup>** 指数得到的**I<sup>th</sup>T21 指数的最大可能总和。所以，dp(n，0)是我们需要的答案。
**基础条件:******

1.  **dp[0][0] = 0**
2.  **dp[0][1] = INT_MIN**

****复发关系:****

1.  **dp[i + 1][0] = max（dp[i][0] + scar[i]， dp[i][1] – scar[i]）**
2.  **dp[i + 1][1] = max（dp[i][0] – scar[i]， dp[i][1] + scar[i]）**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum possible
// sum after performing the given operation
int max_sum(int a[], int n)
{
    // Dp vector to store the answer
    vector<vector<int> > dp(n + 1,
                            vector<int>(2, 0));

    // Base value
    dp[0][0] = 0, dp[0][1] = -999999;

    for (int i = 0; i <= n - 1; i++) {
        dp[i + 1][0] = max(dp[i][0] + a[i],
                           dp[i][1] - a[i]);
        dp[i + 1][1] = max(dp[i][0] - a[i],
                           dp[i][1] + a[i]);
    }

    // Return the maximum sum
    return dp[n][0];
}

// Driver code
int main()
{
    int a[] = { -10, 5, -4 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << max_sum(a, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum possible
// sum after performing the given operation
static int max_sum(int a[], int n)
{
    // Dp vector to store the answer
    int [][]dp = new int[n + 1][2];

    // Base value
    dp[0][0] = 0; dp[0][1] = -999999;

    for (int i = 0; i <= n - 1; i++)
    {
        dp[i + 1][0] = Math.max(dp[i][0] + a[i],
                                dp[i][1] - a[i]);
        dp[i + 1][1] = Math.max(dp[i][0] - a[i],
                                dp[i][1] + a[i]);
    }

    // Return the maximum sum
    return dp[n][0];
}

// Driver code
public static void main(String[] args)
{
    int a[] = { -10, 5, -4 };
    int n = a.length;

    System.out.println(max_sum(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python implementation of the approach

# Function to return the maximum possible
# sum after performing the given operation
def max_sum(a, n):
    # Dp vector to store the answer
    dp = [[0 for i in range(2)] for j in range(n+1)]

    # Base value
    dp[0][0] = 0; dp[0][1] = -999999;

    for i in range(0, n):
        dp[i + 1][0] = max(dp[i][0] + a[i],
                                dp[i][1] - a[i]);
        dp[i + 1][1] = max(dp[i][0] - a[i],
                                dp[i][1] + a[i]);

    # Return the maximum sum
    return dp[n][0];

# Driver code
if __name__ == '__main__':
    a = [-10, 5, -4 ];
    n = len(a);

    print(max_sum(a, n));

# This code is contributed by 29AjayKumar
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum possible
// sum after performing the given operation
static int max_sum(int []a, int n)
{
    // Dp vector to store the answer
    int [,]dp = new int[n + 1, 2];

    // Base value
    dp[0, 0] = 0; dp[0, 1] = -999999;

    for (int i = 0; i <= n - 1; i++)
    {
        dp[i + 1, 0] = Math.Max(dp[i, 0] + a[i],
                                dp[i, 1] - a[i]);
        dp[i + 1, 1] = Math.Max(dp[i, 0] - a[i],
                                dp[i, 1] + a[i]);
    }

    // Return the maximum sum
    return dp[n, 0];
}

// Driver code
public static void Main(String[] args)
{
    int []a = { -10, 5, -4 };
    int n = a.Length;

    Console.WriteLine(max_sum(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>
// javascript implementation of the approach    // Function to return the maximum possible
    // sum after performing the given operation
    function max_sum(a , n) {
        // Dp vector to store the answer
        var dp = Array(n + 1).fill().map(()=>Array(2).fill(0));

        // Base value
        dp[0][0] = 0;
        dp[0][1] = -999999;

        for (i = 0; i <= n - 1; i++) {
            dp[i + 1][0] = Math.max(dp[i][0] + a[i], dp[i][1] - a[i]);
            dp[i + 1][1] = Math.max(dp[i][0] - a[i], dp[i][1] + a[i]);
        }

        // Return the maximum sum
        return dp[n][0];
    }

    // Driver code

        var a = [ -10, 5, -4 ];
        var n = a.length;

        document.write(max_sum(a, n));

// This code is contributed by todaysgaurav
</script>
```

****Output:** 

```
19
```** 

****时间复杂度:** O(N)**

****辅助空间:** O(N)**