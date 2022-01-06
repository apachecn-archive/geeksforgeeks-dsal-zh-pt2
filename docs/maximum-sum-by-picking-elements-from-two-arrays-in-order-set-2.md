# 按顺序从两个数组中选取元素的最大和|集合 2

> 原文:[https://www . geeksforgeeks . org/按顺序从两个数组中选取元素的最大和集-2/](https://www.geeksforgeeks.org/maximum-sum-by-picking-elements-from-two-arrays-in-order-set-2/)

给定两个数组**A【】**和**B【】**，每个数组大小为 **N** ，以及两个整数 **X** 和 **Y** 分别表示可以从 A【】和 B【】中选择的元素的最大数量，任务是通过选择 **N** 元素找到最大可能的和，使得对于任何索引 **i** ，可以选择 A[i]或 B[i]。
**注:**保证**(X+Y)>= n .**
**例:**

> **输入:** A[] = {1，2，3，4，5}，B[] = {5，4，3，2，1}，X = 3， Y = 2
> **输出:** 21
> i = 0 - > 5 采摘
> i = 1 - > 4 采摘
> i = 2 - > 3 采摘
> i = 3 - > 4 采摘
> i = 4 - > 5 采摘
> 5 + 4 + 3 + 4 + 5 = 21
> **输入:** A[] = {1，4，3，2，7，5

**贪心法:**解决这个问题的[贪心法](https://www.geeksforgeeks.org/greedy-algorithms/)已经在[这个帖子](https://www.geeksforgeeks.org/maximum-sum-by-picking-elements-from-two-arrays-in-order/)讨论过了。
**动态规划方法:**在本文中，我们将讨论一个基于[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的解决方案。
按照以下步骤解决问题:

1.  最大 **min (N，X)** 元素可选自**A【】**和 **min(N，Y)** 元素可选自**B【】**。
2.  初始化 2D 数组 **dp[][]** ，通过从 **A[]** 和 **j** 中选择 **i** 元素，使 **dp[i][j]** 包含最大可能的和，其中 I 和 j 的范围分别在 **min (N，X)** 和 **min (N，X)** 内。
3.  初始化一个变量 **max_sum** 来存储可能的最大和。
4.  遍历数组，对于每个数组，元素执行以下操作:
    *   第元素的 **(i + j) <sup>可以是**A【I+j–1】**或**B【I+j–1】**。</sup>**
    *   如果从**A【】**中选择 **(i + j) <sup>第</sup>个**元素，那么 A【】中 **(i + 1) <sup>第</sup>** 个元素的成本将被加到总成本中。因此，在这种情况下，选择 **(i + 1) <sup>第</sup>** 元素的成本为**DP[I][j]= DP[I–1][j]+A[I+j–1]**。
    *   如果从**B【】**中选择**(I+j)<sup>元素，那么选择 **(i + 1) <sup>第</sup>** 元素的成本为**DP[I][j]= DP[I–1][j]+B[I+j–1]**。</sup>**
5.  现在的目标是成本最大化。因此，递推关系为:

> dp[i][j] =最大值(DP[I–1][j]+a[I+j–1]，DP[I–1][j]+b[I+j–1])t 0]

1.  每次迭代后继续更新 **max_sum** 。完成数组遍历后，打印 **max_sum** 的最终值。

以下是上述方法的实现:

## C++

```
// C++ program to find maximum sum
// possible by selecting an element
// from one of two arrays for every index

#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum sum
int maximumSum(int A[], int B[],
               int length,
               int X, int Y)
{
    int l = length;
    // Maximum elements that can be
    // chosen from array A
    int l1 = min(length, X);

    // Maximum elements that can be
    // chosen from array B
    int l2 = min(length, Y);

    int dp[l1 + 1][l2 + 1];
    memset(dp, 0, sizeof(dp));
    dp[0][0] = 0;

    // Stores the maximum
    // sum possible
    int max_sum = INT_MIN;

    // Fill the dp[][] for base case when
    // all elements are selected from A[]
    for (int i = 1; i <= l1; i++) {
        dp[i][0] = dp[i - 1][0] + A[i - 1];
        max_sum = max(max_sum, dp[i][0]);
    }

    // Fill the dp[][] for base case when
    // all elements are selected from B[]
    for (int i = 1; i <= l2; i++) {
        dp[0][i] = dp[0][i - 1] + B[i - 1];
        max_sum = max(max_sum, dp[0][i]);
    }

    for (int i = 1; i <= l1; i++) {
        for (int j = 1; j <= l2; j++) {
            if (i + j <= l)
                dp[i][j]
                    = max(dp[i - 1][j]
                              + A[i + j - 1],
                          dp[i][j - 1]
                              + B[i + j - 1]);
            max_sum = max(dp[i][j],
                          max_sum);
        }
    }

    // Return the final answer
    return max_sum;
}

// Driver Program
int main()
{
    int A[] = { 1, 2, 3, 4, 5 };
    int B[] = { 5, 4, 3, 2, 1 };
    int X = 3, Y = 2;

    int N = sizeof(A) / sizeof(A[0]);

    cout << maximumSum(A, B, N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum
// possible by selecting an element
// from one of two arrays for every index
class GFG{

// Function to calculate maximum sum
static int maximumSum(int A[], int B[],
                      int length, int X,
                      int Y)
{
    int l = length;

    // Maximum elements that can be
    // chosen from array A
    int l1 = Math.min(length, X);

    // Maximum elements that can be
    // chosen from array B
    int l2 = Math.min(length, Y);

    int dp[][] = new int [l1 + 1][l2 + 1];

    // Stores the maximum
    // sum possible
    int max_sum = Integer.MIN_VALUE;

    // Fill the dp[][] for base case when
    // all elements are selected from A[]
    for(int i = 1; i <= l1; i++)
    {
        dp[i][0] = dp[i - 1][0] + A[i - 1];
        max_sum = Math.max(max_sum, dp[i][0]);
    }

    // Fill the dp[][] for base case when
    // all elements are selected from B[]
    for(int i = 1; i <= l2; i++)
    {
        dp[0][i] = dp[0][i - 1] + B[i - 1];
        max_sum = Math.max(max_sum, dp[0][i]);
    }

    for(int i = 1; i <= l1; i++)
    {
        for(int j = 1; j <= l2; j++)
        {
            if (i + j <= l)
                dp[i][j] = Math.max(dp[i - 1][j] +
                                     A[i + j - 1],
                                    dp[i][j - 1] +
                                     B[i + j - 1]);
            max_sum = Math.max(dp[i][j], max_sum);
        }
    }

    // Return the final answer
    return max_sum;
}

// Driver code
public static void main (String[] args)
{
    int A[] = new int[]{ 1, 2, 3, 4, 5 };
    int B[] = new int[]{ 5, 4, 3, 2, 1 };

    int X = 3, Y = 2;
    int N = A.length;

    System.out.println(maximumSum(A, B, N, X, Y));
}
}

// This code is contributed by Pratima Pandey
```

## 计算机编程语言

```
# Python3 program to find maximum sum
# possible by selecting an element
# from one of two arrays for every index
# Function to calculate maximum sum
def maximumSum(A, B, length, X, Y):
    l = length

    # Maximum elements that can be
    # chosen from array A
    l1 = min(length, X)

    # Maximum elements that can be
    # chosen from array B
    l2 = min(length, Y)

    dp=[[ 0 for i in range(l2 + 1)]
        for i in range(l1 + 1)]
    dp[0][0] = 0

    # Stores the maximum
    # sum possible
    max_sum = -10 * 9

    # Fill the dp[]for base case when
    # all elements are selected from A[]
    for i in range(1, l1 + 1):
        dp[i][0] = dp[i - 1][0] + A[i - 1]
        max_sum = max(max_sum, dp[i][0])

    # Fill the dp[]for base case when
    # all elements are selected from B[]
    for i in range(1, l2 + 1):
        dp[0][i] = dp[0][i - 1] + B[i - 1]
        max_sum = max(max_sum, dp[0][i])

    for i in range(1, l1 + 1):
        for j in range(1, l2 + 1):
            if (i + j <= l):
                dp[i][j]= max(dp[i - 1][j] + A[i + j - 1],
                              dp[i][j - 1] + B[i + j - 1])
            max_sum = max(dp[i][j], max_sum)

    # Return the final answer
    return max_sum

# Driver Program
if __name__ == '__main__':
    A=  [1, 2, 3, 4, 5]
    B=  [5, 4, 3, 2, 1]
    X = 3
    Y = 2
    N = len(A)
    print(maximumSum(A, B, N, X, Y))

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to find maximum sum
// possible by selecting an element
// from one of two arrays for every index
using System;

class GFG{

// Function to calculate maximum sum
static int maximumSum(int []A, int []B,
                      int length, int X,
                      int Y)
{
    int l = length;

    // Maximum elements that can be
    // chosen from array A
    int l1 = Math.Min(length, X);

    // Maximum elements that can be
    // chosen from array B
    int l2 = Math.Min(length, Y);

    int [,]dp = new int [l1 + 1, l2 + 1];

    // Stores the maximum
    // sum possible
    int max_sum = int.MinValue;

    // Fill the [,]dp for base case when
    // all elements are selected from []A
    for(int i = 1; i <= l1; i++)
    {
        dp[i, 0] = dp[i - 1, 0] + A[i - 1];
        max_sum = Math.Max(max_sum, dp[i, 0]);
    }

    // Fill the [,]dp for base case when
    // all elements are selected from []B
    for(int i = 1; i <= l2; i++)
    {
        dp[0, i] = dp[0, i - 1] + B[i - 1];
        max_sum = Math.Max(max_sum, dp[0, i]);
    }

    for(int i = 1; i <= l1; i++)
    {
        for(int j = 1; j <= l2; j++)
        {
            if (i + j <= l)
                dp[i, j] = Math.Max(dp[i - 1, j] +
                                     A[i + j - 1],
                                    dp[i, j - 1] +
                                     B[i + j - 1]);
            max_sum = Math.Max(dp[i, j], max_sum);
        }
    }

    // Return the readonly answer
    return max_sum;
}

// Driver code
public static void Main(String[] args)
{
    int []A = new int[]{ 1, 2, 3, 4, 5 };
    int []B = new int[]{ 5, 4, 3, 2, 1 };

    int X = 3, Y = 2;
    int N = A.Length;

    Console.WriteLine(maximumSum(A, B, N, X, Y));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to find maximum sum
// possible by selecting an element
// from one of two arrays for every index

// Function to calculate maximum sum
function maximumSum(A, B, length, X, Y)
{
    var l = length;
    // Maximum elements that can be
    // chosen from array A
    var l1 = Math.min(length, X);

    // Maximum elements that can be
    // chosen from array B
    var l2 = Math.min(length, Y);

    var dp = Array.from(Array(l1+1),
    ()=> Array(l2+1).fill(0));
    dp[0][0] = 0;

    // Stores the maximum
    // sum possible
    var max_sum = -1000000000;

    // Fill the dp[][] for base case when
    // all elements are selected from A[]
    for (var i = 1; i <= l1; i++) {
        dp[i][0] = dp[i - 1][0] + A[i - 1];
        max_sum = Math.max(max_sum, dp[i][0]);
    }

    // Fill the dp[][] for base case when
    // all elements are selected from B[]
    for (var i = 1; i <= l2; i++) {
        dp[0][i] = dp[0][i - 1] + B[i - 1];
        max_sum = Math.max(max_sum, dp[0][i]);
    }

    for (var i = 1; i <= l1; i++) {
        for (var j = 1; j <= l2; j++) {
            if (i + j <= l)
                dp[i][j]
                    = Math.max(dp[i - 1][j]
                              + A[i + j - 1],
                          dp[i][j - 1]
                              + B[i + j - 1]);
            max_sum = Math.max(dp[i][j],
                          max_sum);
        }
    }

    // Return the final answer
    return max_sum;
}

// Driver Program
var A = [ 1, 2, 3, 4, 5 ];
var B = [ 5, 4, 3, 2, 1 ];
var X = 3, Y = 2;
var N = A.length;
document.write( maximumSum(A, B, N, X, Y));

</script>
```

**Output:** 

```
21
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*