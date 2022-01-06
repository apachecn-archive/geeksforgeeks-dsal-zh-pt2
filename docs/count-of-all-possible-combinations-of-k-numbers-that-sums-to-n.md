# 对所有可能的 K 个数组合进行计数，总计为 N

> 原文:[https://www . geesforgeks . org/k-numbers-sum-to-n 的所有可能组合的计数/](https://www.geeksforgeeks.org/count-of-all-possible-combinations-of-k-numbers-that-sums-to-n/)

给定一个数 **N** ，任务是统计从 **1** 到 **N** 的 **K** 数的组合，其和等于 **N** ，允许重复。

**示例:**

> **输入:** N = 7，K = 3
> **输出:** 15
> **说明:**导致 N = 7 之和的组合为:{1，1，5}、{1，5，1}、{5，1，1}、{2，1，4}、{1，2，4}，{1，4，2}、{2，4，1}、{4，1，2}、{4，1，2}、{ 4，2，1}，{3，1，3}
> 
> **输入:** N = 5，K = 5
> **输出:** 1
> **说明:** {1，1，1，1，1}是唯一的组合。

**天真方法:**这个问题可以通过使用[递归](https://www.geeksforgeeks.org/recursion/)然后[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)的结果来提高时间复杂度来解决。要解决此问题，请遵循以下步骤:

1.  创建一个函数，比如 **countWaysUtil** ，它将接受四个参数，分别是 **N** 、 **K** 、 **sum** 和 **dp** 。这里 **N** 是要求 **K** 元素拥有的总和， **K** 是消耗的元素数量， **sum** 是到现在累计的总和， **dp** 是对结果进行加权的矩阵。该功能将给出获取 **K** 数字中**和**的方法数。
2.  现在最初用参数 **N** 、 **K** 、 **sum=0** 和 **dp** 来调用 **countWaysUtil** 作为一个矩阵，其中填充了所有的 **-1** 。
3.  在每次递归调用中:
    *   检查基本案例:
        *   如果**和**等于 **N** 和 **K** 变为 0，则返回 1。
        *   如果**和**超过 **N** 和 **K** 仍然大于 0，则返回 0。
    *   现在，运行从 1 到 **N** 的 for 循环，检查每个结果的结果。
    *   将变量 **cnt** 中的所有结果相加，并在记忆后返回 **cnt** 。
4.  根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count
// all the possible combinations
// of K numbers having sum equals to N
int countWaysUtil(int N, int K, int sum,
                  vector<vector<int> >& dp)
{

    // Base Cases
    if (sum == N and K == 0) {
        return 1;
    }

    if (sum >= N and K >= 0) {
        return 0;
    }

    if (K < 0) {
        return 0;
    }

    // If the result is already memoised
    if (dp[sum][K] != -1) {
        return dp[sum][K];
    }

    // Recursive Calls
    int cnt = 0;
    for (int i = 1; i <= N; i++) {
        cnt += countWaysUtil(
            N, K - 1,
            sum + i, dp);
    }

    // Returning answer
    return dp[sum][K] = cnt;
}

void countWays(int N, int K)
{
    vector<vector<int> > dp(N + 1,
                            vector<int>(
                                K + 1, -1));
    cout << countWaysUtil(N, K, 0, dp);
}

// Driver Code
int main()
{
    int N = 7, K = 3;
    countWays(N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
class GFG {

    // Function to count
    // all the possible combinations
    // of K numbers having sum equals to N
    static int countWaysUtil(int N, int K, int sum,
                             int[][] dp)
    {

        // Base Cases
        if (sum == N && K == 0) {
            return 1;
        }

        if (sum >= N && K >= 0) {
            return 0;
        }

        if (K < 0) {
            return 0;
        }

        // If the result is already memoised
        if (dp[sum][K] != -1) {
            return dp[sum][K];
        }

        // Recursive Calls
        int cnt = 0;
        for (int i = 1; i <= N; i++) {
            cnt += countWaysUtil(N, K - 1, sum + i, dp);
        }

        // Returning answer
        return dp[sum][K] = cnt;
    }

    static void countWays(int N, int K)
    {
        int[][] dp = new int[N + 1][K + 1];
        for (int i = 0; i < N + 1; i++) {
            for (int j = 0; j < K + 1; j++) {

                dp[i][j] = -1;
            }
        }
        System.out.print(countWaysUtil(N, K, 0, dp));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 7, K = 3;
        countWays(N, K);
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count all the possible
# combinations of K numbers having
# sum equals to N
def countWaysUtil(N, K, sum, dp):

    # Base Cases
    if (sum == N and K == 0):
        return 1

    if (sum >= N and K >= 0):
        return 0

    if (K < 0):
        return 0

    # If the result is already memoised
    if (dp[sum][K] != -1):
        return dp[sum][K]

    # Recursive Calls
    cnt = 0
    for i in range(1, N+1):
        cnt += countWaysUtil(N, K - 1, sum + i, dp)

    # Returning answer
    dp[sum][K] = cnt
    return dp[sum][K]

def countWays(N, K):

    dp = [[-1 for _ in range(K + 1)]
              for _ in range(N + 1)]
    print(countWaysUtil(N, K, 0, dp))

# Driver Code
if __name__ == "__main__":

    N = 7
    K = 3

    countWays(N, K)

# This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
class GFG
{

// Function to count
// all the possible combinations
// of K numbers having sum equals to N
static int countWaysUtil(int N, int K, int sum,
                  int [,]dp)
{

    // Base Cases
    if (sum == N && K == 0) {
        return 1;
    }

    if (sum >= N && K >= 0) {
        return 0;
    }

    if (K < 0) {
        return 0;
    }

    // If the result is already memoised
    if (dp[sum, K] != -1) {
        return dp[sum, K];
    }

    // Recursive Calls
    int cnt = 0;
    for (int i = 1; i <= N; i++) {
        cnt += countWaysUtil(
            N, K - 1,
            sum + i, dp);
    }

    // Returning answer
    return dp[sum, K] = cnt;
}

static void countWays(int N, int K)
{
    int [,]dp = new int[N + 1, K + 1];
    for(int i = 0; i < N + 1; i++) {
        for(int j = 0; j < K + 1; j++) {

            dp[i, j] = -1;
        }
    }
    Console.Write(countWaysUtil(N, K, 0, dp));
}

// Driver Code
public static void Main()
{
    int N = 7, K = 3;
    countWays(N, K);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count
// all the possible combinations
// of K numbers having sum equals to N
function countWaysUtil(N, K, sum, dp) {

    // Base Cases
    if (sum == N && K == 0) {
        return 1;
    }

    if (sum >= N && K >= 0) {
        return 0;
    }

    if (K < 0) {
        return 0;
    }

    // If the result is already memoised
    if (dp[sum][K] != -1) {
        return dp[sum][K];
    }

    // Recursive Calls
    let cnt = 0;
    for (let i = 1; i <= N; i++) {
        cnt += countWaysUtil(
            N, K - 1,
            sum + i, dp);
    }

    // Returning answer
    return dp[sum][K] = cnt;
}

function countWays(N, K) {
    let dp = new Array(N + 1).fill(0).map(() => new Array(K + 1).fill(-1))
    document.write(countWaysUtil(N, K, 0, dp));
}

// Driver Code
let N = 7, K = 3;
countWays(N, K);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
15
```

**时间复杂度:**O(N * K)
T3】空间复杂度: O(N*K)

**有效途径:**这个问题也可以用[二项式定理](https://www.geeksforgeeks.org/binomial-theorem/)来解决。由于所需的和是具有 K 个元素的 N，因此假设 K 个数字是:

> **a1 + a2 + a3 + a4 + ……..+ aK = N**
> 根据二项式定理中划分的标准原理，上述方程有一个解是**<sup>N+K-1</sup>C<sub>K-1</sub>T8】，其中 **K > =0** 。
> 但在我们的情况下， **K > =1** 。
> 因此 **N** 应替换为 **N-K** ，等式变为**<sup>N-1</sup>C<sub>K-1</sub>****

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Method to find factorial of given number
int factorial(int n)
{
    if (n == 0)
        return 1;

    return n * factorial(n - 1);
}

// Function to count all the possible
// combinations of K numbers having
// sum equals to N
int totalWays(int N, int K)
{

    // If N<K
    if (N < K)
        return 0;

    // Storing numerator
    int  n1 = factorial(N - 1);

    // Storing denominator
    int n2 = factorial(K - 1) * factorial(N - K);
    int ans = (n1 / n2);

    // Returning answer
    return ans;
}

// Driver code
int main()
{
    int N = 7;
    int K = 3;
    int ans = totalWays(N, K);

    cout << ans;

    return 0;
}

// This code is contributed by Shubham Singh
```

## C

```
// C Program for the above approach
#include <stdio.h>

 // method to find factorial of given number
 int factorial(int n)
 {
    if (n == 0)
      return 1;

    return n*factorial(n - 1);
 }

 // Function to count
 // all the possible combinations
 // of K numbers having sum equals to N
 int totalWays(int N, int K) {

    // If N<K
    if (N < K)
      return 0;

    // Storing numerator
    int  n1 = factorial(N - 1);

    // Storing denominator
    int n2 = factorial(K - 1)*factorial(N - K);
    int ans = (n1/n2);

    // Returning answer
    return ans;
 }

  // Driver method
  int main()
  {

    int N = 7;
    int K = 3;
    int ans = totalWays(N, K);
    printf("%d",ans);
    return 0;
  }

// This code is contributed by Shubham Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
class Solution{

  // method to find factorial of given number
  static int factorial(int n)
  {
    if (n == 0)
      return 1;

    return n*factorial(n - 1);
  }

  // Function to count
  // all the possible combinations
  // of K numbers having sum equals to N
  static  int totalWays(int N, int K) {

    // If N<K
    if (N < K)
      return 0;

    // Storing numerator
    int  n1 = factorial(N - 1);

    // Storing denominator
    int n2 = factorial(K - 1)*factorial(N - K);
    int ans = (n1/n2);

    // Returning answer
    return ans;
  }

  // Driver method
  public static void main(String[] args)
  {

    int N = 7;
    int K = 3;
    int ans = totalWays(N, K);
    System.out.println(ans);
  }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python Program for the above approach

from math import factorial

class Solution:

    # Function to count
    # all the possible combinations
    # of K numbers having sum equals to N
    def totalWays(self, N, K):

        # If N<K
        if (N < K):
            return 0

        # Storing numerator
        n1 = factorial(N-1)

        # Storing denominator
        n2 = factorial(K-1)*factorial(N-K)

        ans = (n1//n2)

        # Returning answer
        return ans

# Driver Code
if __name__ == '__main__':
    N = 7
    K = 3
    ob = Solution()
    ans = ob.totalWays(N, K)
    print(ans)
```

## C#

```
// C# Program for the above approach
using System;
public class Solution {

  // method to find factorial of given number
  static int factorial(int n) {
    if (n == 0)
      return 1;

    return n * factorial(n - 1);
  }

  // Function to count
  // all the possible combinations
  // of K numbers having sum equals to N
  static int totalWays(int N, int K) {

    // If N<K
    if (N < K)
      return 0;

    // Storing numerator
    int n1 = factorial(N - 1);

    // Storing denominator
    int n2 = factorial(K - 1) * factorial(N - K);
    int ans = (n1 / n2);

    // Returning answer
    return ans;
  }

  // Driver method
  public static void Main(String[] args) {

    int N = 7;
    int K = 3;
    int ans = totalWays(N, K);
    Console.WriteLine(ans);
  }
}

// This code is contributed by umadevi9616
```

**Output**

```
15
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)