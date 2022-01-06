# 在一个范围内找到素数中出现次数最高的数字

> 原文:[https://www . geesforgeks . org/find-出现次数最多的数字-质数-范围/](https://www.geeksforgeeks.org/find-highest-occurring-digit-prime-numbers-range/)

给定范围 **L** 到 **R** ，任务是找到位于 L 和 R(包括两者)之间的素数中出现频率最高的数字。如果多个数字具有相同的最高频率，则打印其中最大的一个。如果 L 和 R 之间没有质数，输出-1。
**例:**

```
Input : L = 1 and R = 20.
Output : 1
Prime number between 1 and 20 are 2, 3, 5, 7, 11, 13, 17, 19.
1 occur maximum i.e 5 times among 0 to 9.
```

思路是从 L 开始到 R，检查数字是不是质数。如果是质数，则增加质数中出现数字的频率(使用数组)。为了检查数字是否是质数，我们可以使用厄拉多塞的[筛。
以下是本办法的实施情况:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to find the highest occurring digit
// in prime numbers in a range L to R.
#include<bits/stdc++.h>
using namespace std;

// Sieve of Eratosthenes
void sieve(bool prime[], int n)
{
      prime[0] = prime[1] = true;
    for (int p = 2; p * p  <= n; p++)
    {
        if (prime[p] == false)
            for (int i = p*2; i <= n; i+=p)
                prime[i] = true;
    }
}

// Returns maximum occurring digits in primes
// from l to r.
int maxDigitInPrimes(int L, int R)
{
    bool prime[R+1];
    memset(prime, 0, sizeof(prime));

    // Finding the prime number up to R.
    sieve(prime, R);

    // Initialise frequency of all digit to 0.
    int freq[10] = { 0 };
    int val;

    // For all number between L to R, check if prime
    // or not. If prime, incrementing the frequency
    // of digits present in the prime number.
    for (int i = L; i <= R; i++)
    {
        if (!prime[i])
        {
            int p = i; // If i is prime
            while (p)
            {
                freq[p%10]++;
                p /= 10;
            }
        }
    }

    // Finding digit with highest frequency.
    int max = freq[0], ans = 0;
    for (int j = 1; j < 10; j++)
    {
        if (max <= freq[j])
        {
            max = freq[j];
            ans = j;
        }
    }

    return (max != 0)? ans: -1;
}

// Driven Program
int main()
{
    int L = 1, R = 20;

    cout << maxDigitInPrimes(L, R) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the highest occurring digit
// in prime numbers in a range L to R.
import java.util.Arrays;

class GFG {

    // Sieve of Eratosthenes
    static void sieve(boolean prime[], int n) {

        for (int p = 2; p * p <= n; p++) {
            if (prime[p] == false)
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = true;
        }
    }

    // Returns maximum occurring digits in primes
    // from l to r.
    static int maxDigitInPrimes(int L, int R) {

        boolean prime[] = new boolean[R + 1];
        Arrays.fill(prime, false);

        // Finding the prime number up to R.
        sieve(prime, R);

        // Initialise frequency of all digit to 0.
        int freq[] = new int[10];
        int val;

        // For all number between L to R, check if
        // prime or not. If prime, incrementing
        // the frequency of digits present in the
        // prime number.
        for (int i = L; i <= R; i++) {

            if (!prime[i]) {
                int p = i; // If i is prime

                while (p > 0) {
                freq[p % 10]++;
                p /= 10;
                }
            }
        }

        // Finding digit with highest frequency.
        int max = freq[0], ans = 0;

        for (int j = 1; j < 10; j++) {
            if (max <= freq[j]) {
                max = freq[j];
                ans = j;
            }
        }

        return (max != 0) ? ans : -1;
    }

    // Driver code
    public static void main(String[] args) {
        int L = 1, R = 20;
        System.out.println(maxDigitInPrimes(L, R));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to find the highest
# occurring digit in prime numbers
# in a range L to R.

# Sieve of Eratosthenes
def sieve(prime, n):
    p = 2
    while p * p <= n :
        if (prime[p] == False):
            for i in range(p * 2, n, p):
                prime[i] = True

        p += 1

# Returns maximum occurring digits
# in primes from l to r.
def maxDigitInPrimes(L, R):

    prime = [0] * (R + 1)

    # Finding the prime number up to R.
    sieve(prime, R)

    # Initialise frequency of all
    # digit to 0.
    freq = [0] * 10

    # For all number between L to R,
    # check if prime or not. If prime,
    # incrementing the frequency
    # of digits present in the prime number.
    for i in range(L, R + 1):
        if (not prime[i]):
            p = i # If i is prime
            while (p):
                freq[p % 10] += 1
                p //= 10

    # Finding digit with highest frequency.
    max = freq[0]
    ans = 0
    for j in range(1, 10):
        if (max <= freq[j]):
            max = freq[j]
            ans = j
    if max == 0
    return -1
    return ans

# Driver Code
if __name__=="__main__":

    L = 1
    R = 20

    print(maxDigitInPrimes(L, R))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the highest
// occurring digit in prime numbers
// in a range L to R.
using System;

class GFG {

    // Sieve of Eratosthenes
    static void sieve(bool []prime, int n)
    {
        for (int p = 2; p * p <= n; p++)
        {
            if (prime[p] == false)
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = true;
        }
    }

    // Returns maximum occurring digits
    // in primes from l to r.
    static int maxDigitInPrimes(int L, int R) {

        bool []prime = new bool[R + 1];
        for(int i = 0; i < R+1; i++)
        prime[i] = false;

        // Finding the prime number up to R.
        sieve(prime, R);

        // Initialise frequency of all digit to 0.
        int []freq = new int[10];

        // For all number between L to R, check if
        // prime or not. If prime, incrementing
        // the frequency of digits present in the
        // prime number.
        for (int i = L; i <= R; i++) {

            if (!prime[i])
            {
                int p = i; // If i is prime

                while (p > 0) {
                freq[p % 10]++;
                p /= 10;
                }
            }
        }

        // Finding digit with highest frequency.
        int max = freq[0], ans = 0;

        for (int j = 1; j < 10; j++)
        {
            if (max <= freq[j]) {
                max = freq[j];
                ans = j;
            }
        }
        return (max != 0) ? ans : -1;
    }

    // Driver code
    public static void Main()
    {
        int L = 1, R = 20;
        Console.Write(maxDigitInPrimes(L, R));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the highest occurring
// digit in prime numbers in a range L to R.

// Sieve of Eratosthenes
function sieve(&$prime, $n)
{
    for ($p = 2; $p * $p <= $n; $p++)
    {
        if ($prime[$p] == false)
            for ($i = $p * 2;
                 $i <= $n; $i += $p)
                $prime[$i] = true;
    }
}

// Returns maximum occurring digits
// in primes from l to r.
function maxDigitInPrimes($L, $R)
{
    $prime = array_fill(0, $R + 1, false);

    // Finding the prime number up to R.
    sieve($prime, $R);

    // Initialise frequency of all digit to 0.
    $freq = array_fill(0, 10, 0);

    // For all number between L to R, check
    // if prime or not. If prime, incrementing
    // the frequency of digits present in the
    // prime number.
    for ($i = $L; $i <= $R; $i++)
    {
        if (!$prime[$i])
        {
            $p = $i; // If i is prime
            while ($p)
            {
                $freq[$p % 10]++;
                $p = (int)($p / 10);
            }
        }
    }

    // Finding digit with highest frequency.
    $max = $freq[0];
    $ans = 0;
    for ($j = 1; $j < 10; $j++)
    {
        if ($max <= $freq[$j])
        {
            $max = $freq[$j];
            $ans = $j;
        }
    }

    return $ans;
}

// Driver Code
$L = 1;
$R = 20;

echo maxDigitInPrimes($L, $R);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the highest occurring digit
// in prime numbers in a range L to R.

    // Sieve of Eratosthenes
    function sieve(prime,n)
    {
        for (let p = 2; p * p <= n; p++) {
            if (prime[p] == false)
                for (let i = p * 2; i <= n; i += p)
                    prime[i] = true;
        }
    }

     // Returns maximum occurring digits in primes
    // from l to r.
    function maxDigitInPrimes(L,R)
    {
        let prime=new Array(R+1);
        for(let i=0;i<R+1;i++)
        {
            prime[i]=false;
        }
        // Finding the prime number up to R.
        sieve(prime, R);

        let freq=new Array(10);
        for(let i=0;i<10;i++)
        {
            freq[i]=0;
        }
        let val;
        // For all number between L to R, check if
        // prime or not. If prime, incrementing
        // the frequency of digits present in the
        // prime number.
        for (let i = L; i <= R; i++) {

            if (!prime[i]) {
                let p = i; // If i is prime

                while (p > 0) {
                freq[p % 10]++;
                p = Math.floor(p/10);
                }
            }
        }

        // Finding digit with highest frequency.
        let max = freq[0], ans = 0;

        for (let j = 1; j < 10; j++) {
            if (max <= freq[j]) {
                max = freq[j];
                ans = j;
            }
        }

        return ans;
    }

    // Driver code
    let  L = 1, R = 20;
    document.write(maxDigitInPrimes(L, R));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
1
```

本文由[**>Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。