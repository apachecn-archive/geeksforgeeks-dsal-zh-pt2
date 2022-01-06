# 使用给定的 N 个字符计数长度为 M 的非回文字符串

> 原文:[https://www . geeksforgeeks . org/使用给定 n 个字符的长度为 m 的非回文字符串计数/](https://www.geeksforgeeks.org/count-of-non-palindromic-strings-of-length-m-using-given-n-characters/)

给定两个正整数 **N** 和 **M** ，任务是使用给定的 **N** 个不同的字符计算长度为 **M** 的非回文字符串的数量。
**注意:**每个不同的字符可以使用多次。

**示例:**

> **输入:** N = 3，M = 2
> **输出:** 6
> **说明:**
> 由于只给出 3 个字符，这 3 个字符可以组成 **3 <sup>2</sup>** 不同的字符串。其中，只有 3 个字符串是回文。因此，剩下的 6 个字符串是回文。
> 
> **输入:** N = 26，M = 5
> T3】输出: 11863800

**方法:**
按照以下步骤解决问题:

*   使用给定的 **N** 字符的长度为 **M** 的字符串总数将为 **N <sup>M</sup>** 。
*   一个字符串要成为回文，前半部分和后半部分应该相等。对于**甚至 **M** 的**值，我们只需要从给定的 N 个字符中选择 **M/2** 字符。对于**奇数**值，我们需要从给定的 N 个字符中选择 **M/2 + 1** 个字符。由于允许重复，长度为 **M** 的回文串总数将为 **N <sup>(M/2 + M%2)</sup>** 。
*   非回文字符串的所需计数由以下等式给出:

```
N<sup>M - N(M/2 + M%2)</sup>
```

下面是上述方法的实现:

## C++

```
// C++ Program to count
// non-palindromic strings
// of length M using N
// distinct characters
#include <bits/stdc++.h>
using namespace std;

// Iterative Function to calculate
// base^pow in O(log y)
unsigned long long power(
    unsigned long long base,
    unsigned long long pow)
{
    unsigned long long res = 1;
    while (pow > 0) {
        if (pow & 1)
            res = (res * base);
        base = (base * base);
        pow >>= 1;
    }
    return res;
}

// Function to return the
// count of non palindromic strings
unsigned long long countNonPalindromicString(
    unsigned long long n,
    unsigned long long m)
{
    // Count of strings using n
    // characters with
    // repetitions allowed
    unsigned long long total
        = power(n, m);

    // Count of palindromic strings
    unsigned long long palindrome
        = power(n, m / 2 + m % 2);

    // Count of non-palindromic strings
    unsigned long long count
        = total - palindrome;

    return  count;
}
int main()
{

    int n = 3, m = 5;
    cout<< countNonPalindromicString(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count non-palindromic
// strings of length M using N distinct
// characters
import java.util.*;

class GFG{

// Iterative Function to calculate
// base^pow in O(log y)
static long power(long base, long pow)
{
    long res = 1;
    while (pow > 0)
    {
        if ((pow & 1) == 1)
            res = (res * base);
        base = (base * base);
        pow >>= 1;
    }
    return res;
}

// Function to return the
// count of non palindromic strings
static long countNonPalindromicString(long n,
                                      long m)
{

    // Count of strings using n
    // characters with
    // repetitions allowed
    long total = power(n, m);

    // Count of palindromic strings
    long palindrome = power(n, m / 2 + m % 2);

    // Count of non-palindromic strings
    long count = total - palindrome;

    return count;
}

// Driver code
public static void main(String[] args)
{
    int n = 3, m = 5;

    System.out.println(
        countNonPalindromicString(n, m));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to count non-palindromic strings
# of length M using N distinct characters

# Iterative Function to calculate
# base^pow in O(log y)
def power(base, pwr):

    res = 1
    while(pwr > 0):
        if(pwr & 1):
            res = res * base
        base = base * base
        pwr >>= 1

    return res

# Function to return the count
# of non palindromic strings
def countNonPalindromicString(n, m):

    # Count of strings using n
    # characters with
    # repetitions allowed
    total = power(n, m)

    # Count of palindromic strings
    palindrome = power(n, m // 2 + m % 2)

    # Count of non-palindromic strings
    count = total - palindrome

    return count

# Driver code
if __name__ == '__main__':

    n = 3
    m = 5

    print(countNonPalindromicString(n, m))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to count non-palindromic
// strings of length M using N distinct
// characters
using System;

class GFG{

// Iterative Function to calculate
// base^pow in O(log y)
static long power(long Base, long pow)
{
    long res = 1;
    while (pow > 0)
    {
        if ((pow & 1) == 1)
            res = (res * Base);

        Base = (Base * Base);
        pow >>= 1;
    }
    return res;
}

// Function to return the
// count of non palindromic strings
static long countNonPalindromicString(long n,
                                      long m)
{

    // Count of strings using n
    // characters with
    // repetitions allowed
    long total = power(n, m);

    // Count of palindromic strings
    long palindrome = power(n, m / 2 + m % 2);

    // Count of non-palindromic strings
    long count = total - palindrome;

    return count;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3, m = 5;

    Console.WriteLine(
        countNonPalindromicString(n, m));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to count non-palindromic
// strings of length M using N distinct
// characters

// Iterative Function to calculate
// base^pow in O(log y)
function power(base, pow)
{
    let res = 1;
    while (pow > 0)
    {
        if ((pow & 1) == 1)
            res = (res * base);

        base = (base * base);
        pow >>= 1;
    }
    return res;
}

// Function to return the
// count of non palindromic strings
function countNonPalindromicString(n, m)
{

    // Count of strings using n
    // characters with
    // repetitions allowed
    let total = power(n, m);

    // Count of palindromic strings
    let palindrome = power(n, m / 2 + m % 2);

    // Count of non-palindromic strings
    let count = total - palindrome;

    return count;
}

// Driver Code
let n = 3, m = 5;

document.write(countNonPalindromicString(n, m));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
216
```

***时间复杂度:** O(log(N))*