# K 步遍历矩阵并返回原点的次数

> 原文:[https://www . geeksforgeeks . org/k 步遍历矩阵并返回原点的次数/](https://www.geeksforgeeks.org/count-of-ways-to-traverse-a-matrix-and-return-to-origin-in-k-steps/)

给定三个整数 **N** 、 **M** 和 **K** ，其中 **N** 和 **M** 是矩阵的维数，K 是最大可能步数，任务是统计从(0，0)开始遍历矩阵的路数，只使用 K 步返回遍历矩阵。
**注意:**每走一步，可将**上下左右移动**，或**停留在当前位置**。答案可能很大，所以以**10<sup>9</sup>+7**
**为模打印答案示例:**

> **输入:** N = 2，M = 2，K = 2
> **输出:** 3
> **说明:**
> 三种方式分别是:
> 1)停留，停留。
> 2)上、下
> 3)右、左
> **输入:** N = 3，M = 3，K = 4
> **输出:** 23

**方法:**这个问题也可以使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)技术来解决。按照以下步骤解决问题:

*   从位置(0，0)开始，递归调用每个可能的位置，并将步长值减少 1。

*   创建大小为 N * M * K ( **DP[N][M][S]** )
    的三维数组

```
Possible ways for each step
can be calculated by:

 DP[i][j][k]
  =  Recursion(i+1, j, k-1)  +
     Recursion(i-1, j, k-1)  +  
     Recursion(i, j-1, k-1)  +  
     Recursion(i, j+1, k-1)  +  
     Recursion(i, j, k-1).

With base condition returning 0,
whenever
i >= l or i = b or j < 0 or k < 0.
```

以下是上述方法的实现:

## C++

```
// C++ program to count total
// number of ways to return
// to origin after completing
// given number of steps.

#include <bits/stdc++.h>
using namespace std;
#define MOD 1000000007

long long dp[101][101][101];
int N, M, K;

// Function Initialize dp[][][]
// array with -1
void Initialize()
{

    for (int i = 0; i <= 100; i++)
        for (int j = 0; j <= 100; j++)
            for (int z = 0; z <= 100; z++)
                dp[i][j][z] = -1;
}

// Function returns the total count
int CountWays(int i, int j, int k)
{
    if (i >= N || i < 0
        || j >= M || j < 0 || k < 0)
        return 0;

    if (i == 0 && j == 0
        && k == 0)
        return 1;

    if (dp[i][j][k] != -1)
        return dp[i][j][k];
    else
        dp[i][j][k]
            = (CountWays(i + 1, j, k - 1) % MOD
               + CountWays(i - 1, j, k - 1) % MOD
               + CountWays(i, j - 1, k - 1) % MOD
               + CountWays(i, j + 1, k - 1) % MOD
               + CountWays(i, j, k - 1) % MOD)
              % MOD;

    return dp[i][j][k];
}

// Driver Program
int main()
{
    N = 3;
    M = 3;
    K = 4;

    Initialize();
    cout << CountWays(0, 0, K)
         << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total
// number of ways to return
// to origin after completing
// given number of steps.
class GFG{

static int [][][] dp = new int[101][101][101];
static int N, M, K;
static int MOD = 1000000007;

// Function Initialize dp[][][]
// array with -1
public static void Initialize()
{
    for(int i = 0; i <= 100; i++)
       for(int j = 0; j <= 100; j++)
          for(int z = 0; z <= 100; z++)
             dp[i][j][z] = -1;
}

// Function returns the total count
public static int CountWays(int i, int j, int k)
{
    if (i >= N || i < 0 ||
        j >= M || j < 0 || k < 0)
        return 0;

    if (i == 0 && j == 0 && k == 0)
        return 1;

    if (dp[i][j][k] != -1)
        return dp[i][j][k];

    else
        dp[i][j][k] = (CountWays(i + 1, j, k - 1) % MOD +
                       CountWays(i - 1, j, k - 1) % MOD +
                       CountWays(i, j - 1, k - 1) % MOD +
                       CountWays(i, j + 1, k - 1) % MOD +
                       CountWays(i, j, k - 1) % MOD) % MOD;

    return dp[i][j][k];
}

// Driver code
public static void main(String[] args)
{
    N = 3;
    M = 3;
    K = 4;

    Initialize();
    System.out.println(CountWays(0, 0, K));
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program to count total
# number of ways to return
# to origin after completing
# given number of steps.
MOD = 1000000007

dp = [[[0 for i in range(101)]
          for i in range(101)]
          for i in range(101)]
N, M, K = 0, 0, 0

# Function Initialize dp[][][]
# array with -1
def Initialize():

    for i in range(101):
        for j in range(101):
            for z in range(101):
                dp[i][j][z] = -1

# Function returns the total count
def CountWays(i, j, k):

    if (i >= N or i < 0 or
        j >= M or j < 0 or k < 0):
        return 0

    if (i == 0 and j == 0 and k == 0):
        return 1

    if (dp[i][j][k] != -1):
        return dp[i][j][k]
    else:
        dp[i][j][k] = (CountWays(i + 1, j, k - 1) % MOD +
                       CountWays(i - 1, j, k - 1) % MOD +
                       CountWays(i, j - 1, k - 1) % MOD +
                       CountWays(i, j + 1, k - 1) % MOD +
                       CountWays(i, j, k - 1) % MOD) % MOD
    return dp[i][j][k]

# Driver code
if __name__ == '__main__':

    N = 3
    M = 3
    K = 4

    Initialize()
    print(CountWays(0, 0, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count total
// number of ways to return
// to origin after completing
// given number of steps.
using System;

class GFG{

static int [,,] dp = new int[101, 101, 101];
static int N, M, K;
static int MOD = 1000000007;

// Function Initialize [,]dp[]
// array with -1
public static void Initialize()
{
    for(int i = 0; i <= 100; i++)
        for(int j = 0; j <= 100; j++)
            for(int z = 0; z <= 100; z++)
                dp[i, j, z] = -1;
}

// Function returns the total count
public static int CountWays(int i, int j, int k)
{
    if (i >= N || i < 0 ||
        j >= M || j < 0 || k < 0)
        return 0;

    if (i == 0 && j == 0 && k == 0)
        return 1;

    if (dp[i, j, k] != -1)
        return dp[i, j, k];

    else
        dp[i, j, k] = (CountWays(i + 1, j, k - 1) % MOD +
                       CountWays(i - 1, j, k - 1) % MOD +
                       CountWays(i, j - 1, k - 1) % MOD +
                       CountWays(i, j + 1, k - 1) % MOD +
                       CountWays(i, j, k - 1) % MOD) % MOD;

    return dp[i, j, k];
}

// Driver code
public static void Main(String[] args)
{
    N = 3;
    M = 3;
    K = 4;

    Initialize();
    Console.WriteLine(CountWays(0, 0, K));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to count total
// number of ways to return
// to origin after completing
// given number of steps.

var MOD =  1000000007;

var dp = Array.from(Array(101), ()=>Array(101));
for(var i =0; i<101; i++)
        for(var j =0; j<101; j++)
            dp[i][j] = new Array(101).fill(-1);
var N, M, K;

// Function returns the total count
function CountWays(i, j, k)
{
    if (i >= N || i < 0
        || j >= M || j < 0 || k < 0)
        return 0;

    if (i == 0 && j == 0
        && k == 0)
        return 1;

    if (dp[i][j][k] != -1)
        return dp[i][j][k];
    else
        dp[i][j][k]
            = (CountWays(i + 1, j, k - 1) % MOD
               + CountWays(i - 1, j, k - 1) % MOD
               + CountWays(i, j - 1, k - 1) % MOD
               + CountWays(i, j + 1, k - 1) % MOD
               + CountWays(i, j, k - 1) % MOD)
              % MOD;

    return dp[i][j][k];
}

// Driver Program
N = 3;
M = 3;
K = 4;
document.write( CountWays(0, 0, K))

</script>
```

**Output:** 

```
23
```