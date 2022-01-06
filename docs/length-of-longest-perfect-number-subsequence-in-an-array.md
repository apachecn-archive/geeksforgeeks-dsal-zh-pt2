# 数组中最长完全数子序列的长度

> 原文:[https://www . geeksforgeeks . org/最长完全数数组子序列长度/](https://www.geeksforgeeks.org/length-of-longest-perfect-number-subsequence-in-an-array/)

给定一个包含长度为 **N** 的非负整数的**数组 arr[]** ，任务是打印数组中 [**完全数**](https://www.geeksforgeeks.org/perfect-number/) 的最长子序列的长度。

> 如果一个数等于它的适当除数之和，即它的正除数之和，不包括数本身，那么它就是一个[完全数](https://www.geeksforgeeks.org/perfect-number/)。

**示例:**

> **输入:** arr[] = { 3，6，11，2，28，21，8128 }
> **输出:** 3
> **解释:**
> 最长的完全数子序列是{6，28，8128 }，因此答案是 3。
> 
> **输入:** arr[] = { 6，4，10，13，9，25 }
> **输出:** 1
> **解释:**
> 最长的完全数子序列是{6}，因此答案是 1。

**方法:**
要解决上述问题，请按照下面给出的步骤操作:

*   遍历给定的数组，对于数组中的每个元素，检查它是否是[完全数](https://www.geeksforgeeks.org/perfect-number/)。
*   如果元素是一个完全数，它将在最长的完全数子序列中。因此，将最长完全数子序列所需的长度增加 1

下面是上述方法的实现:

## C++

```
// C++ program to find the length of
// Longest Perfect number Subsequence in an Array

#include <bits/stdc++.h>
using namespace std;

// Function to check if
// the number is a Perfect number
bool isPerfect(long long int n)
{
    // To store sum of divisors
    long long int sum = 1;

    // Find all divisors and add them
    for (long long int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }
    // Check if sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Function to find the longest subsequence
// which contain all Perfect numbers
int longestPerfectSubsequence(int arr[], int n)
{
    int answer = 0;

    // Find the length of longest
    // Perfect number subsequence
    for (int i = 0; i < n; i++) {
        if (isPerfect(arr[i]))
            answer++;
    }

    return answer;
}

// Driver code
int main()
{
    int arr[] = { 3, 6, 11, 2, 28, 21, 8128 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << longestPerfectSubsequence(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of
// longest perfect number subsequence
// in an array
class GFG {

// Function to check if the
// number is a perfect number
static boolean isPerfect(long n)
{

    // To store sum of divisors
    long sum = 1;

    // Find all divisors and add them
    for(long i = 2; i * i <= n; i++)
    {
       if (n % i == 0)
       {
           if (i * i != n)
               sum = sum + i + n / i;
           else
               sum = sum + i;
       }
    }

    // Check if sum of divisors is equal 
    // to n, then n is a perfect number
    if (sum == n && n != 1)
    {
        return true;
    }
    return false;
}

// Function to find the longest subsequence
// which contain all Perfect numbers
static int longestPerfectSubsequence(int arr[],
                                     int n)
{
    int answer = 0;

    // Find the length of longest
    // perfect number subsequence
    for(int i = 0; i < n; i++)
    {
       if (isPerfect(arr[i]) == true)
           answer++;
    }
    return answer;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 3, 6, 11, 2, 28, 21, 8128 };
    int n = arr.length;

    System.out.println(longestPerfectSubsequence(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the length of
# Longest Perfect number Subsequence in an Array

# Function to check if
# the number is Perfect number
def isPerfect( n ):

    # To store sum of divisors
    sum = 1

    # Find all divisors and add them
    i = 2
    while i * i <= n:
        if n % i == 0:
            sum = sum + i + n / i
        i += 1

    # Check if sum of divisors is equal to
    # n, then n is a perfect number

    return (True if sum == n and n != 1 else False)

# Function to find the longest subsequence
# which contain all Perfect numbers
def longestPerfectSubsequence( arr, n):

    answer = 0

    # Find the length of longest
    # Perfect number subsequence
    for i in range (n):
        if (isPerfect(arr[i])):
            answer += 1

    return answer

# Driver code
if __name__ == "__main__":
    arr = [ 3, 6, 11, 2, 28, 21, 8128 ]
    n = len(arr)

    print (longestPerfectSubsequence(arr, n))
```

## C#

```
// C# program to find the length of
// longest perfect number subsequence
// in an array
using System;

class GFG {

// Function to check if the
// number is a perfect number
static bool isPerfect(long n)
{

    // To store sum of divisors
    long sum = 1;

    // Find all divisors and add them
    for(long i = 2; i * i <= n; i++)
    {
       if (n % i == 0)
       {
           if (i * i != n)
               sum = sum + i + n / i;
           else
               sum = sum + i;
       }
    }

    // Check if sum of divisors is equal
    // to n, then n is a perfect number
    if (sum == n && n != 1)
    {
        return true;
    }
    return false;
}

// Function to find the longest subsequence
// which contain all perfect numbers
static int longestPerfectSubsequence(int []arr,
                                     int n)
{
    int answer = 0;

    // Find the length of longest
    // perfect number subsequence
    for(int i = 0; i < n; i++)
    {
       if (isPerfect(arr[i]) == true)
           answer++;
    }
    return answer;
}

// Driver code
public static void Main (string[] args)
{
    int []arr = { 3, 6, 11, 2, 28, 21, 8128 };
    int n = arr.Length;

    Console.WriteLine(longestPerfectSubsequence(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to find the length of
// Longest Perfect number Subsequence in an Array

// Function to check if
// the number is a Perfect number
function isPerfect(n)
{
    // To store sum of divisors
    var sum = 1;

    // Find all divisors and add them
    for (var i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            if (i * i != n)
                sum = sum + i + n / i;
            else
                sum = sum + i;
        }
    }
    // Check if sum of divisors is equal to
    // n, then n is a perfect number
    if (sum == n && n != 1)
        return true;

    return false;
}

// Function to find the longest subsequence
// which contain all Perfect numbers
function longestPerfectSubsequence(arr, n)
{
    var answer = 0;

    // Find the length of longest
    // Perfect number subsequence
    for (var i = 0; i < n; i++) {
        if (isPerfect(arr[i]))
            answer++;
    }

    return answer;
}

// Driver code
var arr = [3, 6, 11, 2, 28, 21, 8128];
var n = arr.length;
document.write( longestPerfectSubsequence(arr, n));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N×√N)*
***辅助空间复杂度:** O(1)*