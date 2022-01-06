# 查找从 1 到 N 的几乎素数的计数

> 原文:[https://www . geesforgeks . org/find-count-of-near-质数-从-1 到-n/](https://www.geeksforgeeks.org/find-count-of-almost-prime-numbers-from-1-to-n/)

给定一个数 n，求从 1 到![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")的几乎素数。如果一个数恰好有两个不同的质因数，它就被称为几乎。
**注**:数字可以有任意数量的非质因数，但应该正好有两个质因数。
**例** :

```
Input : N = 10
Output : 2
Explanation : 6, 10 are such numbers.

Input : N = 21
Output : 8
```

一个有效的解决方案是使用厄拉多塞的[筛来寻找素数。对于小于 n 的数
和**找到不同的质因数请参考** :](https://write.geeksforgeeks.org/improve/beginning-java-programming-with-hello-world-example-6/) [几乎质数](https://www.geeksforgeeks.org/almost-prime-numbers/)
以下是上述方法的实现:

## C++

```
// CPP program to count almost prime numbers
// from 1 to n
#include <bits/stdc++.h>
using namespace std;
#define N 100005

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
bool prime[N];

void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));
    prime[1] = false;

    for (int p = 2; p * p < N; p++) {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (int i = p * 2; i < N; i += p)
                prime[i] = false;
        }
    }
}

// Function to count almost prime numbers
// from 1 to n
int almostPrimes(int n)
{
    // to store required answer
    int ans = 0;

    // 6 is first almost prime number
    for (int i = 6; i <= n; i++) {
        // to count prime factors
        int c = 0;
        for (int j = 2; j * j <= i; j++) {
            if (i % j == 0) {
                // if it is perfect square
                if (j * j == i) {
                    if (prime[j])
                        c++;
                }
                else {
                    if (prime[j])
                        c++;
                    if (prime[i / j])
                        c++;
                }
            }
        }

        // if I is almost prime number
        if (c == 2)
            ans++;
    }
    return ans;
}

// Driver code
int main()
{
    SieveOfEratosthenes();
    int n = 21;

    cout << almostPrimes(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count almost prime numbers
// from 1 to n

import java.io.*;

class GFG {

static int N = 100005;

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
static boolean prime[] = new boolean[N];
static void SieveOfEratosthenes()
{
    for(int i=0;i<N;i++)
    prime[i] =true;
    prime[1] = false;

    for (int p = 2; p * p < N; p++) {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (int i = p * 2; i < N; i += p)
                prime[i] = false;
        }
    }
}

// Function to count almost prime numbers
// from 1 to n
static int almostPrimes(int n)
{
    // to store required answer
    int ans = 0;

    // 6 is first almost prime number
    for (int i = 6; i <= n; i++) {
        // to count prime factors
        int c = 0;
        for (int j = 2; j * j <= i; j++) {
            if (i % j == 0) {
                // if it is perfect square
                if (j * j == i) {
                    if (prime[j])
                        c++;
                }
                else {
                    if (prime[j])
                        c++;
                    if (prime[i / j])
                        c++;
                }
            }
        }

        // if I is almost prime number
        if (c == 2)
            ans++;
    }
    return ans;
}

// Driver code

    public static void main (String[] args) {
        SieveOfEratosthenes();
    int n = 21;

    System.out.println( almostPrimes(n));
    }
}
//This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python 3 program to count almost
# prime numbers
# from 1 to n

# from math import everything
from math import *

N = 100005

# Create a boolean array "prime[0..n]"
# and initialize all entries it as true.
# A value in prime[i] will
# finally be false if i is Not a prime, else true.
prime = [True] * N

def SieveOfEratosthenes() :

    prime[1] = False

    for p in range(2, int(sqrt(N))) :

        # If prime[p] is not changed, then
        # it is a prime
        if prime[p] == True :

            # Update all multiples of p
            for i in range(2*p, N, p) :
                prime[i] = False

# Function to count almost prime numbers
# from 1 to n
def almostPrimes(n) :

    # to store required answer
    ans = 0

    # 6 is first almost prime number
    for i in range(6, n + 1) :

        # to count prime factors
        c = 0
        for j in range(2, int(sqrt(i)) + 1) :

            # if it is perfect square
            if i % j == 0 :

                if j * j == i :
                    if prime[j] :
                        c += 1
                else :
                    if prime[j] :
                        c += 1
                    if prime[i // j] :
                        c += 1

        # if I is almost prime number
        if c == 2 :
            ans += 1

    return ans

# Driver Code
if __name__ == "__main__" :

    SieveOfEratosthenes()
    n = 21

    print(almostPrimes(n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to count almost
// prime numbers from 1 to n
using System;

class GFG
{

static int N = 100005;

// Create a boolean array "prime[0..n]"
// and initialize all entries it as
// true. A value in prime[i] will finally
// be false if i is Not a prime, else true.
static bool []prime = new bool[N];
static void SieveOfEratosthenes()
{
    for(int i = 0; i < N; i++)
    prime[i] = true;
    prime[1] = false;

    for (int p = 2; p * p < N; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i = p * 2; i < N; i += p)
                prime[i] = false;
        }
    }
}

// Function to count almost
// prime numbers from 1 to n
static int almostPrimes(int n)
{
    // to store required answer
    int ans = 0;

    // 6 is first almost prime number
    for (int i = 6; i <= n; i++)
    {
        // to count prime factors
        int c = 0;
        for (int j = 2; j * j <= i; j++)
        {
            if (i % j == 0)
            {
                // if it is perfect square
                if (j * j == i)
                {
                    if (prime[j])
                        c++;
                }
                else
                {
                    if (prime[j])
                        c++;
                    if (prime[i / j])
                        c++;
                }
            }
        }

        // if I is almost prime number
        if (c == 2)
            ans++;
    }
    return ans;
}

// Driver code
public static void Main ()
{
    SieveOfEratosthenes();
    int n = 21;

    Console.WriteLine( almostPrimes(n));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count almost prime
// numbers from 1 to n

$N = 100005;

// Create a boolean array "prime[0..n]"
// and initialize all entries it as true.
// A value in prime[i] will
// finally be false if i is Not a prime, else true.
$prime = array_fill(0, $N, true);

function SieveOfEratosthenes()
{
    global $N, $prime;
    $prime[1] = false;

    for($p = 2; $p < (int)(sqrt($N)); $p++)
    {
        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p] == true)

            // Update all multiples of p
            for($i = 2 * $p; $i < $N; $i += $p)
                $prime[$i] = false;
    }
}

// Function to count almost prime
// numbers from 1 to n
function almostPrimes($n)
{
    global $prime;

    // to store required answer
    $ans = 0;

    // 6 is first almost prime number
    for($i = 6; $i < $n + 1; $i++)
    {
        // to count prime factors
        $c = 0;
        for($j = 2; $i >= $j * $j; $j++)
        {

            // if it is perfect square
            if ($i % $j == 0)
            {
                if ($j * $j == $i)
                {
                    if ($prime[$j])
                        $c += 1;
                }
                else
                {
                    if ($prime[$j])
                        $c += 1;
                    if ($prime[($i / $j)])
                        $c += 1;
                }
            }

        }

    // if I is almost prime number
    if ($c == 2)
        $ans += 1;
    }
    return $ans;
}

// Driver Code
SieveOfEratosthenes();
$n = 21;

print(almostPrimes($n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to count almost prime
// numbers from 1 to n

let N = 100005;

// Create a boolean array "prime[0..n]"
// and initialize all entries it as true.
// A value in prime[i] will
// finally be false if i is Not a prime, else true.
let prime = new Array(N).fill(true);

function SieveOfEratosthenes()
{
    prime[1] = false;

    for(let p = 2; p < Math.floor(Math.sqrt(N)); p++)
    {
        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)

            // Update all multiples of p
            for(let i = 2 * p; i < N; i += p)
                prime[i] = false;
    }
}

// Function to count almost prime
// numbers from 1 to n
function almostPrimes(n)
{   
    // to store required answer
    let ans = 0;

    // 6 is first almost prime number
    for(let i = 6; i < n + 1; i++)
    {
        // to count prime factors
        let c = 0;
        for(let j = 2; i >= j * j; j++)
        {

            // if it is perfect square
            if (i % j == 0)
            {
                if (j * j == i)
                {
                    if (prime[j])
                        c += 1;
                }
                else
                {
                    if (prime[j])
                        c += 1;
                    if (prime[(i / j)])
                        c += 1;
                }
            }

        }

    // if I is almost prime number
    if (c == 2)
        ans += 1;
    }
    return ans;
}

// Driver Code
SieveOfEratosthenes();
let n = 21;

document.write(almostPrimes(n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
8
```