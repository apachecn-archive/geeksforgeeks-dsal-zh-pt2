# 计算一个数组中的孪生素数对

> 原文:[https://www . geesforgeks . org/count-twin-prime-pairs-in-a-array/](https://www.geeksforgeeks.org/count-twin-prime-pairs-in-an-array/)

给定一个由 **N** 个自然数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是计算**arr【】**中所有可能的配对，它们是[孪生素数](https://www.geeksforgeeks.org/twin-prime-numbers-between-1-and-n/)。
A **双素数**是那些素数并且两个素数之间相差两(2)的数。换句话说，孪生素数是素数差距为 2 的素数。

**示例:**

> **输入:** arr[] = { 2，3，5，7}
> **输出:** 2
> **解释:**
> 这 2 对是(3，5)和(5，7)。
> 
> **输入:** arr[] = { 2，4，6，11}
> **输出:** 0
> **说明:**
> 不存在这样的成对孪生素数。

**天真方法:**
想法是在给定的[数组中找到所有可能的对](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**并检查成对的两个元素是否都是[素数](https://www.geeksforgeeks.org/prime-numbers/)并且它们相差 **2** ，然后当前对形成[孪生素数](https://www.geeksforgeeks.org/twin-prime-numbers-between-1-and-n/)。

下面是上述方法的实现:

## C++

```
// C++ program to count Twin
// Prime pairs in array
#include <bits/stdc++.h>
using namespace std;

// A utility function to check if
// the number n is prime or not
bool isPrime(int n)
{
    // Base Cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check to skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i += 6) {

        // If n is divisible by i and i+2
        // then it is not prime
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// A utility function that check
// if n1 and n2 are Twin Primes
// or not
bool twinPrime(int n1, int n2)
{
    return (isPrime(n1)
            && isPrime(n2)
            && abs(n1 - n2) == 2);
}

// Function to find Twin Prime
// pairs from the given array
int countTwinPairs(int arr[], int n)
{
    int count = 0;

    // Iterate through all pairs
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Increment count if
            // twin prime pair
            if (twinPrime(arr[i], arr[j])) {
                count++;
            }
        }
    }

    return count;
}

// Driver's code
int main()
{
    int arr[] = { 2, 3, 5, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to find
    // Twin Primes pair
    cout << countTwinPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count Twin
// Prime pairs in array
import java.util.*;

class GFG{

// A utility function to check if
// the number n is prime or not
static boolean isPrime(int n)
{
    // Base Cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check to skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i += 6) {

        // If n is divisible by i and i+2
        // then it is not prime
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// A utility function that check
// if n1 and n2 are Twin Primes
// or not
static boolean twinPrime(int n1, int n2)
{
    return (isPrime(n1)
            && isPrime(n2)
            && Math.abs(n1 - n2) == 2);
}

// Function to find Twin Prime
// pairs from the given array
static int countTwinPairs(int arr[], int n)
{
    int count = 0;

    // Iterate through all pairs
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Increment count if
            // twin prime pair
            if (twinPrime(arr[i], arr[j])) {
                count++;
            }
        }
    }

    return count;
}

// Driver's code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 5, 11 };
    int n = arr.length;

    // Function call to find
    // Twin Primes pair
    System.out.print(countTwinPairs(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to count Twin
# Prime pairs in array
from math import sqrt

# A utility function to check if
# the number n is prime or not
def isPrime(n):

    # Base Cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # Check to skip middle five
    # numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5,int(sqrt(n))+1,6):

        # If n is divisible by i and i+2
        # then it is not prime
        if (n % i == 0 or n % (i + 2) == 0):
            return False

    return True

# A utility function that check
# if n1 and n2 are Twin Primes
# or not
def twinPrime(n1, n2):
    return (isPrime(n1) and isPrime(n2) and abs(n1 - n2) == 2)

# Function to find Twin Prime
# pairs from the given array
def countTwinPairs(arr, n):
    count = 0

    # Iterate through all pairs
    for i in range(n):
        for j in range(i + 1,n):

            # Increment count if
            # twin prime pair
            if (twinPrime(arr[i], arr[j])):
                count += 1

    return count

# Driver's code
if __name__ == '__main__':
    arr = [2, 3, 5, 11]
    n = len(arr)

    # Function call to find
    # Twin Primes pair
    print(countTwinPairs(arr, n))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to count Twin
// Prime pairs in array
using System;

class GFG{

// A utility function to check if
// the number n is prime or not
static bool isPrime(int n)
{
    // Base Cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check to skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i += 6) {

        // If n is divisible by i and i+2
        // then it is not prime
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// A utility function that check
// if n1 and n2 are Twin Primes
// or not
static bool twinPrime(int n1, int n2)
{
    return (isPrime(n1)
            && isPrime(n2)
            && Math.Abs(n1 - n2) == 2);
}

// Function to find Twin Prime
// pairs from the given array
static int countTwinPairs(int []arr, int n)
{
    int count = 0;

    // Iterate through all pairs
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Increment count if
            // twin prime pair
            if (twinPrime(arr[i], arr[j])) {
                count++;
            }
        }
    }

    return count;
}

// Driver's code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 5, 11 };
    int n = arr.Length;

    // Function call to find
    // Twin Primes pair
    Console.Write(countTwinPairs(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// A utility function to check if
// the number n is prime or not
function isPrime(n)
{
    // Base Cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check to skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (var i = 5; i * i <= n; i += 6) {

        // If n is divisible by i and i+2
        // then it is not prime
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// A utility function that check
// if n1 and n2 are Twin Primes
// or not
function twinPrime(n1, n2)
{
    return (isPrime(n1)
            && isPrime(n2)
            && Math.abs(n1 - n2) == 2);
}

// Function to find Twin Prime
// pairs from the given array
function countTwinPairs(arr, n)
{
    var count = 0;

    // Iterate through all pairs
    for (var i = 0; i < n; i++) {
        for (var j = i + 1; j < n; j++) {

            // Increment count if
            // twin prime pair
            if (twinPrime(arr[i], arr[j])) {
                count++;
            }
        }
    }

    return count;
}

// Driver code
var arr=[ 2, 3, 5, 11 ];
var n = arr.length;

document.write(countTwinPairs(arr, n));

// This code is contributed by Shivanisingh
</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(sqrt(M)*N <sup>2</sup> ，其中 N 为给定数组中的元素个数，M 为数组中的最大元素个数。

**有效方法:**

1.  使用厄拉多塞的[筛，预计算所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[素数](https://www.geeksforgeeks.org/prime-numbers/)直到给定数组**arr【】**中的最大数。
2.  为给定的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 存储所有元素的所有频率。
3.  排序给定的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。
4.  对于[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中的每个元素，检查该元素是否为质数。
5.  如果元素是，[质数](https://www.geeksforgeeks.org/prime-numbers/)，那么检查(元素+2)是否是一个[质数](https://www.geeksforgeeks.org/prime-numbers/)并且存在于给定的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**中。
6.  如果(元素+2)存在，那么(元素+2)的频率将给出当前元素的对的计数。
7.  对[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中的所有元素重复上述步骤。