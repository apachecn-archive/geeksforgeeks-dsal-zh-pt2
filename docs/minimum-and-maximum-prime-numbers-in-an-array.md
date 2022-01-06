# 数组中最小和最大素数

> 原文:[https://www . geesforgeks . org/最小和最大素数数组/](https://www.geeksforgeeks.org/minimum-and-maximum-prime-numbers-in-an-array/)

给定一个由 N 个正整数组成的数组 arr[]。任务是找到给定数组中的最小和最大素元素。
**例:**

```
Input: arr[] = 1, 3, 4, 5, 7
Output: Minimum : 3
        Maximum : 7

Input: arr[] = 1, 2, 3, 4, 5, 6, 7, 11
Output: Minimum : 2
        Maximum : 11
```

**天真方法:**
取一个变量最小和最大。用 INT_MAX 初始化最小值，用 INT_MIN 初始化最大值。遍历数组，不断检查每个元素是否是质数，同时更新最小和最大质数。
**高效方法:**
使用厄拉多塞筛生成数组中最大元素的所有素数，并将它们存储在哈希中。现在遍历数组，并使用哈希表找到素数的最小和最大元素。
以下是上述方法的实施:

## C++

```
// CPP program to find minimum and maximum
// prime number in given array.
#include <bits/stdc++.h>
using namespace std;

// Function to find count of prime
void prime(int arr[], int n)
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

    // Minimum and Maximum prime number
    int minimum = INT_MAX;
    int maximum = INT_MIN;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]]) {
            minimum = min(minimum, arr[i]);
            maximum = max(maximum, arr[i]);
        }

    cout << "Minimum : " << minimum << endl;
    cout << "Maximum : " << maximum << endl;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    prime(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum and maximum
// prime number in given array.
import java.util.*;

class GFG {

// Function to find count of prime
static void prime(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = Arrays.stream(arr).max().getAsInt();

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    Vector<Boolean> prime = new Vector<Boolean>();
        for(int i= 0;i<max_val+1;i++)
            prime.add(Boolean.TRUE);

    // Remaining part of SIEVE
    prime.add(0, Boolean.FALSE);
    prime.add(1, Boolean.FALSE);
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime.get(p) == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime.add(i, Boolean.FALSE);
        }
    }

    // Minimum and Maximum prime number
    int minimum = Integer.MAX_VALUE;
    int maximum = Integer.MIN_VALUE;
    for (int i = 0; i < n; i++)
        if (prime.get(arr[i])) {
            minimum = Math.min(minimum, arr[i]);
            maximum = Math.max(maximum, arr[i]);
        }

    System.out.println("Minimum : " + minimum) ;
    System.out.println("Maximum : " + maximum );
}

// Driver code
    public static void main(String[] args) {
        int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = arr.length;

    prime(arr, n);
    }
}
/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python3 program to find minimum and
# maximum prime number in given array.
import math as mt

# Function to find count of prime
def Prime(arr, n):

    # Find maximum value in the array
    max_val = max(arr)

    # USE SIEVE TO FIND ALL PRIME NUMBERS
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    for p in range(2, mt.ceil(mt.sqrt(max_val))):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(2 * p, max_val + 1, p):
                    prime[i] = False

    # Minimum and Maximum prime number
    minimum = 10**9
    maximum = -10**9
    for i in range(n):
        if (prime[arr[i]] == True):
            minimum = min(minimum, arr[i])
            maximum = max(maximum, arr[i])

    print("Minimum : ", minimum )
    print("Maximum : ", maximum )

# Driver code
arr = [1, 2, 3, 4, 5, 6, 7]
n = len(arr)

Prime(arr, n)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// A C# program to find minimum and maximum
// prime number in given array.
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

// Function to find count of prime
static void prime(int []arr, int n)
{
    // Find maximum value in the array
    int max_val = arr.Max();

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    List<bool>prime = new List<bool>();
        for(int i = 0; i < max_val + 1;i++)
            prime.Add(true);

    // Remaining part of SIEVE
    prime.Insert(0, false);
    prime.Insert(1, false);
    for (int p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime.Insert(i, false);
        }
    }

    // Minimum and Maximum prime number
    int minimum = int.MaxValue;
    int maximum = int.MinValue;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
        {
            minimum = Math.Min(minimum, arr[i]);
            maximum = Math.Max(maximum, arr[i]);
        }

    Console.WriteLine("Minimum : " + minimum) ;
    Console.WriteLine("Maximum : " + maximum );
}

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 4, 5, 6, 7 };
        int n = arr.Length;

        prime(arr, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program to find minimum and maximum
// prime number in given array.

// Function to find count of prime
function prime(arr, n)
{
    // Find maximum value in the array
    let max_val = arr.sort((b, a) => a - b)[0];

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

    // Minimum and Maximum prime number
    let minimum = Number.MAX_SAFE_INTEGER;
    let maximum = Number.MIN_SAFE_INTEGER;
    for (let i = 0; i < n; i++)
        if (prime[arr[i]]) {
            minimum = Math.min(minimum, arr[i]);
            maximum = Math.max(maximum, arr[i]);
        }

    document.write("Minimum : " + minimum + "<br>");
    document.write("Maximum : " + maximum + "<br>");
}

// Driver code

let arr = [1, 2, 3, 4, 5, 6, 7];
let n = arr.length;

prime(arr, n);

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
Minimum : 2
Maximum : 7
```

**时间复杂度:** O(n*log(log(n)))