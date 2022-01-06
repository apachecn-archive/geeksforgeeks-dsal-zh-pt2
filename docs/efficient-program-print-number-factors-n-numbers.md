# 高效程序打印 n 个数的因子个数

> 原文:[https://www . geesforgeks . org/efficient-program-print-number-factors-n-numbers/](https://www.geeksforgeeks.org/efficient-program-print-number-factors-n-numbers/)

给定一个整数数组。我们需要编写一个程序来打印给定数组中每个元素的因子数。
**例:**

```
Input: 10 12 14 
Output: 4 6 4 
Explanation: There are 4 factors of 10 (1, 2, 
5, 10) and 6 of 12 and 4 of 14.

Input: 100 1000 10000
Output: 9 16 25 
Explanation: There are 9 factors of 100  and
16 of 1000 and 25 of 10000.
```

**简单方法**:一个简单的方法是运行两个嵌套循环。一个用于遍历数组，另一个用于计算数组元素的所有因子。
**时间复杂度** : O( n * n)
**辅助空间** : O( 1 )
**高效途径**:我们可以通过优化计算一个数的因子所需的运算次数来优化上述途径。我们可以使用[这种](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)方法来计算 sqrt(n)运算中 n 的因子。
**时间复杂度** : O( n * sqrt(n))
**辅助空间** : O( 1 )
**最佳逼近**:如果你通过数论，你会找到一个高效的找到因子个数的方法。如果我们取一个数，比如这里的 30，那么 30 的质因数将是 2，3，5，其中每一个的计数是 1 次，所以 30 的因数总数将是(1+1)*(1+1)*(1+1) = 8。
因此，给定数的因子总数的通式为:

```
Factors = (1+a1) * (1+a2) * (1+a3) * … (1+an)
```

其中 a1，a2，a3 …我们再举一个例子来说明一下。这次设数字为 100，
所以 100 会有 2，2，5，5。所以 100 的不同质因数的计数是 2，2。因此因子的数量将是(2+1)*(2+1) = 9。
现在，寻找素因子分解的最好方法将是最初存储素因子的筛子。创建筛子的方式是，它存储最小的质因数来划分自己。我们可以修改埃拉托色尼的[筛子来做到这一点。然后简单地对每一个数求质因数的个数，再乘以它就得到总因数的个数。
以下是上述方法的实施。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to count number of factors
// of an array of integers
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000001;

// array to store prime factors
int factor[MAX] = { 0 };

// function to generate all prime factors
// of numbers from 1 to 10^6
void generatePrimeFactors()
{
    factor[1] = 1;

    // Initializes all the positions with their value.
    for (int i = 2; i < MAX; i++)
        factor[i] = i;

    // Initializes all multiples of 2 with 2
    for (int i = 4; i < MAX; i += 2)
        factor[i] = 2;

    // A modified version of Sieve of Eratosthenes to
    // store the smallest prime factor that divides
    // every number.
    for (int i = 3; i * i < MAX; i++) {
        // check if it has no prime factor.
        if (factor[i] == i) {
            // Initializes of j starting from i*i
            for (int j = i * i; j < MAX; j += i) {
                // if it has no prime factor before, then
                // stores the smallest prime divisor
                if (factor[j] == j)
                    factor[j] = i;
            }
        }
    }
}

// function to calculate number of factors
int calculateNoOFactors(int n)
{
    if (n == 1)
        return 1;

    int ans = 1;

    // stores the smallest prime number
    // that divides n
    int dup = factor[n];

    // stores the count of number of times
    // a prime number divides n.
    int c = 1;

    // reduces to the next number after prime
    // factorization of n
    int j = n / factor[n];

    // false when prime factorization is done
    while (j != 1) {
        // if the same prime number is dividing n,
        // then we increase the count
        if (factor[j] == dup)
            c += 1;

        /* if its a new prime factor that is factorizing n,
           then we again set c=1 and change dup to the new
           prime factor, and apply the formula explained
           above. */
        else {
            dup = factor[j];
            ans = ans * (c + 1);
            c = 1;
        }

        // prime factorizes a number
        j = j / factor[j];
    }

    // for the last prime factor
    ans = ans * (c + 1);

    return ans;
}

// Driver program to test above function
int main()
{
    // generate prime factors of number
    // upto 10^6
    generatePrimeFactors();

    int a[] = { 10, 30, 100, 450, 987 };

    int q = sizeof(a) / sizeof(a[0]);

    for (int i = 0; i < q; i++)
        cout << calculateNoOFactors(a[i]) << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code For Efficient program to print
// the number of factors of n numbers
import java.util.*;

class GFG {

    static int MAX = 1000001;
    static int factor[];

    // function to generate all prime
    // factors of numbers from 1 to 10^6
    static void generatePrimeFactors()
    {
        factor[1] = 1;

        // Initializes all the positions with
        // their value.
        for (int i = 2; i < MAX; i++)
            factor[i] = i;

        // Initializes all multiples of 2 with 2
        for (int i = 4; i < MAX; i += 2)
            factor[i] = 2;

        // A modified version of Sieve of
        // Eratosthenes to store the
        // smallest prime factor that
        // divides every number.
        for (int i = 3; i * i < MAX; i++) {
            // check if it has no prime factor.
            if (factor[i] == i) {
                // Initializes of j starting from i*i
                for (int j = i * i; j < MAX; j += i) {
                    // if it has no prime factor
                    // before, then stores the
                    // smallest prime divisor
                    if (factor[j] == j)
                        factor[j] = i;
                }
            }
        }
    }

    // function to calculate number of factors
    static int calculateNoOFactors(int n)
    {
        if (n == 1)
            return 1;

        int ans = 1;

        // stores the smallest prime number
        // that divides n
        int dup = factor[n];

        // stores the count of number of times
        // a prime number divides n.
        int c = 1;

        // reduces to the next number after prime
        // factorization of n
        int j = n / factor[n];

        // false when prime factorization is done
        while (j != 1) {
            // if the same prime number is dividing n,
            // then we increase the count
            if (factor[j] == dup)
                c += 1;

            /* if its a new prime factor that is
               factorizing n, then we again set c=1
               and change dup to the new prime factor,
               and apply the formula explained
               above. */
            else {
                dup = factor[j];
                ans = ans * (c + 1);
                c = 1;
            }

            // prime factorizes a number
            j = j / factor[j];
        }

        // for the last prime factor
        ans = ans * (c + 1);

        return ans;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        // array to store prime factors
        factor = new int[MAX];
        factor[0] = 0;

        // generate prime factors of number
        // upto 10^6
        generatePrimeFactors();

        int a[] = { 10, 30, 100, 450, 987 };

        int q = a.length;

        for (int i = 0; i < q; i++)
            System.out.print(calculateNoOFactors(a[i]) + " ");
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to count
# number of factors
# of an array of integers
MAX = 1000001;

# array to store
# prime factors
factor = [0]*(MAX + 1);

# function to generate all
# prime factors of numbers
# from 1 to 10^6
def generatePrimeFactors():
    factor[1] = 1;

    # Initializes all the
    # positions with their value.
    for i in range(2,MAX):
        factor[i] = i;

    # Initializes all
    # multiples of 2 with 2
    for i in range(4,MAX,2):
        factor[i] = 2;

    # A modified version of
    # Sieve of Eratosthenes
    # to store the smallest
    # prime factor that divides
    # every number.
    i = 3;
    while(i * i < MAX):
        # check if it has
        # no prime factor.
        if (factor[i] == i):
            # Initializes of j
            # starting from i*i
            j = i * i;
            while(j < MAX):
                # if it has no prime factor
                # before, then stores the
                # smallest prime divisor
                if (factor[j] == j):
                    factor[j] = i;
                j += i;
        i+=1;

# function to calculate
# number of factors
def calculateNoOFactors(n):
    if (n == 1):
        return 1;
    ans = 1;

    # stores the smallest
    # prime number that
    # divides n
    dup = factor[n];

    # stores the count of
    # number of times a
    # prime number divides n.
    c = 1;

    # reduces to the next
    # number after prime
    # factorization of n
    j = int(n / factor[n]);

    # false when prime
    # factorization is done
    while (j > 1):
        # if the same prime
        # number is dividing
        # n, then we increase
        # the count
        if (factor[j] == dup):
            c += 1;

        # if its a new prime factor
        # that is factorizing n,
        # then we again set c=1 and
        # change dup to the new prime
        # factor, and apply the formula
        # explained above.
        else:
            dup = factor[j];
            ans = ans * (c + 1);
            c = 1;

        # prime factorizes
        # a number
        j = int(j / factor[j]);

    # for the last
    # prime factor
    ans = ans * (c + 1);

    return ans;
# Driver Code

if __name__ == "__main__":

# generate prime factors
# of number upto 10^6
    generatePrimeFactors()
    a = [10, 30, 100, 450, 987]
    q = len(a)
    for i in range (0,q):
        print(calculateNoOFactors(a[i]),end=" ")

# This code is contributed
# by mits.
```

## C#

```
// C# program to count number of factors
// of an array of integers
using System;

class GFG {

    static int MAX = 1000001;

    // array to store prime factors
    static int[] factor;

    // function to generate all prime
    // factors of numbers from 1 to 10^6
    static void generatePrimeFactors()
    {

        factor[1] = 1;

        // Initializes all the positions
        // with their value.
        for (int i = 2; i < MAX; i++)
            factor[i] = i;

        // Initializes all multiples of
        // 2 with 2
        for (int i = 4; i < MAX; i += 2)
            factor[i] = 2;

        // A modified version of Sieve of
        // Eratosthenes to store the
        // smallest prime factor that
        // divides every number.
        for (int i = 3; i * i < MAX; i++)
        {

            // check if it has no prime
            // factor.
            if (factor[i] == i)
            {

                // Initializes of j
                // starting from i*i
                for (int j = i * i;
                          j < MAX; j += i)
                {

                    // if it has no prime
                    // factor before, then
                    // stores the smallest
                    // prime divisor
                    if (factor[j] == j)
                        factor[j] = i;
                }
            }
        }
    }

    // function to calculate number of
    // factors
    static int calculateNoOFactors(int n)
    {
        if (n == 1)
            return 1;

        int ans = 1;

        // stores the smallest prime
        // number that divides n
        int dup = factor[n];

        // stores the count of number
        // of times a prime number
        // divides n.
        int c = 1;

        // reduces to the next number
        // after prime factorization
        // of n
        int j = n / factor[n];

        // false when prime factorization
        // is done
        while (j != 1) {

            // if the same prime number
            // is dividing n, then we
            // increase the count
            if (factor[j] == dup)
                c += 1;

            /* if its a new prime factor
            that is factorizing n, then
            we again set c=1 and change
            dup to the new prime factor,
            and apply the formula explained
            above. */
            else {
                dup = factor[j];
                ans = ans * (c + 1);
                c = 1;
            }

            // prime factorizes a number
            j = j / factor[j];
        }

        // for the last prime factor
        ans = ans * (c + 1);

        return ans;
    }

    /* Driver program to test above
    function */
    public static void Main()
    {

        // array to store prime factors
        factor = new int[MAX];
        factor[0] = 0;

        // generate prime factors of number
        // upto 10^6
        generatePrimeFactors();

        int[] a = { 10, 30, 100, 450, 987 };

        int q = a.Length;

        for (int i = 0; i < q; i++)
            Console.Write(
                   calculateNoOFactors(a[i])
                                     + " ");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// It works properly on
// 64-bit PHP Compiler

// PHP program to count
// number of factors
// of an array of integers
$MAX = 1000001;

// array to store
// prime factors
$factor = array_fill(0, $MAX + 1, 0);

// function to generate all
// prime factors of numbers
// from 1 to 10^6
function generatePrimeFactors()
{
    global $factor;
    global $MAX;
    $factor[1] = 1;

    // Initializes all the
    // positions with their value.
    for ($i = 2; $i < $MAX; $i++)
        $factor[$i] = $i;

    // Initializes all
    // multiples of 2 with 2
    for ($i = 4; $i < $MAX; $i += 2)
        $factor[$i] = 2;

    // A modified version of
    // Sieve of Eratosthenes
    // to store the smallest
    // prime factor that divides
    // every number.
    for ($i = 3; $i * $i < $MAX; $i++)
    {
        // check if it has
        // no prime factor.
        if ($factor[$i] == $i)
        {
            // Initializes of j
            // starting from i*i
            for ($j = $i * $i;
                 $j < $MAX; $j += $i)
            {
                // if it has no prime factor
                // before, then stores the
                // smallest prime divisor
                if ($factor[$j] == $j)
                    $factor[$j] = $i;
            }
        }
    }
}

// function to calculate
// number of factors
function calculateNoOFactors($n)
{
    global $factor;
    if ($n == 1)
        return 1;

    $ans = 1;

    // stores the smallest
    // prime number that
    // divides n
    $dup = $factor[$n];

    // stores the count of
    // number of times a
    // prime number divides n.
    $c = 1;

    // reduces to the next
    // number after prime
    // factorization of n
    $j = (int)($n / $factor[$n]);

    // false when prime
    // factorization is done
    while ($j != 1)
    {
        // if the same prime
        // number is dividing
        // n, then we increase
        // the count
        if ($factor[$j] == $dup)
            $c += 1;

        /* if its a new prime factor
           that is factorizing n,
           then we again set c=1 and
           change dup to the new prime
           factor, and apply the formula 
           explained above. */
        else
        {
            $dup = $factor[$j];
            $ans = $ans * ($c + 1);
            $c = 1;
        }

        // prime factorizes
        // a number
        $j = (int)($j / $factor[$j]);
    }

    // for the last
    // prime factor
    $ans = $ans * ($c + 1);

    return $ans;
}

// Driver Code

// generate prime factors
// of number upto 10^6
generatePrimeFactors();
$a = array(10, 30, 100, 450, 987);
$q = sizeof($a);
for ($i = 0; $i < $q; $i++)
    echo calculateNoOFactors($a[$i]) . " ";

// This code is contributed
// by mits.
?>
```

## java 描述语言

```
<script>
// javascript Code For Efficient program to print
// the number of factors of n numbers

    var MAX = 1000001;
    var factor = [];

    // function to generate all prime
    // factors of numbers from 1 to 10^6
    function generatePrimeFactors() {
        factor[1] = 1;

        // Initializes all the positions with
        // their value.
        for (i = 2; i < MAX; i++)
            factor[i] = i;

        // Initializes all multiples of 2 with 2
        for (i = 4; i < MAX; i += 2)
            factor[i] = 2;

        // A modified version of Sieve of
        // Eratosthenes to store the
        // smallest prime factor that
        // divides every number.
        for (i = 3; i * i < MAX; i++)
        {

            // check if it has no prime factor.
            if (factor[i] == i)
            {

                // Initializes of j starting from i*i
                for (j = i * i; j < MAX; j += i)
                {

                    // if it has no prime factor
                    // before, then stores the
                    // smallest prime divisor
                    if (factor[j] == j)
                        factor[j] = i;
                }
            }
        }
    }

    // function to calculate number of factors
    function calculateNoOFactors(n)
    {
        if (n == 1)
            return 1;

        var ans = 1;

        // stores the smallest prime number
        // that divides n
        var dup = factor[n];

        // stores the count of number of times
        // a prime number divides n.
        var c = 1;

        // reduces to the next number after prime
        // factorization of n
        var j = n / factor[n];

        // false when prime factorization is done
        while (j != 1)
        {

            // if the same prime number is dividing n,
            // then we increase the count
            if (factor[j] == dup)
                c += 1;

            /*
             * if its a new prime factor that is factorizing n, then we again set c=1 and
             * change dup to the new prime factor, and apply the formula explained above.
             */
            else
            {
                dup = factor[j];
                ans = ans * (c + 1);
                c = 1;
            }

            // prime factorizes a number
            j = j / factor[j];
        }

        // for the last prime factor
        ans = ans * (c + 1);
        return ans;
    }

    /* Driver program to test above function */

        // array to store prime factors
        factor = Array(MAX).fill(0);
        factor[0] = 0;

        // generate prime factors of number
        // upto 10^6
        generatePrimeFactors();

        var a = [ 10, 30, 100, 450, 987 ];
        var q = a.length;
        for (i = 0; i < q; i++)
            document.write(calculateNoOFactors(a[i]) + " ");

// This code is contributed by aashish1995
</script>
```

**输出:**

```
4 8 9 18 8 
```

**时间复杂度** : O(n * log(max(number))，其中 n 为数组中元素的总数，max(number)表示数组中的最大个数。
**辅助空间**:计算筛子的 O(n)。
本文由 **Raja Vikramaditya** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。