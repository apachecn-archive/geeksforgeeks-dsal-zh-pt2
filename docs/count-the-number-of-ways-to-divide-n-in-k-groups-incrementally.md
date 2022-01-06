# 递增计数 k 组 N 分频的方式数

> 原文:[https://www . geeksforgeeks . org/count-n 进 k 组的划分方式-递增/](https://www.geeksforgeeks.org/count-the-number-of-ways-to-divide-n-in-k-groups-incrementally/)

给定两个整数 **N** 和 **K** ，任务是计算将 N 划分为 K 组正整数的方法的数量，使得它们的和为 **N** ，并且组中的元素数量遵循非递减顺序(即组[i] < =组[i+1])。
**举例:**

> **输入:** N = 8，K = 4
> **输出:** 5
> **说明:**
> 它们是 5 组，这样它们的和是 8，每组的正整数个数是 4。
> [1，1，1，5]，[1，1，2，4]，[1，1，3，3]，[1，2，2，3]，[2，2，2，2]
> **输入:** N = 24，K = 5
> **输出:** 164
> **解释:**
> 有 164 个这样的组，它们的和是 24，并且是中的正整数数

**不同的方法:**
1。天真进场(时间:O(N)<sup>K</sup>)，空间:O(N)
2。记忆(时间:O((N <sup>3</sup> *K)，空间:O(N <sup>2</sup> *K))
3。自底向上动态规划(时间:0(N * K)，空间:0(N * K))

**天真方法:**我们可以使用[递归](https://www.geeksforgeeks.org/recursion/)来解决这个问题。在递归的每一步，将所有大于等于先前计算值的值。
以下是上述方法的实施:

## C++

```
// C++ implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements

#include <bits/stdc++.h>

using namespace std;

// Function to count the number
// of ways to divide the number N
// in groups such that each group
// has K number of elements
int calculate(int pos, int prev,
                 int left, int k)
{
    // Base Case
    if (pos == k) {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    int answer = 0;

    // put all possible values
    // greater equal to prev
    for (int i = prev; i <= left; i++) {
        answer += calculate(pos + 1, i,
                          left - i, k);
    }
    return answer;
}

// Function to count the number of
// ways to divide the number N
int countWaystoDivide(int n, int k)
{
    return calculate(0, 1, n, k);
}

// Driver Code
int main()
{
    int N = 8;
    int K = 4;

    cout << countWaystoDivide(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements
import java.util.*;
class GFG{

// Function to count the number
// of ways to divide the number N
// in groups such that each group
// has K number of elements
static int calculate(int pos, int prev,
                     int left, int k)
{

    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // If N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    int answer = 0;

    // Put all possible values
    // greater equal to prev
    for(int i = prev; i <= left; i++)
    {
       answer += calculate(pos + 1, i,
                           left - i, k);
    }
    return answer;
}

// Function to count the number of
// ways to divide the number N
static int countWaystoDivide(int n, int k)
{
    return calculate(0, 1, n, k);
}

// Driver Code
public static void main(String[] args)
{
    int N = 8;
    int K = 4;

    System.out.print(countWaystoDivide(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to count the
# number of ways to divide N in
# groups such that each group
# has K number of elements

# Function to count the number
# of ways to divide the number N
# in groups such that each group
# has K number of elements
def calculate(pos, prev, left, k):

    # Base Case
    if (pos == k):
        if (left == 0):
            return 1;
        else:
            return 0;

    # If N is divides completely
    # into less than k groups
    if (left == 0):
        return 0;

    answer = 0;

    # Put all possible values
    # greater equal to prev
    for i in range(prev, left + 1):
        answer += calculate(pos + 1, i,
                           left - i, k);

    return answer;

# Function to count the number of
# ways to divide the number N
def countWaystoDivide(n, k):

    return calculate(0, 1, n, k);

# Driver Code
if __name__ == '__main__':

    N = 8;
    K = 4;

    print(countWaystoDivide(N, K));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements
using System;

class GFG{

// Function to count the number
// of ways to divide the number N
// in groups such that each group
// has K number of elements
static int calculate(int pos, int prev,
                     int left, int k)
{

    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // If N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    int answer = 0;

    // Put all possible values
    // greater equal to prev
    for(int i = prev; i <= left; i++)
    {
       answer += calculate(pos + 1, i,
                           left - i, k);
    }
    return answer;
}

// Function to count the number of
// ways to divide the number N
static int countWaystoDivide(int n, int k)
{
    return calculate(0, 1, n, k);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 8;
    int K = 4;

    Console.Write(countWaystoDivide(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements

// Function to count the number
// of ways to divide the number N
// in groups such that each group
// has K number of elements
function calculate(pos, prev,
                left, k)
{
    // Base Case
    if (pos == k) {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    let answer = 0;

    // put all possible values
    // greater equal to prev
    for (let i = prev; i <= left; i++) {
        answer += calculate(pos + 1, i,
                        left - i, k);
    }
    return answer;
}

// Function to count the number of
// ways to divide the number N
function countWaystoDivide(n, k)
{
    return calculate(0, 1, n, k);
}

// Driver Code

    let N = 8;
    let K = 4;

    document.write(countWaystoDivide(N, K));

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
5
```

**时间复杂度:**O(N<sup>K</sup>)
T5】辅助空间: O(N)。
**记忆方法:**在前面的方法中我们可以看到，我们是在重复求解子问题，即遵循[重叠子问题](http://programming)的性质。所以我们可以用 DP 表把[记为](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)一样。
以下是上述方法的实施:

## C++

```
// C++ implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements

#include <bits/stdc++.h>

using namespace std;

// DP Table
int dp[100][100][100];

// Function to count the number
// of ways to divide the number N
// in groups such that each group
// has K number of elements
int calculate(int pos, int prev,
                int left, int k)
{
    // Base Case
    if (pos == k) {
        if (left == 0)
            return 1;
        else
            return 0;
    }
    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    // If the subproblem has been
    // solved, use the value
    if (dp[pos][prev][left] != -1)
        return dp[pos][prev][left];

    int answer = 0;
    // put all possible values
    // greater equal to prev
    for (int i = prev; i <= left; i++) {
        answer += calculate(pos + 1, i,
                           left - i, k);
    }

    return dp[pos][prev][left] = answer;
}

// Function to count the number of
// ways to divide the number N in groups
int countWaystoDivide(int n, int k)
{
    // Initialize DP Table as -1
    memset(dp, -1, sizeof(dp));

    return calculate(0, 1, n, k);
}

// Driver Code
int main()
{
    int N = 8;
    int K = 4;

    cout << countWaystoDivide(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements
import java.util.*;
class GFG{

// DP Table
static int [][][]dp = new int[100][100][100];

// Function to count the number
// of ways to divide the number N
// in groups such that each group
// has K number of elements
static int calculate(int pos, int prev,
                     int left, int k)
{
    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    // If the subproblem has been
    // solved, use the value
    if (dp[pos][prev][left] != -1)
        return dp[pos][prev][left];

    int answer = 0;

    // put all possible values
    // greater equal to prev
    for (int i = prev; i <= left; i++)
    {
        answer += calculate(pos + 1, i,
                           left - i, k);
    }

    return dp[pos][prev][left] = answer;
}

// Function to count the number of
// ways to divide the number N in groups
static int countWaystoDivide(int n, int k)
{
    // Initialize DP Table as -1
        for (int i = 0; i < 100; i++)
        {
            for (int j = 0; j < 100; j++)
            {
                for (int l = 0; l < 100; l++)
                    dp[i][j][l] = -1;
            }
        }

    return calculate(0, 1, n, k);
}

// Driver Code
public static void main(String[] args)
{
    int N = 8;
    int K = 4;

    System.out.print(countWaystoDivide(N, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to count the
# number of ways to divide N in
# groups such that each group
# has K number of elements

# DP Table
dp = [[[0 for i in range(50)]
             for j in range(50)]
          for j in range(50)]

# Function to count the number
# of ways to divide the number N
# in groups such that each group
# has K number of elements
def calculate(pos, prev, left, k):

    # Base Case
    if (pos == k):
        if (left == 0):
            return 1;
        else:
            return 0;

    # if N is divides completely
    # into less than k groups
    if (left == 0):
        return 0;

    # If the subproblem has been
    # solved, use the value
    if (dp[pos][prev][left] != -1):
        return dp[pos][prev][left];

    answer = 0;

    # put all possible values
    # greater equal to prev
    for i in range(prev,left+1):
        answer += calculate(pos + 1, i,
                            left - i, k);
    dp[pos][prev][left] = answer;
    return dp[pos][prev][left];

# Function to count the number of
# ways to divide the number N in groups
def countWaystoDivide(n, k):

    # Initialize DP Table as -1
    for i in range(50):
        for j in range(50):
            for l in range(50):
                dp[i][j][l] = -1;

    return calculate(0, 1, n, k);

# Driver Code
if __name__ == '__main__':
    N = 8;
    K = 4;

    print(countWaystoDivide(N, K));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements
using System;
class GFG{

// DP Table
static int [,,]dp = new int[50, 50, 50];

// Function to count the number
// of ways to divide the number N
// in groups such that each group
// has K number of elements
static int calculate(int pos, int prev,
                     int left, int k)
{
    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    // If the subproblem has been
    // solved, use the value
    if (dp[pos, prev, left] != -1)
        return dp[pos, prev, left];

    int answer = 0;

    // put all possible values
    // greater equal to prev
    for (int i = prev; i <= left; i++)
    {
        answer += calculate(pos + 1, i,
                           left - i, k);
    }

    return dp[pos, prev, left] = answer;
}

// Function to count the number of
// ways to divide the number N in groups
static int countWaystoDivide(int n, int k)
{
    // Initialize DP Table as -1
        for (int i = 0; i < 50; i++)
        {
            for (int j = 0; j < 50; j++)
            {
                for (int l = 0; l < 50; l++)
                    dp[i, j, l] = -1;
            }
        }

    return calculate(0, 1, n, k);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 8;
    int K = 4;

    Console.Write(countWaystoDivide(N, K));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements

// DP Table
let dp = new Array(500);
for(let i=0;i<500;i++)
{
    dp[i]=new Array(500);
    for(let j=0;j<500;j++)
    {
        dp[i][j]=new Array(500);
        for(let k=0;k<500;k++)
            dp[i][j][k]=0;
    }
}

// Function to count the number
// of ways to divide the number N
// in groups such that each group
// has K number of elements
function calculate(pos,prev,left,k)
{
    // Base Case
    if (pos == k)
    {
        if (left == 0)
            return 1;
        else
            return 0;
    }

    // if N is divides completely
    // into less than k groups
    if (left == 0)
        return 0;

    // If the subproblem has been
    // solved, use the value
    if (dp[pos][prev][left] != -1)
        return dp[pos][prev][left];

    let answer = 0;

    // put all possible values
    // greater equal to prev
    for (let i = prev; i <= left; i++)
    {
        answer += calculate(pos + 1, i,
                           left - i, k);
    }

    return dp[pos][prev][left] = answer;
}

// Function to count the number of
// ways to divide the number N in groups
function countWaystoDivide(n,k)
{
    // Initialize DP Table as -1
        for (let i = 0; i < 500; i++)
        {
            for (let j = 0; j < 500; j++)
            {
                for (let l = 0; l < 500; l++)
                    dp[i][j][l] = -1;
            }
        }

    return calculate(0, 1, n, k);
}

// Driver Code
let N = 8;
let K = 4;

document.write(countWaystoDivide(N, K));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
5
```

**时间复杂度:**o(n^3 * k)
T3】辅助空间: O(N^2 * K)。

**自下而上的 DP:** 我们被要求求 CountWaystoDivide(n，k)所以 DP 的递推方法和解释是:

> **CountWaystoDivide( n，k ) = CountWaystoDivide( n-k，k ) + CountWaystoDivide( n-1，k-1 )**
> 
> **解释:**
> 将 CountWaystoDivide( n，k)分为两部分，其中
> 
> 1.  如果第一个元素是 1，那么剩下的构成 n-1 的总数，分成 k-1，所以 CountWaystoDivide( n-1，k-1)
> 2.  如果第一个元素大于 1，那么我们可以从每一个元素中减去 1，得到 n-k 到 k 个部分的有效划分，从而得到 CountWaystoDivide( n-1，k-1)。
> 
> **DP**的数学解释:
> 
> 1.  由于每组必须至少有一个人，所以，给每组一个人，然后我们剩下 n-k 个人，我们可以分为 1，2，3..或者 k 个组。因此，我们的 dp 将是:DP[n][k]= DP[n-k][1]+DP[n-k][2]+DP[n-k][3]+…。+ dp[n-k][k]。
> 2.  乍一看，前面的可能会给出 O(N <sup>3</sup> )的振动，但是通过一点操作我们可以优化它:
>     DP[N][k]= DP[(N-1)-(k-1)][1]+DP[(N-1)-(k-1)][2]+…+DP[(N-1)-(k-1)][k-1]+DP[(N-1)-(k-1)][k]
>     从递归中，我们可以写出:
>     dp[n]

使用差压解决问题的步骤:

*   初始化一个大小为 n+1，k+1 的二维数组 dp[][]，其中 dp[i][j]将存储将 n 分成 k 个组的最优解。
*   对于从 i=0 到 n 的每个值，dp[n][1]将是 1，因为将 n 除 1 的总方法是 1。dp[0][0]也将是 1。

动力定位状态更新如下:

*   如果 i>=j，则 DP[I][j]= DP[I-1][j-1]+DP[I-j][j]
*   否则 i-j <0 and dp[i-j][j] become zero so dp[i][j] = dp[i-1][j-1]

## C++

```
// C++ implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements

#include <bits/stdc++.h>

using namespace std;

// Function to count the number of
// ways to divide the number N in groups
int countWaystoDivide(int n, int k)
{
    if (n < k)
        return 0; // When n is less than k, No way to divide
                  // into groups
    vector<vector<int> > dp(n + 1, vector<int>(k + 1));

    for (int i = 1; i <= n; i++)
        dp[i][1]
            = 1; // exact one way to divide n to 1 group
    dp[0][0] = 1;

    for (int i = 1; i <= n; i++) {
        for (int j = 2; j <= k; j++) {
            if (i >= j)
                dp[i][j] = dp[i - j][j] + dp[i - 1][j - 1];
            else
                dp[i][j]
                    = dp[i - 1][j - 1]; // i<j so dp[i-j][j]
                                        // becomes zero
        }
    }
    return dp[n][k]; // returning number of ways to divide N
                     // in k groups
}

// Driver Code
int main()
{
    int N = 8;
    int K = 4;

    cout << countWaystoDivide(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements
import java.io.*;

class GFG {

  static int countWaystoDivide(int n, int k)
  {
    if (n < k)
      return 0; // When n is less than k, No way to divide
    // into groups

    int [][]dp = new int[n+1][k+1];
    for (int i = 1; i <= n; i++)
      dp[i][1]
      = 1; // exact one way to divide n to 1 group
    dp[0][0] = 1;

    for (int i = 1; i <= n; i++) {
      for (int j = 2; j <= k; j++) {
        if (i >= j)
          dp[i][j] = dp[i - j][j] + dp[i - 1][j - 1];
        else
          dp[i][j]
          = dp[i - 1][j - 1]; // i<j so dp[i-j][j]
        // becomes zero
      }
    }
    return dp[n][k]; // returning number of ways to divide N
    // in k groups
  }

  // Driver code
  public static void main (String[] args)
  {
    int N = 8;
    int K = 4;

    System.out.println(countWaystoDivide(N, K));
  }
}

// This code is contributed by rohitsingh07052.
```

## 蟒蛇 3

```
# Python3 implementation to count the
# number of ways to divide N in
# groups such that each group
# has K number of elements

# DP Table
# Function to count the number of
# ways to divide the number N in groups

def countWaystoDivide(n, k):
    if(n < k):
        return 0

    dp = [[0 for i in range(k+1)] for i in range(n+1)]
    for i in range(1, n+1):
        dp[i][1] = 1
    dp[0][0] = 1
    for i in range(1, n+1):
        for j in range(2, k+1):
            if(i >= j):
                dp[i][j] = dp[i-1][j-1] + dp[i-j][j]

            else:
                dp[i][j] = dp[i-1][j-1]
    return dp[n][k]

# Driver Code
if __name__ == '__main__':
    N = 8
    K = 4

    print(countWaystoDivide(N, K))

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation to count the
// number of ways to divide N in
// groups such that each group
// has K number of elements
using System;
using System.Collections.Generic;
class GFG {

  static int countWaystoDivide(int n, int k)
  {
    if (n < k)
      return 0; // When n is less than k, No way to divide
    // into groups

    int[,] dp = new int[n + 1, k + 1];
    for (int i = 1; i <= n; i++)
      dp[i, 1] = 1; // exact one way to divide n to 1 group
    dp[0, 0] = 1;

    for (int i = 1; i <= n; i++) {
      for (int j = 2; j <= k; j++) {
        if (i >= j)
          dp[i,j] = dp[i - j,j] + dp[i - 1,j - 1];
        else
          dp[i,j] = dp[i - 1, j - 1]; // i<j so dp[i-j][j]
        // becomes zero
      }
    }
    return dp[n,k]; // returning number of ways to divide N
    // in k groups
  }

  static void Main() {
    int N = 8;
    int K = 4;

    Console.Write(countWaystoDivide(N, K));
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>
    // Javascript implementation to count the
    // number of ways to divide N in
    // groups such that each group
    // has K number of elements

    // Function to count the number of
    // ways to divide the number N in groups
    function countWaystoDivide(n, k)
    {
        if (n < k)
            return 0; // When n is less than k, No way to divide
                      // into groups
        let dp = new Array(n + 1);
        for(let i = 0; i < n + 1; i++)
        {
            dp[i] = new Array(k + 1);
            for(let j = 0; j < k + 1; j++)
            {
                dp[i][j] = 0;
            }
        }

        for (let i = 1; i <= n; i++)
            dp[i][1]
                = 1; // exact one way to divide n to 1 group
        dp[0][0] = 1;

        for (let i = 1; i <= n; i++) {
            for (let j = 2; j <= k; j++) {
                if (i >= j)
                    dp[i][j] = dp[i - j][j] + dp[i - 1][j - 1];
                else
                    dp[i][j]
                        = dp[i - 1][j - 1]; // i<j so dp[i-j][j]
                                            // becomes zero
            }
        }
        return dp[n][k]; // returning number of ways to divide N
                         // in k groups
    }

    let N = 8;
    let K = 4;

    document.write(countWaystoDivide(N, K));

// This code is contributed by mukesh07.
</script>
```

**Output**

```
5
```

**时间复杂度:**O(N * K)
T3】辅助空间: O(N * K)