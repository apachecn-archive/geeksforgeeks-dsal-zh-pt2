# 长度为 N 的二进制字符串的计数，使得 1 的频率超过 0 的频率

> 原文:[https://www . geesforgeks . org/长度为 n 的二进制字符串的计数，以至于 1 的频率超过 0 的频率/](https://www.geeksforgeeks.org/count-of-binary-strings-of-length-n-such-that-frequency-of-1s-exceeds-frequency-of-0s/)

给定一个整数 **N** ，任务是找到长度为**N**T5 的[二进制字符串的数量，使得 **1** 的频率大于 **0** 的频率。](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/)

**示例:**

> **输入:** N = 2
> **输出:** 1
> **说明:**长度为 2 的二进制字符串的计数为 4，即{“00”、“01”、“10”、“11”}。
> 频率 1 大于 0 的唯一字符串是“11”。
> 
> **输入:** N = 3
> **输出:** 4
> **说明:**长度为 3 的二进制字符串计数为 8，即{“000”、“001”、“010”、“011”、“100”、“101”、“110”、“111”}。
> 其中，1 的频率大于 0 的字符串有{“011”、“101”、“110”、“111”}。

**天真法:**解决这个问题最简单的方法是[生成所有长度为 N 的二进制字符串](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/)，对每个字符串进行迭代，找出 1 和 0 的频率，如果 1 的频率大于 0 的频率，则递增计数器。最后，打印计数。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**要观察上述方法，需要进行以下观察:

> **S <sub>总计</sub>** =长度为 N 的二进制字符串总数= 2 <sup>N</sup>

> **S <sub>相等</sub>** =长度为 N 的二进制串的个数，其频率为 0 和 1。
> **S<sub>1</sub>**=长度为 N 的二进制串的个数，其频率为 1 大于 0。
> **S<sub>0</sub>**=长度为 N 的二进制串的个数，其频率为 0 大于 1。
> **S<sub>总计</sub>**

1.  对于**S<sub>1</sub>T3】中的每一根弦， **S <sub>0 中存在一根弦。</sub>**
    假设“ **1110** ”是**S<sub>1</sub>T14】中的字符串，那么其在**S<sub>0</sub>T18】中对应的字符串将是“ **0001** ”。同样的， **S <sub>1</sub>** 中的每一根弦，在 **S <sub>0</sub>** 中都存在一根弦。因此，**S<sub>1</sub>= S<sub>0</sub>**<sub>(每 **N** )。</sub>******
2.  如果 **N** 是**奇数**那么 **S <sub>等于</sub> = 0** 。
3.  如果 **N** 是**偶数**，那么 **S <sub>等于</sub> =C(N，N/2)** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// and return the value of
// Binomial Coefficient C(n, k)
unsigned long int binomialCoeff(unsigned long int n,
                                unsigned long int k)
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

// Function to return the count of
// binary strings of length N such
// that frequency of 1's exceed that of 0's
unsigned long int countOfString(int N)
{
    // Count of N-length binary strings
    unsigned long int Stotal = pow(2, N);

    // Count of N- length binary strings
    // having equal count of 0's and 1's
    unsigned long int Sequal = 0;

    // For even length strings
    if (N % 2 == 0)
        Sequal = binomialCoeff(N, N / 2);

    unsigned long int S1 = (Stotal - Sequal) / 2;
    return S1;
}

// Driver Code
int main()
{
    int N = 3;
    cout << countOfString(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to calculate
// and return the value of
// Binomial Coefficient C(n, k)
static int binomialCoeff(int n, int k)
{
    int res = 1;

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

// Function to return the count of
// binary Strings of length N such
// that frequency of 1's exceed that of 0's
static int countOfString(int N)
{

    // Count of N-length binary Strings
    int Stotal = (int) Math.pow(2, N);

    // Count of N- length binary Strings
    // having equal count of 0's and 1's
    int Sequal = 0;

    // For even length Strings
    if (N % 2 == 0)
        Sequal = binomialCoeff(N, N / 2);

    int S1 = (Stotal - Sequal) / 2;
    return S1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    System.out.print(countOfString(N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate
# and return the value of
# Binomial Coefficient C(n, k)
def binomialCoeff(n, k):

    res = 1

    # Since C(n, k) = C(n, n-k)
    if(k > n - k):
        k = n - k

    # Calculate the value of
    # [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
    for i in range(k):
        res *= (n - i)
        res //= (i + 1)

    return res

# Function to return the count of
# binary strings of length N such
# that frequency of 1's exceed that of 0's
def countOfString(N):

    # Count of N-length binary strings
    Stotal = pow(2, N)

    # Count of N- length binary strings
    # having equal count of 0's and 1's
    Sequal = 0

    # For even length strings
    if(N % 2 == 0):
        Sequal = binomialCoeff(N, N // 2)

    S1 = (Stotal - Sequal) // 2

    return S1

# Driver Code
N = 3

print(countOfString(N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to calculate
// and return the value of
// Binomial Coefficient C(n, k)
static int binomialCoeff(int n, int k)
{
    int res = 1;

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

// Function to return the count of
// binary Strings of length N such
// that frequency of 1's exceed that of 0's
static int countOfString(int N)
{

    // Count of N-length binary Strings
    int Stotal = (int) Math.Pow(2, N);

    // Count of N- length binary Strings
    // having equal count of 0's and 1's
    int Sequal = 0;

    // For even length Strings
    if (N % 2 == 0)
        Sequal = binomialCoeff(N, N / 2);

    int S1 = (Stotal - Sequal) / 2;
    return S1;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;
    Console.Write(countOfString(N));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
    // Javascript program to implement
    // the above approach

    // Function to calculate
    // and return the value of
    // Binomial Coefficient C(n, k)
    function binomialCoeff(n, k)
    {
        let res = 1;

        // Since C(n, k) = C(n, n-k)
        if (k > n - k)
            k = n - k;

        // Calculate the value of
        // [n*(n-1)*---*(n-k+1)] / [k*(k-1)*---*1]
        for(let i = 0; i < k; ++i)
        {
            res *= (n - i);
            res /= (i + 1);
        }
        return res;
    }

    // Function to return the count of
    // binary Strings of length N such
    // that frequency of 1's exceed that of 0's
    function countOfString(N)
    {

        // Count of N-length binary Strings
        let Stotal = Math.pow(2, N);

        // Count of N- length binary Strings
        // having equal count of 0's and 1's
        let Sequal = 0;

        // For even length Strings
        if (N % 2 == 0)
            Sequal = binomialCoeff(N, N / 2);

        let S1 = (Stotal - Sequal) / 2;
        return S1;
    }

    let N = 3;
    document.write(countOfString(N));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)