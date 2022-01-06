# 确定给定的数是否是超完美数

> 原文:[https://www . geesforgeks . org/decision-给定的数字是否是超完美的数字/](https://www.geeksforgeeks.org/determine-whether-a-given-number-is-a-hyperperfect-number/)

给定一个数，确定它是否是有效的[超完美数](https://en.wikipedia.org/wiki/Hyperperfect_number)。
一个数 n 被称为 k-超完美如果:**n = 1+k∑<sub>I</sub>d<sub>I</sub>T8【其中所有 d <sub>i</sub> 都是 n 的适当除数。
取 k = 1 会给我们[个完美的数](https://www.geeksforgeeks.org/perfect-number/)。
前几个 k-超完美数是 6，21，28，301，325，496，697，…对应的 k 值是 1，2，1，6，3，1，12，…**

**示例:**

```
Input :  N = 36, K = 1
Output :  34 is not 1-HyperPerfect
Explanation: 
The Divisors of 36 are 2, 3, 4, 6, 9, 12, 18
the sum of the divisors is 54\. 
For N = 36 to be 1-Hyperperfect, it would 
require 36 = 1 + 1(54), which we see, is
invalid

Input :  N = 325, K = 3
Output :  325 is 3-HyperPerfect
Explanation: 
We can use the first condition to evaluate this 
as K is odd and > 1 so here p = (3*k+1)/2 = 5, 
q = (3*k+4) = 13 p and q are both prime, so we 
compute p^2 * q = 5 ^ 2 * 13 = 325
Hence N is a valid HyperPerfect number
```

## C++

```
// C++ 4.3.2 program to check whether a
// given number is  k-hyperperfect
#include <bits/stdc++.h>
using namespace std;

// function to find the sum of all
// proper divisors (excluding 1 and N)
int divisorSum(int N, int K)
{
    int sum = 0;

    // Iterate only until sqrt N as we are
    // going to generate pairs to produce
    // divisors
    for (int i = 2 ; i <= ceil(sqrt(N)) ; i++)

        // As divisors occur in pairs, we can
        // take the values i and N/i as long
        // as i divides N
        if (N % i == 0)
            sum += ( i + N/i );

    return sum;
}

// Function to check whether the given number
// is prime
bool isPrime(int n)
{
    //base and corner cases
    if (n == 1 || n == 0)
        return false;

    if (n <= 3)
        return true;

    // Since integers can be represented as
    // some 6*k + y where y >= 0, we can eliminate
    // all integers that can be expressed in this
    // form
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // start from 5 as this is the next prime number
    for (int i=5; i*i<=n; i=i+6)
        if (n % i == 0 || n % ( i + 2 ) == 0)
            return false;

    return true;
}

// Returns true if N is a K-Hyperperfect number
// Else returns false.
bool isHyperPerfect(int N, int K)
{
    int sum = divisorSum(N, K);

    // Condition from the definition of hyperperfect
    if ((1 + K * (sum)) == N)
        return true;
    else
        return false;
}

// Driver function to test for hyperperfect numbers
int main()
{
    int N1 = 1570153, K1 = 12;
    int N2 = 321, K2 = 3;

    // First two statements test against the condition
    // N = 1 + K*(sum(proper divisors))
    if (isHyperPerfect(N1, K1))
        cout << N1 << " is " << K1
             <<"-HyperPerfect" << "\n";
    else
        cout << N1 << " is not " << K1
             <<"-HyperPerfect" << "\n";

    if (isHyperPerfect(N2, K2))
        cout << N2 << " is " << K2
             <<"-HyperPerfect" << "\n";
    else
        cout << N2 << " is not " << K2
             <<"-HyperPerfect" << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// whether a given number
// is k-hyperperfect
import java.io.*;

class GFG
{

// function to find the
// sum of all proper
// divisors (excluding
// 1 and N)
static int divisorSum(int N,
                      int K)
{
    int sum = 0;

    // Iterate only until
    // sqrt N as we are
    // going to generate
    // pairs to produce
    // divisors
    for (int i = 2 ;
             i <= Math.ceil(Math.sqrt(N));
             i++)

        // As divisors occur in
        // pairs, we can take
        // the values i and N/i
        // as long as i divides N
        if (N % i == 0)
            sum += (i + N / i);

    return sum;
}

// Function to check
// whether the given
// number is prime
static boolean isPrime(int n)
{
    // base and corner cases
    if (n == 1 || n == 0)
        return false;

    if (n <= 3)
        return true;

    // Since integers can be
    // represented as some
    // 6*k + y where y >= 0,
    // we can eliminate all
    // integers that can be
    // expressed in this form
    if (n % 2 == 0 ||
        n % 3 == 0)
        return false;

    // start from 5 as this
    // is the next prime number
    for (int i = 5;
             i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % ( i + 2 ) == 0)
            return false;

    return true;
}

// Returns true if N is
// a K-Hyperperfect number
// Else returns false.
static boolean isHyperPerfect(int N,
                              int K)
{
    int sum = divisorSum(N, K);

    // Condition from the
    // definition of hyperperfect
    if ((1 + K * (sum)) == N)
        return true;
    else
        return false;
}

// Driver Code
public static void main (String[] args)
{
    int N1 = 1570153, K1 = 12;
    int N2 = 321, K2 = 3;

    // First two statements test
    // against the condition
    // N = 1 + K*(sum(proper divisors))
    if (isHyperPerfect(N1, K1))
        System.out.println (N1 + " is " + K1 +
                            "-HyperPerfect" );
    else
        System.out.println(N1 + " is not " + K1 +
                               "-HyperPerfect" );

    if (isHyperPerfect(N2, K2))
        System.out.println( N2 + " is " + K2 +
                            "-HyperPerfect" );
    else
        System.out.println(N2 + " is not " + K2 +
                                "-HyperPerfect");
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 program to check whether a
# given number is  k-hyperperfect
import math

# Function to find the sum of all
# proper divisors (excluding 1 and N)
def divisorSum(N, K):

    Sum = 0

    # Iterate only until sqrt N as we are
    # going to generate pairs to produce
    # divisors
    for i in range(2, math.ceil(math.sqrt(N))):

        # As divisors occur in pairs, we can
        # take the values i and N/i as long
        # as i divides N
        if (N % i == 0):
            Sum += (i + int(N / i))

    return Sum

# Function to check whether the given
# number is prime
def isPrime(n):

    # Base and corner cases
    if (n == 1 or n == 0):
        return False

    if (n <= 3):
        return True

    # Since integers can be represented as
    # some 6*k + y where y >= 0, we can eliminate
    # all integers that can be expressed in this
    # form
    if (n % 2 == 0 or n % 3 == 0):
        return False

    # Start from 5 as this is the next
    # prime number
    i = 5
    while (i * i <= n):
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i += 6

    return True

# Returns true if N is a K-Hyperperfect
# number. Else returns false.
def isHyperPerfect(N, K):

    Sum = divisorSum(N, K)

    # Condition from the definition
    # of hyperperfect
    if ((1 + K * (Sum)) == N):
        return True
    else:
        return False

# Driver code
N1 = 1570153
K1 = 12
N2 = 321
K2 = 3

# First two statements test against the condition
# N = 1 + K*(sum(proper divisors))
if (isHyperPerfect(N1, K1)):
    print(N1, " is ", K1,
          "-HyperPerfect", sep = "")
else:
    print(N1, " is not ", K1,
          "-HyperPerfect", sep = "")

if (isHyperPerfect(N2, K2)):
    print(N2, " is ", K2,
          "-HyperPerfect", sep = "")
else:
    print(N2, " is not ", K2,
          "-HyperPerfect", sep = "")

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to check
// whether a given number
// is k-hyperperfect
using System;

class GFG
{

// function to find the
// sum of all proper
// divisors (excluding
// 1 and N)
static int divisorSum(int N,
                      int K)
{
    int sum = 0;

    // Iterate only until
    // sqrt N as we are
    // going to generate
    // pairs to produce
    // divisors
    for (int i = 2 ;
             i <= Math.Ceiling(Math.Sqrt(N));
             i++)

        // As divisors occur in
        // pairs, we can take
        // the values i and N/i
        // as long as i divides N
        if (N % i == 0)
            sum += (i + N / i);

    return sum;
}

// Function to check
// whether the given
// number is prime
static bool isPrime(int n)
{
    // base and corner cases
    if (n == 1 || n == 0)
        return false;

    if (n <= 3)
        return true;

    // Since integers can be
    // represented as some
    // 6*k + y where y >= 0,
    // we can eliminate all
    // integers that can be
    // expressed in this form
    if (n % 2 == 0 ||
        n % 3 == 0)
        return false;

    // start from 5 as this
    // is the next prime number
    for (int i = 5;
            i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % ( i + 2 ) == 0)
            return false;

    return true;
}

// Returns true if N is
// a K-Hyperperfect number
// Else returns false.
static bool isHyperPerfect(int N,
                           int K)
{
    int sum = divisorSum(N, K);

    // Condition from the
    // definition of hyperperfect
    if ((1 + K * (sum)) == N)
        return true;
    else
        return false;
}

// Driver Code
static public void Main ()
{

int N1 = 1570153, K1 = 12;
int N2 = 321, K2 = 3;

// First two statements
// test against the 
// condition N = 1 + K*
// (sum(proper divisors))
if (isHyperPerfect(N1, K1))
    Console.WriteLine(N1 + " is " + K1 +
                      "-HyperPerfect" );
else
    Console.WriteLine(N1 + " is not " + K1 +
                          "-HyperPerfect" );

if (isHyperPerfect(N2, K2))
    Console.WriteLine( N2 + " is " + K2 +
                       "-HyperPerfect" );
else
    Console.WriteLine(N2 + " is not " + K2 +
                           "-HyperPerfect");
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP 4.3.2 program to check
// whether a given number is
// k-hyperperfect

// function to find the sum
// of all proper divisors
// (excluding 1 and N)
function divisorSum($N, $K)
{
    $sum = 0;

    // Iterate only until
    // sqrt N as we are
    // going to generate
    // pairs to produce
    // divisors
    for ($i = 2 ;
         $i <= ceil(sqrt($N)) ; $i++)

        // As divisors occur in
        // pairs, we can take the
        // values i and N/i as long
        // as i divides N
        if ($N % $i == 0)
            $sum += ( $i + $N / $i);

    return $sum;
}

// Function to check whether
// the given number is prime
function isPrime($n)
{
    // base and corner cases
    if ($n == 1 || $n == 0)
        return false;

    if ($n <= 3)
        return true;

    // Since integers can be
    // represented as some 6*k + y
    // where y >= 0, we can
    // eliminate all integers that
    // can be expressed in this form
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    // start from 5 as this
    // is the next prime number
    for ($i = 5;
         $i * $i <= $n; $i = $i + 6)
        if ($n % $i == 0 ||
            $n % ($i + 2) == 0)
            return false;

    return true;
}

// Returns true if N is a
// K-Hyperperfect number
// Else returns false.
function isHyperPerfect($N, $K)
{
    $sum = divisorSum($N, $K);

    // Condition from the
    // definition of hyperperfect
    if ((1 + $K * ($sum)) == $N)
        return true;
    else
        return false;
}

// Driver Code
$N1 = 1570153;
$K1 = 12;
$N2 = 321;
$K2 = 3;

// First two statements test
// against the condition
// N = 1 + K*(sum(proper divisors))
if (isHyperPerfect($N1, $K1))
    echo $N1 , " is " , $K1,
           "-HyperPerfect" , "\n";
else
    echo $N1 , " is not " , $K1,
         "-HyperPerfect" , "\n";

if (isHyperPerfect($N2, $K2))
    echo $N2 , " is " , K2,
          "-HyperPerfect" , "\n";
else
    echo $N2 , " is not " , $K2 ,
          "-HyperPerfect" , "\n";

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to check
// whether a given number
// is k-hyperperfect

// Function to find the
// sum of all proper
// divisors (excluding
// 1 and N)
function divisorSum(N, K)
{
    let sum = 0;

    // Iterate only until sqrt N as
    // we are going to generate
    // pairs to produce divisors
    for(let i = 2;
            i <= Math.ceil(Math.sqrt(N));
            i++)

        // As divisors occur in
        // pairs, we can take
        // the values i and N/i
        // as long as i divides N
        if (N % i == 0)
            sum += (i + parseInt(N / i, 10));

    return sum;
}

// Function to check
// whether the given
// number is prime
function isPrime(n)
{

    // base and corner cases
    if (n == 1 || n == 0)
        return false;

    if (n <= 3)
        return true;

    // Since integers can be
    // represented as some
    // 6*k + y where y >= 0,
    // we can eliminate all
    // integers that can be
    // expressed in this form
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    // Start from 5 as this
    // is the next prime number
    for(let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Returns true if N is
// a K-Hyperperfect number
// Else returns false.
function isHyperPerfect(N, K)
{
    let sum = divisorSum(N, K);

    // Condition from the
    // definition of hyperperfect
    if ((1 + K * (sum)) == N)
        return true;
    else
        return false;
}

// Driver code
let N1 = 1570153, K1 = 12;
let N2 = 321, K2 = 3;

// First two statements
// test against the
// condition N = 1 + K*
// (sum(proper divisors))
if (isHyperPerfect(N1, K1))
    document.write(N1 + " is " + K1 +
               "-HyperPerfect" + "</br>");
else
    document.write(N1 + " is not " + K1 +
                   "-HyperPerfect" + "</br>");

if (isHyperPerfect(N2, K2))
    document.write(N2 + " is " + K2 +
               "-HyperPerfect" + "</br>");
else
    document.write(N2 + " is not " + K2 +
                   "-HyperPerfect" + "</br>");

// This code is contributed by decode2207

</script>
```

**输出:**

```
1570153 is 12-HyperPerfect
321 is not 3-HyperPerfect
```

给定 k，我们可以在特殊情况下执行一些检查，以确定该数字是否是超完美的:

1.  如果 **K > 1 和 K 是奇数**，那么让 **p = (3*k+1)/2 和 q = 3*k+4** 。如果 p 和 q 是素数，那么 **p <sup>2</sup> q** 就是 k-超完美
2.  如果 p 和 q 是**不同的奇素数**使得**K(p+q)= pq–1**对于 K 的某个正积分值，那么 **pq** 就是 K-超完美的

**参考:**T2[https://en.wikipedia.org/wiki/Hyperperfect_number](https://en.wikipedia.org/wiki/Hyperperfect_number)

本文由 **Deepak Srivatsav** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。