# 移除一个元素后最长的主子阵列

> 原文:[https://www . geeksforgeeks . org/移除一个元素后的最长质数子数组/](https://www.geeksforgeeks.org/longest-prime-subarray-after-removing-one-element/)

给定一个整数数组。我们最多可以从数组中移除一个索引。我们的目标是最大化包含所有素数的子阵的长度。打印最大长度的子阵列，只需从阵列中删除一个元素即可。

**示例:**

```
Input : arr[] = { 2, 8, 5, 7, 9, 5, 7 }
Output : 4
Explanation :If we remove the number 9 which is at index 5 then the remaining array contains a subarray whose length is 4 which is maximum.

Input : arr[] = { 2, 3, 5, 7 }
Output : 3
If we remove the number 3 which is at index 1 then the remaining array contains a subarray whose length is 3 which is maximum.
```

这个想法是在每个索引之前和之后计算连续的素数。现在再次遍历数组，找到一个前后素数之和最大的索引。

## C++

```
// CPP program to find length of the longest
// subarray with all primes except possibly
// one.
#include <bits/stdc++.h>
using namespace std;
#define N 100000

bool prime[N];

void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= N; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= N; i += p)
                prime[i] = false;
        }
    }
}

int longestPrimeSubarray(int arr[], int n)
{
    int left[n], right[n];
    int primecount = 0, res = 0;

    // left array used to count number of
    // continuous prime numbers starting
    // from left of current element
    for (int i = 0; i < n; i++) {
        left[i] = primecount;
        if (prime[arr[i]]) {
            primecount++;
        }
        else
            primecount = 0;
    }

    // right array used to count number of
    // continuous prime numbers starting from
    // right of current element
    primecount = 0;
    for (int i = n - 1; i >= 0; i--) {
        right[i] = primecount;
        if (prime[arr[i]]) {
            primecount++;
        }
        else
            primecount = 0;
    }

    for (int i = 0; i < n; i++)
        res = max(res, left[i] + right[i]);

    return res;
}

// Driver code
int main()
{
    int arr[] = { 2, 8, 5, 7, 9, 5, 7 };

    // used of SieveOfEratosthenes method to
    // detect a number prime or not
    SieveOfEratosthenes();
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "largest length of PrimeSubarray "
         << longestPrimeSubarray(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of the longest
// subarray with all primes except possibly
// one.
import java.util.*;

class GFG
{

static int N = 100000;

static boolean prime[] = new boolean[N];

static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    Arrays.fill(prime,true);

    for (int p = 2; p * p <= N; p++)
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

static int longestPrimeSubarray(int arr[], int n)
{
    int []left = new int[n];int[] right = new int[n];
    int primecount = 0, res = 0;

    // left array used to count number of
    // continuous prime numbers starting
    // from left of current element
    for (int i = 0; i < n; i++)
    {
        left[i] = primecount;
        if (prime[arr[i]])
        {
            primecount++;
        }
        else
            primecount = 0;
    }

    // right array used to count number of
    // continuous prime numbers starting from
    // right of current element
    primecount = 0;
    for (int i = n - 1; i >= 0; i--)
    {
        right[i] = primecount;
        if (prime[arr[i]])
        {
            primecount++;
        }
        else
            primecount = 0;
    }

    for (int i = 0; i < n; i++)
        res = Math.max(res, left[i] + right[i]);

    return res;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 8, 5, 7, 9, 5, 7 };

    // used of SieveOfEratosthenes method to
    // detect a number prime or not
    SieveOfEratosthenes();
    int n = arr.length;

    System.out.println("largest length of PrimeSubarray "
        + longestPrimeSubarray(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find length of the
# longest subarray with all primes except
# possibly one.
from math import sqrt
N = 100000

prime = [True for i in range(N + 1)]

def SieveOfEratosthenes():

    # Create a boolean array "prime[0..n]"
    # and initialize all entries it as true.
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    k = int(sqrt(N)) + 1
    for p in range(2, k, 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, N + 1, p):
                prime[i] = False

def longestPrimeSubarray(arr, n):
    left = [0 for i in range(n)]
    right = [0 for i in range(n)]
    primecount = 0
    res = 0

    # left array used to count number of
    # continuous prime numbers starting
    # from left of current element
    for i in range(n):
        left[i] = primecount
        if (prime[arr[i]]):
            primecount += 1

        else:
            primecount = 0

    # right array used to count number of
    # continuous prime numbers starting
    # from right of current element
    primecount = 0
    i = n - 1
    while(i >= 0):
        right[i] = primecount
        if (prime[arr[i]]):
            primecount += 1

        else:
            primecount = 0

        i -= 1

    for i in range(n):
        res = max(res, left[i] + right[i])

    return res

# Driver code
if __name__ == '__main__':
    arr = [2, 8, 5, 7, 9, 5, 7]

    # used of SieveOfEratosthenes method
    # to detect a number prime or not
    SieveOfEratosthenes()
    n = len(arr)
    print("largest length of PrimeSubarray",
               longestPrimeSubarray(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find length of the longest
// subarray with all primes except possibly
// one.
using System;

class GFG
{

    static int N = 100000;

    static bool []prime = new bool[N];

    static void SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        for(int i =0;i<N;i++)
            prime[i]=true;

        for (int p = 2; p * p <= N; p++)
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

    static int longestPrimeSubarray(int []arr, int n)
    {
        int []left = new int[n];int[] right = new int[n];
        int primecount = 0, res = 0;

        // left array used to count number of
        // continuous prime numbers starting
        // from left of current element
        for (int i = 0; i < n; i++)
        {
            left[i] = primecount;
            if (prime[arr[i]])
            {
                primecount++;
            }
            else
                primecount = 0;
        }

        // right array used to count number of
        // continuous prime numbers starting from
        // right of current element
        primecount = 0;
        for (int i = n - 1; i >= 0; i--)
        {
            right[i] = primecount;
            if (prime[arr[i]])
            {
                primecount++;
            }
            else
                primecount = 0;
        }

        for (int i = 0; i < n; i++)
            res = Math.Max(res, left[i] + right[i]);

        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 2, 8, 5, 7, 9, 5, 7 };

        // used of SieveOfEratosthenes method to
        // detect a number prime or not
        SieveOfEratosthenes();
        int n = arr.Length;

        Console.WriteLine("largest length of PrimeSubarray "
            + longestPrimeSubarray(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of
// the longest subarray with all at most
// primes except possibly one.
$N = 100000;
$prime = array_fill(0, $N, true);

function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as
    // true. A value in prime[i] will 
    // finally be false if i is Not a
    // prime, else true.
    global $prime, $N;

    for ($p = 2; $p * $p <= $N; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $N; $i += $p)
                $prime[$i] = false;
        }
    }
}

function longestPrimeSubarray($arr, $n)
{
    global $prime, $N;
    $left = array($n);
    $right = array($n);
    $primecount = 0;
    $res = 0;

    // left array used to count number of
    // continuous prime numbers starting
    // from left of current element
    for ($i = 0; $i < $n; $i++)
    {
        $left[$i] = $primecount;
        if ($prime[$arr[$i]])
        {
            $primecount++;
        }
        else
            $primecount = 0;
    }

    // right array used to count number
    // of continuous prime numbers starting
    // from right of current element
    $primecount = 0;
    for ($i = $n - 1; $i >= 0; $i--)
    {
        $right[$i] = $primecount;
        if ($prime[$arr[$i]])
        {
            $primecount++;
        }
        else
            $primecount = 0;
    }

    for ($i = 0; $i < $n; $i++)
        $res = max($res, $left[$i] +   
                         $right[$i]);

    return $res;
}

// Driver Code
$arr = array(2, 8, 5, 7, 9, 5, 7);

// used of SieveOfEratosthenes method
// to detect a number prime or not
SieveOfEratosthenes();
$n = count($arr);

echo "largest length of PrimeSubarray " .
      longestPrimeSubarray($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find length of the longest
// subarray with all primes except possibly
// one.
var N = 100000;
var prime = Array.from({length: N}, (_, i) => true);

function SieveOfEratosthenes()
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    for (var p = 2; p * p <= N; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(var i = p * 2; i < N; i += p)
                prime[i] = false;
        }
    }
}

function longestPrimeSubarray(arr , n)
{
    var left = Array.from({length: n}, (_, i) => 0);
    var right = Array.from({length: n}, (_, i) => 0);
    var primecount = 0, res = 0;

    // Left array used to count number of
    // continuous prime numbers starting
    // from left of current element
    for(var i = 0; i < n; i++)
    {
        left[i] = primecount;
        if (prime[arr[i]])
        {
            primecount++;
        }
        else
            primecount = 0;
    }

    // Right array used to count number of
    // continuous prime numbers starting from
    // right of current element
    primecount = 0;
    for(var i = n - 1; i >= 0; i--)
    {
        right[i] = primecount;
        if (prime[arr[i]])
        {
            primecount++;
        }
        else
            primecount = 0;
    }

    for(var i = 0; i < n; i++)
        res = Math.max(res, left[i] + right[i]);

    return res;
}

// Driver code
var arr = [ 2, 8, 5, 7, 9, 5, 7 ];

// Used of SieveOfEratosthenes method to
// detect a number prime or not
SieveOfEratosthenes();
var n = arr.length;

document.write("largest length of PrimeSubarray " +
      longestPrimeSubarray(arr, n));

// This code is contributed by shikhasingrajput

</script>
```

**Output:** 

```
largest length of PrimeSubarray 4
```