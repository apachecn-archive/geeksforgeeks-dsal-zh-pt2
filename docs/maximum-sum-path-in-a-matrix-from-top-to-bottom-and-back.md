# 矩阵中从上到下和从后的最大和路径

> 原文:[https://www . geeksforgeeks . org/矩阵中从上到下再到后的最大路径总和/](https://www.geeksforgeeks.org/maximum-sum-path-in-a-matrix-from-top-to-bottom-and-back/)

给定维度矩阵 **N * M** 。任务是找到从 **arr[0][0]** 到**arr[N-1][M-1]**以及从**arr[N-1][M-1]**到 **arr[0][0]** 的最大路径和。
在 **arr[0][0]** 至**arr[N–1][M–1]**的路径上，可以上下左右方向穿越，在**arr[N–1][M–1]**至 **arr[0][0]** 的路径上，可以上下左右方向穿越。
**注**:两条路径不能相等，即至少要有一个单元格 **arr[i][j]** ，这在两条路径中并不常见。
**举例:**

```
Input: 
mat[][]= {{1, 0, 3, -1},
          {3, 5, 1, -2},
          {-2, 0, 1, 1},
          {2, 1, -1, 1}}
Output: 16
```

![](img/23c6f4926b0654232bfda89a9b301bc0.png)

```
Maximum sum on path from arr[0][0] to arr[3][3] 
= 1 + 3 + 5 + 1 + 1 + 1 + 1 = 13
Maximum sum on path from arr[3][3] to arr[0][0] = 3
Total path sum = 13 + 3 = 16

Input: 
mat[][]= {{1, 0},
          {1, 1}}
Output: 3
```

**方法:**这个问题有点类似于[最小成本路径](https://www.geeksforgeeks.org/min-cost-path-dp-6/)问题，只是在目前的问题中，要找到两个和最大的路径。此外，我们需要注意两条路径上的细胞只贡献一次总和。
首先要注意的是从**arr[N–1][M–1]**到 **arr[0][0]** 的路径只不过是从 **arr[0][0]** 到**arr[N–1][M–1]**的另一条路径。所以，我们要找到从 **arr[0][0]** 到**arr[N–1][M–1]**的两条最大和的路径。
以与最小成本路径问题类似的方式进行处理，我们从 **arr[0][0]** 一起开始两条路径，并重复到矩阵的相邻单元，直到我们到达**arr[N–1][M–1]**。为了确保一个单元不会贡献超过一次，我们检查两条路径上的当前单元是否相同。如果它们相同，则只添加到答案中一次。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Input matrix
int n = 4, m = 4;
int arr[4][4] = { { 1, 0, 3, -1 },
                  { 3, 5, 1, -2 },
                  { -2, 0, 1, 1 },
                  { 2, 1, -1, 1 } };

// DP matrix
int cache[5][5][5];

// Function to return the sum of the cells
// arr[i1][j1] and arr[i2][j2]
int sum(int i1, int j1, int i2, int j2)
{
    if (i1 == i2 && j1 == j2) {
        return arr[i1][j1];
    }
    return arr[i1][j1] + arr[i2][j2];
}

// Recursive function to return the
// required maximum cost path
int maxSumPath(int i1, int j1, int i2)
{

    // Column number of second path
    int j2 = i1 + j1 - i2;

    // Base Case
    if (i1 >= n || i2 >= n || j1 >= m || j2 >= m) {
        return 0;
    }

    // If already calculated, return from DP matrix
    if (cache[i1][j1][i2] != -1) {
        return cache[i1][j1][i2];
    }
    int ans = INT_MIN;

    // Recurring for neighbouring cells of both paths together
    ans = max(ans, maxSumPath(i1 + 1, j1, i2 + 1) + sum(i1, j1, i2, j2));
    ans = max(ans, maxSumPath(i1, j1 + 1, i2) + sum(i1, j1, i2, j2));
    ans = max(ans, maxSumPath(i1, j1 + 1, i2 + 1) + sum(i1, j1, i2, j2));
    ans = max(ans, maxSumPath(i1 + 1, j1, i2) + sum(i1, j1, i2, j2));

    // Saving result to the DP matrix for current state
    cache[i1][j1][i2] = ans;

    return ans;
}

// Driver code
int main()
{
    memset(cache, -1, sizeof(cache));
    cout << maxSumPath(0, 0, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Input matrix
static int n = 4, m = 4;
static int arr[][] = { { 1, 0, 3, -1 },
                { 3, 5, 1, -2 },
                { -2, 0, 1, 1 },
                { 2, 1, -1, 1 } };

// DP matrix
static int cache[][][] = new int[5][5][5];

// Function to return the sum of the cells
// arr[i1][j1] and arr[i2][j2]
static int sum(int i1, int j1, int i2, int j2)
{
    if (i1 == i2 && j1 == j2)
    {
        return arr[i1][j1];
    }
    return arr[i1][j1] + arr[i2][j2];
}

// Recursive function to return the
// required maximum cost path
static int maxSumPath(int i1, int j1, int i2)
{

    // Column number of second path
    int j2 = i1 + j1 - i2;

    // Base Case
    if (i1 >= n || i2 >= n || j1 >= m || j2 >= m)
    {
        return 0;
    }

    // If already calculated, return from DP matrix
    if (cache[i1][j1][i2] != -1)
    {
        return cache[i1][j1][i2];
    }
    int ans = Integer.MIN_VALUE;

    // Recurring for neighbouring cells of both paths together
    ans = Math.max(ans, maxSumPath(i1 + 1, j1, i2 + 1) + sum(i1, j1, i2, j2));
    ans = Math.max(ans, maxSumPath(i1, j1 + 1, i2) + sum(i1, j1, i2, j2));
    ans = Math.max(ans, maxSumPath(i1, j1 + 1, i2 + 1) + sum(i1, j1, i2, j2));
    ans = Math.max(ans, maxSumPath(i1 + 1, j1, i2) + sum(i1, j1, i2, j2));

    // Saving result to the DP matrix for current state
    cache[i1][j1][i2] = ans;

    return ans;
}

// Driver code
public static void main(String args[])
{
    //set initial value
    for(int i=0;i<5;i++)
    for(int i1=0;i1<5;i1++)
    for(int i2=0;i2<5;i2++)
    cache[i][i1][i2]=-1;

    System.out.println( maxSumPath(0, 0, 0));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
import sys

# Input matrix
n = 4
m = 4
arr = [[1, 0, 3, -1],
    [3, 5, 1, -2],
    [-2, 0, 1, 1],
    [2, 1, -1, 1]]

# DP matrix
cache = [[[-1 for i in range(5)] for j in range(5)] for k in range(5)]

# Function to return the sum of the cells
# arr[i1][j1] and arr[i2][j2]
def sum(i1, j1, i2, j2):
    if (i1 == i2 and j1 == j2):
        return arr[i1][j1]
    return arr[i1][j1] + arr[i2][j2]

# Recursive function to return the
# required maximum cost path
def maxSumPath(i1, j1, i2):

    # Column number of second path
    j2 = i1 + j1 - i2

    # Base Case
    if (i1 >= n or i2 >= n or j1 >= m or j2 >= m):
        return 0

    # If already calculated, return from DP matrix
    if (cache[i1][j1][i2] != -1):
        return cache[i1][j1][i2]
    ans = -sys.maxsize-1

    # Recurring for neighbouring cells of both paths together
    ans = max(ans, maxSumPath(i1 + 1, j1, i2 + 1) + sum(i1, j1, i2, j2))
    ans = max(ans, maxSumPath(i1, j1 + 1, i2) + sum(i1, j1, i2, j2))
    ans = max(ans, maxSumPath(i1, j1 + 1, i2 + 1) + sum(i1, j1, i2, j2))
    ans = max(ans, maxSumPath(i1 + 1, j1, i2) + sum(i1, j1, i2, j2))

    # Saving result to the DP matrix for current state
    cache[i1][j1][i2] = ans

    return ans

# Driver code
if __name__ == '__main__':
    print(maxSumPath(0, 0, 0))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Input matrix
static int n = 4, m = 4;
static int [,]arr = { { 1, 0, 3, -1 },
                { 3, 5, 1, -2 },
                { -2, 0, 1, 1 },
                { 2, 1, -1, 1 } };

// DP matrix
static int [,,]cache = new int[5, 5, 5];

// Function to return the sum of the cells
// arr[i1][j1] and arr[i2][j2]
static int sum(int i1, int j1, int i2, int j2)
{
    if (i1 == i2 && j1 == j2)
    {
        return arr[i1, j1];
    }
    return arr[i1, j1] + arr[i2, j2];
}

// Recursive function to return the
// required maximum cost path
static int maxSumPath(int i1, int j1, int i2)
{

    // Column number of second path
    int j2 = i1 + j1 - i2;

    // Base Case
    if (i1 >= n || i2 >= n || j1 >= m || j2 >= m)
    {
        return 0;
    }

    // If already calculated, return from DP matrix
    if (cache[i1, j1, i2] != -1)
    {
        return cache[i1, j1, i2];
    }
    int ans = int.MinValue;

    // Recurring for neighbouring cells of both paths together
    ans = Math.Max(ans, maxSumPath(i1 + 1, j1, i2 + 1) + sum(i1, j1, i2, j2));
    ans = Math.Max(ans, maxSumPath(i1, j1 + 1, i2) + sum(i1, j1, i2, j2));
    ans = Math.Max(ans, maxSumPath(i1, j1 + 1, i2 + 1) + sum(i1, j1, i2, j2));
    ans = Math.Max(ans, maxSumPath(i1 + 1, j1, i2) + sum(i1, j1, i2, j2));

    // Saving result to the DP matrix for current state
    cache[i1, j1, i2] = ans;

    return ans;
}

// Driver code
public static void Main(String []args)
{
    //set initial value
    for(int i = 0; i < 5; i++)
        for(int i1 = 0; i1 < 5; i1++)
            for(int i2 = 0; i2 < 5; i2++)
                cache[i,i1,i2]=-1;

    Console.WriteLine( maxSumPath(0, 0, 0));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Input matrix
let n = 4, m = 4;
let arr=[[ 1, 0, 3, -1 ],
                [ 3, 5, 1, -2 ],
                [ -2, 0, 1, 1 ],
                [ 2, 1, -1, 1 ]];

// DP matrix
let cache=new Array(5);
for(let i = 0; i < 5; i++)
{
    cache[i] = new Array(5);
    for(let j = 0; j < 5; j++)
    {
        cache[i][j] = new Array(5);
        for(let k = 0; k < 5; k++)
        {
            cache[i][j][k] = -1;
        }
    }
}

// Function to return the sum of the cells
// arr[i1][j1] and arr[i2][j2]
function sum(i1, j1, i2, j2)
{
    if (i1 == i2 && j1 == j2)
    {
        return arr[i1][j1];
    }
    return arr[i1][j1] + arr[i2][j2];
}

// Recursive function to return the
// required maximum cost path
function maxSumPath(i1,j1,i2)
{
    // Column number of second path
    let j2 = i1 + j1 - i2;

    // Base Case
    if (i1 >= n || i2 >= n || j1 >= m || j2 >= m)
    {
        return 0;
    }

    // If already calculated, return from DP matrix
    if (cache[i1][j1][i2] != -1)
    {
        return cache[i1][j1][i2];
    }
    let ans = Number.MIN_VALUE;

    // Recurring for neighbouring cells of both paths together
    ans = Math.max(ans, maxSumPath(i1 + 1, j1, i2 + 1) + sum(i1, j1, i2, j2));
    ans = Math.max(ans, maxSumPath(i1, j1 + 1, i2) + sum(i1, j1, i2, j2));
    ans = Math.max(ans, maxSumPath(i1, j1 + 1, i2 + 1) + sum(i1, j1, i2, j2));
    ans = Math.max(ans, maxSumPath(i1 + 1, j1, i2) + sum(i1, j1, i2, j2));

    // Saving result to the DP matrix for current state
    cache[i1][j1][i2] = ans;

    return ans;
}

// Driver code
document.write( maxSumPath(0, 0, 0));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
16
```

**时间复杂度:** O((N <sup>2</sup> ) * M)