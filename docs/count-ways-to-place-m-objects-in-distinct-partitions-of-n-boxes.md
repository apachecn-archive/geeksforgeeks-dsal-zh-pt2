# 计算将 M 个对象放置在 N 个盒子的不同分区中的方法

> 原文:[https://www . geeksforgeeks . org/count-way-to-place-m-objects-in-distinct-partition-of-n-box/](https://www.geeksforgeeks.org/count-ways-to-place-m-objects-in-distinct-partitions-of-n-boxes/)

给定两个正整数 **N** 和 **M** ，任务是找出将 **M** 不同对象放置在偶数索引框的分区中的方法数，偶数索引框依次编号为**【1，N】**，每个 **i** <sup>第</sup>个框都有 **i** 个不同分区。由于答案可能很大，打印[模 1000000007](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** N = 2，M = 1
> T3】输出:2
> T6】说明:自，N = 2。只有一个偶数索引框，即框 2，有 2 个分区。因此，放置对象有两个位置。因此，路数= 2。
> 
> **输入:** N = 5，M = 2
> T3】输出: 32

**方法:**按照以下步骤解决问题:

*   **M** 对象将被放置在偶数索引框的分区中。让 **S** 成为 **N 个盒子中偶数索引盒子的分区总数。**
*   分区数等于所有偶数的和直到 **N.** 因此，和， **S = X * (X + 1)，**其中 **X =楼层(N / 2)。**
*   每个物体可以占据 **S** 不同位置中的一个。因此，**方式总数= S*S*S..(M 次)=**T4 S<sup>M</sup>。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above Approach

#include <bits/stdc++.h>
using namespace std;

const int MOD = 1000000007;

// Iterative Function to calculate
// (x^y)%p in O(log y)
int power(int x, unsigned int y, int p = MOD)
{
    // Initialize Result
    int res = 1;

    // Update x if x >= MOD
    // to avoid multiplication overflow
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * 1LL * x) % p;

        // multiplied by long long int,
        // to avoid overflow
        // because res * x <= 1e18, which is
        // out of bounds for integer

        // n must be even now

        // y = y/2
        y = y >> 1;

        // Change x to x^2
        x = (x * 1LL * x) % p;
    }
    return res;
}

// Utility function to find
// the Total Number of Ways
void totalWays(int N, int M)
{
    // Number of Even Indexed
    // Boxes
    int X = N / 2;

    // Number of partitions of
    // Even Indexed Boxes
    int S = (X * 1LL * (X + 1)) % MOD;

    // Number of ways to distribute
    // objects
    cout << power(S, M, MOD) << "\n";
}

// Driver Code
int main()
{
    // N = number of boxes
    // M = number of distinct objects
    int N = 5, M = 2;

    // Function call to
    // get Total Number of Ways
    totalWays(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above Approach
import java.io.*;
class GFG
{

public static int MOD = 1000000007;

// Iterative Function to calculate
// (x^y)%p in O(log y)
static int power(int x, int y, int p)
{   
      p = MOD;

    // Initialize Result
    int res = 1;

    // Update x if x >= MOD
    // to avoid multiplication overflow
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // multiplied by long long int,
        // to avoid overflow
        // because res * x <= 1e18, which is
        // out of bounds for integer

        // n must be even now

        // y = y/2
        y = y >> 1;

        // Change x to x^2
        x = (x * x) % p;
    }
    return res;
}

// Utility function to find
// the Total Number of Ways
static void totalWays(int N, int M)
{

    // Number of Even Indexed
    // Boxes
    int X = N / 2;

    // Number of partitions of
    // Even Indexed Boxes
    int S = (X * (X + 1)) % MOD;

    // Number of ways to distribute
    // objects
    System.out.println(power(S, M, MOD));
}

// Driver Code
public static void main (String[] args)
{

      // N = number of boxes
    // M = number of distinct objects
    int N = 5, M = 2;

    // Function call to
    // get Total Number of Ways
    totalWays(N, M);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 implementation of the
# above Approach
MOD = 1000000007

# Iterative Function to calculate
# (x^y)%p in O(log y)
def power(x, y, p = MOD):

    # Initialize Result
    res = 1

    # Update x if x >= MOD
    # to avoid multiplication overflow
    x = x % p
    while (y > 0):

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res * x) % p

        # multiplied by long long int,
        # to avoid overflow
        # because res * x <= 1e18, which is
        # out of bounds for integer

        # n must be even now

        # y = y/2
        y = y >> 1

        # Change x to x^2
        x = (x * x) % p
    return res

# Utility function to find
# the Total Number of Ways
def totalWays(N, M):

    # Number of Even Indexed
    # Boxes
    X = N // 2

    # Number of partitions of
    # Even Indexed Boxes
    S = (X * (X + 1)) % MOD

    # Number of ways to distribute
    # objects
    print (power(S, M, MOD))

# Driver Code
if __name__ == '__main__':

    # N = number of boxes
    # M = number of distinct objects
    N, M = 5, 2

    # Function call to
    # get Total Number of Ways
    totalWays(N, M)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# implementation of the
// above Approach

using System;

public class GFG{

public static int MOD = 1000000007;

// Iterative Function to calculate
// (x^y)%p in O(log y)
static int power(int x, int y, int p)
{

      p = MOD;

    // Initialize Result
    int res = 1;

    // Update x if x >= MOD
    // to avoid multiplication overflow
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // multiplied by long long int,
        // to avoid overflow
        // because res * x <= 1e18, which is
        // out of bounds for integer

        // n must be even now

        // y = y/2
        y = y >> 1;

        // Change x to x^2
        x = (x * x) % p;
    }
    return res;
}

// Utility function to find
// the Total Number of Ways
static void totalWays(int N, int M)
{

    // Number of Even Indexed
    // Boxes
    int X = N / 2;

    // Number of partitions of
    // Even Indexed Boxes
    int S = (X * (X + 1)) % MOD;

    // Number of ways to distribute
    // objects
    Console.WriteLine(power(S, M, MOD));
}

// Driver Code
static public void Main ()
{

    // N = number of boxes
    // M = number of distinct objects
    int N = 5, M = 2;

    // Function call to
    // get Total Number of Ways
    totalWays(N, M);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above Approach

var MOD = 1000000007;

// Iterative Function to calculate
// (x^y)%p in O(log y)
function power(x, y, p = MOD)
{
    // Initialize Result
    var res = 1;

    // Update x if x >= MOD
    // to avoid multiplication overflow
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * 1 * x) % p;

        // multiplied by long long int,
        // to avoid overflow
        // because res * x <= 1e18, which is
        // out of bounds for integer

        // n must be even now

        // y = y/2
        y = y >> 1;

        // Change x to x^2
        x = (x * 1 * x) % p;
    }
    return res;
}

// Utility function to find
// the Total Number of Ways
function totalWays(N, M)
{
    // Number of Even Indexed
    // Boxes
    var X = parseInt(N / 2);

    // Number of partitions of
    // Even Indexed Boxes
    var S = (X * 1 * (X + 1)) % MOD;

    // Number of ways to distribute
    // objects
    document.write( power(S, M, MOD) << "<br>");
}

// Driver Code
// N = number of boxes
// M = number of distinct objects
var N = 5, M = 2;
// Function call to
// get Total Number of Ways
totalWays(N, M);

</script>
```

**Output:** 

```
36
```

***时间复杂度:** O(log M)*
***辅助空间:** O(1)*