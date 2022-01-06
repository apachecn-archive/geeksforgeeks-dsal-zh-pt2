# 计数元素平均值等于 K 的子序列

> 原文:[https://www . geesforgeks . org/count-subseries-having-average-equal-k/](https://www.geeksforgeeks.org/count-subsequences-having-average-equal-to-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是用平均值 **K** 来计算给定数组的子序列数。

**示例:**

> **输入:** arr[] = {9，7，8，9}，K = 8
> **输出:** 5
> **解释:**平均值为 8 的子序列为{8}、{9，7}、{7，9}、{9，7，8}、{7，8，9}。
> 
> **输入:** arr[] = {5，5，1}，K = 4
> **输出:** 0
> **说明:**无法获得这样的子序列

**天真方法:**解决问题最简单的方法就是使用[递归](https://www.geeksforgeeks.org/recursion/)。按照以下步骤解决问题:

1.  对于每个数组元素，有两个选项是可能的，即要么在和中包含当前元素，要么在和中排除当前元素，并为每个递归调用增加当前索引。
2.  对于上述两种可能性，返回平均的子序列数 **K** 。
3.  基本情况是检查最后一个索引是否已经到达。基本情况下的平均值可以通过除以该子序列中包含的数组元素的总和来计算。
4.  如果平均值等于 **K** ，则返回 **1** 。否则，返回 **0** 。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。按照以下步骤解决问题:

*   初始化一个 [3D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说 **dp[][][]** ，其中 **dp[i][k][s]** 是从第一个 **i** 整数中选择 **k** 整数的方式数，这样选择的整数之和就是 **s** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   每个元素有两个可能的选项，即包含或排除它。
*   如果包含索引 **i** 处的当前元素，则下一个索引状态将是 **i + 1** ，并且所选元素的计数将从 **k** 增加到 **k + 1** ，并且总和 **s** 将增加到**s+arr【I】**。
*   如果排除索引 **i** 处的当前元素，则只有索引 **i** 将增加到 **i+1** ，所有其他状态将保持不变。
*   下面是这个问题的 dp 转换状态:

> 如果包含第 i <sup>个</sup>元素，则**DP[I+1][k+1][s+arr[I]]+= DP[I][k][s]**
> 如果不包含第 i <sup>个</sup>元素，则**DP[I+1][k][s]+= DP[I][k][s]**

*   最后，答案将是所有 **j** ( *1 ≤ j ≤ N* )的 **dp[N][j][K*j]** 的总和。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the dp states
int dp[101][101][1001];

// Function to find the count of
// subsequences having average K
int countAverage(int n, int K, int* arr)
{

    // Base condition
    dp[0][0][0] = 1;

    // Three loops for three states
    for (int i = 0; i < n; i++) {
        for (int k = 0; k < n; k++) {
            for (int s = 0; s <= 1000; s++) {

                // Recurrence relation
                dp[i + 1][k + 1][s + arr[i]]
                    += dp[i][k][s];
                dp[i + 1][k][s] += dp[i][k][s];
            }
        }
    }

    // Stores the sum of dp[n][j][K*j]
    // all possible values of j with
    // average K and sum K * j
    int cnt = 0;

    // Iterate over the range [1, N]
    for (int j = 1; j <= n; j++) {
        cnt += dp[n][j][K * j];
    }

    // Return the final count
    return cnt;
}

// Driver Code
int main()
{
    int arr[] = { 9, 7, 8, 9 };
    int K = 8;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << countAverage(N, K, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Stores the dp states
static int [][][]dp = new int[101][101][1001];

// Function to find the count of
// subsequences having average K
static int countAverage(int n, int K, int[] arr)
{

    // Base condition
    dp[0][0][0] = 1;

    // Three loops for three states
    for (int i = 0; i < n; i++)
    {
        for (int k = 0; k < n; k++)
        {
            for (int s = 0; s <= 100; s++)
            {

                // Recurrence relation
                dp[i + 1][k + 1][s + arr[i]]
                    += dp[i][k][s];
                dp[i + 1][k][s] += dp[i][k][s];
            }
        }
    }

    // Stores the sum of dp[n][j][K*j]
    // all possible values of j with
    // average K and sum K * j
    int cnt = 0;

    // Iterate over the range [1, N]
    for (int j = 1; j <= n; j++)
    {
        cnt += dp[n][j][K * j];
    }

    // Return the final count
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 9, 7, 8, 9 };
    int K = 8;
    int N = arr.length;
    System.out.print(countAverage(N, K, arr));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the dp states
dp = [[[0 for i in range(1001)] for i in range(101)] for i in range(101)]

# Function to find the count of
# subsequences having average K
def countAverage(n, K, arr):
    global dp
    dp[0][0][0] = 1

    # Three loops for three states
    for i in range(n):
        for k in range(n):
            for s in range(100):

                # Recurrence relation
                dp[i + 1][k + 1][s + arr[i]] += dp[i][k][s]
                dp[i + 1][k][s] += dp[i][k][s]

    # Stores the sum of dp[n][j][K*j]
    # all possible values of j with
    # average K and sum K * j
    cnt = 0

    # Iterate over the range [1, N]
    for j in range(1, n + 1):
        cnt += dp[n][j][K * j]

    # Return the final count
    return cnt

# Driver Code
if __name__ == '__main__':
    arr= [9, 7, 8, 9]
    K = 8
    N = len(arr)

    print(countAverage(N, K, arr))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Stores the dp states
static int [,,]dp = new int[101, 101, 1001];

// Function to find the count of
// subsequences having average K
static int countAverage(int n, int K, int[] arr)
{

    // Base condition
    dp[0, 0, 0] = 1;

    // Three loops for three states
    for (int i = 0; i < n; i++)
    {
        for (int k = 0; k < n; k++)
        {
            for (int s = 0; s <= 100; s++)
            {

                // Recurrence relation
                dp[i + 1, k + 1, s + arr[i]]
                    += dp[i, k, s];
                dp[i + 1, k, s] += dp[i, k, s];
            }
        }
    }

    // Stores the sum of dp[n,j,K*j]
    // all possible values of j with
    // average K and sum K * j
    int cnt = 0;

    // Iterate over the range [1, N]
    for (int j = 1; j <= n; j++)
    {
        cnt += dp[n, j, K * j];
    }

    // Return the readonly count
    return cnt;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 9, 7, 8, 9 };
    int K = 8;
    int N = arr.Length;
    Console.Write(countAverage(N, K, arr));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Stores the dp states
var dp = Array.from(Array(101), ()=> Array(101));

for(var i =0; i<101; i++)
        for(var j =0; j<101; j++)
            dp[i][j] = new Array(1001).fill(0);

// Function to find the count of
// subsequences having average K
function countAverage(n, K, arr)
{

    // Base condition
    dp[0][0][0] = 1;

    // Three loops for three states
    for (var i = 0; i < n; i++) {
        for (var k = 0; k < n; k++) {
            for (var s = 0; s <= 1000; s++) {

                // Recurrence relation
                dp[i + 1][k + 1][s + arr[i]]
                    += dp[i][k][s];
                dp[i + 1][k][s] += dp[i][k][s];
            }
        }
    }

    // Stores the sum of dp[n][j][K*j]
    // all possible values of j with
    // average K and sum K * j
    var cnt = 0;

    // Iterate over the range [1, N]
    for (var j = 1; j <= n; j++) {
        cnt += dp[n][j][K * j];
    }

    // Return the final count
    return cnt;
}

// Driver Code
var arr = [9, 7, 8, 9];
var K = 8;
var N = arr.length
document.write( countAverage(N, K, arr));

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(S*N <sup>2</sup> )其中 S 是数组的和。*
***辅助空间:** O(S*N <sup>2</sup> )*