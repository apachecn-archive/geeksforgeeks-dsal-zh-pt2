# 最长子序列的长度，每个元素的数字之和作为一个合成数

> 原文:[https://www . geesforgeks . org/最长子序列长度每个元素的数字总和为一个复合数字/](https://www.geeksforgeeks.org/length-of-longest-subsequence-having-sum-of-digits-of-each-element-as-a-composite-number/)

给定一个由非负整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是打印给定数组中最长子序列的长度，其每个元素的数字总和是一个[复合数字](https://www.geeksforgeeks.org/composite-number/)。

**示例:**

> **输入:** arr[] = {13，55，7，3，5，21，233，144，89}
> **输出:** 4
> **解释:**以下数组元素的位数总和等于一个复合数:
> 
> *   13 -> 1 + 3 = 4
> *   55 -> 5 + 5 = 10
> *   233 -> 2 + 3 + 3 = 8
> *   144 -> 1 + 4 + 4 = 9
> 
> 因此，所需的最长子序列是长度为 4 的{13，55，233，144}。
> 
> **输入:** arr[] = {34，13，11，8，3，55，23}
> **输出:** 3
> **解释:**以下数组元素的数字总和等于一个复合数字:
> 
> *   13 -> 1 + 3 = 4
> *   8 -> 8 = 8
> *   55 -> 5 + 5 = 10
> 
> 因此，所需的最长子序列是长度为 3 的{13，8，55}。

**方法:**按照下面给出的步骤解决问题:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   对于每个数组元素，检查其数字的[和是](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)[质数](https://www.geeksforgeeks.org/prime-numbers/)还是[质数](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)，其数字的[和是否等于 **1** 。](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)
*   如果它的数字之和是质数，那么进入下一个数组元素。否则，将所需子序列的长度增加 **1** 。
*   最后，在完成数组遍历后，打印得到的子序列的长度。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

#define N 100005

// Function to generate prime numbers
// using Sieve of Eratosthenes
void SieveOfEratosthenes(bool prime[],
                         int p_size)
{
    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for (int p = 2; p * p <= p_size; p++) {

        // If p is a prime
        if (prime[p]) {

            // Set all multiples of p as non-prime
            for (int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the digit sum
// of a given number
int digitSum(int number)
{
    // Stores the sum of digits
    int sum = 0;
    while (number > 0) {

        // Extract digits and
        // add to the sum
        sum += (number % 10);
        number /= 10;
    }

    // Return the sum
    // of the digits
    return sum;
}

// Function to find the longest subsequence
// with sum of digits of each element equal
// to a composite number
void longestCompositeDigitSumSubsequence(
    int arr[], int n)
{
    int count = 0;
    bool prime[N + 1];
    memset(prime, true, sizeof(prime));

    SieveOfEratosthenes(prime, N);

    for (int i = 0; i < n; i++) {

        // Calculate sum of digits
        // of current array element
        int res = digitSum(arr[i]);

        // If sum of digits
        // equal to 1
        if (res == 1) {
            continue;
        }

        // If sum of digits is
        // a prime
        if (!prime[res]) {
            count++;
        }
    }
    cout << count << endl;
}

// Driver Code
int main()
{

    int arr[] = { 13, 55, 7, 3, 5, 1,
                  10, 21, 233, 144, 89 };
    int n = sizeof(arr)
            / sizeof(arr[0]);

    // Function call
    longestCompositeDigitSumSubsequence(
        arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;

class GFG{

static int N = 100005;

// Function to generate prime numbers
// using Sieve of Eratosthenes
static void SieveOfEratosthenes(boolean []prime,
                                int p_size)
{

    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= p_size; p++)
    {

        // If p is a prime
        if (prime[p])
        {

            // Set all multiples of p as non-prime
            for(int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the digit sum
// of a given number
static int digitSum(int number)
{

    // Stores the sum of digits
    int sum = 0;
    while (number > 0)
    {

        // Extract digits and
        // add to the sum
        sum += (number % 10);
        number /= 10;
    }

    // Return the sum
    // of the digits
    return sum;
}

// Function to find the longest subsequence
// with sum of digits of each element equal
// to a composite number
static void longestCompositeDigitSumSubsequence(int []arr,
                                                int n)
{
    int count = 0;
    boolean []prime = new boolean[N + 1];
    for(int i = 0; i <= N; i++)
        prime[i] = true;

    SieveOfEratosthenes(prime, N);

    for(int i = 0; i < n; i++)
    {

        // Calculate sum of digits
        // of current array element
        int res = digitSum(arr[i]);

        // If sum of digits
        // equal to 1
        if (res == 1)
        {
            continue;
        }

        // If sum of digits is
        // a prime
        if (prime[res] == false)
        {
            count++;
        }
    }
    System.out.println(count);
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 13, 55, 7, 3, 5, 1,
                  10, 21, 233, 144, 89 };
    int n = arr.length;

    // Function call
    longestCompositeDigitSumSubsequence(arr, n);
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
N = 100005

# Function to generate prime numbers
# using Sieve of Eratosthenes
def SieveOfEratosthenes(prime,
                        p_size):

    # Set 0 and 1 as non-prime
    prime[0] = False
    prime[1] = False

    p = 2
    while p * p <= p_size:

        # If p is a prime
        if (prime[p]):

            # Set all multiples of
            # p as non-prime
            for i in range(p * 2,
                           p_size + 1, p):
                prime[i] = False
        p += 1

# Function to find
# the digit sum of
# a given number
def digitSum(number):

    # Stores the sum
    # of digits
    sum = 0
    while (number > 0):

        # Extract digits and
        # add to the sum
        sum += (number % 10)
        number //= 10

    # Return the sum
    # of the digits
    return sum

# Function to find the longest subsequence
# with sum of digits of each element equal
# to a composite number
def longestCompositeDigitSumSubsequence(arr, n):

    count = 0
    prime = [True] * (N + 1)
    SieveOfEratosthenes(prime, N)

    for i in range(n):

        # Calculate sum of digits
        # of current array element
        res = digitSum(arr[i])

        # If sum of digits
        # equal to 1
        if (res == 1):
            continue

        # If sum of digits is
        # a prime
        if (not prime[res]):
            count += 1

    print (count)

# Driver Code
if __name__ == "__main__":

    arr = [13, 55, 7, 3, 5, 1,
           10, 21, 233, 144, 89]
    n = len(arr)

    # Function call
    longestCompositeDigitSumSubsequence(arr, n)

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the
// above approach
using System.Collections.Generic;
using System;

class GFG{

static int N = 100005;

// Function to generate prime numbers
// using Sieve of Eratosthenes
static void SieveOfEratosthenes(bool []prime,
                                int p_size)
{

    // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for(int p = 2; p * p <= p_size; p++)
    {

        // If p is a prime
        if (prime[p])
        {

            // Set all multiples of p as non-prime
            for(int i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the digit sum
// of a given number
static int digitSum(int number)
{

    // Stores the sum of digits
    int sum = 0;
    while (number > 0)
    {

        // Extract digits and
        // add to the sum
        sum += (number % 10);
        number /= 10;
    }

    // Return the sum
    // of the digits
    return sum;
}

// Function to find the longest subsequence
// with sum of digits of each element equal
// to a composite number
static void longestCompositeDigitSumSubsequence(int []arr,
                                                int n)
{
    int count = 0;
    bool []prime = new bool[N + 1];
    for(int i = 0; i <= N; i++)
        prime[i] = true;

    SieveOfEratosthenes(prime, N);

    for(int i = 0; i < n; i++)
    {

        // Calculate sum of digits
        // of current array element
        int res = digitSum(arr[i]);

        // If sum of digits
        // equal to 1
        if (res == 1)
        {
            continue;
        }

        // If sum of digits is
        // a prime
        if (prime[res] == false)
        {
            count++;
        }
    }
    Console.WriteLine(count);
}

// Driver Code
public static void Main()
{
    int []arr = { 13, 55, 7, 3, 5, 1,
                  10, 21, 233, 144, 89 };
    int n = arr.Length;

    // Function call
    longestCompositeDigitSumSubsequence(arr, n);
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

    let N = 100005;

    // Function to generate prime numbers
// using Sieve of Eratosthenes
    function SieveOfEratosthenes(prime,p_size)
    {
        // Set 0 and 1 as non-prime
    prime[0] = false;
    prime[1] = false;

    for(let p = 2; p * p <= p_size; p++)
    {

        // If p is a prime
        if (prime[p])
        {

            // Set all multiples of p as non-prime
            for(let i = p * 2; i <= p_size; i += p)
                prime[i] = false;
        }
    }
    }

    // Function to find the digit sum
// of a given number
    function digitSum(number)
    {
        // Stores the sum of digits
    let sum = 0;
    while (number > 0)
    {

        // Extract digits and
        // add to the sum
        sum += (number % 10);
        number =Math.floor(number/ 10);
    }

    // Return the sum
    // of the digits
    return sum;
    }

    // Function to find the longest subsequence
// with sum of digits of each element equal
// to a composite number
    function longestCompositeDigitSumSubsequence(arr,n)
    {
        let count = 0;
    let prime = new Array(N + 1);
    for(let i = 0; i <= N; i++)
        prime[i] = true;

    SieveOfEratosthenes(prime, N);

    for(let i = 0; i < n; i++)
    {

        // Calculate sum of digits
        // of current array element
        let res = digitSum(arr[i]);

        // If sum of digits
        // equal to 1
        if (res == 1)
        {
            continue;
        }

        // If sum of digits is
        // a prime
        if (prime[res] == false)
        {
            count++;
        }
    }
    document.write(count);
    }

    // Driver Code
    let arr=[13, 55, 7, 3, 5, 1,
                  10, 21, 233, 144, 89 ];
    let  n = arr.length;

    // Function call
    longestCompositeDigitSumSubsequence(arr, n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
4
```

***时间复杂度** : O(N)*
***辅助空间:** O(log <sub>10</sub> (maxm))，其中 maxm 为 maxm 数组元素*