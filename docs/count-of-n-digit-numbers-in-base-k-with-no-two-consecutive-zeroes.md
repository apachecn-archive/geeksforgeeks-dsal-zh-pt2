# 以 K 为基数的 N 位数计数，不含两个连续的零

> 原文:[https://www . geeksforgeeks . org/n 位数 k 进制无连续两个零的计数/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-in-base-k-with-no-two-consecutive-zeroes/)

给定两个整数 **N** 和 **K** ，任务是求基数 **K** 中满足以下条件的所有整数的个数:

1.  整数必须正好是 **N** 位。
2.  不应该有前导 **0** 。
3.  不得有任何连续的数字对，使得两个数字都为 **0** 。

**例:**

> **输入:** N = 3，K = 10
> **输出:** 891
> 所有以 10 为基数的 3 位数都在【100，999】
> 范围内，这些数字中只有 100，200，300，400，…，900 无效。
> 因此有效整数为 900–9 = 891
> **输入:** N = 2，K = 10
> **输出:** 90

**简单方法:**编写一个函数 count_numbers(int k，int n，bool 标志)，该函数将返回 **N** 可能的基数为 **K** 的数字的计数，并且标志将告知先前选择的数字是否为 **0** 。对于 count_numbers(int k，int n-1，bool 标志)递归调用这个函数，使用这个标志，可以避免连续出现两个 0。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// n-digit numbers that satisfy
// the given conditions
int count_numbers(int k, int n, bool flag)
{

    // Base case
    if (n == 1) {

        // If 0 wasn't chosen previously
        if (flag) {
            return (k - 1);
        }
        else {
            return 1;
        }
    }

    // If 0 wasn't chosen previously
    if (flag)
        return (k - 1) * (count_numbers(k, n - 1, 0)
                          + count_numbers(k, n - 1, 1));
    else
        return count_numbers(k, n - 1, 1);
}

// Driver code
int main()
{
    int n = 3;
    int k = 10;
    cout << count_numbers(k, n, true);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of
// n-digit numbers that satisfy
// the given conditions
static int count_numbers(int k, int n,
                         boolean flag)
{

    // Base case
    if (n == 1)
    {

        // If 0 wasn't chosen previously
        if (flag)
        {
            return (k - 1);
        }
        else
        {
            return 1;
        }
    }

    // If 0 wasn't chosen previously
    if (flag)
        return (k - 1) * (count_numbers(k, n - 1, false) +
                          count_numbers(k, n - 1, true));
    else
        return count_numbers(k, n - 1, true);
}

// Driver code
public static void main (String[] args)
{
    int n = 3;
    int k = 10;
    System.out.println(count_numbers(k, n, true));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# n-digit numbers that satisfy
# the given conditions
def count_numbers(k, n, flag) :

    # Base case
    if (n == 1) :

        # If 0 wasn't chosen previously
        if (flag) :
            return (k - 1)
        else :
            return 1

    # If 0 wasn't chosen previously
    if (flag) :
        return (k - 1) * (count_numbers(k, n - 1, 0) +
                          count_numbers(k, n - 1, 1))
    else :
        return count_numbers(k, n - 1, 1)

# Driver code
n = 3
k = 10
print(count_numbers(k, n, True))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// n-digit numbers that satisfy
// the given conditions
static int count_numbers(int k, int n,
                         bool flag)
{

    // Base case
    if (n == 1)
    {

        // If 0 wasn't chosen previously
        if (flag)
        {
            return (k - 1);
        }
        else
        {
            return 1;
        }
    }

    // If 0 wasn't chosen previously
    if (flag)
        return (k - 1) * (count_numbers(k, n - 1, false) +
                          count_numbers(k, n - 1, true));
    else
        return count_numbers(k, n - 1, true);
}

// Driver code
public static void Main (String[] args)
{
    int n = 3;
    int k = 10;
    Console.Write(count_numbers(k, n, true));
}
}

// This code is contributed by 29AjayKuma
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of
// n-digit numbers that satisfy
// the given conditions
function count_numbers(k, n, flag)
{

    // Base case
    if (n == 1) {

        // If 0 wasn't chosen previously
        if (flag) {
            return (k - 1);
        }
        else {
            return 1;
        }
    }

    // If 0 wasn't chosen previously
    if (flag)
        return (k - 1) * (count_numbers(k, n - 1, 0)
                          + count_numbers(k, n - 1, 1));
    else
        return count_numbers(k, n - 1, 1);
}

// Driver code
    let n = 3;
    let k = 10;
    document.write(count_numbers(k, n, true));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
891
```

**高效的方法:**既然已经使用递归解决了问题，那么可以使用二维 DP 来解决这个问题 **dp[n + 1][2]** 其中 **dp[i][0]** 将给出以 **0** 结束的 **i** 位数的可能个数 **dp[i][1]** 将给出以非零结束的 **i** 位数的可能个数。
重复关系为:

> dp[i][0] = dp[i – 1][1];
> dp[i][1] = （dp[i – 1][0] + dp[i – 1][1]） * （K – 1）;

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// n-digit numbers that satisfy
// the given conditions
int count_numbers(int k, int n)
{

    // DP array to store the
    // pre-caluclated states
    int dp[n + 1][2];

    // Base cases
    dp[1][0] = 0;
    dp[1][1] = k - 1;
    for (int i = 2; i <= n; i++) {

        // i-digit numbers ending with 0
        // can be formed by concatenating
        // 0 in the end of all the (i - 1)-digit
        // number ending at a non-zero digit
        dp[i][0] = dp[i - 1][1];

        // i-digit numbers ending with non-zero
        // can be formed by concatenating any non-zero
        // digit in the end of all the (i - 1)-digit
        // number ending with any digit
        dp[i][1] = (dp[i - 1][0] + dp[i - 1][1]) * (k - 1);
    }

    // n-digit number ending with
    // and ending with non-zero
    return dp[n][0] + dp[n][1];
}

// Driver code
int main()
{
    int k = 10;
    int n = 3;
    cout << count_numbers(k, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count of
// n-digit numbers that satisfy
// the given conditions
static int count_numbers(int k, int n)
{

    // DP array to store the
    // pre-caluclated states
    int [][]dp = new int[n + 1][2];

    // Base cases
    dp[1][0] = 0;
    dp[1][1] = k - 1;
    for (int i = 2; i <= n; i++)
    {

        // i-digit numbers ending with 0
        // can be formed by concatenating
        // 0 in the end of all the (i - 1)-digit
        // number ending at a non-zero digit
        dp[i][0] = dp[i - 1][1];

        // i-digit numbers ending with non-zero
        // can be formed by concatenating any non-zero
        // digit in the end of all the (i - 1)-digit
        // number ending with any digit
        dp[i][1] = (dp[i - 1][0] +
                    dp[i - 1][1]) * (k - 1);
    }

    // n-digit number ending with
    // and ending with non-zero
    return dp[n][0] + dp[n][1];
}

// Driver code
public static void main(String[] args)
{
    int k = 10;
    int n = 3;
    System.out.println(count_numbers(k, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# n-digit numbers that satisfy
# the given conditions
def count_numbers(k, n):

    # DP array to store the
    # pre-caluclated states
    dp = [[0 for i in range(2)]
             for i in range(n + 1)]

    # Base cases
    dp[1][0] = 0
    dp[1][1] = k - 1
    for i in range(2, n + 1):

        # i-digit numbers ending with 0
        # can be formed by concatenating
        # 0 in the end of all the (i - 1)-digit
        # number ending at a non-zero digit
        dp[i][0] = dp[i - 1][1]

        # i-digit numbers ending with non-zero
        # can be formed by concatenating any non-zero
        # digit in the end of all the (i - 1)-digit
        # number ending with any digit
        dp[i][1] = (dp[i - 1][0] +
                    dp[i - 1][1]) * (k - 1)

    # n-digit number ending with
    # and ending with non-zero
    return dp[n][0] + dp[n][1]

# Driver code
k = 10
n = 3
print(count_numbers(k, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// n-digit numbers that satisfy
// the given conditions
static int count_numbers(int k, int n)
{

    // DP array to store the
    // pre-caluclated states
    int [,]dp = new int[n + 1, 2];

    // Base cases
    dp[1, 0] = 0;
    dp[1, 1] = k - 1;
    for (int i = 2; i <= n; i++)
    {

        // i-digit numbers ending with 0
        // can be formed by concatenating
        // 0 in the end of all the (i - 1)-digit
        // number ending at a non-zero digit
        dp[i, 0] = dp[i - 1, 1];

        // i-digit numbers ending with non-zero
        // can be formed by concatenating any non-zero
        // digit in the end of all the (i - 1)-digit
        // number ending with any digit
        dp[i, 1] = (dp[i - 1, 0] +
                    dp[i - 1, 1]) * (k - 1);
    }

    // n-digit number ending with
    // and ending with non-zero
    return dp[n, 0] + dp[n, 1];
}

// Driver code
public static void Main(String[] args)
{
    int k = 10;
    int n = 3;
    Console.WriteLine(count_numbers(k, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// n-digit numbers that satisfy
// the given conditions
function count_numbers(k, n)
{

    // DP array to store the
    // pre-caluclated states
    let dp = new Array(n + 1);
    for (let i = 0; i < n + 1; i++)
        dp[i] = new Array(2);

    // Base cases
    dp[1][0] = 0;
    dp[1][1] = k - 1;
    for (let i = 2; i <= n; i++) {

        // i-digit numbers ending with 0
        // can be formed by concatenating
        // 0 in the end of all the (i - 1)-digit
        // number ending at a non-zero digit
        dp[i][0] = dp[i - 1][1];

        // i-digit numbers ending with non-zero
        // can be formed by concatenating any non-zero
        // digit in the end of all the (i - 1)-digit
        // number ending with any digit
        dp[i][1] = (dp[i - 1][0] +
                    dp[i - 1][1]) * (k - 1);
    }

    // n-digit number ending with
    // and ending with non-zero
    return dp[n][0] + dp[n][1];
}

// Driver code
    let k = 10;
    let n = 3;
    document.write(count_numbers(k, n));

</script>
```

**Output:** 

```
891
```