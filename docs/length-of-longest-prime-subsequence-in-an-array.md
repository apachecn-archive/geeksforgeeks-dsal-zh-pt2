# 数组中最长素子序列的长度

> 原文:[https://www . geesforgeks . org/最长素子序列数组长度/](https://www.geeksforgeeks.org/length-of-longest-prime-subsequence-in-an-array/)

给定一个包含非负整数的数组 **arr** ，任务是打印数组中[素数](https://www.geeksforgeeks.org/prime-numbers/)的最长子序列的长度。
**例:**

> **输入:** arr[] = { 3，4，11，2，9，21 }
> **输出:** 3
> 最长素子序列是{ 3，2，11}，因此答案是 3。
> **输入:** arr[] = { 6，4，10，13，9，25 }
> **输出:** 1

**进场:**

*   遍历给定的数组。
*   对于数组中的每个元素，[检查它是否是质数](https://www.geeksforgeeks.org/prime-numbers/)。
*   如果元素是素的，它将在最长素子序列中。因此，将最长素子序列所需的长度增加 1

以下是上述方法的实现:

## C++

```
// C++ program to find the length of
// Longest Prime Subsequence in an Array

#include <bits/stdc++.h>
using namespace std;
#define N 100005

// Function to create Sieve
// to check primes
void SieveOfEratosthenes(
    bool prime[], int p_size)
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
                 i <= p_size;
                 i += p)
                prime[i] = false;
        }
    }
}

// Function to find the longest subsequence
// which contain all prime numbers
int longestPrimeSubsequence(int arr[], int n)
{
    bool prime[N + 1];
    memset(prime, true, sizeof(prime));

    // Precompute N primes
    SieveOfEratosthenes(prime, N);

    int answer = 0;

    // Find the length of
    // longest prime subsequence
    for (int i = 0; i < n; i++) {
        if (prime[arr[i]]) {
            answer++;
        }
    }

    return answer;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 11, 2, 9, 21 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << longestPrimeSubsequence(arr, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of
// Longest Prime Subsequence in an Array
import java.util.*;

class GFG
{
static final int N = 100005;

// Function to create Sieve
// to check primes
static void SieveOfEratosthenes(
    boolean prime[], int p_size)
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
                 i <= p_size;
                 i += p)
                prime[i] = false;
        }
    }
}

// Function to find the longest subsequence
// which contain all prime numbers
static int longestPrimeSubsequence(int arr[], int n)
{
    boolean []prime = new boolean[N + 1];
    Arrays.fill(prime, true);

    // Precompute N primes
    SieveOfEratosthenes(prime, N);

    int answer = 0;

    // Find the length of
    // longest prime subsequence
    for (int i = 0; i < n; i++) {
        if (prime[arr[i]]) {
            answer++;
        }
    }

    return answer;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 4, 11, 2, 9, 21 };
    int n = arr.length;

    // Function call
    System.out.print(longestPrimeSubsequence(arr, n)
         +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find the length of
# Longest Prime Subsequence in an Array
N = 100005

# Function to create Sieve
# to check primes
def SieveOfEratosthenes(prime,  p_size):

    # False here indicates
    # that it is not prime
    prime[0] = False
    prime[1] = False

    p = 2
    while  p * p <= p_size:

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p,
            # set them to non-prime
            for i in range( p * 2, p_size + 1, p):
                prime[i] = False

        p += 1

# Function to find the longest subsequence
# which contain all prime numbers
def longestPrimeSubsequence( arr, n):
    prime = [True]*(N + 1)

    # Precompute N primes
    SieveOfEratosthenes(prime, N)

    answer = 0

    # Find the length of
    # longest prime subsequence
    for i in range (n):
        if (prime[arr[i]]):
            answer += 1

    return answer

# Driver code
if __name__ == "__main__":
    arr = [ 3, 4, 11, 2, 9, 21 ]
    n = len(arr)

    # Function call
    print (longestPrimeSubsequence(arr, n))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the length of
// longest Prime Subsequence in an Array
using System;

class GFG
{
static readonly int N = 100005;

// Function to create Sieve
// to check primes
static void SieveOfEratosthenes(
    bool []prime, int p_size)
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
                 i <= p_size;
                 i += p)
                prime[i] = false;
        }
    }
}

// Function to find the longest subsequence
// which contain all prime numbers
static int longestPrimeSubsequence(int []arr, int n)
{
    bool []prime = new bool[N + 1];
    for (int i = 0; i < N+1; i++)
        prime[i] = true;

    // Precompute N primes
    SieveOfEratosthenes(prime, N);

    int answer = 0;

    // Find the length of
    // longest prime subsequence
    for (int i = 0; i < n; i++) {
        if (prime[arr[i]]) {
            answer++;
        }
    }

    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 4, 11, 2, 9, 21 };
    int n = arr.Length;

    // Function call
    Console.Write(longestPrimeSubsequence(arr, n)
         +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the length of
// Longest Prime Subsequence in an Array

let N = 100005

// Function to create Sieve
// to check primes
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
                i <= p_size;
                i += p)
                prime[i] = false;
        }
    }
}

// Function to find the longest subsequence
// which contain all prime numbers
function longestPrimeSubsequence(arr, n)
{
    let prime = new Array(N + 1);
    prime.fill(true)

    // Precompute N primes
    SieveOfEratosthenes(prime, N);

    let answer = 0;

    // Find the length of
    // longest prime subsequence
    for (let i = 0; i < n; i++) {
        if (prime[arr[i]]) {
            answer++;
        }
    }

    return answer;
}

// Driver code

let arr = [ 3, 4, 11, 2, 9, 21 ];
let n = arr.length

// Function call
document.write(longestPrimeSubsequence(arr, n) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output**

```
3
```

**时间复杂度:O(N log (log N))**

**辅助空间:O(N)**