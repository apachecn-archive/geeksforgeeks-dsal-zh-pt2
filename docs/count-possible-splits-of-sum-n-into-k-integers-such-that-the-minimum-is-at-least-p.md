# 计算和 N 到 K 个整数的可能分割，使得最小值至少为 P

> 原文:[https://www . geeksforgeeks . org/count-sum-n-in-k-integer-so-minimum-at-p/](https://www.geeksforgeeks.org/count-possible-splits-of-sum-n-into-k-integers-such-that-the-minimum-is-at-least-p/)

给定三个整数 **N** 、 **P** 和 **K** ，任务是找出将 **N** 划分为具有和 **N** 的 **K** 整数的方法总数，其中每个整数都是≥ **P** 。

**示例:**

> **输入:** K = 3，N = 8，P = 2
> **输出:** 6
> **解释:**
> 六种可能的解分别为:{2，2，4}、{2，3，3}、{2，4，2，3}、{3，3，2}、{4，2，2}
> 以上所有组合中的每个整数都≥ P(= 2)，所有组合之和为 N(=8)。
> 
> **输入:** K = 2，N = 7，P = 2
> **输出:** 4
> **解释:**
> 四种可能的解是:{4，3}、{3，4}、{5，2}、{2，5}
> 以上所有组合中的每个整数都≥ P(= 2)，所有组合的和为 N(= 7)。

**天真方法:**最简单的方法是尝试所有可能的 **K** 整数的组合，它们的和 **N** 并检查它们是否满足上述条件。有 **K** 个位置，每个位置可以放置 **N** 个整数。因此，要检查的组合总数为 **N <sup>K</sup>** 。

***时间复杂度:**O(N<sup>K</sup>)*
***辅助空间:** O(1)*

**有效方法:**要优化上述方法，思路是使用[这篇](https://www.geeksforgeeks.org/different-ways-to-represent-n-as-sum-of-k-non-zero-integers/)文章中讨论的方法，上面给定的条件可以用一个线性方程写成是:

> 求方程 X<sub>1</sub>+X<sub>2</sub>+X<sub>3</sub>+…+X<sub>K</sub>= N 其中 X <sub>i</sub> ≥ P
> 
> 假设**X<sub>I</sub>= X<sub>I</sub>–P**。
> 因此，方程简化为:
> **X<sub>1</sub>'+X<sub>2</sub>'+X<sub>3</sub>'+…+X<sub>K</sub>' = N–K * P**

根据上面的等式，给定的问题简化为[找到将**N–K * P**分割成 **K** 整数](https://www.geeksforgeeks.org/different-ways-to-represent-n-as-sum-of-k-non-zero-integers/)的方法的总数。打印上面找到的方法总数作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that finds the value of
// the Binomial Coefficient C(n, k)
int binomialCoeff(int n, int k)
{
    int C[n + 1][k + 1];
    int i, j;

    // Stores the value of Binomial
    // Coefficient in bottom up manner
    for (i = 0; i <= n; i++) {

        for (j = 0; j <= min(i, k); j++) {

            // Base Case
            if (j == 0 || j == i)
                C[i][j] = 1;

            // Find the value using
            // previously stored values
            else
                C[i][j] = C[i - 1][j - 1]
                          + C[i - 1][j];
        }
    }

    // Return the value of C(N, K)
    return C[n][k];
}

// Function that count the number of
// ways to divide N into K integers
// >= P such that their sum is N
int waysToSplitN(int k, int n, int P)
{
    // Update the value of N
    int new_N = n - k * P;

    // Find the binomial coefficient
    // recursively
    return binomialCoeff(new_N + k - 1,
                         new_N);
}

// Driver Code
int main()
{
    // Given K, N, and P
    int K = 3, N = 8, P = 2;

    cout << waysToSplitN(K, N, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function that finds the value of
// the Binomial Coefficient C(n, k)
static int binomialCoeff(int n, int k)
{
  int [][]C = new int[n + 1][k + 1];
  int i, j;

  // Stores the value of Binomial
  // Coefficient in bottom up manner
  for (i = 0; i <= n; i++)
  {
    for (j = 0; j <= Math.min(i, k); j++)
    {
      // Base Case
      if (j == 0 || j == i)
        C[i][j] = 1;

      // Find the value using
      // previously stored values
      else
        C[i][j] = C[i - 1][j - 1] +
                  C[i - 1][j];
    }
  }

  // Return the value of C(N, K)
  return C[n][k];
}

// Function that count the number of
// ways to divide N into K integers
// >= P such that their sum is N
static int waysToSplitN(int k,
                        int n, int P)
{
  // Update the value of N
  int new_N = n - k * P;

  // Find the binomial coefficient
  // recursively
  return binomialCoeff(new_N + k - 1,
                       new_N);
}

// Driver Code
public static void main(String[] args)
{
  // Given K, N, and P
  int K = 3, N = 8, P = 2;

  System.out.print(waysToSplitN(K, N, P));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the value of
# the Binomial Coefficient C(n, k)
def binomialCoeff(n, k):

    C = [[0 for x in range(k + 1)]
            for y in range(n + 1)]

    # Stores the value of Binomial
    # Coefficient in bottom up manner
    for i in range(n + 1):
        for j in range(min(i, k) + 1):

            # Base Case
            if(j == 0 or j == i):
                C[i][j] = 1

            # Find the value using
            # previously stored values
            else:
                C[i][j] = (C[i - 1][j - 1] +
                           C[i - 1][j])

    # Return the value of C(N, K)
    return C[n][k]

# Function that count the number of
# ways to divide N into K integers
# >= P such that their sum is N
def waysToSplitN(k, n, P):

    # Update the value of N
    new_N = n - k * P

    # Find the binomial coefficient
    # recursively
    return binomialCoeff(new_N + k - 1,
                         new_N)

# Driver Code

# Given K, N, and P
K = 3
N = 8
P = 2

print(waysToSplitN(K, N, P))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that finds the value of
// the Binomial Coefficient C(n, k)
static int binomialCoeff(int n, int k)
{
    int [,] C = new int[n + 1, k + 1];
    int i, j;

    // Stores the value of Binomial
    // Coefficient in bottom up manner
    for(i = 0; i <= n; i++)
    {
        for(j = 0; j <= Math.Min(i, k); j++)
        {

            // Base Case
            if (j == 0 || j == i)
                C[i, j] = 1;

            // Find the value using
            // previously stored values
            else
                C[i, j] = C[i - 1, j - 1] +
                          C[i - 1, j];
        }
    }

    // Return the value of C(N, K)
    return C[n, k];
}

// Function that count the number of
// ways to divide N into K integers
// >= P such that their sum is N
static int waysToSplitN(int k, int n,
                        int P)
{

    // Update the value of N
    int new_N = n - k * P;

    // Find the binomial coefficient
    // recursively
    return binomialCoeff(new_N + k - 1,
                         new_N);
}

// Driver Code
public static void Main()
{

    // Given K, N, and P
    int K = 3, N = 8, P = 2;

    Console.Write(waysToSplitN(K, N, P));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function that finds the value of
// the Binomial Coefficient C(n, k)
function binomialCoeff(n, k)
{
      let C = new Array(n + 1);

    // Loop to create 2D array using 1D array
    for (let i = 0; i < C.length; i++) {
        C[i] = new Array(2);
    }

  let i, j;

  // Stores the value of Binomial
  // Coefficient in bottom up manner
  for (i = 0; i <= n; i++)
  {
    for (j = 0; j <= Math.min(i, k); j++)
    {
      // Base Case
      if (j == 0 || j == i)
        C[i][j] = 1;

      // Find the value using
      // previously stored values
      else
        C[i][j] = C[i - 1][j - 1] +
                  C[i - 1][j];
    }
  }

  // Return the value of C(N, K)
  return C[n][k];
}

// Function that count the number of
// ways to divide N into K integers
// >= P such that their sum is N
function waysToSplitN(k, n, P)
{
  // Update the value of N
  let new_N = n - k * P;

  // Find the binomial coefficient
  // recursively
  return binomialCoeff(new_N + k - 1,
                       new_N);
}

// Driver Code

     // Given K, N, and P
  let K = 3, N = 8, P = 2;

  document.write(waysToSplitN(K, N, P));

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*