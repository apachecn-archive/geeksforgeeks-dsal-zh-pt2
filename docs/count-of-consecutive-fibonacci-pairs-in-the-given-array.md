# 给定数组中连续斐波那契对的计数

> 原文:[https://www . geesforgeks . org/给定数组中连续斐波那契对的计数/](https://www.geeksforgeeks.org/count-of-consecutive-fibonacci-pairs-in-the-given-array/)

给定一个数组 **arr[]** ，任务是计算这个数组中连续斐波那契对的数量。
**例:**

> **输入:** arr[] = { 3，5，6，11 }
> **输出:** 1
> 唯一的一对是(3，5)这是数组中连续的斐波那契对
> **输入:** arr[] = { 3，5，8，11 }
> **输出:** 2
> 数组中有两对(3，5)和(5，8)，这是连续的斐波那契对。

**进场:**

*   [找出数组的所有对](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n)。
*   对于每一对，
    *   求该对的最小值和最大值
    *   在**最小 _ 元素**之后找到[下一个连续的斐波那契数](https://www.geeksforgeeks.org/find-the-next-fibonacci-number/)，并检查它是否等于该对的**最大值**。
    *   如果下一个连续的斐波那契数等于该对中的最大元素，则将计数增加 1。
*   将总计数作为所需的对数返回。

以下是上述方法的实现:

## C++

```
// C++ implementation to count the
// consecutive fibonacci pairs in the array

#include <bits/stdc++.h>
using namespace std;

// Function to find the previous
// fibonacci for the number N
int previousFibonacci(int n)
{
    double a = n / ((1 + sqrt(5)) / 2.0);
    return round(a);
}

// Function to find the next
// fibonacci number for the number N
int nextFibonacci(int n)
{
    double a = n * (1 + sqrt(5)) / 2.0;
    return round(a);
}

// Function to check that a Number
// is a perfect square or not
bool isPerfectSquare(int x)
{
    int s = sqrt(x);
    return (s * s == x);
}

// Function to check that a number
// is fibonacci number or not
bool isFibonacci(int n)
{
    // N is Fibinacci if one of
    // (5*n*n + 4) or (5*n*n - 4)
    // is a perferct square
    return (isPerfectSquare(5 * n * n + 4)
            || isPerfectSquare(5 * n * n - 4));
}

// Function to count the fibonacci
// pairs in the array
int countFibonacciPairs(int arr[], int n)
{
    int res = 0;

    // Loop to iterate over the array
    // to choose all pairs of the array
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // Condition to check if both
            // the number of pair is a
            // fibonacci number
            if (isFibonacci(arr[i])
                && isFibonacci(arr[j])) {

                int prevFib = previousFibonacci(arr[i]);
                int nextFib = nextFibonacci(arr[i]);

                // Condition to check if both
                // the number form consecutive
                // fibonacci numbers
                if (prevFib == arr[j]
                    || nextFib == arr[j]) {
                    res++;
                }
            }

    return res;
}

// Driver Code
int main()
{
    int a[] = { 3, 5, 8, 11 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countFibonacciPairs(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// consecutive fibonacci pairs in the array
import java.util.*;
import java.lang.*;

class GFG
{

// Function to find the previous
// fibonacci for the number N
static int previousFibonacci(int n)
{
    double a = n / ((1 + (int)Math.sqrt(5)) / 2.0);
    return (int)Math.round(a);
}

// Function to find the next
// fibonacci number for the number N
static int nextFibonacci(int n)
{
    double a = n * (1 + (int)Math.sqrt(5)) / 2.0;
    return (int)Math.round(a);
}

// Function to check that a Number
// is a perfect square or not
static boolean isPerfectSquare(int x)
{
    int s = (int)Math.sqrt(x);
    return (s * s == x);
}

// Function to check that a number
// is fibonacci number or not
static boolean isFibonacci(int n)
{
    // N is Fibinacci if one of
    // (5*n*n + 4) or (5*n*n - 4)
    // is a perferct square
    return (isPerfectSquare(5 * n * n + 4)
            || isPerfectSquare(5 * n * n - 4));
}

// Function to count the fibonacci
// pairs in the array
static int countFibonacciPairs(int arr[], int n)
{
    int res = 0;

    // Loop to iterate over the array
    // to choose all pairs of the array
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // Condition to check if both
            // the number of pair is a
            // fibonacci number
            if (isFibonacci(arr[i])
                && isFibonacci(arr[j])) {

                int prevFib = previousFibonacci(arr[i]);
                int nextFib = nextFibonacci(arr[i]);

                // Condition to check if both
                // the number form consecutive
                // fibonacci numbers
                if (prevFib == arr[j]
                    || nextFib == arr[j]) {
                    res++;
                }
            }

    return res;
}

// Driver Code
public static void main(String []args)
{
    int []a = { 3, 5, 8, 11 };
    int n = a.length;
    System.out.print(countFibonacciPairs(a, n));   
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to count the
# consecutive fibonacci pairs in the array
from math import sqrt

# Function to find the previous
# fibonacci for the number N
def previousFibonacci(n):

    a = n / ((1 + sqrt(5)) / 2.0)
    return round(a)

# Function to find the next
# fibonacci number for the number N
def nextFibonacci(n):

    a = n * (1 + sqrt(5)) / 2.0
    return round(a)

# Function to check that a Number
# is a perfect square or not
def isPerfectSquare(x):

    s = sqrt(x)
    return (s * s == x)

# Function to check that a number
# is fibonacci number or not
def isFibonacci(n):

    # N is Fibinacci if one of
    # (5*n*n + 4) or (5*n*n - 4)
    # is a perferct square
    return (isPerfectSquare(5 * n * n + 4)
            or isPerfectSquare(5 * n * n - 4))

# Function to count the fibonacci
# pairs in the array
def countFibonacciPairs(arr, n):

    res = 0

    # Loop to iterate over the array
    # to choose all pairs of the array
    for i in range(n):
        for j in range(i+1,n):

            # Condition to check if both
            # the number of pair is a
            # fibonacci number
            if (isFibonacci(arr[i])
                and isFibonacci(arr[j])):

                prevFib = previousFibonacci(arr[i])
                nextFib = nextFibonacci(arr[i])

                # Condition to check if both
                # the number form consecutive
                # fibonacci numbers
                if (prevFib == arr[j]
                    or nextFib == arr[j]):
                    res += 1

    return res

# Driver Code
a = [3, 5, 8, 11]
n = len(a)
print(countFibonacciPairs(a, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to count the
// consecutive fibonacci pairs in the array
using System;

class GFG
{

// Function to find the previous
// fibonacci for the number N
static int previousFibonacci(int n)
{
    double a = n / ((1 + (int)Math.Sqrt(5)) / 2.0);
    return (int)Math.Round(a);
}

// Function to find the next
// fibonacci number for the number N
static int nextFibonacci(int n)
{
    double a = n * (1 + Math.Sqrt(5)) / 2.0;
    return (int)Math.Round(a);
}

// Function to check that a Number
// is a perfect square or not
static bool isPerfectSquare(int x)
{
    int s = (int)Math.Sqrt(x);
    return (s * s == x);
}

// Function to check that a number
// is fibonacci number or not
static bool isFibonacci(int n)
{
    // N is Fibinacci if one of
    // (5*n*n + 4) or (5*n*n - 4)
    // is a perferct square
    return (isPerfectSquare(5 * n * n + 4)
            || isPerfectSquare(5 * n * n - 4));
}

// Function to count the fibonacci
// pairs in the array
static int countFibonacciPairs(int []arr, int n)
{
    int res = 0;

    // Loop to iterate over the array
    // to choose all pairs of the array
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // Condition to check if both
            // the number of pair is a
            // fibonacci number
            if (isFibonacci(arr[i])
                && isFibonacci(arr[j])) {

                int prevFib = previousFibonacci(arr[i]);
                int nextFib = nextFibonacci(arr[i]);

                // Condition to check if both
                // the number form consecutive
                // fibonacci numbers
                if (prevFib == arr[j]
                    || nextFib == arr[j]) {
                    res++;
                }
            }

    return res;
}

// Driver Code
public static void Main(String []args)
{
    int []a = { 3, 5, 8, 11 };
    int n = a.Length;
    Console.Write(countFibonacciPairs(a, n));   
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation to count the
// consecutive fibonacci pairs in the array

// Function to find the previous
// fibonacci for the number N
function previousFibonacci(n)
{
    var a = n / ((1 + Math.sqrt(5)) / 2.0);
    return Math.round(a);
}

// Function to find the next
// fibonacci number for the number N
function nextFibonacci(n)
{
    var a = n * (1 + Math.sqrt(5)) / 2.0;
    return Math.round(a);
}

// Function to check that a Number
// is a perfect square or not
function isPerfectSquare(x)
{
    var s = Math.sqrt(x);
    return (s * s == x);
}

// Function to check that a number
// is fibonacci number or not
function isFibonacci(n)
{
    // N is Fibinacci if one of
    // (5*n*n + 4) or (5*n*n - 4)
    // is a perferct square
    return (isPerfectSquare(5 * n * n + 4)
            || isPerfectSquare(5 * n * n - 4));
}

// Function to count the fibonacci
// pairs in the array
function countFibonacciPairs(arr, n)
{
    var res = 0;

    // Loop to iterate over the array
    // to choose all pairs of the array
    for (var i = 0; i < n; i++)
        for (var j = i + 1; j < n; j++)

            // Condition to check if both
            // the number of pair is a
            // fibonacci number
            if (isFibonacci(arr[i])
                && isFibonacci(arr[j])) {

                var prevFib = previousFibonacci(arr[i]);
                var nextFib = nextFibonacci(arr[i]);

                // Condition to check if both
                // the number form consecutive
                // fibonacci numbers
                if (prevFib == arr[j]
                    || nextFib == arr[j]) {
                    res++;
                }
            }

    return res;
}

// Driver Code
var a = [ 3, 5, 8, 11 ];
var n = a.length;
document.write(countFibonacciPairs(a, n));

</script>
```

**Output:** 

```
2
```

**业绩分析:**

*   **时间复杂度:**和上面的方法一样，有两个嵌套的循环需要 O(N <sup>2</sup> )个时间，因此时间复杂度为 **O(N <sup>2</sup> )** 。
*   **空间复杂度:**和上面的方法一样，没有使用额外的空间，因此空间复杂度为 **O(1)** 。