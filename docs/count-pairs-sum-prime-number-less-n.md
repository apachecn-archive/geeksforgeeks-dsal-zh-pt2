# 以和为素数且小于 n 的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-sum-prime-number-less-n/](https://www.geeksforgeeks.org/count-pairs-sum-prime-number-less-n/)

给定正整数 n，计算满足以下条件的不同对数(x，y):

*   (x + y)是一个素数。
*   (x + y) < n
*   x！= y
*   1 <= x，y

**示例:**

```
Input : n = 6
Output : 3
prime pairs whose sum is less than 6 are:
(1,2), (1,4), (2,3) 

Input : 12
Output : 11
prime pairs whose sum is less than 12 are:
(1,2),  (1,4), (2,3), (1,6), (2,5), (3,4), 
(1,10), (2,9), (3,8), (4,7), (5,6)
```

**进场:**

```
1) Find all prime numbers less than n using
   Sieve of Sundaram

2) For each prime number p, count distinct
   pairs that sum up to p.

For any odd number n, number of distinct pairs
that add upto n are n/2
Since, a prime number is a odd number, the 
same applies for it too. 
```

**例如，**
对于素数 p = 7
不同的对加起来是 p: p/2 = 7/2 = 3
这三对是(1，6)，(2，5)，(3，4)
对于素数 p = 23
不同的对加起来是 p: p/2 = 23/2 = 11

## C++

```
// C++ implementation of prime pairs
// whose sum is less than n
#include <bits/stdc++.h>
using namespace std;

// Sieve of Sundaram for generating
// prime numbers less than n
void SieveOfSundaram(bool marked[], int nNew)
{
    // Main logic of Sundaram.  Mark all numbers
    // of the form i + j + 2ij as true where
    // 1 <= i <= j
    for (int i=1; i<=nNew; i++)
        for (int j=i; (i + j + 2*i*j) <= nNew; j++)
            marked[i + j + 2*i*j] = true;
}

// Returns number of pairs with fiven conditions.
int countPrimePairs(int n)
{
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a number
    // given number x. Since we want primes smaller
    // than n, we reduce n to half
    int nNew = (n-2)/2;

    // This array is used to separate numbers of
    // the form i+j+2ij from others where
    // 1 <= i <= j
    bool marked[nNew + 1];

    // Initialize all elements as not marked
    memset(marked, false, sizeof(marked));

    SieveOfSundaram(marked, nNew);

    int count = 0, prime_num;

    // Find primes. Primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for (int i=1; i<=nNew; i++)
    {
        if (marked[i] == false)
        {
            prime_num = 2*i + 1;

            // For a given prime number p
            // number of distinct pairs(i,j)
            // where (i+j) = p are p/2
            count = count + (prime_num / 2);
        }
    }

    return count;
}

// Driver program to test above
int main(void)
{
    int n = 12;
    cout << "Number of prime pairs: "
         << countPrimePairs(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of prime pairs
// whose sum is less than n

class GFG
{

// Sieve of Sundaram for generating
// prime numbers less than n
static void SieveOfSundaram(boolean marked[], int nNew)
{

    // Main logic of Sundaram. Mark all numbers
    // of the form i + j + 2ij as true where
    // 1 <= i <= j
    for (int i = 1; i <= nNew; i++)
        for (int j = i; (i + j + 2 * i * j) <= nNew; j++)
            marked[i + j + 2 * i * j] = true;
}

// Returns number of pairs with fiven conditions.
static int countPrimePairs(int n)
{
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a number
    // given number x. Since we want primes smaller
    // than n, we reduce n to half
    int nNew = (n - 2) / 2;

    // This array is used to separate numbers of
    // the form i+j+2ij from others where
    // 1 <= i <= j
    // Initialize all elements as not marked
    boolean marked[]=new boolean[nNew + 1];

    SieveOfSundaram(marked, nNew);
    int count = 0, prime_num;

    // Find primes. Primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= nNew; i++)
    {
        if (marked[i] == false)
        {
            prime_num = 2 * i + 1;

            // For a given prime number p
            // number of distinct pairs(i, j)
            // where (i + j) = p are p/2
            count = count + (prime_num / 2);
        }
    }
    return count;
}

// Driver code
public static void main (String[] args)
{
    int n = 12;
    System.out.println("Number of prime pairs: " +
    countPrimePairs(n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of prime pairs
# whose sum is less than n

# Sieve of Sundaram for generating
# prime numbers less than n
def SieveOfSundaram(marked, nNew):

    # Main logic of Sundaram. Mark all numbers
    # of the form i + j + 2ij as true where
    # 1 <= i <= j
    for i in range(1, nNew + 1):
        for j in range(i, nNew):
            if i + j + 2 * i * j > nNew:
                break
            marked[i + j + 2 * i * j] = True

# Returns number of pairs with fiven conditions.
def countPrimePairs(n):

    # In general Sieve of Sundaram, produces
    # primes smaller than (2*x + 2) for a number
    # given number x. Since we want primes smaller
    # than n, we reduce n to half
    nNew = (n - 2) // 2

    # This array is used to separate numbers
    # of the form i+j+2ij from others where
    # 1 <= i <= j
    marked = [ False for i in range(nNew + 1)]

    SieveOfSundaram(marked, nNew)

    count, prime_num = 0, 0

    # Find primes. Primes are of the form
    # 2*i + 1 such that marked[i] is false.
    for i in range(1, nNew + 1):
        if (marked[i] == False):

            prime_num = 2 * i + 1

            # For a given prime number p
            # number of distinct pairs(i,j)
            # where (i+j) = p are p/2
            count = count + (prime_num // 2)

    return count

# Driver Code
n = 12
print("Number of prime pairs: ",
             countPrimePairs(n))

# This code is contributed by Mohit kumar 29
```

## C#

```
// C# implementation of prime pairs
// whose sum is less than n
using System;

class GFG
{

// Sieve of Sundaram for generating
// prime numbers less than n
static void SieveOfSundaram(bool[] marked,
                            int nNew)
{

    // Main logic of Sundaram. Mark all numbers
    // of the form i + j + 2ij as true where
    // 1 <= i <= j
    for (int i = 1; i <= nNew; i++)
        for (int j = i;
            (i + j + 2 * i * j) <= nNew; j++)
            marked[i + j + 2 * i * j] = true;
}

// Returns number of pairs with fiven conditions.
static int countPrimePairs(int n)
{
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a 
    // number given number x. Since we want
    // primes smaller than n, we reduce n to half
    int nNew = (n - 2) / 2;

    // This array is used to separate numbers
    // of the form i+j+2ij from others where
    // 1 <= i <= j
    // Initialize all elements as not marked
    bool[] marked = new bool[nNew + 1];

    SieveOfSundaram(marked, nNew);
    int count = 0, prime_num;

    // Find primes. Primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= nNew; i++)
    {
        if (marked[i] == false)
        {
            prime_num = 2 * i + 1;

            // For a given prime number p
            // number of distinct pairs(i, j)
            // where (i + j) = p are p/2
            count = count + (prime_num / 2);
        }
    }
    return count;
}

// Driver code
public static void Main ()
{
    int n = 12;
    Console.WriteLine("Number of prime pairs: " +
                             countPrimePairs(n));
}
}

// This Code is Contribute by Mukul Singh.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of prime pairs
// whose sum is less than n

// Sieve of Sundaram for generating
// prime numbers less than n
function SieveOfSundaram(&$marked, $nNew)
{
    // Main logic of Sundaram. Mark all
    // numbers of the form i + j + 2ij
    // as true where 1 <= i <= j
    for ($i = 1; $i <= $nNew; $i++)
        for ($j = $i;
            ($i + $j + 2 * $i * $j) <= $nNew; $j++)
            $marked[$i + $j + 2 * $i * $j] = true;
}

// Returns number of pairs with
// given conditions.
function countPrimePairs($n)
{
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a
    // number given number x. Since we want
    // primes smaller than n, we reduce n to half
    $nNew = ($n - 2) / 2;

    // This array is used to separate numbers
    // of the form i+j+2ij from others where
    // 1 <= i <= j
    $marked = array_fill(0, $nNew + 1, false);

    SieveOfSundaram($marked, $nNew);

    $count = 0;

    // Find primes. Primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for ($i = 1; $i <= $nNew; $i++)
    {
        if ($marked[$i] == false)
        {
            $prime_num = 2 * $i + 1;

            // For a given prime number p
            // number of distinct pairs(i,j)
            // where (i+j) = p are p/2
            $count = $count + (int)($prime_num / 2);
        }
    }

    return $count;
}

// Driver Code
$n = 12;
echo "Number of prime pairs: " .
            countPrimePairs($n);

// This code is contributed by
// chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of prime pairs
// whose sum is less than n   

// Sieve of Sundaram for generating
// prime numbers less than n
function SieveOfSundaram(marked, nNew)
{

    // Main logic of Sundaram. Mark all numbers
    // of the form i + j + 2ij as true where
    // 1 <= i <= j
    for(i = 1; i <= nNew; i++)
        for(j = i; (i + j + 2 * i * j) <= nNew; j++)
            marked[i + j + 2 * i * j] = true;
}

// Returns number of pairs with fiven conditions.
function countPrimePairs(n)
{

    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a number
    // given number x. Since we want primes smaller
    // than n, we reduce n to half
    var nNew = parseInt((n - 2) / 2);

    // This array is used to separate numbers of
    // the form i+j+2ij from others where
    // 1 <= i <= j
    // Initialize all elements as not marked
    marked = Array.from({length: nNew + 1}, (_, i) => false);

    SieveOfSundaram(marked, nNew);
    var count = 0, prime_num;

    // Find primes. Primes are of the form
    // 2*i + 1 such that marked[i] is false.
    for(i = 1; i <= nNew; i++)
    {
        if (marked[i] == false)
        {
            prime_num = 2 * i + 1;

            // For a given prime number p
            // number of distinct pairs(i, j)
            // where (i + j) = p are p/2
            count = count + parseInt(prime_num / 2);
        }
    }
    return count;
}

// Driver code
var n = 12;
document.write("Number of prime pairs: " +
               countPrimePairs(n));

// This code is contributed by Princi Singh

</script>
```

**输出:**

```
Number of prime pairs: 11
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。