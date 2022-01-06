# 矩阵中通过仅移动 X 的值差的最小成本路径

> 原文:[https://www . geesforgeks . org/通过移动矩阵中的最小成本路径-仅基于 x 的值差/](https://www.geeksforgeeks.org/minimum-cost-path-in-a-matrix-by-moving-only-on-value-difference-of-x/)

给定一个矩阵 **mat[][]** 和一个整数 **X** ，任务是找到从![(1, 1)     ](img/4fbfefd6d4bd2611c4f2795e6a983afd.png "Rendered by QuickLaTeX.com")到达
![(N, M)     ](img/84014d98ab9a0122abe67ab51ac613c7.png "Rendered by QuickLaTeX.com")所需的最小操作数。在每次移动中，我们可以在矩阵中向右或向下移动，但是要移动到矩阵中的下一个单元格，该单元格的值必须是![mat[i][j] + X     ](img/c01a2154db27b2f8c95f315671948aa2.png "Rendered by QuickLaTeX.com")。在一个操作中，任何单元的值都可以减 1。

**示例:**

> **输入:** mat[][] = {{8，10，14}，{5，41，19}，{10，2，25}}，X = 3
> **输出:** 11
> **解释:**
> 对矩阵进行运算后:
> 7 10 13
> 5 41 16
> 10 2 19
> 这里要求的最小运算量为 11。
> 8 =>7 = 1
> 14 =>13 = 1
> 19 =>16 = 3
> 25 =>19 = 6
> 路径:7 =>10 =>13 =>16 =>19
> 
> **输入:** mat[][] = {{15，153}，{135，17}}，X = 3
> T3】输出: 125

**方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决这个问题。一般的想法是迭代矩阵的每一个可能的单元，并且如果当前单元的值在最终路径中没有改变，则找到所需的运算次数。如果当前单元格的值是![mat[i][j]     ](img/647b3a2d0118d907c38d8b7b30888c3f.png "Rendered by QuickLaTeX.com")，那么该单元格的要求值是![mat[i][j] - X * (i + j)     ](img/7cecfd17af1fec87ed503de35694eeb3.png "Rendered by QuickLaTeX.com")。同样，我们可以递归计算所需的操作次数。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of operations
// required to move from
// (1, 1) to (N, M)

#include <bits/stdc++.h>
using namespace std;

const long long MAX = 1e18;

long long n, m;
vector<long long> v[151];
long long dp[151][151];

// Function to find the minimum
// operations required to move
// to bottom-right cell of matrix
long long min_operation(long long i,
    long long j, long long val, long long x) {

    // Condition to check if the
    // current cell is the bottom-right
    // cell of the matrix
    if (i == n - 1 && j == m - 1) {
        if (val > v[i][j]) {
            return dp[i][j] = MAX;
        }
        else {
            return dp[i][j] =
                v[i][j] - val;
        }
    }

    // Condition to check if the
    // current cell is out of
    // matrix
    if (i == n || j == m) {
        return dp[i][j] = MAX;
    }

    // Condition to check if the
    // current indices is already
    // computed
    if (dp[i][j] != -1) {
        return dp[i][j];
    }

    // Condition to check that the
    // movement with the current
    // value is not possible
    if (val > v[i][j]) {
        return dp[i][j] = MAX;
    }
    long long tmp = v[i][j] - val;

    // Recursive call to compute the
    // number of operation required
    // to compute the value
    tmp += min(min_operation(i + 1,
            j, val + x, x),
            min_operation(i,
            j + 1, val + x, x));
    return dp[i][j] = tmp;
}

// Function to find the minimum
// number of operations required
// to reach the bottom-right cell
long long solve(long long x)
{
    long long ans = INT64_MAX;

    // Loop to iterate over every
    // possible cell of the matrix
    for (long long i = 0;
        i < n; i++) {

        for (long long j = 0;
            j < m; j++) {

            long long val =
                v[i][j] - x * (i + j);

            memset(dp, -1,
                sizeof(dp));

            val = min_operation(
                0, 0, val, x);

            ans = min(ans, val);
        }
    }
    return ans;
}

// Driver Code
int main()
{
    n = 2, m = 2;
    long long x = 3;

    v[0] = { 15, 153 };
    v[1] = { 135, 17 };

    // Function Call
    cout << solve(x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the 
// minimum number of operations
// required to move from 
// (1, 1) to (N, M)
import java.lang.*;
import java.util.*;

class GFG{

static final long MAX = (long)1e18;
static long n, m;

static List<List<Long>> v = new ArrayList<>(151);
static long[][] dp = new long[151][151];

// Function to find the minimum
// operations required to move
// to bottom-right cell of matrix
static long min_operation(long i, long j,
                          long val, long x)
{

    // Condition to check if the
    // current cell is the bottom-right
    // cell of the matrix
    if (i == n - 1 && j == m - 1)
    {
        if (val > v.get((int)i).get((int)j))
        {
            return dp[(int)i][(int)j] = MAX;
        }
        else
        {
            return dp[(int)i][(int)j] =
                v.get((int)i).get((int)j) - val;
        }
    }

    // Condition to check if the
    // current cell is out of
    // matrix
    if (i == n || j == m)
    {
        return dp[(int)i][(int)j] = MAX;
    }

    // Condition to check if the
    // current indices is already
    // computed
    if (dp[(int)i][(int)j] != -1)
    {
        return dp[(int)i][(int)j];
    }

    // Condition to check that the
    // movement with the current
    // value is not possible
    if (val > v.get((int)i).get((int)j))
    {
        return dp[(int)i][(int)j] = MAX;
    }
    long tmp = v.get((int)i).get((int)j) - val;

    // Recursive call to compute the
    // number of operation required
    // to compute the value
    tmp += Math.min(min_operation(i + 1,
                             j, val + x, x),
                    min_operation(i, j + 1,
                                   val + x, x));

    return dp[(int)i][(int)j] = tmp;
}

// Function to find the minimum
// number of operations required
// to reach the bottom-right cell
static long solve(long x)
{
    long ans = Long.MAX_VALUE;

    // Loop to iterate over every
    // possible cell of the matrix
    for(long i = 0; i < n; i++)
    {
        for(long j = 0; j < m; j++)
        {
            long val = v.get((int)i).get((int)j) -
                       x * (i + j);

            for(int k = 0; k < dp.length; k++)
                for(int l = 0; l < dp[k].length; l++)
                    dp[k][l] = -1;

            val = min_operation(0l, 0l, val, x);
            ans = Math.min(ans, val);
        }
    }
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    n = 2; m = 2;
    long x = 3;

    v.add(Arrays.asList(15l, 153l));
    v.add(Arrays.asList(135l, 17l));

    // Function call
    System.out.println(solve(x));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of operations
# required to move from
# (1, 1) to (N, M)
MAX = 1e18
v = [[ 0, 0]] * (151)
dp = [[-1 for i in range(151)]
        for i in range(151)]

# Function to find the minimum
# operations required to move
# to bottom-right cell of matrix
def min_operation(i, j, val, x):

    # Condition to check if the
    # current cell is the bottom-right
    # cell of the matrix
    if (i == n - 1 and j == m - 1):
        if (val > v[i][j]):
            dp[i][j] = MAX
            return MAX

        else:
            dp[i][j] = v[i][j] - val
            return dp[i][j]

    # Condition to check if the
    # current cell is out of
    # matrix
    if (i == n or j == m):
        dp[i][j] = MAX
        return MAX

    # Condition to check if the
    # current indices is already
    # computed
    if (dp[i][j] != -1):
        return dp[i][j]

    # Condition to check that the
    # movement with the current
    # value is not possible
    if (val > v[i][j]):
        dp[i][j] = MAX
        return MAX

    tmp = v[i][j] - val

    # Recursive call to compute the
    # number of operation required
    # to compute the value
    tmp += min(min_operation(i + 1, j,
                        val + x, x),
            min_operation(i, j + 1,
                            val + x, x))
    dp[i][j] = tmp

    return tmp

# Function to find the minimum
# number of operations required
# to reach the bottom-right cell
def solve(x):

    ans = 10 ** 19

    # Loop to iterate over every
    # possible cell of the matrix
    for i in range(n):
        for j in range(m):
            val = v[i][j] - x * (i + j)

            for ii in range(151):
                for jj in range(151):
                    dp[ii][jj] = -1

            val = min_operation(0, 0, val, x)
            ans = min(ans, val)
    return ans

# Driver Code
if __name__ == '__main__':

    n = 2
    m = 2
    x = 3

    v[0] = [ 15, 153 ]
    v[1] = [ 135, 17 ]

    # Function Call
    print(solve(x))

# This code is contributed by mohit kumar 29    
```

## C#

```
// C# implementation to find the  
// minimum number of operations 
// required to move from  
// (1, 1) to (N, M) 
using System;
using System.Collections.Generic;

class GFG{

static long MAX = (long)1e18;
static long n, m;
static List<List<long>> v = new List<List<long>>();

static long[,] dp = new long[151, 151];

// Function to find the minimum 
// operations required to move
// to bottom-right cell of matrix
static long min_operation(long i, long j,
                          long val, long x)
{

    // Condition to check if the 
    // current cell is the bottom-right
    // cell of the matrix
    if (i == n - 1 && j == m - 1)
    {
        if (val > v[(int)i][(int)j])
        {
            return dp[(int)i, (int)j] = MAX;
        }
        else
        {
            return dp[(int)i, (int)j] = v[(int)i][(int)j] - val;
        }
    }

    // Condition to check if the
    // current cell is out of 
    // matrix
    if (i == n || j == m) 
    {
        return dp[(int)i, (int)j] = MAX;
    }

    // Condition to check if the
    // current indices is already 
    // computed 
    if (dp[(int)i, (int)j] != -1)
    {
        return dp[(int)i, (int)j];
    }

    // Condition to check that the 
    // movement with the current 
    // value is not possible 
    if (val > v[(int)i][(int)j])
    {
        return dp[(int)i, (int)j] = MAX;

    }

    long temp = v[(int)i][(int)j] - val;

    // Recursive call to compute the 
    // number of operation required
    // to compute the value
    temp += Math.Min(min_operation(i + 1, j, val + x, x),
                     min_operation(i, j + 1, val + x, x));
    return dp[(int)i, (int)j] = temp;
}

// Function to find the minimum
// number of operations required
// to reach the bottom-right cell
static long solve(long x)
{

    long ans = Int64.MaxValue;

    // Loop to iterate over every 
    // possible cell of the matrix
    for(long i = 0; i < n; i++)
    {
        for(long j = 0; j < m; j++)
        {
            long val = v[(int)i][(int)j] - x * (i + j);
            for(long k = 0; k < dp.GetLength(0); k++)
            {
                for(long l = 0; l < dp.GetLength(1); l++)
                {
                    dp[k, l] = -1;
                }
            }
            val = min_operation(0, 0, val, x);
            ans = Math.Min(ans, val);
        }
    }
    return ans;
}

// Driver Code
static public void Main()
{
    for(int i = 0; i < 151; i++)
    {
        v.Add(new List<long>());
        v[i].Add(0);
        v[i].Add(0);
    }
    v[0][0] = 15;
    v[0][1] = 153;
    v[1][0] = 135;
    v[1][1] = 17;
    n = 2; m = 2;
    long x = 3;

    // Function call
    Console.WriteLine(solve(x));
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum number of operations
// required to move from
// (1, 1) to (N, M)
let MAX = 1e18;

let n, m;
let v = new Array(151);
for(let i = 0; i < 151; i++)
{
    v[i] = [0, 0];
}
let dp = new Array(151);
for(let i = 0; i < 151; i++)
{
    dp[i] = new Array(151);
}

// Function to find the minimum
// operations required to move
// to bottom-right cell of matrix
function min_operation(i, j, val, x)
{

    // Condition to check if the
    // current cell is the bottom-right
    // cell of the matrix
    if (i == n - 1 && j == m - 1)
    {
        if (val > v[i][j])
        {
            return dp[i][j] = MAX;
        }
        else
        {
            return dp[i][j] = v[i][j] - val;
        }
    }

    // Condition to check if the
    // current cell is out of
    // matrix
    if (i == n || j == m)
    {
        return dp[i][j] = MAX;
    }

    // Condition to check if the
    // current indices is already
    // computed
    if (dp[i][j] != -1)
    {
        return dp[i][j];
    }

    // Condition to check that the
    // movement with the current
    // value is not possible
    if (val > v[i][j])
    {
        return dp[i][j] = MAX;
    }
    let tmp = v[i][j] - val;

    // Recursive call to compute the
    // number of operation required
    // to compute the value
    tmp += Math.min(min_operation(i + 1,
                             j, val + x, x),
                    min_operation(i, j + 1,
                                   val + x, x));

    return dp[i][j] = tmp;
}

// Function to find the minimum
// number of operations required
// to reach the bottom-right cell
function solve(x)
{
    let ans = Number.MAX_VALUE;

    // Loop to iterate over every
    // possible cell of the matrix
    for(let i = 0; i < n; i++)
    {
        for(let j = 0; j < m; j++)
        {
            let val = v[i][j] -
                       x * (i + j);

            for(let k = 0; k < dp.length; k++)
                for(let l = 0; l < dp[k].length; l++)
                    dp[k][l] = -1;

            val = min_operation(0, 0, val, x);
            ans = Math.min(ans, val);
        }
    }
    return ans;
}

// Driver Code
let x = 3;
n = 2; m = 2;

v[0] = [ 15, 153 ];
v[1] = [ 135, 17 ];

// Function call
document.write(solve(x)+"<br>");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
125
```