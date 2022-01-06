# 素数和在[1，N]

范围内的半素数的无序对的计数

> 原文:[https://www . geeksforgeeks . org/1-n 范围内带素数和的无序半素数对的计数/](https://www.geeksforgeeks.org/count-of-unordered-pairs-of-semi-prime-numbers-with-prime-sum-in-range-1-n/)

给定一个正整数 **N** ，任务是在范围**【1，N】**内寻找[半素数](https://www.geeksforgeeks.org/check-whether-number-semiprime-not/)的无序对的个数，使得它们的和为[素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。

**示例:**

> **输入:** N = 25
> **输出:** 5
> **解释:**
> 和也是素数的半素数的有效对是(10，21)、(14，15)、(15，22)、(20，21)和(21，22)。这样的数字是 5。
> 
> **输入:**N = 100
> T3】输出: 313

**方法:**给定的问题可以用厄拉多塞的[筛解决。可以创建一个](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[数组](https://www.geeksforgeeks.org/array-data-structure/) **质数[]** ，其中**质数[i]** 使用筛子存储数字的[不同质数因子](https://www.geeksforgeeks.org/number-of-distinct-prime-factors-of-first-n-natural-numbers/)。具有 2 个不同质因数的[1，N]范围内的所有数字可以存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **半质数**中。此后，迭代向量的所有无序对**半素数**，并用[素数](https://www.geeksforgeeks.org/tag/prime-number/)和保持对的计数。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

const int maxn = 100000;

// Stores the count of distinct prime
// number in factor of current number
int prime[maxn] = {};

// Function to return the vector of
// semi prime numbers in range [1, N]
vector<int> semiPrimes(int N)
{
    // Count of distinct prime number
    // in the factor of current number
    // using Sieve of Eratosthenes
    for (int p = 2; p <= maxn; p++) {

        // If current number is prime
        if (prime[p] == 0) {
            for (int i = 2 * p; i <= maxn; i += p)
                prime[i]++;
        }
    }

    // Stores the semi prime numbers
    vector<int> sPrimes;

    for (int p = 2; p <= N; p++)

        // If p has 2 distinct prime factors
        if (prime[p] == 2)
            sPrimes.push_back(p);

    // Return vector
    return sPrimes;
}

// Function to count unordered pairs of
// semi prime numbers with prime sum
int countPairs(vector<int> semiPrimes)
{
    // Stores the final count
    int cnt = 0;

    // Loop to iterate over al the
    // l unordered pairs
    for (int i = 0;
         i < semiPrimes.size(); i++) {
        for (int j = i + 1;
             j < semiPrimes.size(); j++) {

            // If sum of current semi prime
            // numbers is a prime number
            if (prime[semiPrimes[i]
                      + semiPrimes[j]]
                == 0) {
                cnt++;
            }
        }
    }

    // Return answer
    return cnt;
}

// Driver Code
int main()
{
    int N = 100;
    cout << countPairs(semiPrimes(N));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{
    static int maxn = 100000;

    // Stores the count of distinct prime
    // number in factor of current number
    static int[] prime = new int[maxn + 1];

    // Function to return the vector of
    // semi prime numbers in range [1, N]
    static ArrayList<Integer> semiPrimes(int N)
    {

        // Count of distinct prime number
        // in the factor of current number
        // using Sieve of Eratosthenes
        for (int p = 2; p <= maxn; p++) {

            // If current number is prime
            if (prime[p] == 0) {
                for (int i = 2 * p; i <= maxn; i += p)
                    prime[i]++;
            }
        }

        // Stores the semi prime numbers
        ArrayList<Integer> sPrimes
            = new ArrayList<Integer>();

        for (int p = 2; p <= N; p++)

            // If p has 2 distinct prime factors
            if (prime[p] == 2)
                sPrimes.add(p);

        // Return vector
        return sPrimes;
    }

    // Function to count unordered pairs of
    // semi prime numbers with prime sum
    static int countPairs(ArrayList<Integer> semiPrimes)
    {

        // Stores the final count
        int cnt = 0;

        // Loop to iterate over al the
        // l unordered pairs
        for (int i = 0; i < semiPrimes.size(); i++) {
            for (int j = i + 1; j < semiPrimes.size(); j++) {

                // If sum of current semi prime
                // numbers is a prime number
                if (prime[semiPrimes.get(i) + semiPrimes.get(j)] == 0) {
                    cnt++;
                }
            }
        }

        // Return answer
        return cnt;
    }

// Driver Code
public static void main(String[] args)
{
    int N = 100;
    System.out.print(countPairs(semiPrimes(N)));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# python program of the above approach

maxn = 100000

# Stores the count of distinct prime
# number in factor of current number
prime = [0 for _ in range(maxn)]

# Function to return the vector of
# semi prime numbers in range [1, N]

def semiPrimes(N):

    # Count of distinct prime number
    # in the factor of current number
    # using Sieve of Eratosthenes
    for p in range(2, maxn):

        # If current number is prime
        if (prime[p] == 0):
            for i in range(2*p, maxn, p):
                prime[i] += 1

    # Stores the semi prime numbers
    sPrimes = []

    for p in range(2, N+1):

        # If p has 2 distinct prime factors
        if (prime[p] == 2):
            sPrimes.append(p)

    # Return vector
    return sPrimes

# Function to count unordered pairs of
# semi prime numbers with prime sum
def countPairs(semiPrimes):

    # Stores the final count
    cnt = 0

    # Loop to iterate over al the
    # l unordered pairs
    for i in range(0, len(semiPrimes)):
        for j in range(i+1, len(semiPrimes)):

            # If sum of current semi prime
            # numbers is a prime number
            if (prime[semiPrimes[i] + semiPrimes[j]] == 0):
                cnt += 1

    # Return answer
    return cnt

# Driver Code
if __name__ == "__main__":

    N = 100
    print(countPairs(semiPrimes(N)))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program of the above approach
using System;
using System.Collections.Generic;
class GFG {
    const int maxn = 100000;

    // Stores the count of distinct prime
    // number in factor of current number
    static int[] prime = new int[maxn + 1];

    // Function to return the vector of
    // semi prime numbers in range [1, N]
    static List<int> semiPrimes(int N)
    {
        // Count of distinct prime number
        // in the factor of current number
        // using Sieve of Eratosthenes
        for (int p = 2; p <= maxn; p++) {

            // If current number is prime
            if (prime[p] == 0) {
                for (int i = 2 * p; i <= maxn; i += p)
                    prime[i]++;
            }
        }

        // Stores the semi prime numbers
        List<int> sPrimes = new List<int>();

        for (int p = 2; p <= N; p++)

            // If p has 2 distinct prime factors
            if (prime[p] == 2)
                sPrimes.Add(p);

        // Return vector
        return sPrimes;
    }

    // Function to count unordered pairs of
    // semi prime numbers with prime sum
    static int countPairs(List<int> semiPrimes)
    {
        // Stores the final count
        int cnt = 0;

        // Loop to iterate over al the
        // l unordered pairs
        for (int i = 0; i < semiPrimes.Count; i++) {
            for (int j = i + 1; j < semiPrimes.Count; j++) {

                // If sum of current semi prime
                // numbers is a prime number
                if (prime[semiPrimes[i] + semiPrimes[j]]
                    == 0) {
                    cnt++;
                }
            }
        }

        // Return answer
        return cnt;
    }

    // Driver Code
    public static void Main()
    {
        int N = 100;
        Console.WriteLine(countPairs(semiPrimes(N)));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        const maxn = 100000;

        // Stores the count of distinct prime
        // number in factor of current number
        let prime = new Array(maxn).fill(0);

        // Function to return the vector of
        // semi prime numbers in range [1, N]
        function semiPrimes(N) {
            // Count of distinct prime number
            // in the factor of current number
            // using Sieve of Eratosthenes
            for (let p = 2; p <= maxn; p++) {

                // If current number is prime
                if (prime[p] == 0) {
                    for (let i = 2 * p; i <= maxn; i += p)
                        prime[i]++;
                }
            }

            // Stores the semi prime numbers
            let sPrimes = [];

            for (let p = 2; p <= N; p++)

                // If p has 2 distinct prime factors
                if (prime[p] == 2)
                    sPrimes.push(p);

            // Return vector
            return sPrimes;
        }

        // Function to count unordered pairs of
        // semi prime numbers with prime sum
        function countPairs(semiPrimes) {
            // Stores the final count
            let cnt = 0;

            // Loop to iterate over al the
            // l unordered pairs
            for (let i = 0;
                i < semiPrimes.length; i++) {
                for (let j = i + 1;
                    j < semiPrimes.length; j++) {

                    // If sum of current semi prime
                    // numbers is a prime number
                    if (prime[semiPrimes[i]
                        + semiPrimes[j]]
                        == 0) {
                        cnt++;
                    }
                }
            }

            // Return answer
            return cnt;
        }

        // Driver Code

        let N = 100;
        document.write(countPairs(semiPrimes(N)));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
313
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*