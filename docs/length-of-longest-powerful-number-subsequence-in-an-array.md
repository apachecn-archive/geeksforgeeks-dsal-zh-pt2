# 数组中最长的幂次数子序列的长度

> 原文:[https://www . geeksforgeeks . org/最长有效数字数组中的子序列长度/](https://www.geeksforgeeks.org/length-of-longest-powerful-number-subsequence-in-an-array/)

给定一个包含长度为 **N** 的非负整数的**数组 arr[]** ，任务是打印数组中最长的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)[**的长度**](https://www.geeksforgeeks.org/powerful-number/) 。

> 如果一个数 n 的每一个质因数 p，p <sup>2</sup> 也对其进行除法运算，那么这个数 n 就被称为[强数](https://www.geeksforgeeks.org/powerful-number/)。

**例:**

> **输入:** arr[] = { 3，4，11，2，9，21 }
> **输出:** 2
> **解释:**
> 最长强力数子序列是{4，9}，因此答案是 2。
> **输入:** arr[] = { 6，4，10，13，9，25 }
> **输出:** 3
> **解释:**
> 最长的强力数子序列是{4，9，25 }，因此答案是 3。

**方法:**要解决上面提到的问题，我们必须遵循下面给出的步骤:

*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于数组中的每个元素，检查它是否是[强子数](https://www.geeksforgeeks.org/powerful-number/)。
*   如果元素是一个幂数，它将在最长幂数子序列中。
*   因此，将最长有效数子序列所需的长度增加 1
*   达到数组大小后返回最终长度。

以下是上述方法的实现:

## C++

```
// C++ program to find the length of
// Longest Powerful Subsequence in an Array

#include <bits/stdc++.h>
using namespace std;

// Function to check if the number is powerful
bool isPowerful(int n)
{
    // First divide the number repeatedly by 2
    while (n % 2 == 0) {
        int power = 0;
        while (n % 2 == 0) {
            n /= 2;
            power++;
        }

        // Check if only 2^1 divides n,
        // then return false
        if (power == 1)
            return false;
    }

    // Check if n is not a power of 2
    // then this loop will execute
    // repeat above process
    for (int factor = 3;
         factor <= sqrt(n);
         factor += 2) {

        // Find highest power of "factor"
        // that divides n
        int power = 0;
        while (n % factor == 0) {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n,
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now
    // if it is not a prime number.
    // Since prime numbers
    // are not powerful, we return
    // false if n is not 1.
    return (n == 1);
}

// Function to find the longest subsequence
// which contain all powerful numbers
int longestPowerfulSubsequence(
    int arr[], int n)
{
    int answer = 0;

    for (int i = 0; i < n; i++) {
        if (isPowerful(arr[i]))
            answer++;
    }

    return answer;
}

// Driver code
int main()
{
    int arr[] = { 6, 4, 10, 13, 9, 25 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << longestPowerfulSubsequence(arr, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of
// Longest Powerful Subsequence in an Array
class GFG{

// Function to check if the number is powerful
static boolean isPowerful(int n)
{

    // First divide the number repeatedly by 2
    while (n % 2 == 0)
    {
        int power = 0;
        while (n % 2 == 0)
        {
            n /= 2;
            power++;
        }

        // Check if only 2^1 divides n,
        // then return false
        if (power == 1)
            return false;
    }

    // Check if n is not a power of 2
    // then this loop will execute
    // repeat above process
    for(int factor = 3;
            factor <= Math.sqrt(n);
            factor += 2)
    {

       // Find highest power of "factor"
       // that divides n
       int power = 0;
       while (n % factor == 0)
       {
           n = n / factor;
           power++;
       }

       // If only factor^1 divides n,
       // then return false
       if (power == 1)
       return false;

    }

    // n must be 1 now
    // if it is not a prime number.
    // Since prime numbers
    // are not powerful, we return
    // false if n is not 1.
    return (n == 1);
}

// Function to find the longest subsequence
// which contain all powerful numbers
static int longestPowerfulSubsequence(int arr[],
                                      int n)
{
    int answer = 0;

    for(int i = 0; i < n; i++)
    {
       if (isPowerful(arr[i]))
       answer++;
    }

    return answer;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 6, 4, 10, 13, 9, 25 };
    int n = arr.length;

    System.out.print(longestPowerfulSubsequence(arr,
                                                n) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the length of
# Longest Powerful Subsequence in an Array
import math

# Function to check if the number is powerful
def isPowerful(n):

    # First divide the number repeatedly by 2
    while (n % 2 == 0):
        power = 0

        while (n % 2 == 0):
            n //= 2
            power += 1

        # Check if only 2^1 divides n,
        # then return false
        if (power == 1):
            return False

    # Check if n is not a power of 2
    # then this loop will execute
    # repeat above process
    for factor in range(3, int(math.sqrt(n)) + 1, 2):

        # Find highest power of "factor"
        # that divides n
        power = 0
        while (n % factor == 0):
            n = n // factor
            power += 1

        # If only factor^1 divides n,
        # then return false
        if (power == 1):
            return False

    # n must be 1 now
    # if it is not a prime number.
    # Since prime numbers
    # are not powerful, we return
    # false if n is not 1.
    return (n == 1)

# Function to find the longest subsequence
# which contain all powerful numbers
def longestPowerfulSubsequence(arr, n):

    answer = 0

    for i in range(n):
        if (isPowerful(arr[i])):
            answer += 1

    return answer

# Driver code
arr = [ 6, 4, 10, 13, 9, 25 ]

n = len(arr)

print(longestPowerfulSubsequence(arr, n))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to find the length of
// longest Powerful Subsequence in
// an array
using System;
class GFG{

// Function to check if the
// number is powerful
static bool isPowerful(int n)
{

    // First divide the number
    // repeatedly by 2
    while (n % 2 == 0)
    {
        int power = 0;
        while (n % 2 == 0)
        {
            n /= 2;
            power++;
        }

        // Check if only 2^1 divides
        // n, then return false
        if (power == 1)
            return false;
    }

    // Check if n is not a power of 2
    // then this loop will execute
    // repeat above process
    for(int factor = 3;
            factor <= Math.Sqrt(n);
            factor += 2)
    {

       // Find highest power of "factor"
       // that divides n
       int power = 0;
       while (n % factor == 0)
       {
           n = n / factor;
           power++;
       }

       // If only factor^1 divides n,
       // then return false
       if (power == 1)
           return false;
    }

    // n must be 1 now
    // if it is not a prime number.
    // Since prime numbers
    // are not powerful, we return
    // false if n is not 1.
    return (n == 1);
}

// Function to find the longest subsequence
// which contain all powerful numbers
static int longestPowerfulSubsequence(int []arr,
                                      int n)
{
    int answer = 0;

    for(int i = 0; i < n; i++)
    {
       if (isPowerful(arr[i]))
           answer++;
    }
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 6, 4, 10, 13, 9, 25 };
    int n = arr.Length;

    Console.Write(longestPowerfulSubsequence(arr,
                                             n) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to find the length of
// Longest Powerful Subsequence in an Array

// Function to check if the number is powerful
function isPowerful(n)
{

    // First divide the number repeatedly by 2
    while (n % 2 == 0)
    {
        let power = 0;
        while (n % 2 == 0)
        {
            n /= 2;
            power++;
        }

        // Check if only 2^1 divides n,
        // then return false
        if (power == 1)
            return false;
    }

    // Check if n is not a power of 2
    // then this loop will execute
    // repeat above process
    for(let factor = 3;
            factor <= Math.sqrt(n);
            factor += 2)
    {

       // Find highest power of "factor"
       // that divides n
       let power = 0;
       while (n % factor == 0)
       {
           n = n / factor;
           power++;
       }

       // If only factor^1 divides n,
       // then return false
       if (power == 1)
       return false;

    }

    // n must be 1 now
    // if it is not a prime number.
    // Since prime numbers
    // are not powerful, we return
    // false if n is not 1.
    return (n == 1);
}

// Function to find the longest subsequence
// which contain all powerful numbers
function longestPowerfulSubsequence(arr,
                                      n)
{
    let answer = 0;

    for(let i = 0; i < n; i++)
    {
       if (isPowerful(arr[i]))
       answer++;
    }

    return answer;
}

// Driver code
    let arr = [ 6, 4, 10, 13, 9, 25 ];
    let n = arr.length;
    document.write(longestPowerfulSubsequence(arr,
                                                n) + "\n");

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*√N)*
***辅助空间复杂度:** O(1)*