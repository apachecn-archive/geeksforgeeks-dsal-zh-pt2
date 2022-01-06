# 和等于给定 N 的最大素数

> 原文:[https://www . geesforgeks . org/maximum-primes-其和等于给定的-n/](https://www.geeksforgeeks.org/maximum-primes-whose-sum-is-equal-to-given-n/)

给定正整数 **N > 1** 。求和等于给定 n 的素数的最大个数。

**示例:**

> **输入:** N = 5
> **输出:** 2
> **解释** : 2 和 3 是两个和为 5 的素数。
> **输入:** N = 6
> **输出:** 3
> **解释** : 2、2、2 是三个素数，其和为 6。

对于和等于给定 n 的最大素数，素数必须尽可能小。所以，2 是最小可能的素数，是偶数。下一个大于 2 的质数是 3，这是奇数。所以，对于任何给定的 n，有两个条件，要么 n 是奇数，要么 n 是偶数。

*   **情况 1: n 为偶数**，这种情况下， **n/2** 将是答案(2 的 n/2 数将得到 n 的和)。

*   **情况 2: n 为奇数**，这种情况下，**楼(n/2)** 将是答案((n-3)/2 数为 2，一个 3 将得到 n 的和。

以下是上述方法的实现:

## C++

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find max count of primes
int maxPrimes(int n)
{
    // if n is even n/2 is required answer
    // if n is odd floor(n/2)  = (int)(n/2) is required answer
    return n / 2;
}

// Driver Code
int main()
{
    int n = 17;

    cout << maxPrimes(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG
{

// Function to find max count of primes
static int maxPrimes(int n)
{
    // if n is even n/2 is required answer
    // if n is odd floor(n/2) = (int)(n/2)
    // is required answer
    return n / 2;
}

// Driver Code
public static void main(String[] args)
{
    int n = 17;

    System.out.println(maxPrimes(n));
}
}

// This code is contributed
// by Code_Mech
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find max count of primes
def maxPrmimes(n):

    # if n is even n/2 is required answer
    # if n is odd floor(n/2) = (int)(n/2)
    # is required answer
    return n // 2

# Driver code
n = 17
print(maxPrmimes(n))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# program for above approach
using System;

class GFG
{

// Function to find max count of primes
static int maxPrimes(int n)
{
    // if n is even n/2 is required answer
    // if n is odd floor(n/2) = (int)(n/2)
    // is required answer
    return n / 2;
}

// Driver Code
public static void Main()
{
    int n = 17;

    Console.WriteLine(maxPrimes(n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above approach

// Function to find max count of primes
function maxPrimes($n)
{
    // if n is even n/2 is required answer
    // if n is odd floor(n/2) = (int)(n/2) is required answer
    return (int)($n / 2);
}

    // Driver Code
    $n = 17;
    echo maxPrimes($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to find max count of primes
function maxPrimes(n)
{
    // if n is even n/2 is required answer
    // if n is odd floor(n/2)  = (int)(n/2) is required answer
    return parseInt(n / 2);
}

// Driver Code
var n = 17;
document.write( maxPrimes(n)); 

</script>   
```

**Output:** 

```
8
```