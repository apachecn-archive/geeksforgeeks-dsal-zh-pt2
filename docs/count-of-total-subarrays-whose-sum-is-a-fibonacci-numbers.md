# 总和为斐波那契数的子阵列总数

> 原文:[https://www . geeksforgeeks . org/总数子数组-其和是斐波那契数/](https://www.geeksforgeeks.org/count-of-total-subarrays-whose-sum-is-a-fibonacci-numbers/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算其和为[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的子数组的总数。
**举例:**

> **输入:** arr[] = {6，7，8，9}
> **输出:** 3
> **解释:**
> 其和为斐波那契数的子阵为:
> 1。{6，7}，总和= 13 (5 + 8)
> 2。{6，7，8}，总和= 21 (8 + 13)
> 3。{8}，和= 8 (3 + 5)
> **输入:** arr[] = {1，1，1，1}
> **输出:** 4
> **解释:**
> 和为斐波那契数的子阵为:
> 1。{4，2，2}，总和= 8 (3 + 5)
> 2。{2}，总和= 2 (1 + 1)
> 3。{2}，总和= 2 (1 + 1)
> 4。{2}，总和= 2 (1 + 1)

**逼近:**思路是[生成所有可能的子阵](https://www.geeksforgeeks.org/sum-of-all-subarrays/)求每个子阵的和。现在，对于每个和，使用本文[中讨论的方法检查它是否是斐波那契数列。如果是，则计算所有这些总和并打印总数。
以下是上述方法的实现:](https://www.geeksforgeeks.org/check-number-fibonacci-number/) 

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether a number
// is perfect square or not
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s * s == x);
}

// Function to check whether a number
// is fibonacci number or not
bool isFibonacci(int n)
{
    // If 5*n*n + 4 or 5*n*n - 5 is a
    // perfect square, then the number
    // is Fibonacci
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to count the subarray with
// sum fibonacci number
void fibonacciSubarrays(int arr[], int n)
{
    int count = 0;

    // Traverse the array arr[] to find
    // the sum of each subarray
    for (int i = 0; i < n; ++i) {

        // To store the sum
        int sum = 0;

        for (int j = i; j < n; ++j) {
            sum += arr[j];

            // Check whether sum of subarray
            // between [i, j] is fibonacci
            // or not
            if (isFibonacci(sum)) {
                ++count;
            }
        }
    }

    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 6, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    fibonacciSubarrays(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG{

// Function to check whether a number
// is perfect square or not
static boolean isPerfectSquare(int x)
{
    int s = (int) Math.sqrt(x);
    return (s * s == x);
}

// Function to check whether a number
// is fibonacci number or not
static boolean isFibonacci(int n)
{
    // If 5*n*n + 4 or 5*n*n - 5 is a
    // perfect square, then the number
    // is Fibonacci
    return isPerfectSquare(5 * n * n + 4)
        || isPerfectSquare(5 * n * n - 4);
}

// Function to count the subarray
// with sum fibonacci number
static void fibonacciSubarrays(int arr[], int n)
{
    int count = 0;

    // Traverse the array arr[] to find
    // the sum of each subarray
    for (int i = 0; i < n; ++i) {

        // To store the sum
        int sum = 0;

        for (int j = i; j < n; ++j) {
            sum += arr[j];

            // Check whether sum of subarray
            // between [i, j] is fibonacci
            // or not
            if (isFibonacci(sum)) {
                ++count;
            }
        }
    }

    System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 6, 7, 8, 9 };
    int n = arr.length;

    // Function Call
    fibonacciSubarrays(arr, n);
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check whether a number
# is perfect square or not
def isPerfectSquare(x):

    s = int(math.sqrt(x))
    if s * s == x:
        return True
    return False

# Function to check whether a number
# is fibonacci number or not
def isFibonacci(n):

    # If 5*n*n + 4 or 5*n*n - 5 is a
    # perfect square, then the number
    # is Fibonacci
    return (isPerfectSquare(5 * n * n + 4) or
            isPerfectSquare(5 * n * n - 4))

# Function to count the subarray with
# sum fibonacci number
def fibonacciSubarrays(arr, n):

    count = 0

    # Traverse the array arr[] to find
    # the sum of each subarray
    for i in range(n):

        # To store the sum
        sum = 0

        for j in range(i, n):
            sum += arr[j]

            # Check whether sum of subarray
            # between [i, j] is fibonacci
            # or not
            if (isFibonacci(sum)):
                count += 1

    print(count)

# Driver Code
arr = [ 6, 7, 8, 9 ]
n = len(arr)

# Function Call
fibonacciSubarrays(arr, n)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check whether a number
// is perfect square or not
static bool isPerfectSquare(int x)
{
    int s = (int) Math.Sqrt(x);
    return (s * s == x);
}

// Function to check whether a number
// is fibonacci number or not
static bool isFibonacci(int n)
{
    // If 5*n*n + 4 or 5*n*n - 5 is a
    // perfect square, then the number
    // is Fibonacci
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// Function to count the subarray
// with sum fibonacci number
static void fibonacciSubarrays(int []arr, int n)
{
    int count = 0;

    // Traverse the array []arr to find
    // the sum of each subarray
    for(int i = 0; i < n; ++i)
    {

       // To store the sum
       int sum = 0;
       for(int j = i; j < n; ++j)
       {
          sum += arr[j];

          // Check whether sum of subarray
          // between [i, j] is fibonacci
          // or not
          if (isFibonacci(sum))
          {
              ++count;
          }
       }
    }
    Console.Write(count);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 6, 7, 8, 9 };
    int n = arr.Length;

    // Function Call
    fibonacciSubarrays(arr, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check whether a number
// is perfect square or not
function isPerfectSquare(x)
{
    var s = parseInt(Math.sqrt(x));
    return (s * s == x);
}

// Function to check whether a number
// is fibonacci number or not
function isFibonacci(n)
{
    // If 5*n*n + 4 or 5*n*n - 5 is a
    // perfect square, then the number
    // is Fibonacci
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to count the subarray with
// sum fibonacci number
function fibonacciSubarrays(arr, n)
{
    var count = 0;

    // Traverse the array arr[] to find
    // the sum of each subarray
    for (var i = 0; i < n; ++i) {

        // To store the sum
        var sum = 0;

        for (var j = i; j < n; ++j) {
            sum += arr[j];

            // Check whether sum of subarray
            // between [i, j] is fibonacci
            // or not
            if (isFibonacci(sum)) {
                ++count;
            }
        }
    }

    document.write( count);
}

// Driver Code

var arr = [ 6, 7, 8, 9 ];
var n = arr.length;

// Function Call
fibonacciSubarrays(arr, n);

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N <sup>2</sup> )* ，其中 N 为元素个数。

***辅助空间:**O(1)*T4】