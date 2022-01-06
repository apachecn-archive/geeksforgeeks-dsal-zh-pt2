# 长度为 N 的二进制串的计数，偶数位计数，最多 K 个连续 1

> 原文:[https://www . geeksforgeeks . org/长度为 n 的二进制字符串的计数，偶数集位计数和最多 k 个连续 1/](https://www.geeksforgeeks.org/count-of-binary-strings-of-length-n-with-even-set-bit-count-and-at-most-k-consecutive-1s/)

给定两个整数 **N** 和 **K** ，任务是找出长度为 N 的二进制串的数量，其中偶数为 1，少于 K 的串是连续的。
**例:**

> **输入:** N = 4，K = 2
> **输出:** 4
> **解释:**
> 可能的二进制字符串有 0000，0101，1001，1010。它们都有偶数个 1，其中少于 2 个连续出现。
> **输入:** N = 3，K = 2
> **输出:** 2
> **解释:**
> 可能的二进制字符串为 000，101。所有其他字符串 001、010、011、100、110、111 都不符合标准。

**进场:**
这个问题可以通过[动态规划解决。](https://www.geeksforgeeks.org/dynamic-programming/)
让我们考虑一个 3D 表 **dp[][][]** 来存储每个子问题的解，这样， **dp[n][i][s]** 表示长度为**n 的二进制字符串的数量**具有 **i 个连续的 1**和**个 1 的和= s** 。由于只需要检查 1 的总数是否为偶数，所以我们存储 **s % 2** 。因此， **dp[n][i][s]** 可计算如下:

1.  如果我们将 **0** 放置在 **n <sup>第</sup>位置**，1 的数量保持不变。因此，**DP[n][I][s]= DP[n–1][0][s]**。
2.  如果我们将 1 放在第 **n <sup>个</sup>位置**，**DP[n][I][s]= DP[n–1][I+1][(s+1)% 2]**。
3.  由以上两点形成的递推关系由下式给出:

> ![dp[n][i][s] = dp[n-1][0][s] + dp[n - 1][i + 1][(s + 1)mod 2] ](img/f1fc9a8bc052caf5eb6ae08b29f030ab.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Table to store solution
// of each subproblem
int dp[100001][20][2];

// Function to calculate
// the possible binary
// strings
int possibleBinaries(int pos,
                     int ones,
                     int sum,
                     int k)
{
    // If number of ones
    // is equal to K
    if (ones == k)
        return 0;

    // pos: current position
    // Base Case: When n
    // length is traversed
    if (pos == 0)

        // sum: count of 1's
        // Return the count
        // of 1's obtained
        return (sum == 0) ? 1 : 0;

    // If the subproblem has already
    // been solved
    if (dp[pos][ones][sum] != -1)
        // Return the answer
        return dp[pos][ones][sum];

    // Recursive call when current
    // position is filled with 1
    int ret = possibleBinaries(pos - 1,
                               ones + 1,
                               (sum + 1) % 2,
                               k)
              // Recursive call when current
              // position is filled with 0
              + possibleBinaries(pos - 1, 0,
                                 sum, k);

    // Store the solution
    // to this subproblem
    dp[pos][ones][sum] = ret;

    return dp[pos][ones][sum];
}

// Driver Code
int main()
{
    int N = 3;
    int K = 2;

    // Initialising the
    // table with -1
    memset(dp, -1, sizeof dp);

    cout << possibleBinaries(N, 0, 0, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Table to store solution
// of each subproblem
static int [][][]dp = new int[100001][20][2];

// Function to calculate
// the possible binary
// Strings
static int possibleBinaries(int pos, int ones,
                            int sum, int k)
{

    // If number of ones
    // is equal to K
    if (ones == k)
        return 0;

    // pos: current position
    // Base Case: When n
    // length is traversed
    if (pos == 0)

        // sum: count of 1's
        // Return the count
        // of 1's obtained
        return (sum == 0) ? 1 : 0;

    // If the subproblem has already
    // been solved
    if (dp[pos][ones][sum] != -1)

        // Return the answer
        return dp[pos][ones][sum];

    // Recursive call when current
    // position is filled with 1
    int ret = possibleBinaries(pos - 1,
                              ones + 1,
                              (sum + 1) % 2, k) +

              // Recursive call when current
              // position is filled with 0
              possibleBinaries(pos - 1, 0,
                               sum, k);

    // Store the solution
    // to this subproblem
    dp[pos][ones][sum] = ret;

    return dp[pos][ones][sum];
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    int K = 2;

    // Initialising the
    // table with -1
    for(int i = 0; i < 100001; i++)
    {
        for(int j = 0; j < 20; j++)
        {
            for(int l = 0; l < 2; l++)
                dp[i][j][l] = -1;
        }
    }

    System.out.print(possibleBinaries(N, 0, 0, K));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach
import numpy as np

# Table to store solution
# of each subproblem
dp = np.ones(((100002, 21, 3)))
dp = -1 * dp

# Function to calculate
# the possible binary
# strings
def possibleBinaries(pos, ones, sum, k):

    # If number of ones
    # is equal to K
    if (ones == k):
        return 0

    # pos: current position
    # Base Case: When n
    # length is traversed
    if (pos == 0):

        # sum: count of 1's
        # Return the count
        # of 1's obtained
        return 1 if (sum == 0) else 0

    # If the subproblem has already
    # been solved
    if (dp[pos][ones][sum] != -1):

        # Return the answer
        return dp[pos][ones][sum]

    # Recursive call when current
    # position is filled with 1
    ret = (possibleBinaries(pos - 1,
                           ones + 1,
                           (sum + 1) % 2, k) +

           # Recursive call when current
           # position is filled with 0
           possibleBinaries(pos - 1, 0, sum, k))

    # Store the solution
    # to this subproblem
    dp[pos][ones][sum] = ret

    return dp[pos][ones][sum]

# Driver Code
N = 3
K = 2

print(int(possibleBinaries(N, 0, 0, K)))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Table to store solution
// of each subproblem
static int [,,]dp = new int[100001, 20, 2];

// Function to calculate the
// possible binary Strings
static int possibleBinaries(int pos, int ones,
                            int sum, int k)
{

    // If number of ones
    // is equal to K
    if (ones == k)
        return 0;

    // pos: current position
    // Base Case: When n
    // length is traversed
    if (pos == 0)

        // sum: count of 1's
        // Return the count
        // of 1's obtained
        return (sum == 0) ? 1 : 0;

    // If the subproblem has already
    // been solved
    if (dp[pos, ones, sum] != -1)

        // Return the answer
        return dp[pos, ones, sum];

    // Recursive call when current
    // position is filled with 1
    int ret = possibleBinaries(pos - 1,
                                ones + 1,
                                (sum + 1) % 2, k) +
              // Recursive call when current
              // position is filled with 0
              possibleBinaries(pos - 1, 0,
                               sum, k);

    // Store the solution
    // to this subproblem
    dp[pos, ones, sum] = ret;

    return dp[pos, ones, sum];
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;
    int K = 2;

    // Initialising the
    // table with -1
    for(int i = 0; i < 100001; i++)
    {
        for(int j = 0; j < 20; j++)
        {
            for(int l = 0; l < 2; l++)
                dp[i, j, l] = -1;
        }
    }
    Console.Write(possibleBinaries(N, 0, 0, K));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Table to store solution
// of each subproblem
let dp = new Array(100001).fill(-1).map((t) => new Array(20).fill(-1).map((r) => new Array(2).fill(-1)));

// Function to calculate
// the possible binary
// strings
function possibleBinaries(pos, ones, sum, k)
{

    // If number of ones
    // is equal to K
    if (ones == k)
        return 0;

    // pos: current position
    // Base Case: When n
    // length is traversed
    if (pos == 0)

        // sum: count of 1's
        // Return the count
        // of 1's obtained
        return (sum == 0) ? 1 : 0;

    // If the subproblem has already
    // been solved
    if (dp[pos][ones][sum] != -1)
        // Return the answer
        return dp[pos][ones][sum];

    // Recursive call when current
    // position is filled with 1
    let ret = possibleBinaries(pos - 1,
        ones + 1,
        (sum + 1) % 2,
        k)

        // Recursive call when current
        // position is filled with 0
        + possibleBinaries(pos - 1, 0,
            sum, k);

    // Store the solution
    // to this subproblem
    dp[pos][ones][sum] = ret;

    return dp[pos][ones][sum];
}

// Driver Code
let N = 3;
let K = 2;

// Initialising the
// table with -1
document.write(possibleBinaries(N, 0, 0, K));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
2
```

**时间复杂度:**T2【O(2 * N * K)T4】