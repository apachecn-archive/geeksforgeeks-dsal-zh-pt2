# 通过遵循给定路径

最大化矩阵和

> 原文:[https://www . geesforgeks . org/maximum-matrix-sum-by-follow-the-给定路径/](https://www.geeksforgeeks.org/maximise-matrix-sum-by-following-the-given-path/)

给定一个由正整数组成的 2d 矩阵 **mat[][]** ，任务是找到如果我们必须从**mat【0】【0】**开始进入单元格**mat【0】【N–1】**我们可以达到的最大得分。我们必须分两个阶段覆盖矩阵:

1.  **阶段 1:** 如果我们在细胞**mat【I】【j】**那么我们只能去细胞**mat【I】【j+1】**或**mat【I+1】【j】**而不改变阶段，否则我们可以去细胞**mat【I–1】【j】**并切换到阶段 2。
2.  **阶段 2:** 如果我们在细胞**mat【I】【j】**那么我们只能去细胞**mat【I】【j+1】**或**mat【I–1】【j】**。
    我们不能出界，相位之间的切换最多发生一次。

**注意:**我们可能能够访问到我们两次切换相位的列的单元。
**例:**

> **输入:** mat[][] = {
> {1，1，1}，
> {1，5，1}，
> {1，1，1}}
> **输出:** 15
> 路径:(0，0)—>(0，1)—>(1，1)—>(2，1)—>(1，1)—>(0，1)—>(0，2)
> 1) - > (0，2)
> 总分= 1 + 1 + 5 + 1 + 5 + 1 + 1 = 15
> **输入:** mat[][] = {
> {1，1，1}，
> {1，1，1}，
> {1，1，1}}
> **输出:** 7

**先决条件:** [矩阵中从上到下的最大和路径。](https://www.geeksforgeeks.org/maximum-sum-path-matrix-top-bottom/)
**方法:**这个问题可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决，让我们假设我们在单元格 **mat[i][j]** 并且 **S** 是收缩因子。如果它是 0，那么我们处于阶段 1(增长阶段)，否则我们处于阶段 2(收缩阶段)。因此， **S** 只能取两个值。我们一退下就设置 **S = 1** 。
**dp[i][j][S]** 将被定义为从单元格 **mat[i][j]** 到**mat[0][N–1]**的最大得分。现在，让我们讨论一下我们可以走的路。
让我们假设我们在细胞**mat【I】【j】**。

*   **情况 1:** 当 **S = 0** 时，我们有三种可能的路径，
    1.  转到单元格 **mat[i + 1][j]** 。
    2.  转到单元格 **mat[i][j + 1]** 。
    3.  转到单元格**mat[I–1][j]**并更新 **S = 1** 。
*   **情况 2:** 当 **S = 1** 时，那么我们有两条可能的路径，
    1.  转到单元格**mat[I–1][j]**。
    2.  转到单元格 **mat[i][j + 1]** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define n 3

// To store the states of the DP
int dp[n][n][2];
bool v[n][n][2];

// Function to return the maximum
// of the three integers
int max(int a, int b, int c)
{
    int m = a;
    if (m < b)
        m = b;
    if (m < c)
        m = c;
    return m;
}

// Function to return the maximum score
int maxScore(int arr[][n], int i, int j, int s)
{
    // Base cases
    if (i > n - 1 || i < 0 || j > n - 1)
        return 0;
    if (i == 0 and j == n - 1)
        return arr[i][j];

    // If the state has already
    // been solved then return it
    if (v[i][j][s])
        return dp[i][j][s];

    // Marking the state as solved
    v[i][j][s] = 1;

    // Growing phase
    if (!s)
        dp[i][j][s] = arr[i][j] + max(maxScore(arr, i + 1, j, s),
                                      maxScore(arr, i, j + 1, s),
                                      maxScore(arr, i - 1, j, !s));

    // Shrinking phase
    else
        dp[i][j][s] = arr[i][j] + max(maxScore(arr, i - 1, j, s),
                                      maxScore(arr, i, j + 1, s));

    // Returning the solved state
    return dp[i][j][s];
}

// Driver code
int main()
{
    int arr[n][n] = { { 1, 1, 1 },
                      { 1, 5, 1 },
                      { 1, 1, 1 } };

    cout << maxScore(arr, 0, 0, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int n = 3;

    // To store the states of the DP
    static int[][][] dp = new int[n][n][2];
    static boolean[][][] v = new boolean[n][n][2];

    // Function to return the maximum
    // of the three integers
    static int max(int a, int b, int c)

    {
        int m = a;
        if (m < b)
        {
            m = b;
        }
        if (m < c)
        {
            m = c;
        }
        return m;
    }

// Function to return the maximum score
    static int maxScore(int arr[][], int i, int j, int s)
    {
        // Base cases
        if (i > n - 1 || i < 0 || j > n - 1)
        {
            return 0;
        }
        if (i == 0 && j == n - 1)
        {
            return arr[i][j];
        }

        // If the state has already
        // been solved then return it
        if (v[i][j][s])

        {
            return dp[i][j][s];
        }

        // Marking the state as solved
        v[i][j][s] = true;

        // Growing phase
        if (s != 1)
        {
            dp[i][j][s] = arr[i][j] + Math.max(maxScore(arr, i + 1, j, s),
                                    Math.max(maxScore(arr, i, j + 1, s),
                                    maxScore(arr, i - 1, j, (s==1)?0:1)));
        } // Shrinking phase
        else
        {
            dp[i][j][s] = arr[i][j] + Math.max(maxScore(arr, i - 1, j, s),
                    maxScore(arr, i, j + 1, s));
        }

        // Returning the solved state
        return dp[i][j][s];
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[][] = {{1, 1, 1},
        {1, 5, 1},
        {1, 1, 1}};

        System.out.println(maxScore(arr, 0, 0, 0));

    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

n = 3

# To store the states of the DP
dp = np.zeros((n,n,2));
v = np.zeros((n,n,2));

# Function to return the maximum
# of the three integers
def max_three(a, b, c) :

    m = a;
    if (m < b) :
        m = b;

    if (m < c) :
        m = c;

    return m;

# Function to return the maximum score
def maxScore(arr, i, j, s) :

    # Base cases
    if (i > n - 1 or i < 0 or j > n - 1) :
        return 0;

    if (i == 0 and j == n - 1) :
        return arr[i][j];

    # If the state has already
    # been solved then return it
    if (v[i][j][s]) :
        return dp[i][j][s];

    # Marking the state as solved
    v[i][j][s] = 1;

    # Growing phase
    if (not bool(s)) :
        dp[i][j][s] = arr[i][j] + max_three(maxScore(arr, i + 1, j, s),
                                    maxScore(arr, i, j + 1, s),
                                    maxScore(arr, i - 1, j, not bool(s)));

    # Shrinking phase
    else :
        dp[i][j][s] = arr[i][j] + max(maxScore(arr, i - 1, j, s),
                                    maxScore(arr, i, j + 1, s));

    # Returning the solved state
    return dp[i][j][s];

# Driver code
if __name__ == "__main__" :

    arr = [ [ 1, 1, 1 ],
                    [ 1, 5, 1 ],
                    [ 1, 1, 1 ] ,
                    ];

    print(maxScore(arr, 0, 0, 0));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int n = 3;

    // To store the states of the DP
    static int[,,] dp = new int[n,n,2];
    static bool[,,] v = new bool[n,n,2];

    // Function to return the maximum
    // of the three integers
    static int max(int a, int b, int c)

    {
        int m = a;
        if (m < b)
        {
            m = b;
        }
        if (m < c)
        {
            m = c;
        }
        return m;
    }

    // Function to return the maximum score
    static int maxScore(int [,]arr, int i, int j, int s)
    {
        // Base cases
        if (i > n - 1 || i < 0 || j > n - 1)
        {
            return 0;
        }
        if ((i == 0) && (j == (n - 1)))
        {
            return arr[i, j];
        }

        // If the state has already
        // been solved then return it
        if (v[i, j, s])

        {
            return dp[i, j, s];
        }

        // Marking the state as solved
        v[i, j, s] = true;

        // Growing phase
        if (s != 1)
        {
            dp[i,j,s] = arr[i,j] + Math.Max(maxScore(arr, i + 1, j, s),
                                    Math.Max(maxScore(arr, i, j + 1, s),
                                    maxScore(arr, i - 1, j, (s==1)?0:1)));
        } // Shrinking phase
        else
        {
            dp[i,j,s] = arr[i,j] + Math.Max(maxScore(arr, i - 1, j, s),
                    maxScore(arr, i, j + 1, s));
        }

        // Returning the solved state
        return dp[i, j, s];
    }

    // Driver code
    static public void Main ()
    {
        int [,]arr = {{1, 1, 1},
        {1, 5, 1},
        {1, 1, 1}};

        Console.WriteLine(maxScore(arr, 0, 0, 0));
    }
}

/* This code contributed by @Tushil..... */
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let n = 3;

    // To store the states of the DP
    let dp = new Array(n);
    let v = new Array(n);

    for(let i = 0; i < n; i++)
    {
        dp[i] = new Array(n);
        v[i] = new Array(n);
        for(let j = 0; j < n; j++)
        {
            dp[i][j] = new Array(2);
            v[i][j] = new Array(2);
            for(let k = 0; k < 2; k++)
            {
                dp[i][j][k] = 0;
                v[i][j][k] = 0;
            }
        }
    }

    // Function to return the maximum
    // of the three integers
    function max(a, b, c)

    {
        let m = a;
        if (m < b)
        {
            m = b;
        }
        if (m < c)
        {
            m = c;
        }
        return m;
    }

    // Function to return the maximum score
    function maxScore(arr, i, j, s)
    {
        // Base cases
        if (i > n - 1 || i < 0 || j > n - 1)
        {
            return 0;
        }
        if (i == 0 && j == n - 1)
        {
            return arr[i][j];
        }

        // If the state has already
        // been solved then return it
        if (v[i][j][s])

        {
            return dp[i][j][s];
        }

        // Marking the state as solved
        v[i][j][s] = true;

        // Growing phase
        if (s != 1)
        {
            dp[i][j][s] = arr[i][j] + Math.max(maxScore(arr, i + 1, j, s),
                                    Math.max(maxScore(arr, i, j + 1, s),
                                    maxScore(arr, i - 1, j, (s==1)?0:1)));
        } // Shrinking phase
        else
        {
            dp[i][j][s] = arr[i][j] + Math.max(maxScore(arr, i - 1, j, s),
                    maxScore(arr, i, j + 1, s));
        }

        // Returning the solved state
        return dp[i][j][s];
    }

    let arr = [[1, 1, 1],
               [1, 5, 1],
               [1, 1, 1]];

    document.write(maxScore(arr, 0, 0, 0));

</script>
```

**Output:** 

```
15
```