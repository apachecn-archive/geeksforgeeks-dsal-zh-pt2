# 梅森素数

> 原文:[https://www.geeksforgeeks.org/mersenne-prime/](https://www.geeksforgeeks.org/mersenne-prime/)

梅森素数是一个小于二的幂的素数。换句话说，如果任何素数的形式是 2 <sup>k</sup> -1，其中 k 是大于或等于 2 的整数，那么它就是梅森素数。前几个梅森素数是 3，7，31 和 127。
任务是打印所有小于输入正整数 n 的梅森素数
**示例:**

```
Input: 10
Output: 3 7
3 and 7 are prime numbers smaller than or
equal to 10 and are of the form 2k-1

Input: 100
Output: 3 7 31 
```

其思想是利用厄拉多塞的[筛生成所有小于或等于给定数 n 的素数。一旦我们生成了所有这样的素数，我们就遍历形式 2 <sup>k</sup> -1 的所有数字，并检查它们是否是素数。
下面是这个想法的实现。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// Program to generate mersenne primes
#include<bits/stdc++.h>
using namespace std;

// Generate all prime numbers less than n.
void SieveOfEratosthenes(int n, bool prime[])
{
    // Initialize all entries of boolean array
    // as true. A value in prime[i] will finally
    // be false if i is Not a prime, else true
    // bool prime[n+1];
    for (int i=0; i<=n; i++)
        prime[i] = true;

    for (int p=2; p*p<=n; p++)
    {
        // If prime[p] is not changed, then it
        // is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i=p*2; i<=n; i += p)
                prime[i] = false;
        }
    }
}

// Function to generate mersenne primes less
// than or equal to n
void mersennePrimes(int n)
{
    // Create a boolean array "prime[0..n]"
    bool prime[n+1];

    // Generating primes using Sieve
    SieveOfEratosthenes(n,prime);

    // Generate all numbers of the form 2^k - 1
    // and smaller than or equal to n.
    for (int k=2; ((1<<k)-1) <= n; k++)
    {
        long long num = (1<<k) - 1;

        // Checking whether number is prime and is
        // one less then the power of 2
        if (prime[num])
            cout << num << " ";
    }
}

// Driven program
int main()
{
    int n = 31;
    cout << "Mersenne prime numbers smaller "
         << "than or equal to " << n << endl;
    mersennePrimes(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to generate
// mersenne primes
import java.io.*;

class GFG {

    // Generate all prime numbers
    // less than n.
    static void SieveOfEratosthenes(int n,
                          boolean prime[])
    {
        // Initialize all entries of
        // boolean array as true. A
        // value in prime[i] will finally
        // be false if i is Not a prime,
        // else true bool prime[n+1];
        for (int i = 0; i <= n; i++)
            prime[i] = true;

        for (int p = 2; p * p <= n; p++)
        {
            // If prime[p] is not changed
            // , then it is a prime
            if (prime[p] == true)
            {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to generate mersenne
    // primes lessthan or equal to n
    static void mersennePrimes(int n)
    {
        // Create a boolean array
        // "prime[0..n]"
        boolean prime[]=new boolean[n + 1];

        // Generating primes
        // using Sieve
        SieveOfEratosthenes(n, prime);

        // Generate all numbers of
        // the form 2^k - 1 and
        // smaller than or equal to n.
        for (int k = 2; (( 1 << k) - 1) <= n; k++)
        {
            long num = ( 1 << k) - 1;

            // Checking whether number is
            // prime and is one less then
            // the power of 2
            if (prime[(int)(num)])
                System.out.print(num + " ");
        }
    }

    // Driven program
    public static void main(String args[])
    {
        int n = 31;
        System.out.println("Mersenne prime"+
                     "numbers smaller than"+
                          "or equal to "+n);

        mersennePrimes(n);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Program to generate mersenne primes

# Generate all prime numbers
# less than n.
def SieveOfEratosthenes(n, prime):

    # Initialize all entries of boolean
    # array as true. A value in prime[i]
    # will finally be false if i is Not
    # a prime, else true bool prime[n+1]
    for i in range(0, n + 1) :
        prime[i] = True

    p = 2
    while(p * p <= n):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True) :

            # Update all multiples of p
            for i in range(p * 2, n + 1, p):
                prime[i] = False

        p += 1

# Function to generate mersenne
# primes less than or equal to n
def mersennePrimes(n) :

    # Create a boolean array
    # "prime[0..n]"
    prime = [0] * (n + 1)

    # Generating primes using Sieve
    SieveOfEratosthenes(n, prime)

    # Generate all numbers of the
    # form 2^k - 1 and smaller
    # than or equal to n.
    k = 2
    while(((1 << k) - 1) <= n ):

        num = (1 << k) - 1

        # Checking whether number
        # is prime and is one
        # less then the power of 2
        if (prime[num]) :
            print(num, end = " " )

        k += 1

# Driver Code
n = 31
print("Mersenne prime numbers smaller",
              "than or equal to " , n )
mersennePrimes(n)

# This code is contributed
# by Smitha
```

## C#

```
// C# Program to generate mersenne primes
using System;

class GFG {

    // Generate all prime numbers less than n.
    static void SieveOfEratosthenes(int n,
                                bool []prime)
    {

        // Initialize all entries of
        // boolean array as true. A
        // value in prime[i] will finally
        // be false if i is Not a prime,
        // else true bool prime[n+1];
        for (int i = 0; i <= n; i++)
            prime[i] = true;

        for (int p = 2; p * p <= n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to generate mersenne
    // primes lessthan or equal to n
    static void mersennePrimes(int n)
    {

        // Create a boolean array
        // "prime[0..n]"
        bool []prime = new bool[n + 1];

        // Generating primes
        // using Sieve
        SieveOfEratosthenes(n, prime);

        // Generate all numbers of
        // the form 2^k - 1 and
        // smaller than or equal to n.
        for (int k = 2; (( 1 << k) - 1) <= n; k++)
        {
            long num = ( 1 << k) - 1;

            // Checking whether number is
            // prime and is one less then
            // the power of 2
            if (prime[(int)(num)])
                Console.Write(num + " ");
        }
    }

    // Driven program
    public static void Main()
    {
        int n = 31;

        Console.WriteLine("Mersenne prime numbers"
               + " smaller than or equal to " + n);

        mersennePrimes(n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to generate mersenne primes

// Generate all prime numbers less than n.
function SieveOf($n)
{
    // Initialize all entries of boolean
    // array as true. A value in prime[i]
    // will finally be false if i is Not
    // a prime, else true
    $prime = array($n + 1);
    for ($i = 0; $i <= $n; $i++)
        $prime[$i] = true;

    for ($p = 2; $p * $p <= $n; $p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {
            // Update all multiples of p
            for ($i = $p * 2; $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }
    return $prime;
}

// Function to generate mersenne
// primes less than or equal to n
function mersennePrimes($n)
{
    // Create a boolean array "prime[0..n]"
    // bool prime[n+1];

    // Generating primes using Sieve
    $prime = SieveOf($n);

    // Generate all numbers of the
    // form 2^k - 1 and smaller
    // than or equal to n.
    for ($k = 2; ((1 << $k) - 1) <= $n; $k++)
    {
        $num = (1 << $k) - 1;

        // Checking whether number is prime
        // and is one less then the power of 2
        if ($prime[$num])
            echo $num . " ";

    }
}

// Driver Code
$n = 31;
echo "Mersenne prime numbers smaller " .
     "than or equal to $n " .
      mersennePrimes($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript to generate
// mersenne primes

    // Generate all prime numbers
    // less than n.
    function SieveOfEratosthenes( n,
                          prime)
    {
        // Initialize all entries of
        // boolean array as true. A
        // value in prime[i] will finally
        // be false if i is Not a prime,
        // else true bool prime[n+1];
        for (let i = 0; i <= n; i++)
            prime[i] = true;

        for (let p = 2; p * p <= n; p++)
        {
            // If prime[p] is not changed
            // , then it is a prime
            if (prime[p] == true)
            {
                // Update all multiples of p
                for (let i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to generate mersenne
    // primes lessthan or equal to n
    function mersennePrimes(n)
    {
        // Create a boolean array
        // "prime[0..n]"
        let prime=[];

        // Generating primes
        // using Sieve
        SieveOfEratosthenes(n, prime);

        // Generate all numbers of
        // the form 2^k - 1 and
        // smaller than or equal to n.
        for (let k = 2; (( 1 << k) - 1) <= n; k++)
        {
            let num = ( 1 << k) - 1;

            // Checking whether number is
            // prime and is one less then
            // the power of 2
            if (prime[(num)])
               document.write(num + " ");
        }
    }

// Driver Code
        let n = 31;
        document.write("Mersenne prime"+
                     "numbers smaller than"+
                          "or equal to "+n + "<br/>");

        mersennePrimes(n);

// This code is contributed by code_hunt.
</script>
```

**输出:**

```
Mersenne prime numbers smaller than or equal to 31
3 7 31 
```

**参考文献:**
https://en.wikipedia.org/wiki/Mersenne_prime
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。