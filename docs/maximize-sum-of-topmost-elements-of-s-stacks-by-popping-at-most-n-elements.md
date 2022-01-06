# 通过弹出最多 N 个元素

来最大化 S 堆叠最顶端元素的总和

> 原文:[https://www . geeksforgeeks . org/通过弹出最多 n 个元素来最大化 s 个堆栈的最顶层元素的总和/](https://www.geeksforgeeks.org/maximize-sum-of-topmost-elements-of-s-stacks-by-popping-at-most-n-elements/)

给定长度为 **M** 的 **S** 堆叠，任务是通过弹出最多 **N** 个元素来最大化每个堆叠顶部的元素总和。
**例:**

> **输入:** S = 1，N = 3，叠加= { 5，1，2，8，9 }
> **输出:** 8
> **说明:**
> 最多可以移除 3 个元素。
> 栈顶当前元素为 5。
> 去掉 5，顶部新元素为 1。
> 移除 1 时，顶部的新元素为 2。
> 去掉 2，顶部新元素为 8。
> 不允许进一步的弹出操作。
> 因此，堆栈顶部的最大可能值为 8。
> **输入:** S = 2，N = 2，栈= { { 2，6，4，5}，{1，6，15，10} }
> **输出:** 17
> **解释:**
> 顶部元素的当前和= 2 + 1 = 3。
> 从第二个堆栈顶部弹出 1 只等于总和 8 (5 + 2 = 8)
> 从第二个堆栈顶部弹出 2 只等于总和 7 (6 + 1)。
> 从每个堆栈顶部弹出 1 和 2，使总和为 12 (6 + 6)。
> 从第一个堆栈中弹出 2 和 6，使总和为 5 (4 + 1)。
> 从第二堆中弹出 1 和 6 会在顶部留下 15 作为元素。
> 因此，两个堆栈顶部的元素总和最大化(15 + 2 = 17)。

**方法:**这个问题可以简化为一个 [0/1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)问题。要解决问题，请按照以下步骤操作:

1.  创建一个 2D 表 **dp[][]** ，其中有 **(S + 1)** 行和 **(N + 1)** 列。在每个索引**DP【I】【j】**处，通过将 **j** 元素弹出到**I**堆栈来存储最大可能的总和。
2.  将所有索引 **dp[][]** 初始化为 0。
3.  迭代每个堆栈，从 i = 0 到 S–1
4.  现在，对于每一个 **i <sup>第</sup>T3】栈，通过弹出 j (1 到 N)个元素来计算最大可能和..**
5.  这些 j 元素可以从所有已经访问过的 I 栈中选择。因此， **dp[i+1][j]** 存储从 **0 到最小(j，堆栈大小)**的所有 k 值的**堆栈[I][k]+DP[I][j–k]【T3]的最大值。关系**栈[i][k] + dp[i][j-k]** 表示通过从当前 **i <sup>第</sup>** 栈弹出 k 个元素而获得的总和，以及通过从已经访问的栈弹出**j–k**元素而获得的最大可能总和。**
6.  一旦完成所有 **i** 堆叠，找到范围**【1，N–1】**内所有 I 的最大**DP【S】【I】**。
7.  上一步得到的最大值就是要求的答案。

下面的代码是上述方法的实现:

## C++

```
// C++ Program to maximize the
// sum of top of the stack
// values of S stacks by popping
// at most N elements

#include <bits/stdc++.h>
using namespace std;

// Function for computing the
// maximum sum at the top of
// the stacks after popping at
// most N elements from S stack
int maximumSum(int S, int M, int N,
            vector<vector<int> >& stacks)
{
    // Constructing a dp matrix
    // of dimensions (S+1) x (N+1)
    int dp[S + 1][N + 1];

    // Initialize all states
    memset(dp, INT_MIN, sizeof(dp));

    // Loop over all i stacks
    for (int i = 0; i < S; i++) {
        for (int j = 0; j <= N; j++) {
            for (int k = 0; k <= min(j, M); k++) {

                // Store the maximum of
                // popping j elements
                // up to the current stack
                // by popping k elements
                // from current stack and
                // j - k elements from all
                // previous stacks combined
                dp[i + 1][j]
                    = max(dp[i + 1][j],
                        stacks[i][k]
                            + dp[i][j - k]);
            }
        }
    }

    // Store the maximum sum of
    // popping N elements across
    // all stacks
    int result = INT_MIN;
    for (int i = 0; i <= N; i++) {
        result = max(result, dp[S][i]);
    }

    // dp[S][N] has the maximum sum
    return result;
}

// Driver Program
int main()
{
    // Number of stacks
    int S = 2;
    // Length of each stack
    int M = 4;

    vector<vector<int> > stacks = {
        { 2, 6, 4, 5 },
        { 1, 6, 15, 10 }
    };

    // Maximum elements that
    // can be popped
    int N = 3;

    cout << maximumSum(S, M, N, stacks);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to maximize the
// sum of top of the stack
// values of S stacks by popping
// at most N elements
import java.util.*;
class GFG{

// Function for computing the
// maximum sum at the top of
// the stacks after popping at
// most N elements from S stack
static int maximumSum(int S, int M, int N,
                      int [][]stacks)
{
    // Constructing a dp matrix
    // of dimensions (S+1) x (N+1)
    int [][]dp = new int[S + 1][N + 1];

    // Loop over all i stacks
    for (int i = 0; i < S; i++)
    {
        for (int j = 0; j <= N; j++)
        {
            for (int k = 0; k <= Math.min(j, M); k++)
            {

                // Store the maximum of
                // popping j elements
                // up to the current stack
                // by popping k elements
                // from current stack and
                // j - k elements from all
                // previous stacks combined
                dp[i + 1][j] = Math.max(dp[i + 1][j],
                                        stacks[i][k] +
                                        dp[i][j - k]);
            }
        }
    }

    // Store the maximum sum of
    // popping N elements across
    // all stacks
    int result = Integer.MIN_VALUE;
    for (int i = 0; i <= N; i++)
    {
        result = Math.max(result, dp[S][i]);
    }

    // dp[S][N] has the maximum sum
    return result;
}

// Driver Program
public static void main(String[] args)
{
    // Number of stacks
    int S = 2;

    // Length of each stack
    int M = 4;

    int [][]stacks = {{ 2, 6, 4, 5 },
                      { 1, 6, 15, 10 }};

    // Maximum elements that
    // can be popped
    int N = 3;

    System.out.print(maximumSum(S, M, N, stacks));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to maximize the
# sum of top of the stack values
# of S stacks by popping at most
# N element
import sys

# Function for computing the
# maximum sum at the top of
# the stacks after popping at
# most N elements from S stack
def maximumSum(S, M, N, stacks):

    # Constructing a dp matrix
    # of dimensions (S+1) x (N+1)
    dp = [[0 for x in range(N + 1)]
             for y in range(S + 1)]

    # Loop over all i stacks
    for i in range(S):
        for j in range(N + 1):
            for k in range(min(j, M) + 1):

                # Store the maximum of
                # popping j elements
                # up to the current stack
                # by popping k elements
                # from current stack and
                # j - k elements from all
                # previous stacks combined
                dp[i + 1][j] = max(dp[i + 1][j],
                                   stacks[i][k] +
                                   dp[i][j - k])

    # Store the maximum sum of
    # popping N elements across
    # all stacks
    result = -sys.maxsize - 1
    for i in range(N + 1):
        result = max(result, dp[S][i])

    # dp[S][N] has the maximum sum
    return result

# Driver code
if __name__ == "__main__":

    # Number of stacks
    S = 2

    # Length of each stack
    M = 4

    stacks = [ [ 2, 6, 4, 5 ],
               [ 1, 6, 15, 10 ] ]

    # Maximum elements that
    # can be popped
    N = 3

    print(maximumSum(S, M, N, stacks))

# This code is contributed by chitranayal
```

## C#

```
// C# program to maximize the sum
// of top of the stack values of
// S stacks by popping at most N
// elements
using System;

class GFG{

// Function for computing the
// maximum sum at the top of
// the stacks after popping at
// most N elements from S stack
static int maximumSum(int S, int M, int N,
                      int [,]stacks)
{

    // Constructing a dp matrix
    // of dimensions (S+1) x (N+1)
    int [,]dp = new int[S + 1, N + 1];

    // Loop over all i stacks
    for(int i = 0; i < S; i++)
    {
        for(int j = 0; j <= N; j++)
        {
            for(int k = 0;
                    k <= Math.Min(j, M); k++)
            {

                // Store the maximum of popping
                // j elements up to the current
                // stack by popping k elements
                // from current stack and
                // j - k elements from all
                // previous stacks combined
                dp[i + 1, j] = Math.Max(dp[i + 1, j],
                                        stacks[i, k] +
                                        dp[i, j - k]);
            }
        }
    }

    // Store the maximum sum of
    // popping N elements across
    // all stacks
    int result = int.MinValue;
    for(int i = 0; i <= N; i++)
    {
        result = Math.Max(result, dp[S, i]);
    }

    // dp[S,N] has the maximum sum
    return result;
}

// Driver code
public static void Main(String[] args)
{

    // Number of stacks
    int S = 2;

    // Length of each stack
    int M = 4;

    int [,]stacks = { { 2, 6, 4, 5 },
                      { 1, 6, 15, 10 } };

    // Maximum elements that
    // can be popped
    int N = 3;

    Console.Write(maximumSum(S, M, N, stacks));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript Program to maximize the
// sum of top of the stack
// values of S stacks by popping
// at most N elements

// Function for computing the
// maximum sum at the top of
// the stacks after popping at
// most N elements from S stack
function maximumSum(S, M, N, stacks)
{
    // Constructing a dp matrix
    // of dimensions (S+1) x (N+1)
    var dp = Array.from(Array(S+1), ()=> Array(N+1).fill(0));

    // Loop over all i stacks
    for (var i = 0; i < S; i++) {
        for (var j = 0; j <= N; j++) {
            for (var k = 0; k <= Math.min(j, M); k++) {

                // Store the maximum of
                // popping j elements
                // up to the current stack
                // by popping k elements
                // from current stack and
                // j - k elements from all
                // previous stacks combined
                dp[i + 1][j]
                    = Math.max(dp[i + 1][j],
                        stacks[i][k]
                            + dp[i][j - k]);
            }
        }
    }

    // Store the maximum sum of
    // popping N elements across
    // all stacks
    var result = -1000000000;
    for (var i = 0; i <= N; i++) {
        result = Math.max(result, dp[S][i]);
    }

    // dp[S][N] has the maximum sum
    return result;
}

// Driver Program
// Number of stacks
var S = 2;
// Length of each stack
var M = 4;
var stacks = [
    [ 2, 6, 4, 5 ],
    [ 1, 6, 15, 10 ]
    ];
// Maximum elements that
// can be popped
var N = 3;
document.write( maximumSum(S, M, N, stacks));

</script>
```

**Output:** 

```
21
```

***时间复杂度:** O( S*(M + N * (min(N，M))*