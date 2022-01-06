# 从 a 到 b 正好 n 个不同的质因数

> 原文:[https://www . geesforgeks . org/just-n-distinct-prime-factor-numbers-b/](https://www.geeksforgeeks.org/exactly-n-distinct-prime-factor-numbers-b/)

给你两个数字 a 和 b (1 <= a,b <= 10^8 ) and n. The task is to find all numbers between a and b inclusively having exactly n distinct prime factors. The solution should be designed in a way that it efficiently handles multiple queries for different values of a and b like in Competitive Programming.
**举例:**

```
Input  : a = 1, b = 10, n = 2
Output : 2
// Only 6 = 2*3 and 10 = 2*5 have exactly two 
// distinct prime factors

Input : a = 1, b = 100, n = 3
Output: 8
// only 30 = 2*3*5, 42 = 2*3*7, 60 = 2*2*3*5, 66 = 2*3*11,
// 70 = 2*5*7, 78 = 2*3*13, 84 = 2*2*3*7 and 90 = 2*3*3*5 
// have exactly three distinct prime factors
```

这个问题基本上是[分段筛](https://www.geeksforgeeks.org/segmented-sieve/)的应用。我们知道，一个数的所有质因数总是小于或等于数的平方根，即:sqrt(n)。所以我们生成所有小于或等于 10^8 的质数，并将它们存储在一个数组中。现在，使用这个分段的筛子，我们检查从 a 到 b 的每个数字是否有 n 个质因数。

## C++

```
// C++ program to find numbers with exactly n distinct
// prime factor numbers from a to b
#include<bits/stdc++.h>
using namespace std;

// Stores all primes less than and equals to sqrt(10^8) = 10000
vector <int> primes;

// Generate all prime numbers less than or equals to sqrt(10^8)
// = 10000 using sieve of sundaram
void segmentedSieve()
{
    int n = 10000; // Square root of 10^8

    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x.
    // Since we want primes smaller than n=10^4, we reduce
    // n to half
    int nNew = (n-2)/2;

    // This array is used to separate numbers of the form
    // i+j+2ij from others where  1 <= i <= j
    bool marked[nNew + 1];

    // Initialize all elements as not marked
    memset(marked, false, sizeof(marked));

    // Main logic of Sundaram.  Mark all numbers of the
    // form i + j + 2ij as true where 1 <= i <= j
    for (int i=1; i<=nNew; i++)
        for (int j=i; (i + j + 2*i*j) <= nNew; j++)
            marked[i + j + 2*i*j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Remaining primes are of the form 2*i + 1 such that
    // marked[i] is false.
    for (int i=1; i<=nNew; i++)
        if (marked[i] == false)
            primes.push_back(2*i+1);
}

// Function to count all numbers from a to b having exactly
// n prime factors
int Nfactors(int a, int b, int n)
{
    segmentedSieve();

    // result --> all numbers between a and b having
    // exactly n prime factors
    int result = 0;

    //  check for each number
    for (int i=a; i<=b; i++)
    {
        // tmp  --> stores square root of current number because
        //          all prime factors are always less than and
        //          equal to square root of given number
        // copy --> it holds the copy of current number
        int tmp = sqrt(i), copy = i;

        // count -->  it counts the number of distinct prime
        // factors of number
        int count = 0;

        // check divisibility of 'copy' with each prime less
        // than 'tmp' and divide it until it is divisible by
        // current prime factor
        for (int j=0; primes[j]<=tmp; j++)
        {
            if (copy%primes[j]==0)
            {
                // increment count for distinct prime
                count++;
                while (copy%primes[j]==0)
                    copy = copy/primes[j];
            }
        }

        // if number is completely divisible then at last
        // 'copy' will be 1 else 'copy' will be prime, so
        // increment count by one
        if (copy != 1)
            count++;

        // if number has exactly n distinct primes then
        // increment result by one
        if (count==n)
            result++;
    }
    return result;
}

// Driver program to run the case
int main()
{
    int a = 1, b = 100, n = 3;
    cout << Nfactors(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find numbers with exactly n distinct
// prime factor numbers from a to b
import java.util.*;

class GFG
{

// Stores all primes less than and
// equals to sqrt(10^8) = 10000
static ArrayList<Integer> primes = new ArrayList<Integer>();

// Generate all prime numbers less
// than or equals to sqrt(10^8)
// = 10000 using sieve of sundaram
static void segmentedSieve()
{
    int n = 10000; // Square root of 10^8

    // In general Sieve of Sundaram,
    // produces primes smaller
    // than (2*x + 2) for a number
    // given number x. Since we want
    // primes smaller than n=10^4,
    // we reduce n to half
    int nNew = (n - 2)/2;

    // This array is used to separate
    // numbers of the form i+j+2ij
    // from others where 1 <= i <= j
    boolean[] marked=new boolean[nNew + 1];

    // Main logic of Sundaram. Mark all
    // numbers of the form i + j + 2ij
    // as true where 1 <= i <= j
    for (int i = 1; i <= nNew; i++)
        for (int j = i; (i + j + 2 * i * j) <= nNew; j++)
            marked[i + j + 2 * i * j] = true;

    // Since 2 is a prime number
    primes.add(2);

    // Remaining primes are of the form 2*i + 1 such that
    // marked[i] is false.
    for (int i = 1; i <= nNew; i++)
        if (marked[i] == false)
            primes.add(2 * i + 1);
}

// Function to count all numbers from a to b having exactly
// n prime factors
static int Nfactors(int a, int b, int n)
{
    segmentedSieve();

    // result --> all numbers between a and b having
    // exactly n prime factors
    int result = 0;

    // check for each number
    for (int i = a; i <= b; i++)
    {
        // tmp --> stores square root of current number because
        //     all prime factors are always less than and
        //     equal to square root of given number
        // copy --> it holds the copy of current number
        int tmp = (int)Math.sqrt(i), copy = i;

        // count --> it counts the number of distinct prime
        // factors of number
        int count = 0;

        // check divisibility of 'copy' with each prime less
        // than 'tmp' and divide it until it is divisible by
        // current prime factor
        for (int j = 0; primes.get(j) <= tmp; j++)
        {
            if (copy % primes.get(j) == 0)
            {
                // increment count for distinct prime
                count++;
                while (copy % primes.get(j) == 0)
                    copy = copy/primes.get(j);
            }
        }

        // if number is completely divisible then at last
        // 'copy' will be 1 else 'copy' will be prime, so
        // increment count by one
        if (copy != 1)
            count++;

        // if number has exactly n distinct primes then
        // increment result by one
        if (count == n)
            result++;
    }
    return result;
}

// Driver code
public static void main (String[] args)
{
    int a = 1, b = 100, n = 3;
    System.out.println(Nfactors(a, b, n));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 program to find numbers with
# exactly n distinct prime factor numbers
# from a to b
import math

# Stores all primes less than and
# equals to sqrt(10^8) = 10000
primes = [];

# Generate all prime numbers less than
# or equals to sqrt(10^8) = 10000
# using sieve of sundaram
def segmentedSieve():

    n = 10000; # Square root of 10^8

    # In general Sieve of Sundaram, produces
    # primes smaller than (2*x + 2) for a
    # given number x. Since we want primes
    # smaller than n=10^4, we reduce n to half
    nNew = int((n - 2) / 2);

    # This array is used to separate
    # numbers of the form i+j+2ij
    # from others where 1 <= i <= j
    marked = [False] * (nNew + 1);

    # Main logic of Sundaram. Mark all
    # numbers of the form i + j + 2ij
    # as true where 1 <= i <= j
    for i in range(1, nNew + 1):
        j = i;
        while ((i + j + 2 * i * j) <= nNew):
            marked[i + j + 2 * i * j] = True;
            j += 1;

    # Since 2 is a prime number
    primes.append(2);

    # Remaining primes are of the
    # form 2*i + 1 such that
    # marked[i] is false.
    for i in range(1, nNew + 1):
        if (marked[i] == False):
            primes.append(2 * i + 1);

# Function to count all numbers
# from a to b having exactly n
# prime factors
def Nfactors(a, b, n):

    segmentedSieve();

    # result --> all numbers between
    # a and b having exactly n prime
    # factors
    result = 0;

    # check for each number
    for i in range(a, b + 1):

        # tmp --> stores square root of 
        # current number because all prime
        # factors are always less than and
        # equal to square root of given number
        # copy --> it holds the copy of
        #           current number
        tmp = math.sqrt(i);
        copy = i;

        # count --> it counts the number of
        # distinct prime factors of number
        count = 0;

        # check divisibility of 'copy' with
        # each prime less than 'tmp' and 
        # divide it until it is divisible
        # by current prime factor
        j = 0;
        while (primes[j] <= tmp):
            if (copy % primes[j] == 0):

                # increment count for
                # distinct prime
                count += 1;
                while (copy % primes[j] == 0):
                    copy = (copy // primes[j]);
            j += 1;

        # if number is completely divisible
        # then at last 'copy' will be 1 else
        # 'copy' will be prime, so increment
        # count by one
        if (copy != 1):
            count += 1;

        # if number has exactly n distinct
        # primes then increment result by one
        if (count == n):
            result += 1;

    return result;

# Driver Code
a = 1;
b = 100;
n = 3;
print(Nfactors(a, b, n));

# This code is contributed
# by chandan_jnu
```

## C#

```
// C# program to find numbers with exactly n
// distinct prime factor numbers from a to b
using System;
using System.Collections;

class GFG
{

// Stores all primes less than and
// equals to sqrt(10^8) = 10000
static ArrayList primes = new ArrayList();

// Generate all prime numbers less
// than or equals to sqrt(10^8)
// = 10000 using sieve of sundaram
static void segmentedSieve()
{
    int n = 10000; // Square root of 10^8

    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a number
    // given number x. Since we want primes
    // smaller than n=10^4, we reduce n to half
    int nNew = (n - 2) / 2;

    // This array is used to separate
    // numbers of the form i+j+2ij
    // from others where 1 <= i <= j
    bool[] marked = new bool[nNew + 1];

    // Main logic of Sundaram. Mark all
    // numbers of the form i + j + 2ij
    // as true where 1 <= i <= j
    for (int i = 1; i <= nNew; i++)
        for (int j = i;
            (i + j + 2 * i * j) <= nNew; j++)
            marked[i + j + 2 * i * j] = true;

    // Since 2 is a prime number
    primes.Add(2);

    // Remaining primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= nNew; i++)
        if (marked[i] == false)
            primes.Add(2 * i + 1);
}

// Function to count all numbers from
// a to b having exactly n prime factors
static int Nfactors(int a, int b, int n)
{
    segmentedSieve();

    // result --> all numbers between a and b
    // having exactly n prime factors
    int result = 0;

    // check for each number
    for (int i = a; i <= b; i++)
    {
        // tmp --> stores square root of current
        // number because all prime factors are
        // always less than and equal to square
        // root of given number
        // copy --> it holds the copy of current number
        int tmp = (int)Math.Sqrt(i), copy = i;

        // count --> it counts the number of
        // distinct prime factors of number
        int count = 0;

        // check divisibility of 'copy' with each
        // prime less than 'tmp' and divide it until
        // it is divisible by current prime factor
        for (int j = 0; (int)primes[j] <= tmp; j++)
        {
            if (copy % (int)primes[j] == 0)
            {
                // increment count for distinct prime
                count++;
                while (copy % (int)primes[j] == 0)
                    copy = copy / (int)primes[j];
            }
        }

        // if number is completely divisible then
        // at last 'copy' will be 1 else 'copy'
        // will be prime, so increment count by one
        if (copy != 1)
            count++;

        // if number has exactly n distinct
        // primes then increment result by one
        if (count == n)
            result++;
    }
    return result;
}

// Driver code
public static void Main()
{
    int a = 1, b = 100, n = 3;
    Console.WriteLine(Nfactors(a, b, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find numbers with exactly n
// distinct prime factor numbers from a to b

// Stores all primes less than and equals
// to sqrt(10^8) = 10000
$primes = array();

// Generate all prime numbers less than or
// equals to sqrt(10^8) = 10000 using
// sieve of sundaram
function segmentedSieve()
{
    global $primes;
    $n = 10000; // Square root of 10^8

    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a
    // given number x. Since we want primes
    // smaller than n=10^4, we reduce n to half
    $nNew = (int)(($n-2)/2);

    // This array is used to separate numbers of
    // the form i+j+2ij from others where 1 <= i <= j
    $marked = array_fill(0, $nNew + 1, false);

    // Main logic of Sundaram. Mark all numbers of the
    // form i + j + 2ij as true where 1 <= i <= j
    for ($i = 1; $i <= $nNew; $i++)
        for ($j = $i;
            ($i + $j + 2 * $i * $j) <= $nNew; $j++)
            $marked[$i + $j + 2 * $i * $j] = true;

    // Since 2 is a prime number
    array_push($primes, 2);

    // Remaining primes are of the form 2*i + 1
    // such that marked[i] is false.
    for ($i = 1; $i <= $nNew; $i++)
        if ($marked[$i] == false)
            array_push($primes, 2 * $i + 1);
}

// Function to count all numbers from a to b
// having exactly n prime factors
function Nfactors($a, $b, $n)
{
    global $primes;
    segmentedSieve();

    // result --> all numbers between a and b
    // having exactly n prime factors
    $result = 0;

    // check for each number
    for ($i = $a; $i <= $b; $i++)
    {
        // tmp --> stores square root of current
        // number because all prime factors are
        // always less than and equal to square
        // root of given number
        // copy --> it holds the copy of current number
        $tmp = sqrt($i);
        $copy = $i;

        // count --> it counts the number of
        // distinct prime factors of number
        $count = 0;

        // check divisibility of 'copy' with each
        // prime less than 'tmp' and divide it until
        // it is divisible by current prime factor
        for ($j = 0; $primes[$j] <= $tmp; $j++)
        {
            if ($copy % $primes[$j] == 0)
            {
                // increment count for distinct prime
                $count++;
                while ($copy % $primes[$j] == 0)
                    $copy = (int)($copy / $primes[$j]);
            }
        }

        // if number is completely divisible then
        // at last 'copy' will be 1 else 'copy'
        // will be prime, so increment count by one
        if ($copy != 1)
            $count++;

        // if number has exactly n distinct primes
        // then increment result by one
        if ($count == $n)
            $result++;
    }
    return $result;
}

// Driver Code
$a = 1;
$b = 100;
$n = 3;
print(Nfactors($a, $b, $n));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find numbers with exactly n
    // distinct prime factor numbers from a to b

    // Stores all primes less than and
    // equals to sqrt(10^8) = 10000
    let primes = [];

    // Generate all prime numbers less
    // than or equals to sqrt(10^8)
    // = 10000 using sieve of sundaram
    function segmentedSieve()
    {
        let n = 10000; // Square root of 10^8

        // In general Sieve of Sundaram, produces
        // primes smaller than (2*x + 2) for a number
        // given number x. Since we want primes
        // smaller than n=10^4, we reduce n to half
        let nNew = parseInt((n - 2) / 2, 10);

        // This array is used to separate
        // numbers of the form i+j+2ij
        // from others where 1 <= i <= j
        let marked = new Array(nNew + 1);
        marked.fill(false);

        // Main logic of Sundaram. Mark all
        // numbers of the form i + j + 2ij
        // as true where 1 <= i <= j
        for (let i = 1; i <= nNew; i++)
            for (let j = i;
                (i + j + 2 * i * j) <= nNew; j++)
                marked[i + j + 2 * i * j] = true;

        // Since 2 is a prime number
        primes.push(2);

        // Remaining primes are of the form
        // 2*i + 1 such that marked[i] is false.
        for (let i = 1; i <= nNew; i++)
            if (marked[i] == false)
                primes.push(2 * i + 1);
    }

    // Function to count all numbers from
    // a to b having exactly n prime factors
    function Nfactors(a, b, n)
    {
        segmentedSieve();

        // result --> all numbers between a and b
        // having exactly n prime factors
        let result = 0;

        // check for each number
        for (let i = a; i <= b; i++)
        {
            // tmp --> stores square root of current
            // number because all prime factors are
            // always less than and equal to square
            // root of given number
            // copy --> it holds the copy of current number
            let tmp = parseInt(Math.sqrt(i), 10), copy = i;

            // count --> it counts the number of
            // distinct prime factors of number
            let count = 0;

            // check divisibility of 'copy' with each
            // prime less than 'tmp' and divide it until
            // it is divisible by current prime factor
            for (let j = 0; primes[j] <= tmp; j++)
            {
                if (copy % primes[j] == 0)
                {
                    // increment count for distinct prime
                    count++;
                    while (copy % primes[j] == 0)
                        copy = parseInt(copy / primes[j], 10);
                }
            }

            // if number is completely divisible then
            // at last 'copy' will be 1 else 'copy'
            // will be prime, so increment count by one
            if (copy != 1)
                count++;

            // if number has exactly n distinct
            // primes then increment result by one
            if (count == n)
                result++;
        }
        return result;
    }

    let a = 1, b = 100, n = 3;
    document.write(Nfactors(a, b, n));

</script>
```

**输出:**

```
8
```

如果你有另一种方法来解决这个问题，那么请在评论中分享。
本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。