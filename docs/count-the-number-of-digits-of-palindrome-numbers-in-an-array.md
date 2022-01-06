# 统计数组中回文数字的位数

> 原文:[https://www . geesforgeks . org/count-数组中回文数字的位数/](https://www.geeksforgeeks.org/count-the-number-of-digits-of-palindrome-numbers-in-an-array/)

给定一个带有 **N** 整数的数组 **arr[]** 。任务是计算数组中所有[回文](https://www.geeksforgeeks.org/given-a-string-print-all-possible-palindromic-partition/)数字的所有数字。
**举例:**

> **输入:** arr[] = {121，56，434 }
> T3】输出: 6
> 只有 121 和 434 是回文
> 和 digit count(121)+digit count(434)= 3+3 = 6
> **输入:** arr[] = {56，455，546，234}
> **输出:**0【T11

**方法:**对于数组的每个元素，如果它是一个一位数的数字，那么在它的数字的答案上加 1，否则检查这个数字是否是回文。如果是，那么找到它的数字计数，并将其添加到答案中。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the reverse of n
int reverse(int n)
{
    int rev = 0;
    while (n > 0)
    {
        int d = n % 10;
        rev = rev * 10 + d;
        n = n / 10;
    }
    return rev;
}

// Function that returns true
// if n is a palindrome
bool isPalin(int n)
{
    return (n == reverse(n));
}

// Function to return the
// count of digits of n
int countDigits(int n)
{
    int c = 0;
    while (n > 0)
    {
        n = n / 10;
        c++;
    }
    return c;
}

// Function to return the count of digits
// in all the palindromic numbers of arr[]
int countPalinDigits(int arr[], int n)
{
    int s = 0;
    for (int i = 0; i < n; i++)
    {

        // If arr[i] is a one digit number
        // or it is a palindrome
        if (arr[i] < 10 || isPalin(arr[i]))
        {
            s += countDigits(arr[i]);
        }
    }
    return s;
}

// Driver code
int main()
{
    int arr[] = { 121, 56, 434 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << (countPalinDigits(arr, n));
    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the reverse of n
    static int reverse(int n)
    {
        int rev = 0;
        while (n > 0) {
            int d = n % 10;
            rev = rev * 10 + d;
            n = n / 10;
        }
        return rev;
    }

    // Function that returns true
    // if n is a palindrome
    static boolean isPalin(int n)
    {
        return (n == reverse(n));
    }

    // Function to return the
    // count of digits of n
    static int countDigits(int n)
    {
        int c = 0;
        while (n > 0) {
            n = n / 10;
            c++;
        }
        return c;
    }

    // Function to return the count of digits
    // in all the palindromic numbers of arr[]
    static int countPalinDigits(int[] arr, int n)
    {
        int s = 0;
        for (int i = 0; i < n; i++) {

            // If arr[i] is a one digit number
            // or it is a palindrome
            if (arr[i] < 10 || isPalin(arr[i])) {
                s += countDigits(arr[i]);
            }
        }
        return s;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 121, 56, 434 };
        int n = arr.length;
        System.out.println(countPalinDigits(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the reverse of n
def reverse(n):
    rev = 0;
    while (n > 0):
        d = n % 10;
        rev = rev * 10 + d;
        n = n // 10;
    return rev;

# Function that returns true
# if n is a palindrome
def isPalin(n):
    return (n == reverse(n));

# Function to return the
# count of digits of n
def countDigits(n):
    c = 0;
    while (n > 0):
        n = n // 10;
        c += 1;
    return c;

# Function to return the count of digits
# in all the palindromic numbers of arr[]
def countPalinDigits(arr, n):
    s = 0;
    for i in range(n):

        # If arr[i] is a one digit number
        # or it is a palindrome
        if (arr[i] < 10 or isPalin(arr[i])):
            s += countDigits(arr[i]);

    return s;

# Driver code
arr = [ 121, 56, 434 ];
n = len(arr);
print(countPalinDigits(arr, n));

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the reverse of n
    static int reverse(int n)
    {
        int rev = 0;
        while (n > 0)
        {
            int d = n % 10;
            rev = rev * 10 + d;
            n = n / 10;
        }
        return rev;
    }

    // Function that returns true
    // if n is a palindrome
    static bool isPalin(int n)
    {
        return (n == reverse(n));
    }

    // Function to return the
    // count of digits of n
    static int countDigits(int n)
    {
        int c = 0;
        while (n > 0)
        {
            n = n / 10;
            c++;
        }
        return c;
    }

    // Function to return the count of digits
    // in all the palindromic numbers of arr[]
    static int countPalinDigits(int[] arr, int n)
    {
        int s = 0;
        for (int i = 0; i < n; i++)
        {

            // If arr[i] is a one digit number
            // or it is a palindrome
            if (arr[i] < 10 || isPalin(arr[i]))
            {
                s += countDigits(arr[i]);
            }
        }
        return s;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 121, 56, 434 };
        int n = arr.Length;
        Console.WriteLine(countPalinDigits(arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the reverse of n
function reverse(n)
{
    let rev = 0;
    while (n > 0)
    {
        let d = n % 10;
        rev = rev * 10 + d;
        n = parseInt(n / 10);
    }
    return rev;
}

// Function that returns true
// if n is a palindrome
function isPalin(n)
{
    return (n == reverse(n));
}

// Function to return the
// count of digits of n
function countDigits(n)
{
    let c = 0;
    while (n > 0)
    {
        n = parseInt(n / 10);
        c++;
    }
    return c;
}

// Function to return the count of digits
// in all the palindromic numbers of arr[]
function countPalinDigits(arr, n)
{
    let s = 0;
    for (let i = 0; i < n; i++)
    {

        // If arr[i] is a one digit number
        // or it is a palindrome
        if (arr[i] < 10 || isPalin(arr[i]))
        {
            s += countDigits(arr[i]);
        }
    }
    return s;
}

// Driver code
    let arr = [ 121, 56, 434 ];
    let n = arr.length;
    document.write(countPalinDigits(arr, n));

</script>
```

**Output:** 

```
6
```

**更短的 Python 实现**

## 蟒蛇 3

```
# Function to return the count of digits
# in all the palindromic numbers of arr[]
def countPalinDigits(arr):
   sum = 0

   for n in arr:
      n_str = str(n)
      l = len(n_str)
      if n_str[l::-1] == n_str: # if palindrome
         sum += l
   return sum

# Driver code
arr = [ 121, 56, 434 ];
print(countPalinDigits(arr));
```

**Output:** 

```
6
```