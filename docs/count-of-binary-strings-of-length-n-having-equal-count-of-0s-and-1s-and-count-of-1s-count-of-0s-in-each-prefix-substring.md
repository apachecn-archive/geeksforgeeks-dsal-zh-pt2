# 长度为 N 的二进制串的计数，每个前缀子串中 0 和 1 的计数相等，1 的计数≥0 的计数

> 原文:[https://www . geesforgeks . org/长度为 n 的二进制字符串的计数在每个前缀子字符串中具有相等的 0s 和 1s 计数以及 0s 计数/](https://www.geeksforgeeks.org/count-of-binary-strings-of-length-n-having-equal-count-of-0s-and-1s-and-count-of-1s-count-of-0s-in-each-prefix-substring/)

给定一个整数 **N** ，任务是找到长度为 **N** 的可能二进制串的数量，其频率为 **0** 和 **1** 的频率相等，其中 **1** 的频率大于或等于每个前缀子串中 **0** 的频率。

**示例:**

> **输入:** N = 2
> **输出:** 1
> **解释:**
> 长度为 2 的所有可能的二进制字符串为{“00”、“01”、“10”和“11”}。
> 在这 4 个字符串中，只有“ **01** ”和“ **10** ”的 0 和 1 个数相等，
> 在这两个字符串中，只有“ **10** ”在每个前缀子串中包含的 1 个数比 0 个数多或相等。
> 
> **输入:** N = 4
> **输出:** 2
> **解释:**
> 所有可能的长度为 4 的二进制字符串，满足要求的条件为“1100”和“1010”。

**天真方法:**
最简单的方法是[生成所有长度为 N 的二进制字符串](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/)并迭代 [](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/) 每个字符串以检查其是否包含相等计数的 **0** 和 **1** ，并检查其所有*前缀子字符串*中 **1** 的频率是否等于或大于 **0** 的频率。

***时间复杂度:**o(n * 2<sup>^n</sup>)*
T7**辅助空间:** O(1)

**高效途径:**
利用[加泰罗尼亚号](https://www.geeksforgeeks.org/program-nth-catalan-number/)的概念可以进一步优化上述途径。我们只需要检查 n 的奇偶性。

*   如果 **N** 是一个 ***奇数*** 整数，则 0 和 1 的频率不能相等。因此，此类所需字符串的计数为 **0** 。
*   如果 **N** 是一个 ***甚至*** 的整数，那么所需子串的数量等于 ***(N/2) <sup>第</sup>个加泰罗尼亚数字*** 。

> **图解:**
> **N = 2**
> 唯一可能的字符串是“ **10** ”。因此，计数为 1。
> **N = 4**
> 唯一可能的字符串是“1100”和“1010”。因此，计数为 2。
> **N = 6**
> 唯一可能的字符串是“111000”、“110100”、“110010”、“101010”和“101100”。
> 因此计数为 5。
> 因此，对于 N 的每个 ***甚至*** 值，它遵循序列 1 2 5 14 ……
> 因此，该序列是加泰罗尼亚数字的序列。
> 因此可以得出，如果 N 为偶数，则计数等于 **(N/2) <sup>th</sup> 加泰罗尼亚数。**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and returns the
// value of Binomial Coefficient C(n, k)
unsigned long int binomialCoeff(unsigned int n,
                                unsigned int k)
{
    unsigned long int res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
    for (int i = 0; i < k; ++i) {
        res *= (n - i);
        res /= (i + 1);
    }

    return res;
}

// Function to return the count of all
// binary strings having equal count of 0's
// and 1's and each prefix substring having
// frequency of 1's >= frequencies of 0's
unsigned long int countStrings(unsigned int N)
{
    // If N is odd
    if (N % 2 == 1)

        // No such strings possible
        return 0;

    // Otherwise
    else {
        N /= 2;

        // Calculate value of 2nCn
        unsigned long int c
            = binomialCoeff(2 * N, N);

        // Return 2nCn/(n+1)
        return c / (N + 1);
    }
}

// Driver Code
int main()
{
    int N = 6;
    cout << countStrings(N) << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Function to calculate and returns the
// value of Binomial Coefficient C(n, k)
static long binomialCoeff(int n, int k)
{
    long res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
    for(int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }
    return res;
}

// Function to return the count of all
// binary strings having equal count of 0's
// and 1's and each prefix substring having
// frequency of 1's >= frequencies of 0's
static long countStrings(int N)
{

    // If N is odd
    if (N % 2 == 1)

        // No such strings possible
        return 0;

    // Otherwise
    else
    {
        N /= 2;

        // Calculate value of 2nCn
        long c = binomialCoeff(2 * N, N);

        // Return 2nCn/(n+1)
        return c / (N + 1);
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 6;

    System.out.print(countStrings(N) + " ");
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to calculate and returns the
# value of Binomial Coefficient C(n, k)
def binomialCoeff(n, k):
    res = 1

    # Since C(n, k) = C(n, n-k)
    if (k > n - k):
        k = n - k

    # Calculate the value of
    # [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
    for i in range(k):
        res *= (n - i)
        res //= (i + 1)

    return res

# Function to return the count of all
# binary strings having equal count of 0's
# and 1's and each prefix substring having
# frequency of 1's >= frequencies of 0's
def countStrings(N):

    # If N is odd
    if (N % 2 == 1):

        # No such strings possible
        return 0

    # Otherwise
    else:
        N //= 2

        # Calculate value of 2nCn
        c= binomialCoeff(2 * N, N)

        # Return 2nCn/(n+1)
        return c // (N + 1)

# Driver Code
if __name__ == '__main__':
    N = 6
    print(countStrings(N))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to implement the
// above approach
using System;

class GFG{

// Function to calculate and returns the
// value of Binomial Coefficient C(n, k)
static long binomialCoeff(int n, int k)
{
    long res = 1;

    // Since C(n, k) = C(n, n-k)
    if (k > n - k)
        k = n - k;

    // Calculate the value of
    // [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
    for(int i = 0; i < k; ++i)
    {
        res *= (n - i);
        res /= (i + 1);
    }
    return res;
}

// Function to return the count of all
// binary strings having equal count of 0's
// and 1's and each prefix substring having
// frequency of 1's >= frequencies of 0's
static long countStrings(int N)
{

    // If N is odd
    if (N % 2 == 1)

        // No such strings possible
        return 0;

    // Otherwise
    else
    {
        N /= 2;

        // Calculate value of 2nCn
        long c = binomialCoeff(2 * N, N);

        // Return 2nCn/(n+1)
        return c / (N + 1);
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 6;

    Console.Write(countStrings(N) + " ");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript program to implement the
// above approach

    // Function to calculate and returns the
    // value of Binomial Coefficient C(n, k)
    function binomialCoeff(n , k) {
        var res = 1;

        // Since C(n, k) = C(n, n-k)
        if (k > n - k)
            k = n - k;

        // Calculate the value of
        // [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
        for (var i = 0; i < k; ++i) {
            res *= (n - i);
            res /= (i + 1);
        }
        return res;
    }

    // Function to return the count of all
    // binary strings having equal count of 0's
    // and 1's and each prefix substring having
    // frequency of 1's >= frequencies of 0's
    function countStrings(N) {

        // If N is odd
        if (N % 2 == 1)

            // No such strings possible
            return 0;

        // Otherwise
        else
        {
            N /= 2;

            // Calculate value of 2nCn
            var c = binomialCoeff(2 * N, N);

            // Return 2nCn/(n+1)
            return c / (N + 1);
        }
    }

    // Driver code
    var N = 6;
    document.write(countStrings(N) + " ");

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)*
***辅助空间:******O(1)***