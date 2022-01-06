# 使用平方根或除以 2 将 A 和 B 减少到 0 的最小成本

> 原文:[https://www . geeksforgeeks . org/使用平方根或除以 2 将 a 和 b 减少到 0 的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-reduce-a-and-b-to-0-using-square-root-or-divide-by-2/)

给定两个整数 A 和 B，任务是通过执行以下两种类型的操作，以最小的成本将给定的两个整数转换为零:

*   用 A 和 B 的乘积的平方根替换整数 A 和 B。这个操作将花费 2 个单位。
*   分别用 A/2 代替 A 或用 B/2 代替 B。这项操作将花费 1 个单位。

**示例:**

> **输入:** A = 2，B = 2
> **输出:** 4
> **说明:**
> 操作 1:对 A 进行第一次操作，使 A=1，B = 2。成本=1
> 操作 2:在 A 上再次应用第一个操作，使 A=0，B=2。成本=2
> 操作 3:对 A 和 B 都进行第二次操作，使 A=0，B=0。成本=4。
> 
> **输入:** A = 53，B = 16
> T3】输出: 7

**进场:**

这个问题可以通过使用递归树探索所有可能性，然后[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)矩阵中的解来解决。要解决此问题，请执行以下步骤:

1.  创建一个函数**获取微操作**，五个参数为 **A、B、** **普雷瓦**、**普雷瓦**和一个 **dp 矩阵**，这里**普雷瓦**和**普雷瓦**是 **A** 和 **B** 的前一个值。该功能将使 **A** 和 **B** 所需的最低成本归零。
2.  现在，首先用参数调用这个函数， **A，B，普雷瓦** = -1，**普雷瓦** = -1 和 **dp** 。
3.  在每次通话中:
    *   首先，检查 **A** 和 **B** 的值是否等于**普雷瓦**和**普雷沃**的值。如果是，则从该调用返回 INT_MAX，因为该调用不会导致 **A** 和 **B** 的值发生变化，因此将导致无限递归循环。
    *   检查基本情况，即 **A** 和 **B** 均为零。如果是，从这个调用返回 0，因为在这个阶段将 **A** 和 **B** 转换为零的最小成本是 0。
    *   另外，检查这个递归调用是否已经存储在 **dp** 矩阵中。如果是，则从矩阵中返回值。
    *   现在，每个递归调用的答案是三个子问题提供的答案中的最小值:
        *   如果 **A** 减少到 **A/2** ，则成本最低。
        *   如果 **B** 减少到 **B/2** ，则成本最低。
        *   如果 **A** 和 **B** 都减少到 **sqrt(A*B)** ，则成本最低。
    *   找到这三个值中的最小值，并在从当前递归调用返回时记住它。
4.  该函数将在所有递归调用完成后返回最小开销。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost
// of converting A and B to 0
int getMinOperations(int A, int B,
                     int prevA, int prevB,
                     vector<vector<int> >& dp)
{

    // If both A and B doesn't change in
    // this recursive call, then return INT_MAX
    // to save the code from going into
    // infinite loop
    if (A == prevA and B == prevB) {
        return INT_MAX;
    }

    // Base Case
    if (A == 0 and B == 0) {
        return 0;
    }

    // If the answer of this recursive call
    // is already memoised
    if (dp[A][B] != -1) {
        return dp[A][B];
    }

    // If A is reduced to A/2
    int ans1 = getMinOperations(
        A / 2, B, A, B, dp);
    if (ans1 != INT_MAX) {
        ans1 += 1;
    }

    // If B is reduced to B/2
    int ans2 = getMinOperations(
        A, B / 2, A, B, dp);
    if (ans2 != INT_MAX) {
        ans2 += 1;
    }

    // If both A and B is reduced to sqrt(A * B)
    int ans3 = getMinOperations(sqrt(A * B),
                                sqrt(A * B), A,
                                B, dp);
    if (ans3 != INT_MAX) {
        ans3 += 2;
    }

    // Return the minimum of the value given
    // by the above three subproblems, also
    // memoize the value while returning
    return dp[A][B] = min({ ans1, ans2, ans3 });
}

// Driver Code
int main()
{
    int A = 53, B = 16;
    int mx = max(A, B);
    vector<vector<int> > dp(
        mx + 1,
        vector<int>(mx + 1, -1));

    cout << getMinOperations(
        A, B, -1, -1, dp);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

    // Function to return the minimum cost
    // of converting A and B to 0
    static int getMinOperations(int A, int B, int prevA,
                                int prevB, int dp[][])
    {

        // If both A and B doesn't change in
        // this recursive call, then return INT_MAX
        // to save the code from going into
        // infinite loop
        if (A == prevA && B == prevB) {
            return Integer.MAX_VALUE;
        }

        // Base Case
        if (A == 0 && B == 0) {
            return 0;
        }

        // If the answer of this recursive call
        // is already memoised
        if (dp[A][B] != -1) {
            return dp[A][B];
        }

        // If A is reduced to A/2
        int ans1 = getMinOperations(A / 2, B, A, B, dp);
        if (ans1 != Integer.MAX_VALUE) {
            ans1 += 1;
        }

        // If B is reduced to B/2
        int ans2 = getMinOperations(A, B / 2, A, B, dp);
        if (ans2 != Integer.MAX_VALUE) {
            ans2 += 1;
        }

        // If both A and B is reduced to sqrt(A * B)
        int ans3 = getMinOperations((int)Math.sqrt(A * B),
                                    (int)Math.sqrt(A * B),
                                    A, B, dp);
        if (ans3 != Integer.MAX_VALUE) {
            ans3 += 2;
        }
        // Return the minimum of the value given
        // by the above three subproblems, also
        // memoize the value while returning
        return dp[A][B]
            = Math.min(ans1, Math.min(ans2, ans3));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A = 53, B = 16;
        int mx = Math.max(A, B);
        int dp[][] = new int[mx + 1][mx + 1];
        for (int i = 0; i <= mx; i++) {
            for (int j = 0; j <= mx; j++)
                dp[i][j] = -1;
        }
        System.out.println(
            getMinOperations(A, B, -1, -1, dp));
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# Python program for the above approach
import math as Math

# Function to return the minimum cost
# of converting A and B to 0
def getMinOperations(A, B, prevA, prevB, dp):

  # If both A and B doesn't change in
  # this recursive call, then return INT_MAX
  # to save the code from going into
  # infinite loop
  if (A == prevA and B == prevB):
    return 10**9;

  # Base Case
  if (A == 0 and B == 0):
    return 0;

  # If the answer of this recursive call
  # is already memoised
  if (dp[A][B] != -1):
    return dp[A][B];

  # If A is reduced to A/2
  ans1 = getMinOperations(A // 2, B, A, B, dp);
  if (ans1 != 10**9):
    ans1 += 1;

  # If B is reduced to B/2
  ans2 = getMinOperations(A, B // 2, A, B, dp);
  if (ans2 != 10**9):
    ans2 += 1;

  # If both A and B is reduced to sqrt(A * B)
  ans3 = getMinOperations(
    Math.floor(Math.sqrt(A * B)),
    Math.floor(Math.sqrt(A * B)),
    A,
    B,
    dp
  );
  if (ans3 != 10**9):
    ans3 += 2;

  # Return the minimum of the value given
  # by the above three subproblems, also
  # memoize the value while returning
  dp[A][B] = min(ans1, min(ans2, ans3))
  return dp[A][B];

# Driver Code
A = 53
B = 16
mx = max(A, B);
dp = [[-1 for i in range(mx + 1)] for i in range(mx + 1)]

print(getMinOperations(A, B, -1, -1, dp));

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG
{

    // Function to return the minimum cost
    // of converting A and B to 0
    static int getMinOperations(int A, int B, int prevA,
                                int prevB, int [,]dp)
    {

        // If both A and B doesn't change in
        // this recursive call, then return INT_MAX
        // to save the code from going into
        // infinite loop
        if (A == prevA && B == prevB) {
            return Int32.MaxValue;
        }

        // Base Case
        if (A == 0 && B == 0) {
            return 0;
        }

        // If the answer of this recursive call
        // is already memoised
        if (dp[A, B] != -1) {
            return dp[A, B];
        }

        // If A is reduced to A/2
        int ans1 = getMinOperations(A / 2, B, A, B, dp);
        if (ans1 != Int32.MaxValue) {
            ans1 += 1;
        }

        // If B is reduced to B/2
        int ans2 = getMinOperations(A, B / 2, A, B, dp);
        if (ans2 != Int32.MaxValue) {
            ans2 += 1;
        }

        // If both A and B is reduced to sqrt(A * B)
        int ans3 = getMinOperations((int)Math.Sqrt(A * B),
                                    (int)Math.Sqrt(A * B),
                                    A, B, dp);
        if (ans3 != Int32.MaxValue) {
            ans3 += 2;
        }
        // Return the minimum of the value given
        // by the above three subproblems, also
        // memoize the value while returning
        return dp[A, B]
            = Math.Min(ans1, Math.Min(ans2, ans3));
    }

    // Driver Code
    public static void Main()
    {
        int A = 53, B = 16;
        int mx = Math.Max(A, B);
        int [,]dp = new int[mx + 1, mx + 1];
        for (int i = 0; i <= mx; i++) {
            for (int j = 0; j <= mx; j++)
                dp[i, j] = -1;
        }
        Console.Write(
            getMinOperations(A, B, -1, -1, dp));
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to return the minimum cost
// of converting A and B to 0
function getMinOperations(A, B, prevA, prevB, dp) {
  // If both A and B doesn't change in
  // this recursive call, then return INT_MAX
  // to save the code from going into
  // infinite loop
  if (A == prevA && B == prevB) {
    return Number.MAX_SAFE_INTEGER;
  }

  // Base Case
  if (A == 0 && B == 0) {
    return 0;
  }

  // If the answer of this recursive call
  // is already memoised
  if (dp[A][B] != -1) {
    return dp[A][B];
  }

  // If A is reduced to A/2
  let ans1 = getMinOperations(Math.floor(A / 2), B, A, B, dp);
  if (ans1 != Number.MAX_SAFE_INTEGER) {
    ans1 += 1;
  }

  // If B is reduced to B/2
  let ans2 = getMinOperations(A, Math.floor(B / 2), A, B, dp);
  if (ans2 != Number.MAX_SAFE_INTEGER) {
    ans2 += 1;
  }

  // If both A and B is reduced to sqrt(A * B)
  let ans3 = getMinOperations(
    Math.floor(Math.sqrt(A * B)),
    Math.floor(Math.sqrt(A * B)),
    A,
    B,
    dp
  );
  if (ans3 != Number.MAX_SAFE_INTEGER) {
    ans3 += 2;
  }

  // Return the minimum of the value given
  // by the above three subproblems, also
  // memoize the value while returning
  return (dp[A][B] = Math.min(ans1, Math.min(ans2, ans3)));
}

// Driver Code

let A = 53,
  B = 16;
let mx = Math.max(A, B);
let dp = new Array(mx + 1).fill(0).map(() => new Array(mx + 1).fill(-1));

document.write(getMinOperations(A, B, -1, -1, dp));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
7
```

**时间复杂度:** O(max(A，B)^2)
**辅助空间:** O(max(A，B)^2)