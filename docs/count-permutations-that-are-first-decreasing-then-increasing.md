# 统计先减少后增加的排列。

> 原文:[https://www . geesforgeks . org/count-排列-先减后增/](https://www.geeksforgeeks.org/count-permutations-that-are-first-decreasing-then-increasing/)

给定一个整数 **N** ，计算**A =【1，2，…，N】**先递减后递增的排列数。

**示例:**

> **输入:** N = 5
> **输出:** 14
> 以下是先减后增的子序列:
> 【2，1，3，4，5】，【3，1，2，4，5】，【4，1，2，3，5】，【5，1，2，3，4】，
> 【3，2，1，4，5】，【5，2，1，3，3】 2]，[5，4，2，1，3]，
> [5，3，2，1，4]，[4，3，2，1，5]
> **输入:** N = 1
> **输出:** 0

**方法:**很明显，序列从减少到增加的点被排列的**最小元素 1** 占据。此外，递减序列之后总是有递增序列，这意味着最小元素的位置范围为**【2，…，N-1】**。否则，将导致完全递增或完全递减的序列。
例如**考虑 N = 5，位置= 2** ，即序列中位置 2 的最小元素。用**配置= [_，1，_，_，_]统计所有可能的序列。**
从剩余的 4 个元素(2、3、4、5)中选择任意 1 个元素填充位置 1。例如，我们选择元素= 3。配置看起来像[3，1，_，_，_]。只有一个序列是可能的，即[3，1，2，4，5]。因此，对于要在位置 1 填充的每个选定元素，序列是可能的。通过这种配置，总共有**<sup>4</sup>C<sub>1</sub>**种排列是可能的。
现在考虑**配置= [_，_，1，_，_]。**
通过从剩余的 4 个元素中选择任意 2 个元素，可以应用类似的方法，并且对于每对元素，单个有效排列是可能的。因此，该配置的排列数量=**<sup>4</sup>C<sub>2</sub>**
N = 5 的最终配置可能是 **[_，_，1，_]**
选择剩余 4 个元素中的任意 3 个，并且对于每个三元组，获得排列。本例中的排列数=**<sup>4</sup>C<sub>3</sub>**
**最终计数=<sup>4</sup>C<sub>1</sub>+<sup>4</sup>C+<sup>4</sup>C<sub>3</sub>N = 5**
N 的广义结果:

```
Count = N-1C1 + N-1C2 + ... + N-1CN-2 which simplifies to,
 N-1Ci = 2N-1 - 2 (from binomial theorem)
```

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

#define ll long long
using namespace std;

const int mod = 1000000007;

// Function to compute a^n % mod
ll power(ll a, ll n)
{

    if (n == 0)
        return 1;

    ll p = power(a, n / 2) % mod;
    p = (p * p) % mod;
    if (n & 1)
        p = (p * a) % mod;

    return p;
}

// Function to count permutations that are
// first decreasing and then increasing
int countPermutations(int n)
{

    // For n = 1 return 0
    if (n == 1) {
        return 0;
    }

    // Calculate and return result
    return (power(2, n - 1) - 2) % mod;
}

// Driver code
int main()
{
    int n = 5;
    cout << countPermutations(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

static final int mod = 1000000007;

// Function to compute a^n % mod
static long power(long a, long n)
{

    if (n == 0)
        return 1;

    long p = power(a, n / 2) % mod;
    p = (p * p) % mod;
    if ((n & 1) == 1)
        p = (p * a) % mod;

    return p;
}

// Function to count permutations that are
// first decreasing and then increasing
static int countPermutations(int n)
{

    // For n = 1 return 0
    if (n == 1)
    {
        return 0;
    }

    // Calculate and return result
    return ((int)power(2, n - 1) - 2) % mod;
}

// Driver code
public static void main(String args[])
{
    int n = 5;
    System.out.println(countPermutations(n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
mod = 1000000007

# Function to compute a^n % mod
def power(a, n):
    if(n == 0):
        return 1

    p = power(a, int(n / 2)) % mod;
    p = (p * p) % mod
    if (n & 1):
        p = (p * a) % mod

    return p

# Function to count permutations that are
# first decreasing and then increasing
def countPermutations(n):

    # For n = 1 return 0
    if (n == 1):
        return 0

    # Calculate and return result
    return (power(2, n - 1) - 2) % mod

# Driver code
if __name__ == '__main__':
    n = 5
    print(countPermutations(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

static int mod = 1000000007;

// Function to compute a^n % mod
static long power(long a, long n)
{

    if (n == 0)
        return 1;

    long p = power(a, n / 2) % mod;
    p = (p * p) % mod;
    if ((n & 1) == 1)
        p = (p * a) % mod;

    return p;
}

// Function to count permutations that are
// first decreasing and then increasing
static int countPermutations(int n)
{

    // For n = 1 return 0
    if (n == 1)
    {
        return 0;
    }

    // Calculate and return result
    return ((int)power(2, n - 1) - 2) % mod;
}

// Driver code
static public void Main ()
{
    int n = 5;
    Console.WriteLine(countPermutations(n));
}
}

// This code is contributed by ajit..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

$mod = 1000000007;

// Function to compute a^n % mod
function power($a, $n)
{
    global $mod;
    if ($n == 0)
        return 1;

    $p = power($a, $n / 2) % $mod;
    $p = ($p * $p) % $mod;
    if ($n & 1)
        $p = ($p * $a) % $mod;

    return $p;
}

// Function to count permutations that are
// first decreasing and then increasing
function countPermutations($n)
{
    global $mod;

    // For n = 1 return 0
    if ($n == 1)
    {
        return 0;
    }

    // Calculate and return result
    return (power(2, $n - 1) - 2) % $mod;
}

// Driver Code
$n = 5;
echo countPermutations($n);

// This code is contributed by Tushil.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    let mod = 1000000007;

    // Function to compute a^n % mod
    function power(a, n)
    {

        if (n == 0)
            return 1;

        let p = power(a, parseInt(n / 2, 10)) % mod;
        p = (p * p) % mod;
        if ((n & 1) == 1)
            p = (p * a) % mod;

        return p;
    }

    // Function to count permutations that are
    // first decreasing and then increasing
    function countPermutations(n)
    {

        // For n = 1 return 0
        if (n == 1)
        {
            return 0;
        }

        // Calculate and return result
        return (power(2, n - 1) - 2) % mod;
    }

    let n = 5;
    document.write(countPermutations(n));

</script>
```

**Output:** 

```
14
```