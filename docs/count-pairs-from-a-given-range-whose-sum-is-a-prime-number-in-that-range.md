# 对给定范围内的配对进行计数，其和为该范围内的素数

> 原文:[https://www . geesforgeks . org/count-pairs-from-a-给定范围-其和是该范围内的质数/](https://www.geeksforgeeks.org/count-pairs-from-a-given-range-whose-sum-is-a-prime-number-in-that-range/)

给定两个整数 **L** 和 **R** ，任务是从范围**【L，R】**中计数对的数量，其和是范围**【L，R】**中的[素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。

**示例:**

> **输入:** L = 1，R = 5
> **输出:** 4
> **说明:**和为素数且在[L，R]范围内的对为{ (1，1)，(1，2)，(1，4)，(2，3) }。因此，所需的输出为 4。
> 
> **输入:** L = 1，R = 100
> T3】输出: 518

**天真方法:**解决这个问题最简单的方法是[从范围**【1，R】**中生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，对于每一对，[检查该对的元素之和是否为范围**【L，R】**中的素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。如果发现为真，则增加**计数**。最后，打印**计数**的值。

***时间复杂度:**O(N<sup>5/2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> 如果 N 是素数，那么和为 N 的对是{ (1，N–1)，(2，N–2)，…..地板(2 层)，天花板(2 层)。因此，总和为 N = N / 2 的对的总数

按照以下步骤解决问题:

*   初始化一个变量，比如说 **cntPairs** 来存储对的计数，使得对的元素之和是一个质数并且在**【L，R】**的范围内。
*   使用厄拉多塞的[筛，初始化一个数组，比如**segmented seve【】**来存储**【L，R】**范围内的所有素数。](https://www.geeksforgeeks.org/segmented-sieve-print-primes-in-a-range/)
*   [使用变量 **i** 遍历**段**段](https://www.geeksforgeeks.org/segmented-sieve-print-primes-in-a-range/)段
    段[段**段**段](https://www.geeksforgeeks.org/segmented-sieve-print-primes-in-a-range/)段**段**段，检查 **i** 段是否为素数。如果发现为真，则将 **cntPairs** 的值增加 **(i / 2)。**
*   最后，打印 **cntPairs** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all prime numbers in range
// [1, lmt] using sieve of Eratosthenes
void simpleSieve(int lmt, vector<int>& prime)
{

    // segmentedSieve[i]: Stores if i is
    // a prime number (True) or not (False)
    bool Sieve[lmt + 1];

    // Initialize all elements of
    // segmentedSieve[] to false
    memset(Sieve, true, sizeof(Sieve));

    // Set 0 and 1 as non-prime
    Sieve[0] = Sieve[1] = false;

    // Iterate over the range [2, lmt]
    for (int i = 2; i <= lmt; ++i) {

        // If i is a prime number
        if (Sieve[i] == true) {

            // Append i into prime
            prime.push_back(i);

            // Set all multiple of i non-prime
            for (int j = i * i; j <= lmt; j += i) {

                // Update Sieve[j]
                Sieve[j] = false;
            }
        }
    }
}

// Function to find all the prime numbers
// in the range [low, high]
vector<bool> SegmentedSieveFn(
    int low, int high)
{

    // Stores square root of high + 1
    int lmt = floor(sqrt(high)) + 1;

    // Stores all the prime numbers
    // in the range [1, lmt]
    vector<int> prime;

    // Find all the prime numbers in
    // the range [1, lmt]
    simpleSieve(lmt, prime);

    // Stores count of elements in
    // the range [low, high]
    int n = high - low + 1;

    // segmentedSieve[i]: Check if (i - low)
    // is a prime number or not
    vector<bool> segmentedSieve(n + 1, true);

    // Traverse the array prime[]
    for (int i = 0; i < prime.size(); i++) {

        // Store smallest multiple of prime[i]
        // in the range[low, high]
        int lowLim = floor(low / prime[i])
                     * prime[i];

        // If lowLim is less than low
        if (lowLim < low) {

            // Update lowLim
            lowLim += prime[i];
        }

        // Iterate over all multiples of prime[i]
        for (int j = lowLim; j <= high;
             j += prime[i]) {

            // If j not equal to prime[i]
            if (j != prime[i]) {

                // Update segmentedSieve[j - low]
                segmentedSieve[j - low] = false;
            }
        }
    }

    return segmentedSieve;
}

// Function to count the number of pairs
// in the range [L, R] whose sum is a
// prime number in the range [L, R]
int countPairsWhoseSumPrimeL_R(int L, int R)
{

    // segmentedSieve[i]: Check if (i - L)
    // is a prime number or not
    vector<bool> segmentedSieve
        = SegmentedSieveFn(L, R);

    // Stores count of pairs whose sum of
    // elements is a prime and in range [L, R]
    int cntPairs = 0;

    // Iterate over [L, R]
    for (int i = L; i <= R; i++) {

        // If (i - L) is a prime
        if (segmentedSieve[i - L]) {

            // Update cntPairs
            cntPairs += i / 2;
        }
    }
    return cntPairs;
}

// Driver Code
int main()
{
    int L = 1, R = 5;
    cout << countPairsWhoseSumPrimeL_R(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find all prime numbers in range
// [1, lmt] using sieve of Eratosthenes
static ArrayList<Integer> simpleSieve(int lmt,
       ArrayList<Integer> prime)
{

    // segmentedSieve[i]: Stores if i is
    // a prime number (True) or not (False)
    boolean[] Sieve = new boolean[lmt + 1];

    // Initialize all elements of
    // segmentedSieve[] to false
    Arrays.fill(Sieve, true);

    // Set 0 and 1 as non-prime
    Sieve[0] = Sieve[1] = false;

    // Iterate over the range [2, lmt]
    for(int i = 2; i <= lmt; ++i)
    {

        // If i is a prime number
        if (Sieve[i] == true)
        {

            // Append i into prime
            prime.add(i);

            // Set all multiple of i non-prime
            for(int j = i * i; j <= lmt; j += i)
            {

                // Update Sieve[j]
                Sieve[j] = false;
            }
        }
    }
    return prime;
}

// Function to find all the prime numbers
// in the range [low, high]
static boolean[] SegmentedSieveFn(int low, int high)
{

    // Stores square root of high + 1
    int lmt = (int)(Math.sqrt(high)) + 1;

    // Stores all the prime numbers
    // in the range [1, lmt]
    ArrayList<Integer> prime = new ArrayList<Integer>();

    // Find all the prime numbers in
    // the range [1, lmt]
    prime = simpleSieve(lmt, prime);

    // Stores count of elements in
    // the range [low, high]
    int n = high - low + 1;

    // segmentedSieve[i]: Check if (i - low)
    // is a prime number or not
    boolean[] segmentedSieve = new boolean[n + 1];
    Arrays.fill(segmentedSieve, true);

    // Traverse the array prime[]
    for(int i = 0; i < prime.size(); i++)
    {

        // Store smallest multiple of prime[i]
        // in the range[low, high]
        int lowLim = (int)(low / prime.get(i)) *
                                 prime.get(i);

        // If lowLim is less than low
        if (lowLim < low)
        {

            // Update lowLim
            lowLim += prime.get(i);
        }

        // Iterate over all multiples of prime[i]
        for(int j = lowLim; j <= high;
                j += prime.get(i))
        {

            // If j not equal to prime[i]
            if (j != prime.get(i))
            {

                // Update segmentedSieve[j - low]
                segmentedSieve[j - low] = false;
            }
        }
    }
    return segmentedSieve;
}

// Function to count the number of pairs
// in the range [L, R] whose sum is a
// prime number in the range [L, R]
static int countPairsWhoseSumPrimeL_R(int L, int R)
{

    // segmentedSieve[i]: Check if (i - L)
    // is a prime number or not
    boolean[] segmentedSieve = SegmentedSieveFn(L, R);

    // Stores count of pairs whose sum of
    // elements is a prime and in range [L, R]
    int cntPairs = 0;

    // Iterate over [L, R]
    for(int i = L; i <= R; i++)
    {

        // If (i - L) is a prime
        if (segmentedSieve[i - L])
        {

            // Update cntPairs
            cntPairs += i / 2;
        }
    }
    return cntPairs;
}

// Driver Code
public static void main(String[] args)
{
    int L = 1, R = 5;

    System.out.println(
        countPairsWhoseSumPrimeL_R(L, R));
}
}

// This code is contributed by akhilsaini
```

## 计算机编程语言

```
# Python program to implement
# the above approach
import math

# Function to find all prime numbers in range
# [1, lmt] using sieve of Eratosthenes
def simpleSieve(lmt, prime):

    # segmentedSieve[i]: Stores if i is
    # a prime number (True) or not (False)
    Sieve = [True] * (lmt + 1)

    # Set 0 and 1 as non-prime
    Sieve[0] = Sieve[1] = False

    # Iterate over the range [2, lmt]
    for i in range(2, lmt + 1):

        # If i is a prime number
        if (Sieve[i] == True):

            # Append i into prime
            prime.append(i)

            # Set all multiple of i non-prime
            for j in range(i * i,
              int(math.sqrt(lmt)) + 1, i):

                # Update Sieve[j]
                Sieve[j] = false

    return prime

# Function to find all the prime numbers
# in the range [low, high]
def SegmentedSieveFn(low, high):

    # Stores square root of high + 1
    lmt = int(math.sqrt(high)) + 1

    # Stores all the prime numbers
    # in the range [1, lmt]
    prime = []

    # Find all the prime numbers in
    # the range [1, lmt]
    prime = simpleSieve(lmt, prime)

    # Stores count of elements in
    # the range [low, high]
    n = high - low + 1

    # segmentedSieve[i]: Check if (i - low)
    # is a prime number or not
    segmentedSieve = [True] * (n + 1)

    # Traverse the array prime[]
    for i in range(0, len(prime)):

        # Store smallest multiple of prime[i]
        # in the range[low, high]
        lowLim = int(low // prime[i]) * prime[i]

        # If lowLim is less than low
        if (lowLim < low):

            # Update lowLim
            lowLim += prime[i]

            # Iterate over all multiples of prime[i]
            for j in range(lowLim, high + 1, prime[i]):

                # If j not equal to prime[i]
                if (j != prime[i]):

                    # Update segmentedSieve[j - low]
                    segmentedSieve[j - low] = False

    return segmentedSieve

# Function to count the number of pairs
# in the range [L, R] whose sum is a
# prime number in the range [L, R]
def countPairsWhoseSumPrimeL_R(L, R):

    # segmentedSieve[i]: Check if (i - L)
    #  is a prime number or not
    segmentedSieve = SegmentedSieveFn(L, R)

    # Stores count of pairs whose sum of
    # elements is a prime and in range [L, R]
    cntPairs = 0

    # Iterate over [L, R]
    for i in range(L, R + 1):

        # If (i - L) is a prime
        if (segmentedSieve[i - L] == True):

            # Update cntPairs
            cntPairs += i / 2

    return cntPairs

# Driver Code
if __name__ == '__main__':

    L = 1
    R = 5

    print(countPairsWhoseSumPrimeL_R(L, R))

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;

class GFG{

// Function to find all prime numbers in range
// [1, lmt] using sieve of Eratosthenes
static ArrayList simpleSieve(int lmt, ArrayList prime)
{

    // segmentedSieve[i]: Stores if i is
    // a prime number (True) or not (False)
    bool[] Sieve = new bool[lmt + 1];

    // Initialize all elements of
    // segmentedSieve[] to false
    Array.Fill(Sieve, true);

    // Set 0 and 1 as non-prime
    Sieve[0] = Sieve[1] = false;

    // Iterate over the range [2, lmt]
    for(int i = 2; i <= lmt; ++i)
    {

        // If i is a prime number
        if (Sieve[i] == true)
        {

            // Append i into prime
            prime.Add(i);

            // Set all multiple of i non-prime
            for(int j = i * i; j <= lmt; j += i)
            {

                // Update Sieve[j]
                Sieve[j] = false;
            }
        }
    }
    return prime;
}

// Function to find all the prime numbers
// in the range [low, high]
static bool[] SegmentedSieveFn(int low, int high)
{

    // Stores square root of high + 1
    int lmt = (int)(Math.Sqrt(high)) + 1;

    // Stores all the prime numbers
    // in the range [1, lmt]
    ArrayList prime = new ArrayList();

    // Find all the prime numbers in
    // the range [1, lmt]
    prime = simpleSieve(lmt, prime);

    // Stores count of elements in
    // the range [low, high]
    int n = high - low + 1;

    // segmentedSieve[i]: Check if (i - low)
    // is a prime number or not
    bool[] segmentedSieve = new bool[n + 1];
    Array.Fill(segmentedSieve, true);

    // Traverse the array prime[]
    for(int i = 0; i < prime.Count; i++)
    {

        // Store smallest multiple of prime[i]
        // in the range[low, high]
        int lowLim = (int)(low / (int)prime[i]) *
                     (int)prime[i];

        // If lowLim is less than low
        if (lowLim < low)
        {

            // Update lowLim
            lowLim += (int)prime[i];
        }

        // Iterate over all multiples of prime[i]
        for(int j = lowLim; j <= high;
                j += (int)prime[i])
        {

            // If j not equal to prime[i]
            if (j != (int)prime[i])
            {

                // Update segmentedSieve[j - low]
                segmentedSieve[j - low] = false;
            }
        }
    }
    return segmentedSieve;
}

// Function to count the number of pairs
// in the range [L, R] whose sum is a
// prime number in the range [L, R]
static int countPairsWhoseSumPrimeL_R(int L, int R)
{

    // segmentedSieve[i]: Check if (i - L)
    // is a prime number or not
    bool[] segmentedSieve = SegmentedSieveFn(L, R);

    // Stores count of pairs whose sum of
    // elements is a prime and in range [L, R]
    int cntPairs = 0;

    // Iterate over [L, R]
    for(int i = L; i <= R; i++)
    {

        // If (i - L) is a prime
        if (segmentedSieve[i - L])
        {

            // Update cntPairs
            cntPairs += i / 2;
        }
    }
    return cntPairs;
}

// Driver Code
public static void Main()
{
    int L = 1, R = 5;

    Console.Write(countPairsWhoseSumPrimeL_R(L, R));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find all prime numbers in range
// [1, lmt] using sieve of Eratosthenes
function simpleSieve(lmt, prime)
{

    // segmentedSieve[i]: Stores if i is
    // a prime number (True) or not (False)
    let Sieve = new Array(lmt + 1);

    // Initialize all elements of
    // segmentedSieve[] to false
    Sieve.fill(true)

    // Set 0 and 1 as non-prime
    Sieve[0] = Sieve[1] = false;

    // Iterate over the range [2, lmt]
    for (let i = 2; i <= lmt; ++i) {

        // If i is a prime number
        if (Sieve[i] == true) {

            // Append i into prime
            prime.push(i);

            // Set all multiple of i non-prime
            for (let j = i * i; j <= lmt; j += i) {

                // Update Sieve[j]
                Sieve[j] = false;
            }
        }
    }
}

// Function to find all the prime numbers
// in the range [low, high]
function SegmentedSieveFn(low, high)
{

    // Stores square root of high + 1
    let lmt = Math.floor(Math.sqrt(high)) + 1;

    // Stores all the prime numbers
    // in the range [1, lmt]
    let prime = new Array();

    // Find all the prime numbers in
    // the range [1, lmt]
    simpleSieve(lmt, prime);

    // Stores count of elements in
    // the range [low, high]
    let n = high - low + 1;

    // segmentedSieve[i]: Check if (i - low)
    // is a prime number or not
    let segmentedSieve = new Array(n + 1).fill(true);

    // Traverse the array prime[]
    for (let i = 0; i < prime.length; i++) {

        // Store smallest multiple of prime[i]
        // in the range[low, high]
        let lowLim = Math.floor(low / prime[i])
                     * prime[i];

        // If lowLim is less than low
        if (lowLim < low) {

            // Update lowLim
            lowLim += prime[i];
        }

        // Iterate over all multiples of prime[i]
        for (let j = lowLim; j <= high;
             j += prime[i]) {

            // If j not equal to prime[i]
            if (j != prime[i]) {

                // Update segmentedSieve[j - low]
                segmentedSieve[j - low] = false;
            }
        }
    }

    return segmentedSieve;
}

// Function to count the number of pairs
// in the range [L, R] whose sum is a
// prime number in the range [L, R]
function countPairsWhoseSumPrimeL_R(L, R)
{

    // segmentedSieve[i]: Check if (i - L)
    // is a prime number or not
    let segmentedSieve = SegmentedSieveFn(L, R);

    // Stores count of pairs whose sum of
    // elements is a prime and in range [L, R]
    let cntPairs = 0;

    // Iterate over [L, R]
    for (let i = L; i <= R; i++) {

        // If (i - L) is a prime
        if (segmentedSieve[i - L]) {

            // Update cntPairs
            cntPairs += Math.floor(i / 2);
        }
    }
    return cntPairs;
}

// Driver Code

    let L = 1, R = 5;
    document.write(countPairsWhoseSumPrimeL_R(L, R));

    // This code is contributed by gfgking

</script>
```

**Output:** 

```
4
```

***时间复杂度:**o((r-l+1)* log⁡(log⁡(r))+sqrt(r)* log⁡(log⁡(sqrt(r))*
***辅助空间:**o(r-l+1+sqrt(r))*