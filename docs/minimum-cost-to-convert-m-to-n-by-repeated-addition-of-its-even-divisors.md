# 通过重复添加偶数因子将 M 转换为 N 的最小成本

> 原文:[https://www . geeksforgeeks . org/通过重复添加偶数因子将 m 转换为 n 的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-convert-m-to-n-by-repeated-addition-of-its-even-divisors/)

给定两个整数 **M** 和 **N** ，任务是通过重复相加 **M** 当前值的偶数因子(M 除外)找到将 **M** 转换为 **N** 的最小成本。

> 把 M 的当前值，比如 d，加一个偶数除数的成本等于 M / d

如果无法将 **M** 转换为 **N** ，则打印**-1】**。

**示例:**

> **输入:** M = 6，N = 24
> T3】输出: 10
> **解释:**
> 步 1: M = 6 + 2 = 8，成本= (6 / 2) = 3
> 步 2: M = 8 + 4 = 12，成本= 3 + (8 / 2) = 5
> 步 3: M = 12 + 6 = 18， 成本= 5 + (12/ 6) = 7
> 第四步:M = 18 + 6 = 24，成本= 7 + (18 / 6) = 10
> 因此，将 M 转换为 N 的最小成本等于 10。
> 
> **输入:** M = 9，N = 17
> **输出:** -1
> **说明:**
> 由于没有 9 的偶数除数，因此，转换是不可能的。

**天真法**:最简单的方法是迭代给定数的所有可能的偶数除数 **M** 递归计算最小代价将 **M** 改为 **N** 。形成的递归关系由下式给出:

> min_cost = Math.min(min_cost，m / i + minSteps(m + i，n))

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

int inf = 1000000008;

// Function to find the value of
// minimum steps to convert m to n
int minSteps(int m, int n)
{

    // Base Case
    if (n == m)
        return 0;

    // If n exceeds m
    if (m > n)
        return inf;

    int min_cost = inf;

    // Iterate through all possible
    // even divisors of m
    for(int i = 2; i < m; i += 2)
    {

        // If m is divisible by i,
        // then find the minimum cost
        if (m % i == 0)
        {

            // Add the cost to convert
            // m to m+i and recursively
            // call next state
            min_cost = min(min_cost,
                           m / i +
                           minSteps(m + i, n));
        }
    }

    // Return min_cost
    return min_cost;
}

// Driver code
int main()
{
    int M = 6;
    int N = 24;

    // Function call
    int minimum_cost = minSteps(M, N);

    // If conversion is
    // not possible
    if (minimum_cost == inf)
        minimum_cost = -1;

    // Print the cost
    cout << minimum_cost;

    return 0;
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

public class GFG {

    static int inf = 1000000008;

    // Function to find the value of
    // minimum steps to convert m to n
    public static int
    minSteps(int m, int n)
    {
        // Base Case
        if (n == m)
            return 0;

        // If n exceeds m
        if (m > n)
            return inf;

        int min_cost = inf;

        // Iterate through all possible
        // even divisors of m
        for (int i = 2; i < m; i += 2) {

            // If m is divisible by i,
            // then find the minimum cost
            if (m % i == 0) {

                // Add the cost to convert
                // m to m+i and recursively
                // call next state
                min_cost
                    = Math.min(
                        min_cost,
                        m / i
                            + minSteps(m + i, n));
            }
        }

        // Return min_cost
        return min_cost;
    }

    // Driver Code
    public static void
    main(String args[])
    {
        int M = 6;
        int N = 24;

        // Function Call
        int minimum_cost
            = minSteps(M, N);

        // If conversion is
        // not possible
        minimum_cost
            = minimum_cost
                      == inf
                  ? -1
                  : minimum_cost;

        // Print the cost
        System.out.println(minimum_cost);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
inf = 1000000008

# Function to find the value of
# minimum steps to convert m to n
def minSteps(m, n):

    # Base Case
    if (n == m):
        return 0

    # If n exceeds m
    if (m > n):
        return inf

    min_cost = inf

    # Iterate through all possible
    # even divisors of m
    for i in range(2, m, 2):

        # If m is divisible by i,
        # then find the minimum cost
        if (m % i == 0):

            # Add the cost to convert
            # m to m+i and recursively
            # call next state
            min_cost = min(min_cost, m / i +
                            minSteps(m + i, n))

    # Return min_cost
    return min_cost

# Driver Code
if __name__ == '__main__':

    M = 6
    N = 24

    # Function call
    minimum_cost = minSteps(M, N)

    # If conversion is
    # not possible
    if minimum_cost == inf:
        minimum_cost = -1

    # Print the cost
    print(minimum_cost)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

  static int inf = 1000000008;

  // Function to find the value of
  // minimum steps to convert m to n
  public static int minSteps(int m,
                             int n)
  {
    // Base Case
    if (n == m)
      return 0;

    // If n exceeds m
    if (m > n)
      return inf;

    int min_cost = inf;

    // Iterate through all possible
    // even divisors of m
    for (int i = 2; i < m; i += 2)
    {
      // If m is divisible by i,
      // then find the minimum cost
      if (m % i == 0)
      {
        // Add the cost to convert
        // m to m+i and recursively
        // call next state
        min_cost = Math.Min(min_cost, m / i +
                            minSteps(m + i, n));
      }
    }

    // Return min_cost
    return min_cost;
  }

  // Driver Code
  public static void Main(String []args)
  {
    int M = 6;
    int N = 24;

    // Function Call
    int minimum_cost = minSteps(M, N);

    // If conversion is
    // not possible
    minimum_cost = minimum_cost == inf ? -1 :
                   minimum_cost;

    // Print the cost
    Console.WriteLine(minimum_cost);
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

let inf = 1000000008;

    // Function to find the value of
    // minimum steps to convert m to n
    function
    minSteps(m, n)
    {
        // Base Case
        if (n == m)
            return 0;

        // If n exceeds m
        if (m > n)
            return inf;

        let min_cost = inf;

        // Iterate through all possible
        // even divisors of m
        for (let i = 2; i < m; i += 2) {

            // If m is divisible by i,
            // then find the minimum cost
            if (m % i == 0) {

                // Add the cost to convert
                // m to m+i and recursively
                // call next state
                min_cost
                    = Math.min(
                        min_cost,
                        m / i
                            + minSteps(m + i, n));
            }
        }

        // Return min_cost
        return min_cost;
    }

// Driver Code

    let M = 6;
        let N = 24;

        // Function Call
        let minimum_cost
            = minSteps(M, N);

        // If conversion is
        // not possible
        minimum_cost
            = minimum_cost
                      == inf
                  ? -1
                  : minimum_cost;

        // Print the cost
        document.write(minimum_cost);

</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)对上述实现进行优化。而不是一次又一次地计算状态，将其存储在数组 **dp[]** 中，并在需要时使用。

> 对于 m 小于 m 的所有偶数因子，dp(m) = min(dp(m)，(m/i) + dp(m+i))

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

int inf = 1000000008;

// Utility function to calculate the
// minimum cost
int minStepsUtil(int m, int n, int dp[])
{

    // Positive base case
    if (n == m)
        return 0;

    // Negative base case
    if (m > n)
        return inf;

    // If current state is already
    // computed then return the
    // current state value
    if (dp[m] != inf)
        return dp[m];

    int min_cost = inf;

    // Iterate through all possible
    // even divisors
    for(int i = 2; i < m; i += 2)
    {
        if (m % i == 0)
        {
            min_cost = min(min_cost,
                           m / i +
                           minStepsUtil(m + i,
                                        n, dp));
        }
    }

    // Store the precomputed answer
    return dp[m] = min_cost;
}

void minSteps(int M, int N)
{

    // Initialise the dp array
    // with infinity
    int dp[N + 5];
    for(int i = 0; i < N + 5; i++)
    {
        dp[i] = inf;
    }

    // Function call
    int minimum_cost = minStepsUtil(M, N, dp);

    if (minimum_cost == inf)
        minimum_cost = -1;

    // Print the minimum cost
    cout << minimum_cost;
}

// Driver code
int main()
{
    int M = 6;
    int N = 24;

    // Function call
    minSteps(M, N);
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

public class GFG {

    static int inf = 1000000008;

    // Utility function to calculate the
    // minimum cost
    public static int
    minStepsUtil(int m, int n, int dp[])
    {
        // Positive base case
        if (n == m)
            return 0;

        // Negative base case
        if (m > n)
            return inf;

        // If current state is already
        // computed then return the
        // current state value
        if (dp[m] != inf)
            return dp[m];

        int min_cost = inf;

        // Iterate through all possible
        // even divisors
        for (int i = 2; i < m; i += 2) {
            if (m % i == 0) {
                min_cost = Math.min(
                    min_cost,
                    m / i
                        + minStepsUtil(m + i, n, dp));
            }
        }

        // Store the precomputed answer
        return dp[m] = min_cost;
    }

    public static void
    minSteps(int M, int N)
    {

        // Initialise the dp array
        // with infinity
        int dp[] = new int[N + 5];

        Arrays.fill(dp, inf);

        // Function Call
        int minimum_cost
            = minStepsUtil(M, N, dp);

        minimum_cost
            = minimum_cost
                      == inf
                  ? -1
                  : minimum_cost;

        // Print the minimum cost
        System.out.println(minimum_cost);
    }

    // Driver code
    public static void main(String args[])
    {
        int M = 6;
        int N = 24;

        // Function Call
        minSteps(M, N);
    }
}
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static int inf = 1000000008;

// Utility function to calculate the
// minimum cost
public static int minStepsUtil(int m,
                               int n, int []dp)
{
    // Positive base case
    if (n == m)
        return 0;

    // Negative base case
    if (m > n)
        return inf;

    // If current state is already
    // computed then return the
    // current state value
    if (dp[m] != inf)
        return dp[m];

    int min_cost = inf;

    // Iterate through all possible
    // even divisors
    for (int i = 2; i < m; i += 2)
    {
        if (m % i == 0)
        {
            min_cost = Math.Min(min_cost, m / i +
                                minStepsUtil(m + i,
                                             n, dp));
        }
    }

    // Store the precomputed answer
    return dp[m] = min_cost;
    }

    public static void minSteps(int M,
                                int N)
    {
        // Initialise the dp array
        // with infinity
        int []dp = new int[N + 5];
        for(int i = 0; i < dp.GetLength(0);
                i++)
            dp[i] = inf;

        // Function Call
        int minimum_cost = minStepsUtil(M, N, dp);

        minimum_cost = minimum_cost ==
                       inf ? -1 : minimum_cost;

        // Print the minimum cost
        Console.WriteLine(minimum_cost);
    }

    // Driver code
    public static void Main(String []args)
    {
        int M = 6;
        int N = 24;

        // Function Call
        minSteps(M, N);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach
inf = 1000000008;

# Utility function to calculate the
# minimum cost
def minStepsUtil(m, n, dp):
    # Positive base case
    if (n == m):
        return 0;

    # Negative base case
    if (m > n):
        return inf;

    # If current state is already
    # computed then return the
    # current state value
    if (dp[m] != inf):
        return dp[m];

    min_cost = inf;

    # Iterate through all possible
    # even divisors
    for i in range(2,m,2):
        if (m % i == 0):
            min_cost = min(min_cost, m // i + minStepsUtil(m + i, n, dp));

    # Store the precomputed answer
    dp[m] = min_cost
    return dp[m];

def minSteps(M, N):
    # Initialise the dp array
    # with infinity
    dp = [inf]*(N + 5);

    # Function Call
    minimum_cost = minStepsUtil(M, N, dp);

    minimum_cost = -1 if minimum_cost == inf else minimum_cost;

    # Print the minimum cost
    print(minimum_cost);

# Driver code
if __name__ == '__main__':
    M = 6;
    N = 24;

    # Function Call
    minSteps(M, N);

# This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach
var inf = 1000000008;

// Utility function to calculate the
// minimum cost
function minStepsUtil(m, n, dp)
{

    // Positive base case
    if (n == m)
        return 0;

    // Negative base case
    if (m > n)
        return inf;

    // If current state is already
    // computed then return the
    // current state value
    if (dp[m] != inf)
        return dp[m];

    var min_cost = inf;

    // Iterate through all possible
    // even divisors
    for(var i = 2; i < m; i += 2)
    {
        if (m % i == 0)
        {
            min_cost = Math.min(min_cost,
                           m / i +
                           minStepsUtil(m + i,
                                        n, dp));
        }
    }

    // Store the precomputed answer
    return dp[m] = min_cost;
}

function minSteps(M,  N)
{

    // Initialise the dp array
    // with infinity
    var dp = Array(N+5);
    for(var i = 0; i < N + 5; i++)
    {
        dp[i] = inf;
    }

    // Function call
    var minimum_cost = minStepsUtil(M, N, dp);

    if (minimum_cost == inf)
        minimum_cost = -1;

    // Print the minimum cost
    document.write( minimum_cost);
}

// Driver code
var M = 6;
var N = 24;

// Function call
minSteps(M, N);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(Nlog(M))*
***辅助空间:** O(N)*