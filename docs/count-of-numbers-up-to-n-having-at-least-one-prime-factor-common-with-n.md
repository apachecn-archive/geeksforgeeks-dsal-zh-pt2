# 具有至少一个与 N 相同的质因数的 N 个数的计数

> 原文:[https://www . geeksforgeeks . org/count-of-numbers-up-n-with-n-common-至少有一个质因数/](https://www.geeksforgeeks.org/count-of-numbers-up-to-n-having-at-least-one-prime-factor-common-with-n/)

给定一个整数 **N** ，任务是从范围**【1，N】**中计算整数的数量，该范围与除 **1** 之外的 **N** 至少有一个相同的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。

**示例:**

> **输入:** N = 5
> **输出:** 1
> **说明:**
> 既然 5 是质数。因此，除了 N 本身之外，没有其他最多为 N 的数与 N 至少有一个公因数。因此，计数为 1。
> 
> **输入:**N = 12
> T3】输出: 8

**天真法:**解决给定问题最简单的方法是遍历**【1，N】**范围内的所有数字，对于每一个元素，如果每一个带有 **N** 的数字的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 大于 **1** ，则递增计数。否则，检查下一个号码。核对所有数字后，我们打印得到的总数**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count all the numbers
// in the range [1, N] having common
// factor with N other than 1
int countNumbers(int N)
{
    // Stores the count of numbers
    // having more than 1 factor with N
    int count = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {

        // If gcd is not 1 then
        // increment the count
        if (__gcd(i, N) != 1)
            count++;
    }

    // Print the resultant count
    cout << count;
}

// Driver Code
int main()
{
    int N = 5;
    countNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count all the numbers
// in the range [1, N] having common
// factor with N other than 1
static void countNumbers(int N)
{

    // Stores the count of numbers
    // having more than 1 factor with N
    int count = 0;

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // If gcd is not 1 then
        // increment the count
        if (__gcd(i, N) != 1)
            count++;
    }

    // Print the resultant count
    System.out.print(count);
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    countNumbers(N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import math

# Function to count all the numbers
# in the range [1, N] having common
# factor with N other than 1
def countNumbers(N):

    # Stores the count of numbers
    # having more than 1 factor with N
    count = 0

    # Iterate over the range [1, N]
    for i in range(1, N + 1):

        # If gcd is not 1 then
        # increment the count
        if (math.gcd(i, N) != 1):
            count += 1

    # Print the resultant count
    print(count)

# Driver Code
if __name__ == "__main__":

    N = 5
    countNumbers(N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to count all the numbers
// in the range [1, N] having common
// factor with N other than 1
static void countNumbers(int N)
{

    // Stores the count of numbers
    // having more than 1 factor with N
    int count = 0;

    // Iterate over the range [1, N]
    for(int i = 1; i <= N; i++)
    {

        // If gcd is not 1 then
        // increment the count
        if (__gcd(i, N) != 1)
            count++;
    }

    // Print the resultant count
    Console.Write(count);
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5;
    countNumbers(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to count all the numbers
// in the range [1, N] having common
// factor with N other than 1
function countNumbers(N)
{

    // Stores the count of numbers
    // having more than 1 factor with N
    var count = 0;

    // Iterate over the range [1, N]
    for(var i = 1; i <= N; i++)
    {

        // If gcd is not 1 then
        // increment the count
        if (__gcd(i, N) != 1)
            count++;
    }

    // Print the resultant count
    document.write(count);
}

function __gcd(a , b)
{
    return b == 0 ? a : __gcd(b, a % b);
}

// Driver Code
var N = 5;
countNumbers(N);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过使用欧拉全能性函数进行优化，该函数给出的计数小于 **N** 的数字与 **N** 没有共同的质因数。按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**，它存储的是除了 **1** 以外的具有公共质因数的数字。
*   定义一个函数**φ()**来计算[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)的值，它代表小于 **N** 的整数的计数，与 **N** 没有公因数。
*   完成上述步骤后，打印**(N–φ(N)**的值作为结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the value of
// Euler's totient function
int phi(int N)
{
    // Initialize result with N
    int result = N;

    // Find all prime factors of N
    // and subtract their multiples
    for (int p = 2; p * p <= N; ++p) {

        // Check if p is a prime factor
        if (N % p == 0) {

            // If found to be true,
            // then update N and result
            while (N % p == 0)
                N /= p;

            result -= result / p;
        }
    }

    // If N has a prime factor greater
    // than sqrt(N), then there can be
    // at-most one such prime factor
    if (N > 1)
        result -= result / N;

    return result;
}

// Function to count all the numbers
// in the range [1, N] having common
// factor with N other than 1
int countNumbers(int N)
{
    // Stores the resultant count
    int count = N - phi(N);

    // Print the count
    cout << count;
}

// Driver Code
int main()
{
    int N = 5;
    countNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

 // Function to calculate the value of
// Euler's totient function
static int phi(int N)
{

    // Initialize result with N
    int result = N;

    // Find all prime factors of N
    // and subtract their multiples
    for (int p = 2; p * p <= N; ++p)
    {

        // Check if p is a prime factor
        if (N % p == 0) {

            // If found to be true,
            // then update N and result
            while (N % p == 0)
                N /= p;

            result -= result / p;
        }
    }

    // If N has a prime factor greater
    // than sqrt(N), then there can be
    // at-most one such prime factor
    if (N > 1)
        result -= result / N;

    return result;
}

// Function to count all the numbers
// in the range [1, N] having common
// factor with N other than 1
static void countNumbers(int N)
{

    // Stores the resultant count
    int count = N - phi(N);

    // Print the count
   System.out.print(count);
}

  // Driver code
public static void main (String[] args)
{
     int N = 5;
    countNumbers(N);
}
}

// This code is contributed by offbeat.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the value of
# Euler's totient function
def phi(N):

    # Initialize result with N
    result = N

    # Find all prime factors of N
    # and subtract their multiples
    for p in range(2, int(pow(N, 1 / 2)) + 1):

        # Check if p is a prime factor
        if (N % p == 0):

            # If found to be true,
            # then update N and result
            while (N % p == 0):
                N = N / p

            result -= result // p

    # If N has a prime factor greater
    # than sqrt(N), then there can be
    # at-most one such prime factor
    if (N > 1):
        result -= result // N

    return result

# Function to count all the numbers
# in the range [1, N] having common
# factor with N other than 1
def countNumbers(N):

    # Stores the resultant count
    count = N - phi(N)

    # Print the count
    print(count)

# Driver Code
N = 5

countNumbers(N)

# This code is contributed by SoumikMondal
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

 // Function to calculate the value of
// Euler's totient function
static int phi(int N)
{

    // Initialize result with N
    int result = N;

    // Find all prime factors of N
    // and subtract their multiples
    for (int p = 2; p * p <= N; ++p)
    {

        // Check if p is a prime factor
        if (N % p == 0) {

            // If found to be true,
            // then update N and result
            while (N % p == 0)
                N /= p;

            result -= result / p;
        }
    }

    // If N has a prime factor greater
    // than sqrt(N), then there can be
    // at-most one such prime factor
    if (N > 1)
        result -= result / N;

    return result;
}

// Function to count all the numbers
// in the range [1, N] having common
// factor with N other than 1
static void countNumbers(int N)
{

    // Stores the resultant count
    int count = N - phi(N);

    // Print the count
   Console.Write(count);
}

  // Driver code
public static void Main(String[] args)
{
     int N = 5;
    countNumbers(N);
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation
// for the above approach

// Function to calculate the value of
// Euler's totient function
function phi(N)
{

    // Initialize result with N
    let result = N;

    // Find all prime factors of N
    // and subtract their multiples
    for (let p = 2; p * p <= N; ++p)
    {

        // Check if p is a prime factor
        if (N % p == 0) {

            // If found to be true,
            // then update N and result
            while (N % p == 0)
                N /= p;

            result -= result / p;
        }
    }

    // If N has a prime factor greater
    // than sqrt(N), then there can be
    // at-most one such prime factor
    if (N > 1)
        result -= result / N;

    return result;
}

// Function to count all the numbers
// in the range [1, N] having common
// factor with N other than 1
function countNumbers(N)
{

    // Stores the resultant count
    let count = N - phi(N);

    // Print the count
       document.write(count);
}

// Driver Code

    let N = 5;
    countNumbers(N);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>1/2</sup>)*
***辅助空间:** O(1)*