# 给定数组中最长递增素子序列的长度

> 原文:[https://www . geeksforgeeks . org/给定数组中最长递增素子序列的长度/](https://www.geeksforgeeks.org/length-of-longest-increasing-prime-subsequence-from-a-given-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出给定数组中由[个素数](https://www.geeksforgeeks.org/prime-numbers/)组成的[个最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence/)的长度。

**示例:**

> **输入:** arr[] = {1，2，5，3，2，5，1，7}
> **输出:** 4
> **解释:**
> 最长的递增素子序列是{2，3，5，7}。
> 所以，答案是 4。
> 
> **输入:** arr[] = {6，11，7，13，9，25}
> **输出:** 2
> **解释:**
> 最长的递增素子序列是{11，13}和{7，13}。
> 所以，答案是 2。

**朴素方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能的子序列，并按递增顺序打印由[素数](https://www.geeksforgeeks.org/prime-numbers/)组成的最长子序列的长度。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法对上述方法进行优化。这个问题是[最长增子序列问题的一个基本变种。](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)以下是步骤:

*   初始化大小为 **N** 的辅助数组 **dp[]** ，使得 **dp[i]** 将存储以索引 **i** 结束的素数 LIS 的长度。
*   下面是寻找最长递增素数的递推关系:

> 如果 arr[i]是素数，那么
> dp[i] = 1 + max(dp[j]，对于 j 属于(0，I–1))，其中 0 < j < i 和 arr[j]<arr[I]；
> dp[i] = 1，如果不存在这样的 j
> 否则如果 arr[i]是非素数，那么
> dp[i] = 0

*   使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)储存所有质数至**10<sup>5</sup>T5。**
*   在给定数组上迭代两个嵌套循环，并根据上述递归关系更新数组 **dp[]** 。
*   经过以上所有步骤后，数组 **dp[]** 中的最大元素就是给定数组中素数最长递增子序列的长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define N 100005

// Function to find the prime numbers
// till 10^5 using Sieve of Eratosthenes
void SieveOfEratosthenes(bool prime[],
                         int p_size)
{
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2;
                 i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function which computes the length
// of the LIS of Prime Numbers
int LISPrime(int arr[], int n)
{
    // Create an array of size n
    int lisp[n];

    // Create boolean array to
    // mark prime numbers
    bool prime[N + 1];

    // Initialize all values to true
    memset(prime, true, sizeof(prime));

    // Precompute N primes
    SieveOfEratosthenes(prime, N);

    lisp[0] = prime[arr[0]] ? 1 : 0;

    // Compute optimized LIS having
    // prime numbers in bottom up manner
    for (int i = 1; i < n; i++) {
        if (!prime[arr[i]]) {
            lisp[i] = 0;
            continue;
        }

        lisp[i] = 1;
        for (int j = 0; j < i; j++) {

            // Check for LIS and prime
            if (prime[arr[j]]
                && arr[i] > arr[j]
                && lisp[i] < lisp[j] + 1) {
                lisp[i] = lisp[j] + 1;
            }
        }
    }

    // Return maximum value in lis[]
    return *max_element(lisp, lisp + n);
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 5, 3, 2, 5, 1, 7 };

    // Size of array
    int M = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << LISPrime(arr, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static final int N = 100005;

// Function to find the prime numbers
// till 10^5 using Sieve of Eratosthenes
static void SieveOfEratosthenes(boolean prime[],
                                int p_size)
{

    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= p_size; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p,
            // set them to non-prime
            for(int i = p * 2;
                    i <= p_size;
                    i += p)
                prime[i] = false;
        }
    }
}

// Function which computes the length
// of the LIS of Prime Numbers
static int LISPrime(int arr[], int n)
{

    // Create an array of size n
    int []lisp = new int[n];

    // Create boolean array to
    // mark prime numbers
    boolean []prime = new boolean[N + 1];

    // Initialize all values to true
    for(int i = 0; i < prime.length; i++)
        prime[i] = true;

    // Precompute N primes
    SieveOfEratosthenes(prime, N);

    lisp[0] = prime[arr[0]] ? 1 : 0;

    // Compute optimized LIS having
    // prime numbers in bottom up manner
    for(int i = 1; i < n; i++)
    {
        if (!prime[arr[i]])
        {
            lisp[i] = 0;
            continue;
        }

        lisp[i] = 1;
        for(int j = 0; j < i; j++)
        {

            // Check for LIS and prime
            if (prime[arr[j]] &&
                arr[i] > arr[j] &&
               lisp[i] < lisp[j] + 1)
            {
                lisp[i] = lisp[j] + 1;
            }
        }
    }

    // Return maximum value in lis[]
    return Arrays.stream(lisp).max().getAsInt();
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 1, 2, 5, 3, 2, 5, 1, 7 };

    // Size of array
    int M = arr.length;

    // Function call
    System.out.print(LISPrime(arr, M));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
N = 100005

# Function to find the prime numbers
# till 10^5 using Sieve of Eratosthenes
def SieveOfEratosthenes(prime, p_size):

  # False here indicates
  # that it is not prime
  prime[0] = False
  prime[1] = False

  p = 2
  while p * p <= p_size:

    # If prime[p] is not changed,
    # then it is a prime
    if (prime[p]):

      # Update all multiples of p,
      # set them to non-prime
      for i in range (p * 2,
                      p_size + 1, p):
        prime[i] = False

        p += 1

# Function which computes the length
# of the LIS of Prime Numbers
def LISPrime(arr, n):

  # Create an array of size n
  lisp = [0] * n

  # Create boolean array to
  # mark prime numbers
  prime = [True] * (N + 1)

  # Precompute N primes
  SieveOfEratosthenes(prime, N)

  if prime[arr[0]]:
    lisp[0] = 1
    else:
      lisp[0] = 0

      # Compute optimized LIS having
      # prime numbers in bottom up manner
      for i in range (1, n):
        if (not prime[arr[i]]):
          lisp[i] = 0
          continue

          lisp[i] = 1
          for j in range (i):
            # check for LIS and prime
            if (prime[arr[j]] and
                arr[i] > arr[j] and
                lisp[i] < lisp[j] + 1):
              lisp[i] = lisp[j] + 1

              # Return maximum value in lis[]
              return max(lisp)

# Driver Code
if __name__ == "__main__":

  # Given array
  arr = [1, 2, 5, 3,
         2, 5, 1, 7]

  # Size of array
  M = len(arr)

  # Function Call
  print (LISPrime(arr, M))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

class GFG{

static readonly int N = 100005;

// Function to find the prime numbers
// till 10^5 using Sieve of Eratosthenes
static void SieveOfEratosthenes(bool []prime,
                                int p_size)
{

    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= p_size; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p,
            // set them to non-prime
            for(int i = p * 2;
                    i <= p_size;
                    i += p)
                prime[i] = false;
        }
    }
}

// Function which computes the length
// of the LIS of Prime Numbers
static int LISPrime(int []arr, int n)
{

    // Create an array of size n
    int []lisp = new int[n];

    // Create bool array to
    // mark prime numbers
    bool []prime = new bool[N + 1];

    // Initialize all values to true
    for(int i = 0; i < prime.Length; i++)
        prime[i] = true;

    // Precompute N primes
    SieveOfEratosthenes(prime, N);

    lisp[0] = prime[arr[0]] ? 1 : 0;

    // Compute optimized LIS having
    // prime numbers in bottom up manner
    for(int i = 1; i < n; i++)
    {
        if (!prime[arr[i]])
        {
            lisp[i] = 0;
            continue;
        }

        lisp[i] = 1;
        for(int j = 0; j < i; j++)
        {

            // Check for LIS and prime
            if (prime[arr[j]] &&
                arr[i] > arr[j] &&
               lisp[i] < lisp[j] + 1)
            {
                lisp[i] = lisp[j] + 1;
            }
        }
    }

    // Return maximum value in lis[]
    return lisp.Max();
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 1, 2, 5, 3, 2, 5, 1, 7 };

    // Size of array
    int M = arr.Length;

    // Function call
    Console.Write(LISPrime(arr, M));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let N = 100005

// Function to find the prime numbers
// till 10^5 using Sieve of Eratosthenes
function SieveOfEratosthenes(prime, p_size)
{
    // False here indicates
    // that it is not prime
    prime[0] = false;
    prime[1] = false;

    for (let p = 2; p * p <= p_size; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (let i = p * 2;
                 i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function which computes the length
// of the LIS of Prime Numbers
function LISPrime(arr, n)
{
    // Create an array of size n
    let lisp = new Array(n);

    // Create boolean array to
    // mark prime numbers
    let prime = new Array(N + 1);

    // Initialize all values to true
    prime.fill(true);

    // Precompute N primes
    SieveOfEratosthenes(prime, N);

    lisp[0] = prime[arr[0]] ? 1 : 0;

    // Compute optimized LIS having
    // prime numbers in bottom up manner
    for (let i = 1; i < n; i++) {
        if (!prime[arr[i]]) {
            lisp[i] = 0;
            continue;
        }

        lisp[i] = 1;
        for (let j = 0; j < i; j++) {

            // Check for LIS and prime
            if (prime[arr[j]]
                && arr[i] > arr[j]
                && lisp[i] < lisp[j] + 1) {
                lisp[i] = lisp[j] + 1;
            }
        }
    }

    // Return maximum value in lis[]
    return lisp.sort((a, b) => b - a)[0];
}

// Driver Code

    // Given array
    let arr = [ 1, 2, 5, 3, 2, 5, 1, 7 ];

    // Size of array
    let M = arr.length;

    // Function Call
    document.write(LISPrime(arr, M));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*