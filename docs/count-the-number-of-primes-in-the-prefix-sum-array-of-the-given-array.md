# 统计给定数组的前缀和数组中的素数

> 原文:[https://www . geesforgeks . org/count-给定数组的前缀和数组中的素数数/](https://www.geeksforgeeks.org/count-the-number-of-primes-in-the-prefix-sum-array-of-the-given-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是计算给定数组的前缀和数组中的素数。
**例:**

> **输入:** arr[] = {1，4，8，4}
> **输出:** 3
> 前缀和数组为{1，5，13，17}
> ，三个素数为 5，13，17。
> **输入:** arr[] = {1，5，2，3，7，9}
> **输出:** 1

**方法:**创建前缀和数组，然后使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)统计前缀和数组中的素数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of primes
// in the given array
int primeCount(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr + n);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Find all primes in arr[]
    int count = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            count++;

    return count;
}

// Function to generate the prefix array
void getPrefixArray(int arr[], int n, int pre[])
{

    // Fill the prefix array
    pre[0] = arr[0];
    for (int i = 1; i < n; i++) {
        pre[i] = pre[i - 1] + arr[i];
    }
}

// Driver code
int main()
{

    int arr[] = { 1, 4, 8, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Prefix array of arr[]
    int pre[n];
    getPrefixArray(arr, n, pre);

    // Count of primes in the prefix array
    cout << primeCount(pre, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

//returns the max element
static int max_element(int a[])
{
    int m = a[0];
    for(int i = 0; i < a.length; i++)
        m = Math.max(a[i], m);

    return m;
}

// Function to return the count of primes
// in the given array
static int primeCount(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = max_element(arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean prime[] = new boolean[max_val + 1];
    for (int p = 0; p <= max_val; p++)
        prime[p] = true;

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Find all primes in arr[]
    int count = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            count++;

    return count;
}

// Function to generate the prefix array
static int[] getPrefixArray(int arr[], int n, int pre[])
{

    // Fill the prefix array
    pre[0] = arr[0];
    for (int i = 1; i < n; i++)
    {
        pre[i] = pre[i - 1] + arr[i];
    }
    return pre;
}

// Driver code
public static void main(String args[])
{

    int arr[] = { 1, 4, 8, 4 };
    int n = arr.length;

    // Prefix array of arr[]
    int pre[]=new int[n];
    pre=getPrefixArray(arr, n, pre);

    // Count of primes in the prefix array
    System.out.println(primeCount(pre, n));

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of primes in the given array
def primeCount(arr, n):

    # Find maximum value in the array
    max_val = max(arr)

    # USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    # THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]". A
    # value in prime[i] will finally be False
    # if i is Not a prime, else True.
    prime = [True] * (max_val+1)

    # Remaining part of SIEVE
    prime[0] = prime[1] = False
    p = 2
    while p * p <= max_val: 

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True: 

            # Update all multiples of p
            for i in range(p * 2, max_val+1, p):
                prime[i] = False

        p += 1

    # Find all primes in arr[]
    count = 0
    for i in range(0, n):
        if prime[arr[i]]:
            count += 1

    return count

# Function to generate the prefix array
def getPrefixArray(arr, n, pre):

    # Fill the prefix array
    pre[0] = arr[0]
    for i in range(1, n): 
        pre[i] = pre[i - 1] + arr[i]

# Driver code
if __name__ == "__main__":

    arr = [1, 4, 8, 4] 
    n = len(arr)

    # Prefix array of arr[]
    pre = [None] * n
    getPrefixArray(arr, n, pre)

    # Count of primes in the prefix array
    print(primeCount(pre, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// returns the max element
static int max_element(int[] a)
{
    int m = a[0];
    for(int i = 0; i < a.Length; i++)
        m = Math.Max(a[i], m);

    return m;
}

// Function to return the count of primes
// in the given array
static int primeCount(int[] arr, int n)
{
    // Find maximum value in the array
    int max_val = max_element(arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a bool array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool[] prime = new bool[max_val + 1];
    for (int p = 0; p <= max_val; p++)
        prime[p] = true;

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Find all primes in arr[]
    int count = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            count++;

    return count;
}

// Function to generate the prefix array
static int[] getPrefixArray(int[] arr, int n, int[] pre)
{

    // Fill the prefix array
    pre[0] = arr[0];
    for (int i = 1; i < n; i++)
    {
        pre[i] = pre[i - 1] + arr[i];
    }
    return pre;
}

// Driver code
public static void Main()
{

    int[] arr = { 1, 4, 8, 4 };
    int n = arr.Length;

    // Prefix array of arr[]
    int[] pre = new int[n];
    pre = getPrefixArray(arr, n, pre);

    // Count of primes in the prefix array
    Console.Write(primeCount(pre, n));

}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of primes
// in the given array
function primeCount($arr, $n)
{
    // Find maximum value in the array
    $max_val = max($arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime = array_fill(0, $max_val + 1, true);

    // Remaining part of SIEVE
    $prime[0] = false;
    $prime[1] = false;
    for ($p = 2; $p * $p <= $max_val; $p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $max_val; $i += $p)
                $prime[$i] = false;
        }
    }

    // Find all primes in arr[]
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        if ($prime[$arr[$i]])
            $count++;

    return $count;
}

// Function to generate the prefix array
function getPrefixArray($arr, $n, $pre)
{

    // Fill the prefix array
    $pre[0] = $arr[0];
    for ($i = 1; $i < $n; $i++)
    {
        $pre[$i] = $pre[$i - 1] + $arr[$i];
    }
    return $pre ;
}

// Driver code
$arr = array( 1, 4, 8, 4 );
$n = count($arr) ;

// Prefix array of arr[]
$pre = array();
$pre = getPrefixArray($arr, $n, $pre);

// Count of primes in the prefix array
echo primeCount($pre, $n);

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of primes
// in the given array
function primeCount(arr, n)
{
    // Find maximum value in the array
    let max_val = Math.max(...arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    let prime = new Array(max_val + 1).fill(true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (let p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Find all primes in arr[]
    let count = 0;
    for (let i = 0; i < n; i++)
        if (prime[arr[i]])
            count++;

    return count;
}

// Function to generate the prefix array
function getPrefixArray(arr, n, pre)
{

    // Fill the prefix array
    pre[0] = arr[0];
    for (let i = 1; i < n; i++) {
        pre[i] = pre[i - 1] + arr[i];
    }
}

// Driver code

    let arr = [ 1, 4, 8, 4 ];
    let n = arr.length;

    // Prefix array of arr[]
    let pre = new Array(n);
    getPrefixArray(arr, n, pre);

    // Count of primes in the prefix array
    document.write(primeCount(pre, n));

</script>
```

**Output:** 

```
3
```