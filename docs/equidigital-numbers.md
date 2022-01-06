# 等位数

> 原文:[https://www.geeksforgeeks.org/equidigital-numbers/](https://www.geeksforgeeks.org/equidigital-numbers/)

如果 n 的素因子分解中的位数(包括幂)与 n 中的位数相同，则数字 n 称为等位数。

例如，16 是一个等位数，因为它的素分解是 2^4，它的素分解总共有两位数(2 和 4)，这与 16 中的位数相同。
作为另一个例子，128 不是等数的，因为它的素分解是 2^7，总共有 2 位数(2 和 7)，但是数字有 3 位数。

所有质数都是等数字的。

给定一个数字 n，任务是打印到 n 为止的所有 Equidigital 数字。
**示例:**

```
Input: n = 10 
Output: 1, 2, 3, 5, 7, 10.
Note that 4, 6, 8 and 9 are not Equidigital.

Input :  n = 20
Output :  1 2 3 5 7 10 11 13 14 15 16 17 19

```

**方法**(打印所有小于或等于 n 的等位数)

1.  用圣代拉姆的筛子数 10^6 之前的所有素数。
2.  查找 n 中的位数。
3.  找出 n 的所有质因数，并对每个质因数 p 做以下操作。
    *   查找 p 中的位数。
    *   计算 p 除以 n 的最高幂。
    *   求以上两项之和。
4.  比较两个总和。如果两个和相同，则返回 true。

下面是上述想法的实现。

## C++

```
// C++ Program to find Equidigital Numbers till n
#include<bits/stdc++.h>
using namespace std;
const int MAX  = 10000;

// Array to store all prime less than and equal to MAX.
vector <int> primes;

// Utility function for sieve of sundaram
void sieveSundaram()
{
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than MAX, we reduce MAX to half
    // This array is used to separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    bool marked[MAX/2 + 1] = {0};

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i=1; i<=(sqrt(MAX)-1)/2; i++)
        for (int j=(i*(i+1))<<1; j<=MAX/2; j=j+2*i+1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i=1; i<=MAX/2; i++)
        if (marked[i] == false)
            primes.push_back(2*i + 1);
}

// Returns true if n is a Equidigital number, else
// false.
bool isEquidigital(int n)
{
    if (n == 1)
        return true;

    // Count digits in original number
    int original_no = n;
    int sumDigits = 0;
    while (original_no > 0)
    {
        sumDigits++;
        original_no = original_no/10;
    }

    // Count all digits in prime factors of n
    // pDigit is going to hold this value.
    int pDigit = 0 , count_exp = 0, p;
    for (int i = 0; primes[i] <= n/2; i++)
    {
        // Count powers of p in n
        while (n % primes[i] == 0)
        {
            // If primes[i] is a prime factor,
            p = primes[i];
            n = n/p;

            // Count the power of prime factors
            count_exp++;
        }

        // Add its digits to pDigit.
        while (p > 0)
        {
            pDigit++;
            p = p / 10;
        }

        // Add digits of power of prime factors to pDigit.
        while (count_exp > 1)
        {
            pDigit++;
            count_exp = count_exp / 10;
        }
    }

    // If n!=1 then one prime factor still to be
    // summed up;
    if (n != 1)
    {
        while (n > 0)
        {
            pDigit++;
            n = n/10;
        }
    }

    // If digits in prime factors and
    // digits in original number are same, then
    // return true. Else return false.
    return (pDigit == sumDigits);
}

// Driver code
int main()
{
    // Finding all prime numbers before limit. These
    // numbers are used to find prime factors.
    sieveSundaram();

    cout << "Printing first few Equidigital Numbers"
         " using isEquidigital()\n";
    for (int i=1; i<20; i++)
        if (isEquidigital(i))
            cout << i << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Equidigital Numbers till n

import java.util.Vector;
import static java.lang.Math.sqrt;

class GFG 
{
    static final int MAX = 10000;
    static Vector<Integer> primes = new Vector<Integer>(MAX+1);

    // Utility function for sieve of sundaram
    static void sieveSundaram()
    {
        // In general Sieve of Sundaram, produces primes smaller
        // than (2*x + 2) for a number given number x. Since
        // we want primes smaller than MAX, we reduce MAX to half
        // This array is used to separate numbers of the form
        // i+j+2ij from others where 1 <= i <= j
        boolean marked[] = new boolean[MAX/2 + 1];

        // Main logic of Sundaram. Mark all numbers which
        // do not generate prime number by doing 2*i+1
        for (int i=1; i<=(sqrt(MAX)-1)/2; i++)
            for (int j=(i*(i+1))<<1; j<=MAX/2; j=j+2*i+1)
                marked[j] = true;

        // Since 2 is a prime number
        primes.add(2);

        // Print other primes. Remaining primes are of the
        // form 2*i + 1 such that marked[i] is false.
        for (int i=1; i<=MAX/2; i++)
            if (marked[i] == false)
                primes.add(2*i + 1);
    }

    // Returns true if n is a Equidigital number, else
    // false.
    static boolean isEquidigital(int n)
    {
        if (n == 1)
            return true;

        // Count digits in original number
        int original_no = n;
        int sumDigits = 0;
        while (original_no > 0)
        {
            sumDigits++;
            original_no = original_no/10;
        }

        // Count all digits in prime factors of n
        // pDigit is going to hold this value.
        int pDigit = 0 , count_exp = 0, p = 0;
        for (int i = 0; primes.elementAt(i) <= n/2; i++)
        {
            // Count powers of p in n
            while (n % primes.elementAt(i) == 0)
            {
                // If primes[i] is a prime factor,
                p = primes.elementAt(i);
                n = n/p;

                // Count the power of prime factors
                count_exp++;
            }

            // Add its digits to pDigit.
            while (p > 0)
            {
                pDigit++;
                p = p / 10;
            }

            // Add digits of power of prime factors to pDigit.
            while (count_exp > 1)
            {
                pDigit++;
                count_exp = count_exp / 10;
            }
        }

        // If n!=1 then one prime factor still to be
        // summed up;
        if (n != 1)
        {
            while (n > 0)
            {
                pDigit++;
                n = n/10;
            }
        }

        // If digits in prime factors and
        // digits in original number are same, then
        // return true. Else return false.
        return (pDigit == sumDigits);
    }

    // Driver method
    public static void main (String[] args)
    {
       // Finding all prime numbers before limit. These
       // numbers are used to find prime factors.
       sieveSundaram();

       System.out.println("Printing first few Equidigital Numbers" +
                           " using isEquidigital()");

       for (int i=1; i<20; i++)
           if (isEquidigital(i))
               System.out.print(i + " ");
    }
}
```

## 蟒蛇 3

```
# Python3 Program to find Equidigital 
# Numbers till n 
import math
MAX = 10000; 

# Array to store all prime less 
# than and equal to MAX. 
primes = []; 

# Utility function for sieve of sundaram 
def sieveSundaram(): 

    # In general Sieve of Sundaram, produces 
    # primes smaller than (2*x + 2) for a number 
    # given number x. Since we want primes smaller 
    # than MAX, we reduce MAX to half. This array 
    # is used to separate numbers of the form 
    # i+j+2ij from others where 1 <= i <= j 
    marked = [False] * int(MAX / 2 + 1); 

    # Main logic of Sundaram. Mark all numbers which 
    # do not generate prime number by doing 2*i+1 
    for i in range(1, int((math.sqrt(MAX) - 1) / 2) + 1): 
        for j in range((i * (i + 1)) << 1, 
                    int(MAX / 2) + 1, 2 * i + 1): 
            marked[j] = True; 

    # Since 2 is a prime number 
    primes.append(2); 

    # Print other primes. Remaining primes 
    # are of the form 2*i + 1 such that 
    # marked[i] is false. 
    for i in range(1, int(MAX / 2) + 1): 
        if (marked[i] == False): 
            primes.append(2 * i + 1); 

# Returns true if n is a Equidigital 
# number, else false. 
def isEquidigital(n):

    if (n == 1): 
        return True; 

    # Count digits in original number 
    original_no = n; 
    sumDigits = 0; 
    while (original_no > 0):
        sumDigits += 1; 
        original_no = int(original_no / 10);

    # Count all digits in prime factors of n 
    # pDigit is going to hold this value. 
    pDigit = 0; 
    count_exp = 0; 
    p = 0;
    i = 0;
    while (primes[i] <= int(n / 2)): 

        # Count powers of p in n 
        while (n % primes[i] == 0):

            # If primes[i] is a prime factor, 
            p = primes[i]; 
            n = int(n / p); 

            # Count the power of prime factors 
            count_exp += 1;

        # Add its digits to pDigit. 
        while (p > 0): 
            pDigit += 1; 
            p = int(p / 10); 

        # Add digits of power of prime 
        # factors to pDigit. 
        while (count_exp > 1): 
            pDigit += 1; 
            count_exp = int(count_exp / 10);
        i += 1;

    # If n!=1 then one prime factor 
    # still to be summed up; 
    if (n != 1): 
        while (n > 0):
            pDigit += 1; 
            n = int(n / 10); 

    # If digits in prime factors and 
    # digits in original number are same, 
    # then return true. Else return false. 
    return (pDigit == sumDigits); 

# Driver code 

# Finding all prime numbers before 
# limit. These numbers are used to
# find prime factors. 
sieveSundaram(); 

print("Printing first few Equidigital", 
      "Numbers using isEquidigital()"); 
for i in range(1, 20): 
    if (isEquidigital(i)): 
        print(i, end = " "); 

# This code is contributed by mits
```

## C#

```
// C# program to find Equidigital Numbers till n
using System; 
using System.Collections;

public class GFG 
{
    static int MAX = 10000;
    static ArrayList primes = new ArrayList(MAX+1);

    // Utility function for sieve of sundaram
    static void sieveSundaram()
    {
        // In general Sieve of Sundaram, produces primes smaller
        // than (2*x + 2) for a number given number x. Since
        // we want primes smaller than MAX, we reduce MAX to half
        // This array is used to separate numbers of the form
        // i+j+2ij from others where 1 <= i <= j
        bool[] marked = new bool[MAX/2 + 1];

        // Main logic of Sundaram. Mark all numbers which
        // do not generate prime number by doing 2*i+1
        for (int i=1; i<=(Math.Sqrt(MAX)-1)/2; i++)
            for (int j=(i*(i+1))<<1; j<=MAX/2; j=j+2*i+1)
                marked[j] = true;

        // Since 2 is a prime number
        primes.Add(2);

        // Print other primes. Remaining primes are of the
        // form 2*i + 1 such that marked[i] is false.
        for (int i=1; i<=MAX/2; i++)
            if (marked[i] == false)
                primes.Add(2*i + 1);
    }

    // Returns true if n is a Equidigital number, else
    // false.
    static bool isEquidigital(int n)
    {
        if (n == 1)
            return true;

        // Count digits in original number
        int original_no = n;
        int sumDigits = 0;
        while (original_no > 0)
        {
            sumDigits++;
            original_no = original_no/10;
        }

        // Count all digits in prime factors of n
        // pDigit is going to hold this value.
        int pDigit = 0 , count_exp = 0, p = 0;
        for (int i = 0; (int)primes[i] <= n/2; i++)
        {
            // Count powers of p in n
            while (n % (int)primes[i] == 0)
            {
                // If primes[i] is a prime factor,
                p = (int)primes[i];
                n = n/p;

                // Count the power of prime factors
                count_exp++;
            }

            // Add its digits to pDigit.
            while (p > 0)
            {
                pDigit++;
                p = p / 10;
            }

            // Add digits of power of prime factors to pDigit.
            while (count_exp > 1)
            {
                pDigit++;
                count_exp = count_exp / 10;
            }
        }

        // If n!=1 then one prime factor still to be
        // summed up;
        if (n != 1)
        {
            while (n > 0)
            {
                pDigit++;
                n = n/10;
            }
        }

        // If digits in prime factors and
        // digits in original number are same, then
        // return true. Else return false.
        return (pDigit == sumDigits);
    }

    // Driver method
    public static void Main()
    {
    // Finding all prime numbers before limit. These
    // numbers are used to find prime factors.
    sieveSundaram();

    Console.WriteLine("Printing first few Equidigital Numbers using isEquidigital()");

    for (int i=1; i<20; i++)
        if (isEquidigital(i))
            Console.Write(i + " ");
    }
}
// This Code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find Equidigital Numbers till n
$MAX = 10000;

// Array to store all prime less than and equal to MAX.
$primes=array();

// Utility function for sieve of sundaram
function sieveSundaram()
{
    global $primes,$MAX;
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than MAX, we reduce MAX to half
    // This array is used to separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    $marked=array_fill(0,($MAX/2 + 1),false);

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for ($i=1; $i<=((int)sqrt($MAX)-1)/2; $i++)
        for ($j=($i*($i+1))<<1; $j<=(int)($MAX/2); $j=$j+2*$i+1)
            $marked[$j] = true;

    // Since 2 is a prime number
    array_push($primes,2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for ($i=1; $i<=(int)($MAX/2); $i++)
        if ($marked[$i] == false)
            array_push($primes,2*$i + 1);
}

// Returns true if n is a Equidigital number, else
// false.
function isEquidigital($n)
{
    global $primes,$MAX;
    if ($n == 1)
        return true;

    // Count digits in original number
    $original_no = $n;
    $sumDigits = 0;
    while ($original_no > 0)
    {
        $sumDigits++;
        $original_no = (int)($original_no/10);
    }

    // Count all digits in prime factors of n
    // pDigit is going to hold this value.
    $pDigit = 0;
    $count_exp = 0;
    $p=0;
    for ($i = 0; $primes[$i] <= (int)($n/2); $i++)
    {
        // Count powers of p in n
        while ($n % $primes[$i] == 0)
        {
            // If primes[i] is a prime factor,
            $p = $primes[$i];
            $n = (int)($n/$p);

            // Count the power of prime factors
            $count_exp++;
        }

        // Add its digits to pDigit.
        while ($p > 0)
        {
            $pDigit++;
            $p =(int)($p / 10);
        }

        // Add digits of power of prime factors to pDigit.
        while ($count_exp > 1)
        {
            $pDigit++;
            $count_exp = (int)($count_exp / 10);
        }
    }

    // If n!=1 then one prime factor still to be
    // summed up;
    if ($n != 1)
    {
        while ($n > 0)
        {
            $pDigit++;
            $n = (int)($n/10);
        }
    }

    // If digits in prime factors and
    // digits in original number are same, then
    // return true. Else return false.
    return ($pDigit == $sumDigits);
}

// Driver code

    // Finding all prime numbers before limit. These
    // numbers are used to find prime factors.
    sieveSundaram();

    echo "Printing first few Equidigital Numbers using isEquidigital()\n";
    for ($i=1; $i<20; $i++)
        if (isEquidigital($i))
            echo $i." ";

// This code is contributed by mits
?>
```

**Output:**

```
Printing first few Equidigital Numbers using isEquidigital()
1 2 3 5 7 10 11 13 14 15 16 17 19

```

**参考:**T2[https://en.wikipedia.org/wiki/Equidigital_number](https://en.wikipedia.org/wiki/Equidigital_number)

本文由**[Sahil Chhabra(KILLER)](https://www.facebook.com/sahil.chhabra.965)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。