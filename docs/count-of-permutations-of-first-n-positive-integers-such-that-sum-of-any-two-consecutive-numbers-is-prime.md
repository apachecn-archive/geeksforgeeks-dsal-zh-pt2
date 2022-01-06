# 前 N 个正整数排列的计数，使得任意两个连续数的和为质数

> 原文:[https://www . geesforgeks . org/第一个 n 个正整数的排列计数，这样任何两个连续数的和都是质数/](https://www.geeksforgeeks.org/count-of-permutations-of-first-n-positive-integers-such-that-sum-of-any-two-consecutive-numbers-is-prime/)

求前 N 个正整数的[排列数，使得任意两个连续数的和为素数，其中所有的](https://www.geeksforgeeks.org/permutation-of-first-n-positive-integers-such-that-prime-numbers-are-at-prime-indices/)[循环排列](https://www.geeksforgeeks.org/generate-cyclic-permutations-number/)被认为是相同的。

**注意:**第一个和最后一个元素的和也必须是素数。

**例**:

> **输入:** N = 6
> **输出:** 2
> **解释:**两个有效的排列是{1，4，3，2，5，6}和{1，6，5，2，3，4}。像{3，2，5，6，1，4}这样的置换被认为是第一个置换的循环置换，因此不包括在内。
> 
> **输入** : N = 3
> **输出** : 0
> **解释**:不存在有效排列。

**逼近**:给定的问题可以通过[递归](http://www.geeksforgeeks.org/recursion/)和[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)来解决。可以观察到，为了找到不同的循环数，不失一般性，循环应该从 **1** 开始。可以使用存储一个数是否是质数的厄拉多塞的[筛创建一个**isPrime【】**数组。因此，创建一个](http://www.geeksforgeeks.org/sieve-of-eratosthenes/)[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，并在排列中添加元素，使其与最后一个元素的和为质数。如果第一个和最后一个元素的和也是素数，则递增排列计数。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Initialize a global variable N
const int maxn = 100;

// Stores the final count of permutations
ll ans = 0;

// Stores whether the integer is prime
bool isPrime[maxn];
bool marked[maxn];

void SieveOfEratosthenes(int n)
{
    memset(isPrime, true, sizeof(isPrime));

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of P
            for (int i = p * p; i <= n; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to find the number of valid permutations
void countCycles(int m, int n, int prev, int par)
{
    // If a complete permutation is formed
    if (!m) {
        if (isPrime[prev + 1]) {

            // If the sum of 1st and last element
            // of the current permutation is prime
            ans++;
        }
        return;
    }

    // Iterate from par to N
    for (int i = 1 + par; i <= n; i++) {

        if (!marked[i] && isPrime[i + prev]) {

            // Visit the current number
            marked[i] = true;

            // Recursive Call
            countCycles(m - 1, n, i, 1 - par);

            // Backtrack
            marked[i] = false;
        }
    }
}

int countPermutations(int N)
{
    // Finding all prime numbers upto 2 * N
    SieveOfEratosthenes(2 * N);

    // Initializing all values in marked as 0
    memset(marked, false, sizeof(marked));

    // Initial condition
    marked[1] = true;

    countCycles(N - 1, N, 1, 1);

    // Return Answer
    return ans;
}

// Driver code
int main()
{
    int N = 6;
    cout << countPermutations(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG{

// Initialize a global variable N
static int maxn = 100;

// Stores the final count of permutations
static int ans = 0;

// Stores whether the integer is prime
static boolean []isPrime = new boolean[maxn];
static boolean []marked = new boolean[maxn];

static void SieveOfEratosthenes(int n)
{
    for (int i = 0; i <isPrime.length; i += 1) {
        isPrime[i]=true;
    }

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true) {

            // Update all multiples of P
            for (int i = p * p; i <= n; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to find the number of valid permutations
static void countCycles(int m, int n, int prev, int par)
{
    // If a complete permutation is formed
    if (m==0) {
        if (isPrime[prev + 1]) {

            // If the sum of 1st and last element
            // of the current permutation is prime
            ans++;
        }
        return;
    }

    // Iterate from par to N
    for (int i = 1 + par; i <= n; i++) {

        if (!marked[i] && isPrime[i + prev]) {

            // Visit the current number
            marked[i] = true;

            // Recursive Call
            countCycles(m - 1, n, i, 1 - par);

            // Backtrack
            marked[i] = false;
        }
    }
}

static int countPermutations(int N)
{

    // Finding all prime numbers upto 2 * N
    SieveOfEratosthenes(2 * N);

    // Initializing all values in marked as 0
    for (int i = 0; i <marked.length; i += 1) {
        marked[i]=false;
    }

    // Initial condition
    marked[1] = true;

    countCycles(N - 1, N, 1, 1);

    // Return Answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 6;
    System.out.print(countPermutations(N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python implementation for the above approach

import math

# Initialize a global variable N
maxn = 100

# Stores the final count of permutations
ans = 0

# Stores whether the integer is prime
isPrime = [True for _ in range(maxn)]
marked = [False for _ in range(maxn)]

def SieveOfEratosthenes(n):
    global ans
    global isPrime
    global marked

    for p in range(2, int(math.sqrt(n))+1):

                # If prime[p] is not changed,
                # then it is a prime
        if (isPrime[p] == True):

                        # Update all multiples of P
            for i in range(p*p, n+1, p):
                isPrime[i] = False

# Function to find the number of valid permutations
def countCycles(m, n, prev, par):
    global ans
    global isPrime
    global marked

    # If a complete permutation is formed
    if (not m):
        if (isPrime[prev + 1]):

                        # If the sum of 1st and last element
                        # of the current permutation is prime
            ans += 1

        return

        # Iterate from par to N
    for i in range(1+par, n+1):
        if (not marked[i] and isPrime[i + prev]):

                        # Visit the current number
            marked[i] = True

            # Recursive Call
            countCycles(m - 1, n, i, 1 - par)

            # Backtrack
            marked[i] = False

def countPermutations(N):
    global ans
    global isPrime
    global marked

    # Finding all prime numbers upto 2 * N
    SieveOfEratosthenes(2 * N)

    # Initial condition
    marked[1] = True

    countCycles(N - 1, N, 1, 1)

    # Return Answer
    return ans

# Driver code
if __name__ == "__main__":

    N = 6
    print(countPermutations(N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;

public class GFG
{

  // Initialize a global variable N
  static int maxn = 100;

  // Stores the final count of permutations
  static int ans = 0;

  // Stores whether the integer is prime
  static bool []isPrime = new bool[maxn];
  static bool []marked = new bool[maxn];

  static void SieveOfEratosthenes(int n)
  {
    for (int i = 0; i < isPrime.Length; i += 1) {
      isPrime[i] = true;
    }

    for (int p = 2; p * p <= n; p++) {

      // If prime[p] is not changed,
      // then it is a prime
      if (isPrime[p] == true) {

        // Update all multiples of P
        for (int i = p * p; i <= n; i += p)
          isPrime[i] = false;
      }
    }
  }

  // Function to find the number of valid permutations
  static void countCycles(int m, int n, int prev, int par)
  {
    // If a complete permutation is formed
    if (m==0) {
      if (isPrime[prev + 1]) {

        // If the sum of 1st and last element
        // of the current permutation is prime
        ans++;
      }
      return;
    }

    // Iterate from par to N
    for (int i = 1 + par; i <= n; i++) {

      if (!marked[i] && isPrime[i + prev]) {

        // Visit the current number
        marked[i] = true;

        // Recursive Call
        countCycles(m - 1, n, i, 1 - par);

        // Backtrack
        marked[i] = false;
      }
    }
  }

  static int countPermutations(int N)
  {

    // Finding all prime numbers upto 2 * N
    SieveOfEratosthenes(2 * N);

    // Initializing all values in marked as 0
    for (int i = 0; i <marked.Length; i += 1) {
      marked[i] = false;
    }

    // Initial condition
    marked[1] = true;

    countCycles(N - 1, N, 1, 1);

    // Return Answer
    return ans;
  }

  // Driver code
  public static void Main(string[] args)
  {
    int N = 6;
    Console.WriteLine(countPermutations(N));

  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Initialize a global variable N
const maxn = 100;

// Stores the final count of permutations
let ans = 0;

// Stores whether the integer is prime
let isPrime = new Array(maxn).fill(true);
let marked = new Array(maxn).fill(false);

function SieveOfEratosthenes(n) {

  for (let p = 2; p * p <= n; p++) {

    // If prime[p] is not changed,
    // then it is a prime
    if (isPrime[p] == true) {

      // Update all multiples of P
      for (let i = p * p; i <= n; i += p)
        isPrime[i] = false;
    }
  }
}

// Function to find the number of valid permutations
function countCycles(m, n, prev, par) {
  // If a complete permutation is formed
  if (!m) {
    if (isPrime[prev + 1]) {

      // If the sum of 1st and last element
      // of the current permutation is prime
      ans++;
    }
    return;
  }

  // Iterate from par to N
  for (let i = 1 + par; i <= n; i++) {

    if (!marked[i] && isPrime[i + prev]) {

      // Visit the current number
      marked[i] = true;

      // Recursive Call
      countCycles(m - 1, n, i, 1 - par);

      // Backtrack
      marked[i] = false;
    }
  }
}

function countPermutations(N)
{

  // Finding all prime numbers upto 2 * N
  SieveOfEratosthenes(2 * N);

  // Initial condition
  marked[1] = true;

  countCycles(N - 1, N, 1, 1);

  // Return Answer
  return ans;
}

// Driver code
let N = 6;
document.write(countPermutations(N));

// This code is contributed by gfgking.
</script>
```

**Output**

```
2
```

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*