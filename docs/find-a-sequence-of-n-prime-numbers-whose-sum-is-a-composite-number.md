# 找出 N 个素数的序列，它们的和是一个复合数

> 原文:[https://www . geesforgeks . org/find-a-序列 n-质数-其和是一个复合数/](https://www.geeksforgeeks.org/find-a-sequence-of-n-prime-numbers-whose-sum-is-a-composite-number/)

给定一个整数 **N** ，任务是找到一系列 **N** 素数，它们的和是一个复合数。
**例:**

> **输入:** N = 5
> **输出:** 2 3 5 7 11
> 2 + 3 + 5 + 7 + 11 = 28，复合。
> **输入:** N = 6
> **输出:** 3 5 7 11 13 17

**方法:**两个素数之和总是偶数，这是复合数，因为它们是奇数，除了 **2** 。现在有两种情况，

1.  当 **N 为偶数**时，除了 **2** 之外，我们可以打印任何 **N** 素数，并且它们的和总是偶数，即奇数相加偶数次将得到偶数和。
2.  当 **N 为奇数**时，我们可以打印 **2** 和任何其他**N–1**素数，以确保总和为偶数。既然**N–1**是偶数，那么除了 **2** 之外的任何素数的和都是偶数，那么我们就加上 **2** 作为**N**数，以确保和保持偶数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAXN 100000

// To store prime numbers
vector<int> v;

// Function to find and store
// all the primes <= n
void SieveOfEratosthenes(int n)
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store all the prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            v.push_back(p);
}

// Function to print the required sequence
void GetSequence(int n)
{

    // If n is even then we do not include 2
    // and start the sequence from the 2nd
    // smallest prime else we include 2
    int i = (n % 2 == 0) ? 1 : 0;

    int cnt = 0;
    // Print the sequence
    while (cnt < n) {
        cout << v[i] << " ";
        i++;
        cnt++;
    }
}

// Driver code
int main()
{
    int n = 6;
    SieveOfEratosthenes(MAXN);

    GetSequence(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

static int MAXN = 100000;

// To store prime numbers
static Vector<Integer> v = new Vector<Integer>();

// Function to find and store
// all the primes <= n
static void SieveOfEratosthenes(int n)
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    boolean[] prime = new boolean[n + 1];
    Arrays.fill(prime,true);

    for (int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store all the prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            v.add(p);
}

// Function to print the required sequence
static void GetSequence(int n)
{

    // If n is even then we do not include 2
    // and start the sequence from the 2nd
    // smallest prime else we include 2
    int i = (n % 2 == 0) ? 1 : 0;

    int cnt = 0;

    // Print the sequence
    while (cnt < n)
    {
        System.out.print(v.get(i) + " ");
        i++;
        cnt++;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    SieveOfEratosthenes(MAXN);

    GetSequence(n);
}
}

// This code is contributed by Princi Singh
```

## 大蟒

```
# Python3 implementation of the approach

MAXN=100000

# To store prime numbers
v=[]

# Function to find and store
# all the primes <= n
def SieveOfEratosthenes(n):

    # Create a boolean array "prime[0..n]" and initialize
    # all entries it as true. A value in prime[i] will
    # finally be false if i is Not a prime, else true.
    prime=[True for i in range(n + 1)]

    for p in range(2,n+1):

        # If prime[p] is not changed, then it is a prime
        if (prime[p] == True):

            # Update all multiples of p greater than or
            # equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(2 * p, n + 1, p):
                prime[i] = False

    # Store all the prime numbers
    for p in range(2, n + 1):
        if (prime[p]):
            v.append(p)

# Function to print the required sequence
def GetSequence(n):

    # If n is even then we do not include 2
    # and start the sequence from the 2nd
    # smallest prime else we include 2
    if n % 2 == 0:
        i = 1
    else:
        i = 0

    cnt = 0
    # Print the sequence
    while (cnt < n):
        print(v[i],end=" ")
        i += 1
        cnt += 1

# Driver code
n = 6
SieveOfEratosthenes(MAXN)

GetSequence(n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int MAXN = 100000;

// To store prime numbers
static List<int> v = new List<int>();

// Function to find and store
// all the primes <= n
static void SieveOfEratosthenes(int n)
{
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    Boolean[] prime = new Boolean[n + 1];
    for(int i = 0; i < n + 1; i++)
        prime[i] = true;

    for (int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store all the prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            v.Add(p);
}

// Function to print the required sequence
static void GetSequence(int n)
{

    // If n is even then we do not include 2
    // and start the sequence from the 2nd
    // smallest prime else we include 2
    int i = (n % 2 == 0) ? 1 : 0;

    int cnt = 0;

    // Print the sequence
    while (cnt < n)
    {
        Console.Write(v[i] + " ");
        i++;
        cnt++;
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 6;
    SieveOfEratosthenes(MAXN);

    GetSequence(n);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation
// of the approach

var MAXN = 100000;

// To store prime numbers
var v = [];

// Function to find and store
// all the primes <= n
function SieveOfEratosthenes(n)
{
    // Create a boolean array
    // "prime[0..n]" and initialize
    // all entries it as true.
    // A value in prime[i] will
    // finally be false if i is Not a prime,
    // else true.
    var prime = Array(n + 1).fill(true);
    var p;
    for (p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {
             var i;
            // Update all multiples
            // of p greater than or
            // equal to the square of it
            // numbers which are multiple
            // of p and are
            // less than p^2 are
            // already been marked.
            for (i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store all the prime numbers
    for (p = 2; p <= n; p++)
        if (prime[p])
            v.push(p);
}

// Function to print
// the required sequence
function GetSequence(n)
{

    // If n is even then we do not include 2
    // and start the sequence from the 2nd
    // smallest prime else we include 2
    var i = (n % 2 == 0) ? 1 : 0;

    var cnt = 0;
    // Print the sequence
    while (cnt < n) {
        document.write(v[i] + " ");
        i++;
        cnt++;
    }
}

// Driver code
    n = 6;
    SieveOfEratosthenes(MAXN);
    GetSequence(n);

</script>
```

**Output:** 

```
3 5 7 11 13 17
```