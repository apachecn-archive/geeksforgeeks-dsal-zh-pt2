# 使数组为空的最小回文子数组移除次数

> 原文:[https://www . geeksforgeeks . org/minimum-回文-子数组-移除使数组为空/](https://www.geeksforgeeks.org/minimum-palindromic-subarray-removals-to-make-array-empty/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是找到从数组中移除所有元素所需的最小回文子数组移除量。
**例:**

> **输入:** arr[] = {1，3，4，1，5}，N = 5
> **输出:** 3
> **解释:**
> 从数组中移除 4 会留下{1，3，1，5}。
> 移除{1，3，1}叶片{5}。
> 移除 5 使数组为空。
> **输入:** arr[] = {1，2，3，5，3，1}，N = 5
> **输出:** 2
> **解释:**
> 去除{3，5，3}叶{1，2，1}。
> 移除{1，2，1}会使数组为空。

**方法:**
我们可以用区间[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决这个问题。按照以下步骤解决问题:

*   初始化 **dp[][]** ，使得每个 dp[i][j]代表从 **i <sup>第</sup>T5】位置到 **j <sup>第</sup>T9】位置所需的最小移除次数。****
*   对于 **i** 到 **j** 的区间，答案可能是 **i** 到 **k** 和 **k + 1** 到 **j** 的两个区间之和，即:

> dp [i][j]=最小值(dp [i][j]，dp [i][k] + dp [k + 1][j])，其中 i ≤ k

*   除了这种可能性，我们还需要检查 **arr[i] = arr[j]** ，那么**DP[I][j]= DP[I+1][j–1]**。

以下是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[550][550];
int minSubarrayRemoval(vector<int>& arr)
{
    int i, j, k, l;
    int n = arr.size();

    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            dp[i][j] = n;
        }
    }

    for (i = 0; i < n; i++) {
        dp[i][i] = 1;
    }

    for (i = 0; i < n - 1; i++) {
        if (arr[i] == arr[i + 1]) {
            dp[i][i + 1] = 1;
        }
        else {
            dp[i][i + 1] = 2;
        }
    }
    for (l = 2; l < n; l++) {
        for (i = 0; i + l < n; i++) {
            j = i + l;
            if (arr[i] == arr[j]) {
                dp[i][j] = dp[i + 1][j - 1];
            }
            for (k = i; k < j; k++) {
                dp[i][j]
                    = min(
                        dp[i][j],
                        dp[i][k]
                            + dp[k + 1][j]);
            }
        }
    }
    return dp[0][n - 1];
}
// Driver Program
int main()
{
    vector<int> arr
        = { 2, 3, 1, 2, 2, 1, 2 };
    int ans = minSubarrayRemoval(arr);
    cout << ans << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static int dp[][] = new int[550][550];

static int minSubarrayRemoval(int arr[])
{
    int i, j, k, l;
    int n = arr.length;

    for(i = 0; i < n; i++)
    {
       for(j = 0; j < n; j++)
       {
          dp[i][j] = n;
       }
    }

    for(i = 0; i < n; i++)
    {
       dp[i][i] = 1;
    }

    for(i = 0; i < n - 1; i++)
    {
       if (arr[i] == arr[i + 1])
       {
           dp[i][i + 1] = 1;
       }
       else
       {
           dp[i][i + 1] = 2;
       }
    }

    for(l = 2; l < n; l++)
    {
       for(i = 0; i + l < n; i++)
       {
          j = i + l;
          if (arr[i] == arr[j])
          {
              dp[i][j] = dp[i + 1][j - 1];
          }
          for(k = i; k < j; k++)
          {
             dp[i][j] = Math.min(dp[i][j],
                                 dp[i][k] +
                                 dp[k + 1][j]);
          }
       }
    }
    return dp[0][n - 1];
}

// Driver code
public static void main (String[] args)
{
    int arr [] = new int[]{ 2, 3, 1, 2, 2, 1, 2 };
    int ans = minSubarrayRemoval(arr);

    System.out.println(ans);
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach
def minSubarrayRemoval(arr):

    n = len(arr)
    dp = []

    for i in range(n):
        l = [0] * n
        for j in range(n):
            l[j] = n
        dp.append(l)

    for i in range(n):
        dp[i][i] = 1

    for i in range(n - 1):
        if (arr[i] == arr[i + 1]):
            dp[i][i + 1] = 1
        else:
            dp[i][i + 1] = 2

    for l in range(2, n):
        for i in range(n - l):
            j = i + l
            if (arr[i] == arr[j]):
                dp[i][j] = dp[i + 1][j - 1]

            for k in range(i, j):
                dp[i][j] = min(dp[i][j],
                               dp[i][k] +
                               dp[k + 1][j])

    return dp[0][n - 1]

# Driver code
arr = [ 2, 3, 1, 2, 2, 1, 2 ]
ans = minSubarrayRemoval(arr)

print(ans)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static int [,]dp = new int[550, 550];

static int minSubarrayRemoval(int []arr)
{
    int i, j, k, l;
    int n = arr.Length;

    for(i = 0; i < n; i++)
    {
       for(j = 0; j < n; j++)
       {
          dp[i, j] = n;
       }
    }

    for(i = 0; i < n; i++)
    {
       dp[i, i] = 1;
    }

    for(i = 0; i < n - 1; i++)
    {
       if (arr[i] == arr[i + 1])
       {
           dp[i, i + 1] = 1;
       }
       else
       {
           dp[i, i + 1] = 2;
       }
    }

    for(l = 2; l < n; l++)
    {
       for(i = 0; i + l < n; i++)
       {
          j = i + l;
          if (arr[i] == arr[j])
          {
              dp[i, j] = dp[i + 1, j - 1];
          }
          for(k = i; k < j; k++)
          {
             dp[i, j] = Math.Min(dp[i, j],
                                 dp[i, k] +
                                 dp[k + 1, j]);
          }
       }
    }
    return dp[0, n - 1];
}

// Driver code
public static void Main()
{
    int []arr = new int[]{ 2, 3, 1, 2, 2, 1, 2 };
    int ans = minSubarrayRemoval(arr);

    Console.Write(ans);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

let dp = new Array(550);
// Loop to create 2D array using 1D array
for (var i = 0; i < dp.length; i++) {
    dp[i] = new Array(2);
}

function minSubarrayRemoval(arr)
{
    let i, j, k, l;
    let n = arr.length;

    for(i = 0; i < n; i++)
    {
       for(j = 0; j < n; j++)
       {
          dp[i][j] = n;
       }
    }

    for(i = 0; i < n; i++)
    {
       dp[i][i] = 1;
    }

    for(i = 0; i < n - 1; i++)
    {
       if (arr[i] == arr[i + 1])
       {
           dp[i][i + 1] = 1;
       }
       else
       {
           dp[i][i + 1] = 2;
       }
    }

    for(l = 2; l < n; l++)
    {
       for(i = 0; i + l < n; i++)
       {
          j = i + l;
          if (arr[i] == arr[j])
          {
              dp[i][j] = dp[i + 1][j - 1];
          }
          for(k = i; k < j; k++)
          {
             dp[i][j] = Math.min(dp[i][j],
                                 dp[i][k] +
                                 dp[k + 1][j]);
          }
       }
    }
    return dp[0][n - 1];
}

// Driver Code

    let arr = [ 2, 3, 1, 2, 2, 1, 2 ];
    let ans = minSubarrayRemoval(arr);

    document.write(ans);

</script>
```

**Output**

```
2
```

***时间复杂度:** O(n <sup>3</sup> ，其中 n 为数组长度。*

***辅助空间:** O(n <sup>2</sup> )*