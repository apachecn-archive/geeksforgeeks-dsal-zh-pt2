# 将 N 分为 K 个唯一的部分，使得这些部分的 gcd 最大

> 原文:[https://www . geeksforgeeks . org/divide-n-in-k-unique-parts-so-gcd-of-parts-is-maximum/](https://www.geeksforgeeks.org/divide-n-into-k-unique-parts-such-that-gcd-of-those-parts-is-maximum/)

给定一个正整数 **N** ，任务是将其划分为 **K** 个唯一的部分，使得这些部分之和等于原始数，所有部分的 **gcd** 最大。打印**最大 gcd** 如果存在这样的划分，则打印 **-1** 。

**示例:**

> **输入:** N = 6，K = 3
> **输出:** 1
> 唯一可能具有唯一
> 元素的除法是(1，2，3)和 gcd(1，2，3) = 1。
> **输入:** N = 18，K = 3
> **输出:** 3

**天真的做法:**找出 **N** 所有可能的除法，计算它们的最大 gcd。但是这种方法需要指数级的时间和空间。
**高效进场:**让 **N** 的分部为 A <sub>1</sub> ，A <sub>2</sub> ……..A <sub>K</sub>
现已知 **gcd(a，b) = gcd(a，b，a + b)** 因而， **gcd(A <sub>1</sub> ，A <sub>2</sub> …。A <sub>K</sub> ) = gcd(A <sub>1</sub> ，A <sub>2</sub> …。A <sub>K</sub> ，A <sub>1</sub> + A <sub>2</sub> …。+ A <sub>K</sub> )**
但是 **A <sub>1</sub> + A <sub>2</sub> …。+ A <sub>K</sub> = N** 因此，分部的 gcd 将是 **N** 的因素之一。
让 **a** 成为 **N** 的因子，这可以是可能的答案:
既然 **a** 是 gcd，那么所有的除法都将是 **a** 的倍数，因此，对于 **K** 唯一的 **B <sub>i</sub>** ，
T66】a * B<sub>1+a * B<sub>K</sub>= N
**a *(B<sub>1</sub>+B<sub>2</sub>……。+ B <sub>K</sub> ) = N**
既然所有的 **B <sub>i</sub>** 都是独一无二的，
**B<sub>1</sub>+B<sub>2</sub>……。+ B <sub>K</sub> ≥ 1 + 2 + 3 …..+K**
**B<sub>1</sub>+B<sub>2</sub>……。+B<sub>K</sub>≥K *(K+1)/2**
因此，互补因子大于或等于 **K * (K + 1) / 2** 的 **N** 的所有因子都可以是可能的答案之一，我们已经取了所有可能答案的最大值。</sub>

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum GCD
int maxGCD(int N, int K)
{

    // Minimum possible sum for
    // K unique positive integers
    int minSum = (K * (K + 1)) / 2;

    // It is not possible to divide
    // N into K unique parts
    if (N < minSum)
        return -1;

    // All the factors greater than sqrt(N)
    // are complementary of the factors less
    // than sqrt(N)
    int i = sqrt(N);
    int res = 1;
    while (i >= 1) {

        // If i is a factor of N
        if (N % i == 0) {
            if (i >= minSum)
                res = max(res, N / i);

            if (N / i >= minSum)
                res = max(res, i);
        }
        i--;
    }

    return res;
}

// Driver code
int main()
{
    int N = 18, K = 3;

    cout << maxGCD(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.lang.Math;

class GFG
{
    // Function to calculate maximum GCD
    static int maxGCD(int N, int K)
    {

        // Minimum possible sum for
        // K unique positive integers
        int minSum = (K * (K + 1)) / 2;

        // It is not possible to divide
        // N into K unique parts
        if (N < minSum)
            return -1;

        // All the factors greater than sqrt(N)
        // are complementary of the factors less
        // than sqrt(N)
        int i = (int) Math.sqrt(N);
        int res = 1;
        while (i >= 1)
        {

            // If i is a factor of N
            if (N % i == 0)
            {
                if (i >= minSum)
                    res = Math.max(res, N / i);

                if (N / i >= minSum)
                    res = Math.max(res, i);
            }
            i--;
        }

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 18, K = 3;

        System.out.println(maxGCD(N, K));
    }
}

// This code is contributed by ApurvaRaj
```

## 计算机编程语言

```
# Python3 implementation of the approach
from math import sqrt,ceil,floor

# Function to calculate maximum GCD
def maxGCD(N, K):

    # Minimum possible sum for
    # K unique positive integers
    minSum = (K * (K + 1)) / 2

    # It is not possible to divide
    # N into K unique parts
    if (N < minSum):
        return -1

    # All the factors greater than sqrt(N)
    # are complementary of the factors less
    # than sqrt(N)
    i = ceil(sqrt(N))
    res = 1
    while (i >= 1):

        # If i is a factor of N
        if (N % i == 0):
            if (i >= minSum):
                res = max(res, N / i)

            if (N / i >= minSum):
                res = max(res, i)

        i-=1

    return res

# Driver code

N = 18
K = 3

print(maxGCD(N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to calculate maximum GCD
    static int maxGCD(int N, int K)
    {

        // Minimum possible sum for
        // K unique positive integers
        int minSum = (K * (K + 1)) / 2;

        // It is not possible to divide
        // N into K unique parts
        if (N < minSum)
            return -1;

        // All the factors greater than sqrt(N)
        // are complementary of the factors less
        // than sqrt(N)
        int i = (int) Math.Sqrt(N);
        int res = 1;
        while (i >= 1)
        {

            // If i is a factor of N
            if (N % i == 0)
            {
                if (i >= minSum)
                    res = Math.Max(res, N / i);

                if (N / i >= minSum)
                    res = Math.Max(res, i);
            }
            i--;
        }
        return res;
    }

    // Driver code
    public static void Main()
    {
        int N = 18, K = 3;

        Console.WriteLine(maxGCD(N, K));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to calculate maximum GCD
    function maxGCD(N , K) {

        // Minimum possible sum for
        // K unique positive integers
        var minSum = (K * (K + 1)) / 2;

        // It is not possible to divide
        // N into K unique parts
        if (N < minSum)
            return -1;

        // All the factors greater than sqrt(N)
        // are complementary of the factors less
        // than sqrt(N)
        var i = parseInt( Math.sqrt(N));
        var res = 1;
        while (i >= 1) {

            // If i is a factor of N
            if (N % i == 0) {
                if (i >= minSum)
                    res = Math.max(res, N / i);

                if (N / i >= minSum)
                    res = Math.max(res, i);
            }
            i--;
        }

        return res;
    }

    // Driver code

        var N = 18, K = 3;

        document.write(maxGCD(N, K));

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N <sup>1/2</sup>

**辅助空间:** O(1)