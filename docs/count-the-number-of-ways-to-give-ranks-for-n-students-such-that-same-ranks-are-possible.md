# 计算给 N 个学生排名的方法数量，这样相同的排名是可能的

> 原文:[https://www . geeksforgeeks . org/count-给 n 个学生排名的方法数量-这样相同的排名是可能的/](https://www.geeksforgeeks.org/count-the-number-of-ways-to-give-ranks-for-n-students-such-that-same-ranks-are-possible/)

给定一个代表学生人数的数字 **N** ，任务是根据他们的 CGPA/分数计算所有可能的排名方式，考虑到两个或更多的学生可以有相同的排名。因为答案可能很大，所以用 10 <sup>9</sup> + 7 进行模运算。

**示例:**

> **输入:** N = 1
> **输出:** 1
> **说明:**
> 给学生排名只有一种方法，不分分数高低。
> 
> **输入:** N = 2
> **输出:** 2
> **解释:**
> 通过以下两种方式可以在两个学生之间分配等级:
> 分数高的学生可以被授予第一等级，分数低的学生可以被授予第二等级，如果分数相等，两者可以被授予相同的等级。

**方法:**这个问题的思路是用[铃号](https://www.geeksforgeeks.org/bell-numbers-number-of-ways-to-partition-a-set/)。

*   钟数是对集合中可能的分区进行计数的数字。因此，第 N 个钟数是大小为 N 的集合可以划分成的非空子集的数目。
*   例如，让我们考虑 N = 3 的集合{1，2，3}。N = 3 对应的钟数是 5。这表示给定的集合可以划分为以下 5 个非空子集:

```
{{1}, {2}, {3}}
{{1, 2}, {3}}
{{1, 3}, {2}}
{{2, 3}, {1}}
{{1, 2, 3}}
```

*   显然，上面的铃号代表所有可能的等级。然而，他们不计算子集的排列。
*   因此，通过将每个子集乘以 K！，其中 K 表示相应子集的大小，我们得到所有可能的排列。
*   由于相同的子问题可以重复，我们可以将每个子问题的值存储在数据结构中，以优化复杂性。

下面是上述方法的实现:

## C++

```
// C++ program to calculate the number
// of ways to give ranks for N
// students such that same ranks
// are possible

#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;

// Initializing a table in order to
// store the bell triangle
vector<vector<int> > dp;

// Function to calculate the K-th
// bell number
int f(int n, int k)
{
    // If we have already calculated
    // the bell numbers until the
    // required N
    if (n < k)
        return 0;

    // Base case
    if (n == k)
        return 1;

    // First Bell Number
    if (k == 1)
        return 1;

    // If the value of the bell
    // triangle has already been
    // calculated
    if (dp[n][k] != -1)
        return dp[n][k];

    // Fill the defined dp table
    return dp[n][k] = ((k * f(n - 1, k)) % mod
                       + (f(n - 1, k - 1)) % mod)
                      % mod;
}

// Function to return the number
// of ways to give ranks for N
// students such that same ranks
// are possible
long operation(int n)
{
    // Resizing the dp table for the
    // given value of n
    dp.resize(n + 1, vector<int>(n + 1, -1));

    // Variables to store the answer
    // and the factorial value
    long ans = 0, fac = 1;

    // Iterating till N
    for (int k = 1; k <= n; k++) {

        // Simultaneously calculate the k!
        fac *= k;

        // Computing the K-th bell number
        // and multiplying it with K!
        ans = (ans + (fac * f(n, k)) % mod)
              % mod;
    }
    return ans;
}

// Driver code
int main()
{
    int n = 5;

    cout << operation(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the number
// of ways to give ranks for N
// students such that same ranks
// are possible
import java.util.*;

class GFG{

static int mod = (int)(1e9 + 7);

// Initializing a table in order to
// store the bell triangle
static int [][]dp;

// Function to calculate the K-th
// bell number
static int f(int n, int k)
{

    // If we have already calculated
    // the bell numbers until the
    // required N
    if (n < k)
        return 0;

    // Base case
    if (n == k)
        return 1;

    // First Bell Number
    if (k == 1)
        return 1;

    // If the value of the bell
    // triangle has already been
    // calculated
    if (dp[n][k] != -1)
        return dp[n][k];

    // Fill the defined dp table
    return dp[n][k] = ((k * f(n - 1, k)) % mod +
                       (f(n - 1, k - 1)) % mod) % mod;
}

// Function to return the number
// of ways to give ranks for N
// students such that same ranks
// are possible
static long operation(int n)
{

    // Resizing the dp table for the
    // given value of n
    dp = new int[n + 1][n + 1];
    for(int i = 0; i < n + 1; i++)
    {
       for(int j = 0; j < n + 1; j++)
       {
          dp[i][j] = -1;
       }
    }

    // Variables to store the answer
    // and the factorial value
    long ans = 0, fac = 1;

    // Iterating till N
    for(int k = 1; k <= n; k++)
    {

       // Simultaneously calculate the k!
       fac *= k;

       // Computing the K-th bell number
       // and multiplying it with K!
       ans = (ans + (fac * f(n, k)) % mod) % mod;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    System.out.print(operation(n) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to calculate the number
# of ways to give ranks for N
# students such that same ranks
# are possible
mod = 1e9 + 7

# Initializing a table in order to
# store the bell triangle
dp = [[-1 for x in range(6)]
          for y in range(6)]

# Function to calculate the K-th
# bell number
def f(n, k):

    # If we have already calculated
    # the bell numbers until the
    # required N
    if (n < k):
        return 0

    # Base case
    if (n == k):
        return 1

    # First Bell Number
    if (k == 1):
        return 1

    # If the value of the bell
    # triangle has already been
    # calculated
    if (dp[n][k] != -1):
        return dp[n][k]

    # Fill the defined dp table
    dp[n][k] = ((((k * f(n - 1, k)) % mod +
               (f(n - 1, k - 1)) % mod) % mod))
    return dp[n][k]

# Function to return the number
# of ways to give ranks for N
# students such that same ranks
# are possible
def operation(n):

    # Resizing the dp table for the
    # given value of n
    global dp

    # Variables to store the answer
    # and the factorial value
    ans = 0
    fac = 1

    # Iterating till N
    for k in range(1, n + 1):

        # Simultaneously calculate the k!
        fac *= k

        # Computing the K-th bell number
        # and multiplying it with K!
        ans = (ans + (fac * f(n, k)) % mod) % mod

    return ans

# Driver code
if __name__ == "__main__":

    n = 5

    print(int(operation(n)))

# This code is contributed by ukasp
```

## C#

```
// C# program to calculate the number
// of ways to give ranks for N
// students such that same ranks
// are possible
using System;

class GFG{

static int mod = (int)(1e9 + 7);

// Initializing a table in order to
// store the bell triangle
static int [,]dp;

// Function to calculate the K-th
// bell number
static int f(int n, int k)
{

    // If we have already calculated
    // the bell numbers until the
    // required N
    if (n < k)
        return 0;

    // Base case
    if (n == k)
        return 1;

    // First Bell Number
    if (k == 1)
        return 1;

    // If the value of the bell
    // triangle has already been
    // calculated
    if (dp[n, k] != -1)
        return dp[n, k];

    // Fill the defined dp table
    return dp[n, k] = ((k * f(n - 1, k)) % mod +
                       (f(n - 1, k - 1)) % mod) % mod;
}

// Function to return the number
// of ways to give ranks for N
// students such that same ranks
// are possible
static long operation(int n)
{

    // Resizing the dp table for the
    // given value of n
    dp = new int[n + 1, n + 1];
    for(int i = 0; i < n + 1; i++)
    {
       for(int j = 0; j < n + 1; j++)
       {
          dp[i, j] = -1;
       }
    }

    // Variables to store the answer
    // and the factorial value
    long ans = 0, fac = 1;

    // Iterating till N
    for(int k = 1; k <= n; k++)
    {

       // Simultaneously calculate the k!
       fac *= k;

       // Computing the K-th bell number
       // and multiplying it with K!
       ans = (ans + (fac * f(n, k)) % mod) % mod;
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;

    Console.Write(operation(n) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program to calculate the number
// of ways to give ranks for N
// students such that same ranks
// are possible

    var mod = parseInt( 1e9 + 7);

    // Initializing a table in order to
    // store the bell triangle
    var dp;

    // Function to calculate the K-th
    // bell number
    function f(n , k) {

        // If we have already calculated
        // the bell numbers until the
        // required N
        if (n < k)
            return 0;

        // Base case
        if (n == k)
            return 1;

        // First Bell Number
        if (k == 1)
            return 1;

        // If the value of the bell
        // triangle has already been
        // calculated
        if (dp[n][k] != -1)
            return dp[n][k];

        // Fill the defined dp table
        return dp[n][k] = ((k * f(n - 1, k)) % mod +
        (f(n - 1, k - 1)) % mod) % mod;
    }

    // Function to return the number
    // of ways to give ranks for N
    // students such that same ranks
    // are possible
    function operation(n) {

        // Resizing the dp table for the
        // given value of n
        dp = Array(n + 1).fill().map(()
        =>Array(n + 1).fill(0));
        for (i = 0; i < n + 1; i++) {
            for (j = 0; j < n + 1; j++) {
                dp[i][j] = -1;
            }
        }

        // Variables to store the answer
        // and the factorial value
        var ans = 0, fac = 1;

        // Iterating till N
        for (k = 1; k <= n; k++) {

            // Simultaneously calculate the k!
            fac *= k;

            // Computing the K-th bell number
            // and multiplying it with K!
            ans = (ans + (fac * f(n, k)) % mod) % mod;
        }
        return ans;
    }

    // Driver code

        var n = 5;

        document.write(operation(n) + "\n");

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
541
```