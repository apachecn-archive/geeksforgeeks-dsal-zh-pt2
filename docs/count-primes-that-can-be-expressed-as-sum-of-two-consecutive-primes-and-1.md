# 计数可以表示为两个连续素数和 1 的和的素数

> 原文:[https://www . geesforgeks . org/count-primes-可以表示为两个连续的 primes-and-1 的和/](https://www.geeksforgeeks.org/count-primes-that-can-be-expressed-as-sum-of-two-consecutive-primes-and-1/)

给定一个数字 **N** 。任务是统计从 **2** 到 **N** 的质数，可以表示为两个连续质数和 1 的和。
**举例:**

> **输入:** N = 27
> **输出:** 2
> 13 = 5 + 7 + 1 和 19 = 7 + 11 + 1 是所需的素数。
> **输入:** N = 34
> **输出:** 3
> 13 = 5 + 7 + 1，19 = 7 + 11 + 1 和 31 = 13 + 17 + 1。

**方法:**一个有效的方法是使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)找到 N 以内的所有素数，并将所有素数放在一个向量中。现在，运行一个简单的循环，添加两个连续的素数和 1，然后检查这个和是否也是素数。如果是，则增加计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100005

// To check if a number is prime or not
bool isprime[N];

// To store possible numbers
bool can[N];

// Function to return all prime numbers
vector<int> SieveOfEratosthenes()
{

    memset(isprime, true, sizeof(isprime));

    for (int p = 2; p * p < N; p++) {

        // If prime[p] is not changed, then it is a prime
        if (isprime[p] == true) {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < N; i += p)
                isprime[i] = false;
        }
    }

    vector<int> primes;
    for (int i = 2; i < N; i++)
        if (isprime[i])
            primes.push_back(i);

    return primes;
}

// Function to count all possible prime numbers that can be
// expressed as the sum of two consecutive primes and one
int Prime_Numbers(int n)
{
    vector<int> primes = SieveOfEratosthenes();

    // All possible prime numbers below N
    for (int i = 0; i < (int)(primes.size()) - 1; i++)
        if (primes[i] + primes[i + 1] + 1 < N)
            can[primes[i] + primes[i + 1] + 1] = true;

    int ans = 0;
    for (int i = 2; i <= n; i++) {
        if (can[i] and isprime[i]) {
            ans++;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int n = 50;
    cout << Prime_Numbers(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GfG
{

static int N = 100005;

// To check if a number is prime or not
static boolean isprime[] = new boolean[N];

// To store possible numbers
static boolean can[] = new boolean[N];

// Function to return all prime numbers
static ArrayList<Integer>SieveOfEratosthenes()
{

    for(int a = 0 ; a < isprime.length; a++)
    {
        isprime[a] = true;
    }
    for (int p = 2; p * p < N; p++)
    {

        // If prime[p] is not changed, then it is a prime
        if (isprime[p] == true)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < N; i += p)
                isprime[i] = false;
        }
    }

    ArrayList<Integer> primes = new ArrayList<Integer> ();
    for (int i = 2; i < N; i++)
        if (isprime[i])
            primes.add(i);

    return primes;
}

// Function to count all possible prime numbers that can be
// expressed as the sum of two consecutive primes and one
static int Prime_Numbers(int n)
{
    ArrayList<Integer> primes = SieveOfEratosthenes();

    // All possible prime numbers below N
    for (int i = 0; i < (int)(primes.size()) - 1; i++)
        if (primes.get(i) + primes.get(i + 1) + 1 < N)
            can[primes.get(i) + primes.get(i + 1) + 1] = true;

    int ans = 0;
    for (int i = 2; i <= n; i++)
    {
        if (can[i] && isprime[i] == true)
        {
            ans++;
        }
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 50;
    System.out.println(Prime_Numbers(n));
}
}

// This code is contributed by
// Prerna Saini.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt;

N = 100005;

# To check if a number is prime or not
isprime = [True] * N;

# To store possible numbers
can = [False] * N;

# Function to return all prime numbers
def SieveOfEratosthenes() :

    for p in range(2, int(sqrt(N)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if (isprime[p] == True) :

            # Update all multiples of p greater
            # than or equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(p * p, N , p) :
                isprime[i] = False;

    primes = [];
    for i in range(2, N) :
        if (isprime[i]):
            primes.append(i);

    return primes;

# Function to count all possible prime numbers
# that can be expressed as the sum of two
# consecutive primes and one
def Prime_Numbers(n) :

    primes = SieveOfEratosthenes();

    # All possible prime numbers below N
    for i in range(len(primes) - 1) :
        if (primes[i] + primes[i + 1] + 1 < N) :
            can[primes[i] + primes[i + 1] + 1] = True;

    ans = 0;
    for i in range(2, n + 1) :
        if (can[i] and isprime[i]) :
            ans += 1;

    return ans;

# Driver code
if __name__ == "__main__" :

    n = 50;
    print(Prime_Numbers(n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GfG
{

static int N = 100005;

// To check if a number is prime or not
static bool[] isprime = new bool[N];

// To store possible numbers
static bool[] can = new bool[N];

// Function to return all prime numbers
static ArrayList SieveOfEratosthenes()
{

    for(int a = 0 ; a < N; a++)
    {
        isprime[a] = true;
    }
    for (int p = 2; p * p < N; p++)
    {

        // If prime[p] is not changed, then it is a prime
        if (isprime[p] == true)
        {

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < N; i += p)
                isprime[i] = false;
        }
    }

    ArrayList primes = new ArrayList();
    for (int i = 2; i < N; i++)
        if (isprime[i])
            primes.Add(i);

    return primes;
}

// Function to count all possible prime numbers that can be
// expressed as the sum of two consecutive primes and one
static int Prime_Numbers(int n)
{
    ArrayList primes = SieveOfEratosthenes();

    // All possible prime numbers below N
    for (int i = 0; i < primes.Count - 1; i++)
        if ((int)primes[i] + (int)primes[i + 1] + 1 < N)
            can[(int)primes[i] + (int)primes[i + 1] + 1] = true;

    int ans = 0;
    for (int i = 2; i <= n; i++)
    {
        if (can[i] && isprime[i] == true)
        {
            ans++;
        }
    }

    return ans;
}

// Driver code
static void Main()
{
    int n = 50;
    Console.WriteLine(Prime_Numbers(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$N = 10005;

// To check if a number is prime or not
$isprime = array_fill(0, $N, true);

// To store possible numbers
$can = array_fill(0, $N, false);

// Function to return all prime numbers
function SieveOfEratosthenes()
{
    global $N, $isprime;

    for ($p = 2; $p * $p < $N; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($isprime[$p] == true)
        {

            // Update all multiples of p greater
            // than or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for ($i = $p * $p; $i < $N; $i += $p)
                $isprime[$i] = false;
        }
    }

    $primes = array();
    for ($i = 2; $i < $N; $i++)
        if ($isprime[$i])
            array_push($primes, $i);

    return $primes;
}

// Function to count all possible prime numbers
// that can be expressed as the sum of two
// consecutive primes and one
function Prime_Numbers($n)
{
    global $N, $can, $isprime;
    $primes = SieveOfEratosthenes();

    // All possible prime numbers below N
    for ($i = 0; $i < count($primes) - 1; $i++)
        if ($primes[$i] + $primes[$i + 1] + 1 < $N)
            $can[$primes[$i] + $primes[$i + 1] + 1] = true;

    $ans = 0;
    for ($i = 2; $i <= $n; $i++)
    {
        if ($can[$i] and $isprime[$i])
        {
            $ans++;
        }
    }

    return $ans;
}

// Driver code
$n = 50;
echo Prime_Numbers($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
let N = 10005;

// To check if a number is prime or not
let isprime = new Array(N).fill(true);

// To store possible numbers
let can = new Array(N).fill(false);

// Function to return all prime numbers
function SieveOfEratosthenes()
{

    for (let p = 2; p * p < N; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (isprime[p] == true)
        {

            // Update all multiples of p greater
            // than or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (let i = p * p; i < N; i += p)
                isprime[i] = false;
        }
    }

    let primes = new Array();
    for (let i = 2; i < N; i++)
        if (isprime[i])
            primes.push(i);

    return primes;
}

// Function to count all possible prime numbers
// that can be expressed as the sum of two
// consecutive primes and one
function Prime_Numbers(n)
{
    let primes = SieveOfEratosthenes();

    // All possible prime numbers below N
    for (let i = 0; i < primes.length - 1; i++)
        if (primes[i] + primes[i + 1] + 1 < N)
            can[primes[i] + primes[i + 1] + 1] = true;

    let ans = 0;
    for (let i = 2; i <= n; i++)
    {
        if (can[i] && isprime[i])
        {
            ans++;
        }
    }

    return ans;
}

// Driver code
let n = 50;
document.write(Prime_Numbers(n));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N log (log N))

**辅助空间:** O(100005)