# 计数差也是素数的素数对

> 原文:[https://www . geeksforgeeks . org/count-prime-pairs-其差也是一个素数/](https://www.geeksforgeeks.org/count-prime-pairs-whose-difference-is-also-a-prime-number/)

给定一个整数 **N** ，任务是统计范围**【1，N】**内的[素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)对的个数，使得每对元素之间的差也是一个[素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。

**示例:**

> **输入:** N = 5
> **输出:** 2
> **说明:**
> 元素间差也是素数的[1，5]范围内的一对素数是:
> (2，5) = 3(素数)
> (3，5) = 2(素数)
> 因此，差也是素数的素数对的个数是 2。
> 
> **输入:**N = 11
> T3】输出: 4

**天真方法:**解决这个问题最简单的方法是[生成范围**【1，N】**中所有可能的元素对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，对于每一对，检查这两个元素以及这一对的两个元素之间的差异是否为[质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。如果发现为真，则增加计数。最后，打印计数。

***时间复杂度:**O(N<sup>2</sup>*√N)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 奇数–偶数=奇数
> 奇数–奇数=偶数
> 2 是唯一的偶数素数。
> 因此，问题简化为只检查那些素数对的元素之差等于 2 的素数对。

按照以下步骤解决问题:

*   初始化一个变量，比如说 **cntPairs** 来存储素数对的计数，这样每对元素之间的差也是一个[素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。
*   初始化一个数组，说**筛[]** 检查**【1，N】**范围内的数字是否为[质数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。
*   使用厄拉多塞的[筛找出**【1，N】**范围内的所有素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   迭代范围**【2，N】**，对于给定范围内的每个元素，检查**筛【I】**和**筛【I–2】**是否为真。如果发现为真，则将 **cntPairs** 的值增加 **2** 。
*   最后，打印 **cntPairs** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all prime
// numbers in the range [1, N]
vector<bool> SieveOfEratosthenes(
    int N)
{

    // isPrime[i]: Stores if i is
    // a prime number or not
    vector<bool> isPrime(N, true);

    isPrime[0] = false;
    isPrime[1] = false;

    // Calculate all prime numbers up to
    // Max using Sieve of Eratosthenes
    for (int p = 2; p * p <= N; p++) {

        // If P is a prime number
        if (isPrime[p]) {

            // Set all multiple of P
            // as non-prime
            for (int i = p * p; i <= N;
                 i += p) {

                // Update isPrime
                isPrime[i] = false;
            }
        }
    }
    return isPrime;
}

// Function to count pairs of
// prime numbers in the range [1, N]
// whose difference is prime
int cntPairsdiffOfPrimeisPrime(int N)
{

    // Function to count pairs of
    // prime numbers whose difference  
    // is also a prime number
    int cntPairs = 0;

    // isPrime[i]: Stores if i is
    // a prime number or not
    vector<bool> isPrime
          = SieveOfEratosthenes(N);

    // Iterate over the range [2, N]
    for (int i = 2; i <= N; i++) {

        // If i and i - 2 is
        // a prime number
        if (isPrime[i] &&
            isPrime[i - 2]) {

            // Update cntPairs
            cntPairs += 2;
        }
    }
    return cntPairs;
}

// Driver Code
int main()
{
    int N = 5;
    cout << cntPairsdiffOfPrimeisPrime(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find all prime
// numbers in the range [1, N]
public static boolean[] SieveOfEratosthenes(int N)
{

    // isPrime[i]: Stores if i is
    // a prime number or not
    boolean[] isPrime = new boolean[N + 1];
    Arrays.fill(isPrime, true);

    isPrime[0] = false;
    isPrime[1] = false;

    // Calculate all prime numbers up to
    // Max using Sieve of Eratosthenes
    for(int p = 2; p * p <= N; p++)
    {

        // If P is a prime number
        if (isPrime[p])
        {

            // Set all multiple of P
            // as non-prime
            for(int i = p * p; i <= N; i += p)
            {

                // Update isPrime
                isPrime[i] = false;
            }
        }
    }
    return isPrime;
}

// Function to count pairs of
// prime numbers in the range [1, N]
// whose difference is prime
public static int cntPairsdiffOfPrimeisPrime(int N)
{

    // Function to count pairs of
    // prime numbers whose difference
    // is also a prime number
    int cntPairs = 0;

    // isPrime[i]: Stores if i is
    // a prime number or not
    boolean[] isPrime = SieveOfEratosthenes(N);

    // Iterate over the range [2, N]
    for(int i = 2; i <= N; i++)
    {

        // If i and i - 2 is
        // a prime number
        if (isPrime[i] && isPrime[i - 2])
        {

            // Update cntPairs
            cntPairs += 2;
        }
    }
    return cntPairs;
}

// Driver Code
public static void main(String args[])
{
    int N = 5;

    System.out.println(cntPairsdiffOfPrimeisPrime(N));
}
}

// This code is contributed by hemanth gadarla
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from math import sqrt

# Function to find all prime
# numbers in the range [1, N]
def SieveOfEratosthenes(N):

    # isPrime[i]: Stores if i is
    # a prime number or not
    isPrime = [True for i in range(N + 1)]

    isPrime[0] = False
    isPrime[1] = False

    # Calculate all prime numbers up to
    # Max using Sieve of Eratosthenes
    for p in range(2, int(sqrt(N)) + 1, 1):

        # If P is a prime number
        if (isPrime[p]):

            # Set all multiple of P
            # as non-prime
            for i in range(p * p, N + 1, p):

                # Update isPrime
                isPrime[i] = False

    return isPrime

# Function to count pairs of
# prime numbers in the range [1, N]
# whose difference is prime
def cntPairsdiffOfPrimeisPrime(N):

    # Function to count pairs of
    # prime numbers whose difference  
    # is also a prime number
    cntPairs = 0

    # isPrime[i]: Stores if i is
    # a prime number or not
    isPrime = SieveOfEratosthenes(N)

    # Iterate over the range [2, N]
    for i in range(2, N + 1, 1):

        # If i and i - 2 is
        # a prime number
        if (isPrime[i] and isPrime[i - 2]):

            # Update cntPairs
            cntPairs += 2

    return cntPairs

# Driver Code
if __name__ == '__main__':

    N = 5

    print(cntPairsdiffOfPrimeisPrime(N))

# This code is contributed by ipg2016107
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find all prime
// numbers in the range [1, N]
public static bool[] SieveOfEratosthenes(int N)
{

    // isPrime[i]: Stores if i is
    // a prime number or not
    bool[] isPrime = new bool[N + 1];
    for(int i = 0; i < N + 1; i++)
    {
        isPrime[i] = true;
    }

    isPrime[0] = false;
    isPrime[1] = false;

    // Calculate all prime numbers up to
    // Max using Sieve of Eratosthenes
    for(int p = 2; p * p <= N; p++)
    {

        // If P is a prime number
        if (isPrime[p])
        {

            // Set all multiple of P
            // as non-prime
            for(int i = p * p; i <= N; i += p)
            {

                // Update isPrime
                isPrime[i] = false;
            }
        }
    }
    return isPrime;
}

// Function to count pairs of
// prime numbers in the range [1, N]
// whose difference is prime
public static int cntPairsdiffOfPrimeisPrime(int N)
{

    // Function to count pairs of
    // prime numbers whose difference
    // is also a prime number
    int cntPairs = 0;

    // isPrime[i]: Stores if i is
    // a prime number or not
    bool[] isPrime = SieveOfEratosthenes(N);

    // Iterate over the range [2, N]
    for(int i = 2; i <= N; i++)
    {

        // If i and i - 2 is
        // a prime number
        if (isPrime[i] && isPrime[i - 2])
        {

            // Update cntPairs
            cntPairs += 2;
        }
    }
    return cntPairs;
}

// Driver Code
public static void Main()
{
    int N = 5;

    Console.WriteLine(cntPairsdiffOfPrimeisPrime(N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find all prime
// numbers in the range [1, N]
function SieveOfEratosthenes(N)
{

    // isPrime[i]: Stores if i is
    // a prime number or not
    let isPrime = [];
    for(let i = 0; i < N + 1; i++)
    {
        isPrime[i] = true;
    }

    isPrime[0] = false;
    isPrime[1] = false;

    // Calculate all prime numbers up to
    // Max using Sieve of Eratosthenes
    for(let p = 2; p * p <= N; p++)
    {

        // If P is a prime number
        if (isPrime[p])
        {

            // Set all multiple of P
            // as non-prime
            for(let i = p * p; i <= N; i += p)
            {

                // Update isPrime
                isPrime[i] = false;
            }
        }
    }
    return isPrime;
}

// Function to count pairs of
// prime numbers in the range [1, N]
// whose difference is prime
function cntPairsdiffOfPrimeisPrime(N)
{

    // Function to count pairs of
    // prime numbers whose difference
    // is also a prime number
    let cntPairs = 0;

    // isPrime[i]: Stores if i is
    // a prime number or not
    let isPrime = SieveOfEratosthenes(N);

    // Iterate over the range [2, N]
    for(let i = 2; i <= N; i++)
    {

        // If i and i - 2 is
        // a prime number
        if (isPrime[i] && isPrime[i - 2])
        {

            // Update cntPairs
            cntPairs += 2;
        }
    }
    return cntPairs;
}

// Driver Code

    let N = 5;

    document.write(cntPairsdiffOfPrimeisPrime(N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N * log(log(N))*
***辅助空间:** O(N)*