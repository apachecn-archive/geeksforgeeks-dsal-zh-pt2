# 对数组中的对进行计数，使得至少一个元素是质数

> 原文:[https://www . geesforgeks . org/count-pairs-in-a-array-so-至少有一个元素是质数/](https://www.geeksforgeeks.org/count-pairs-in-an-array-such-that-at-least-one-element-is-prime/)

给定不同元素的数组 **arr[]** ，任务是计算其中至少有一个元素是素数的不同对的总数。
**例:**

```
Input: arr[] = {1, 3, 10, 7, 8}
Output: 7
Pairs with at least one prime are (1, 3), (1, 7), 
(3, 1), (3, 7), (3, 8), (10, 7), (7, 8).

Input:arr[]={4, 6, 8, 2, 9};
Output: 4
```

**进场:**先用 [**筛**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 将所有质数预计算至[阵最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。遍历每一个可能的对，检查对中是否有任何元素是质数。如果是，则增加计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find primes
void sieve(int maxm, int prime[])
{
    prime[0] = prime[1] = 1;

    for (int i = 2; i * i <= maxm; i++)
        if (!prime[i])
            for (int j = 2 * i; j <= maxm; j += i)
                prime[j] = 1;
}

// Function to count the pair
int countPair(int a[], int n)
{
    // Find the maximum element of the array
    int maxm = *max_element(a, a + n);
    int prime[maxm + 1];
    memset(prime, 0, sizeof(prime));

    // Find primes upto maximum
    sieve(maxm, prime);

    // Count pairs with at least prime
    int count = 0;
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (prime[a[i]] == 0 || prime[a[j]] == 0)
                count++;

    return count;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 5, 4, 7 };
    int n = 5;

    cout << countPair(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    // Function to find primes
    static void sieve(int maxm, int prime[])
    {
        prime[0] = prime[1] = 1;

        for (int i = 2; i * i <= maxm; i++)
            if (prime[i] == 0)
                for (int j = 2 * i; j <= maxm; j += i)
                    prime[j] = 1;
    }

    // Function to count the pair
    static int countPair(int a[], int n)
    {
        // Find the maximum element of the array
        int maxm = a[0];

        for(int i = 1; i < n; i++)
            if(a[i] > maxm)
            maxm = a[i];

        int [] prime = new int[maxm + 1];

        for(int i = 0; i < maxm + 1; i++)
            prime[i] = 0;

        // Find primes upto maximum
        sieve(maxm, prime);

        // Count pairs with at least prime
        int count = 0;
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (prime[a[i]] == 0 || prime[a[j]] == 0)
                    count++;

        return count;
    }

    // Driver code
    public static void main(String []args)
    {
        int arr[] = { 2, 3, 5, 4, 7 };
        int n = arr.length;
        System.out.println(countPair(arr, n));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach
from math import sqrt

# Function to count the pair
def countPair(a, n):

    # Find the maximum element of the array
    maxm = a[0]
    for i in range(len(a)):
        if(a[i] > maxm):
            maxm = a[i]
    prime = [0 for i in range(maxm + 1)]

    # Find primes upto maximum
    prime[0] = prime[1] = 1;

    for i in range(2, int(sqrt(maxm)) + 1, 1):
        if (prime[i] == 0):
            for j in range(2 * i, maxm + 1, i):
                prime[j] = 1

    # Count pairs with at least prime
    count = 0
    for i in range(n):
        for j in range(i + 1, n, 1):
            if (prime[a[i]] == 0 or
                prime[a[j]] == 0):
                count += 1

    return count

# Driver code
if __name__ == '__main__':
    arr = [2, 3, 5, 4, 7]
    n = 5

    print(countPair(arr, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Function to find primes
    static void sieve(int maxm, int []prime)
    {
        prime[0] = prime[1] = 1;

        for (int i = 2; i * i <= maxm; i++)
            if (prime[i] == 0)
                for (int j = 2 * i; j <= maxm; j += i)
                    prime[j] = 1;
    }

    // Function to count the pair
    static int countPair(int []a, int n)
    {
        // Find the maximum element of the array
        int maxm = a[0];

        for(int i = 1; i < n; i++)
            if(a[i] > maxm)
            maxm = a[i];

        int [] prime = new int[maxm + 1];

        for(int i = 0; i < maxm + 1; i++)
            prime[i] = 0;

        // Find primes upto maximum
        sieve(maxm, prime);

        // Count pairs with at least prime
        int count = 0;
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)
                if (prime[a[i]] == 0 || prime[a[j]] == 0)
                    count++;

        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 3, 5, 4, 7 };
        int n = arr.Length;
        Console.WriteLine(countPair(arr, n));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find primes
function sieve($maxm, $prime)
{
    $prime[0] = $prime[1] = 1;

    for ($i = 2; $i * $i <= $maxm; $i++)
        if (!$prime[$i])
            for ($j = 2 * $i;
                 $j <= $maxm; $j += $i)
                $prime[$j] = 1;
}

// Function to count the pair
function countPair($a, $n)
{
    // Find the maximum element of the array
    $maxm = max($a);
    $prime = array();

    $prime = array_fill(0, $maxm + 1, 0);

    // Find primes upto maximum
    sieve($maxm, $prime);

    // Count pairs with at least prime
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            if ($prime[$a[$i]] == 0 ||
                $prime[$a[$j]] == 0)
                $count++;

    return $count;
}

// Driver code
$arr = array( 2, 3, 5, 4, 7 );
$n = 5;

echo countPair($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

    // Function to find primes
    function sieve(maxm,prime)
    {
        prime[0] = prime[1] = 1;

        for (let i = 2; i * i <= maxm; i++)
            if (prime[i] == 0)
                for (let j = 2 * i; j <= maxm; j += i)
                    prime[j] = 1;
    }

    // Function to count the pair
    function countPair(a,n)
    {
        // Find the maximum element of the array
        let maxm = a[0];

        for(let i = 1; i < n; i++)
            if(a[i] > maxm)
            maxm = a[i];

        let prime = new Array(maxm + 1);

        for(let i = 0; i < maxm + 1; i++)
            prime[i] = 0;

        // Find primes upto maximum
        sieve(maxm, prime);

        // Count pairs with at least prime
        let count = 0;
        for (let i = 0; i < n; i++)
            for (let j = i + 1; j < n; j++)
                if (prime[a[i]] == 0 || prime[a[j]] == 0)
                    count++;

        return count;
    }

    // Driver code
    let arr=[2, 3, 5, 4, 7];
    let n = arr.length;
    document.write(countPair(arr, n));

    // This code is contributed by unknown2108

</script>
```

**Output:** 

```
10
```

**高效进场:**
**进场:**先用 [**筛**](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 将所有质数预计算至[阵的最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。保持素数和非素数的计数。然后用单质数对，即**非质数*质数**，用两个质数**(质数*(质数–1))/2**计数对。返回两个计数的总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find primes
void sieve(int maxm, int prime[])
{
    prime[0] = prime[1] = 1;

    for (int i = 2; i * i <= maxm; i++)
        if (!prime[i])
            for (int j = 2 * i; j <= maxm; j += i)
                prime[j] = 1;
}

ll countPair(int a[], int n)
{
    // Find the maximum element of the array
    int maxm = *max_element(a, a + n);
    int prime[maxm + 1];
    memset(prime, 0, sizeof(prime));

    // Find primes upto maximum
    sieve(maxm, prime);

    // Count number of primes
    int countPrimes = 0;
    for (int i = 0; i < n; i++)
        if (prime[a[i]] == 0)
            countPrimes++;

    int nonPrimes = n - countPrimes;
    ll pairswith1Prime = nonPrimes * countPrimes;
    ll pairsWith2Primes = (countPrimes * (countPrimes - 1)) / 2;

    return pairswith1Prime + pairsWith2Primes;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 5, 4, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countPair(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    // Function to find primes
    static void sieve(int maxm, int []prime)
    {
        prime[0] = prime[1] = 1;

        for (int i = 2; i * i <= maxm; i++)
            if (prime[i]==0)
                for (int j = 2 * i; j <= maxm; j += i)
                    prime[j] = 1;
    }

    static long countPair(int []a, int n)
    {
        // Find the maximum element of the array
        int maxm = a[0];

        int i;
        for( i = 1; i < n ; i++)
            if(a[i] > maxm)
                maxm = a[i];

        int [] prime = new int[maxm + 1];

        for( i = 0; i < maxm + 1 ;i++)
            prime[i] = 0;

        // Find primes upto maximum
        sieve(maxm, prime);

        // Count number of primes
        int countPrimes = 0;
        for ( i = 0; i < n; i++)
            if (prime[a[i]] == 0)
                countPrimes++;

        int nonPrimes = n - countPrimes;
        long pairswith1Prime = nonPrimes *
                                countPrimes;
        long pairsWith2Primes = (countPrimes *
                            (countPrimes - 1)) / 2;

        return pairswith1Prime + pairsWith2Primes;
    }

    // Driver code
    public static void main(String []args)
    {
        int [] arr = { 2, 3, 5, 4, 7 };
        int n = arr.length;

        System.out.println(countPair(arr, n));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find primes
def sieve(maxm, prime):

    prime[0] = prime[1] = 1;
    i = 2;

    while (i * i <= maxm):
        if (prime[i] == 0):
            for j in range(2 * i, maxm + 1, i):
                prime[j] = 1;
        i += 1;

def countPair(a, n):

    # Find the maximum element
    # of the array
    maxm = max(a);
    prime = [0] * (maxm + 1);

    # Find primes upto maximum
    sieve(maxm, prime);

    # Count number of primes
    countPrimes = 0;
    for i in range(n):
        if (prime[a[i]] == 0):
            countPrimes += 1;

    nonPrimes = n - countPrimes;
    pairswith1Prime = nonPrimes * countPrimes;
    pairsWith2Primes = (countPrimes *
                       (countPrimes - 1)) // 2;

    return pairswith1Prime + pairsWith2Primes;

# Driver code
arr = [ 2, 3, 5, 4, 7 ];
n = len(arr);

print(countPair(arr, n));

# This code is contributed by mits
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    // Function to find primes
    static void sieve(int maxm, int []prime)
    {
        prime[0] = prime[1] = 1;

        for (int i = 2; i * i <= maxm; i++)
            if (prime[i] == 0)
                for (int j = 2 * i; j <= maxm; j += i)
                    prime[j] = 1;
    }

    static long countPair(int []a, int n)
    {
        // Find the maximum element of the array
        int maxm = a[0];

        int i;
        for( i = 1; i < n ;i++)
            if(a[i] > maxm)
                maxm = a[i];

        int [] prime = new int[maxm + 1];

        for( i = 0; i < maxm + 1 ;i++)
            prime[i] = 0;

        // Find primes upto maximum
        sieve(maxm, prime);

        // Count number of primes
        int countPrimes = 0;
        for ( i = 0; i < n; i++)
            if (prime[a[i]] == 0)
                countPrimes++;

        int nonPrimes = n - countPrimes;
        long pairswith1Prime = nonPrimes *
                                countPrimes;
        long pairsWith2Primes = (countPrimes *
                            (countPrimes - 1)) / 2;

        return pairswith1Prime + pairsWith2Primes;
    }

    // Driver code
    public static void Main()
    {
        int [] arr = { 2, 3, 5, 4, 7 };
        int n = arr.Length;
        Console.WriteLine(countPair(arr, n));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find primes
function sieve($maxm, $prime)
{
    $prime[0] = $prime[1] = 1;

    for ($i = 2; $i * $i <= $maxm; $i++)
        if (!$prime[$i])
            for ($j = 2 * $i;
                 $j <= $maxm; $j += $i)
                $prime[$j] = 1;
}

function countPair($a, $n)
{
    // Find the maximum element
    // of the array
    $maxm = max($a);
    $prime = array_fill(0, $maxm + 1,0);

    // Find primes upto maximum
    sieve($maxm, $prime);

    // Count number of primes
    $countPrimes = 0;
    for ($i = 0; $i < $n; $i++)
        if ($prime[$a[$i]] == 0)
            $countPrimes++;

    $nonPrimes = $n - $countPrimes;
    $pairswith1Prime = $nonPrimes * $countPrimes;
    $pairsWith2Primes = ($countPrimes *
                        ($countPrimes - 1)) / 2;

    return $pairswith1Prime + $pairsWith2Primes;
}

// Driver code
$arr = array( 2, 3, 5, 4, 7 );
$n = count($arr);

echo countPair($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Function to find primes
    function sieve(maxm, prime)
    {
        prime[0] = prime[1] = 1;

        for (let i = 2; i * i <= maxm; i++)
            if (prime[i] == 0)
                for (let j = 2 * i; j <= maxm; j += i)
                    prime[j] = 1;
    }

    function countPair(a, n)
    {
        // Find the maximum element of the array
        let maxm = a[0];

        let i;
        for( i = 1; i < n ;i++)
            if(a[i] > maxm)
                maxm = a[i];

        let prime = new Array(maxm + 1);

        for( i = 0; i < maxm + 1 ;i++)
            prime[i] = 0;

        // Find primes upto maximum
        sieve(maxm, prime);

        // Count number of primes
        let countPrimes = 0;
        for ( i = 0; i < n; i++)
            if (prime[a[i]] == 0)
                countPrimes++;

        let nonPrimes = n - countPrimes;
        let pairswith1Prime = nonPrimes * countPrimes;
        let pairsWith2Primes = parseInt((countPrimes *
        (countPrimes - 1)) / 2, 10);

        return (pairswith1Prime + pairsWith2Primes);
    }

    let arr = [ 2, 3, 5, 4, 7 ];
    let n = arr.length;
    document.write(countPair(arr, n));

</script>
```

**Output:** 

```
10
```