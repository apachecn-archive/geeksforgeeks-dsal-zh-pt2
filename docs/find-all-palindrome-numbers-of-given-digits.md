# 查找给定数字的所有回文数字

> 原文:[https://www . geesforgeks . org/find-all-回文-给定位数的数字/](https://www.geeksforgeeks.org/find-all-palindrome-numbers-of-given-digits/)

给定一个整数 **D** ，任务是找到所有的 **D 位** [回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)数字。
**举例:**

> **输入:** D = 1
> **输出:** 1 2 3 4 5 6 7 8 9
> **输入:** D = 2
> **输出:** 11 22 33 44 55 66 77 88 99

**进场:**带 **D 位数字的数字**从**10<sup>(D–1)</sup>**到**10<sup>D</sup>–1**。所以，从这个区间开始检查每个数字是不是回文。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// reverse of num
int reverse(int num)
{
    int rev = 0;
    while (num > 0) {
        rev = rev * 10 + num % 10;
        num = num / 10;
    }
    return rev;
}

// Function that returns true
// if num is palindrome
bool isPalindrome(int num)
{

    // If the number is equal to the
    // reverse of it then it
    // is a palindrome
    if (num == reverse(num))
        return true;

    return false;
}

// Function to print all the
// d-digit palindrome numbers
void printPalindromes(int d)
{
    if (d <= 0)
        return;

    // Smallest and the largest d-digit numbers
    int smallest = pow(10, d - 1);
    int largest = pow(10, d) - 1;

    // Starting from the smallest d-digit
    // number till the largest
    for (int i = smallest;
         i <= largest; i++) {

        // If the current number
        // is palindrome
        if (isPalindrome(i))
            cout << i << " ";
    }
}

// Driver code
int main()
{
    int d = 2;

    printPalindromes(d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the
    // reverse of num
    static int reverse(int num)
    {
        int rev = 0;
        while (num > 0)
        {
            rev = rev * 10 + num % 10;
            num = num / 10;
        }
        return rev;
    }

    // Function that returns true
    // if num is palindrome
    static boolean isPalindrome(int num)
    {

        // If the number is equal to the
        // reverse of it then it
        // is a palindrome
        if (num == reverse(num))
            return true;

        return false;
    }

    // Function to print all the
    // d-digit palindrome numbers
    static void printPalindromes(int d)
    {
        if (d <= 0)
            return;

        // Smallest and the largest d-digit numbers
        int smallest = (int)Math.pow(10, d - 1);
        int largest = (int)Math.pow(10, d) - 1;

        // Starting from the smallest d-digit
        // number till the largest
        for (int i = smallest; i <= largest; i++)
        {

            // If the current number
            // is palindrome
            if (isPalindrome(i))
                System.out.print(i + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int d = 2;

        printPalindromes(d);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the
# reverse of num
def reverse(num):
    rev = 0;
    while (num > 0):
        rev = rev * 10 + num % 10;
        num = num // 10;

    return rev;

# Function that returns true
# if num is palindrome
def isPalindrome(num):
    # If the number is equal to the
    # reverse of it then it
    # is a palindrome
    if (num == reverse(num)):
        return True;

    return False;

# Function to prall the
# d-digit palindrome numbers
def printPalindromes(d):

    if (d <= 0):
        return;

    # Smallest and the largest d-digit numbers
    smallest = pow(10, d - 1);
    largest = pow(10, d) - 1;

    # Starting from the smallest d-digit
    # number till the largest
    for i in range(smallest, largest + 1):

        # If the current number
        # is palindrome
        if (isPalindrome(i)):
            print(i, end = " ");

# Driver code
d = 2;

printPalindromes(d);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // reverse of num
    static int reverse(int num)
    {
        int rev = 0;
        while (num > 0)
        {
            rev = rev * 10 + num % 10;
            num = num / 10;
        }
        return rev;
    }

    // Function that returns true
    // if num is palindrome
    static bool isPalindrome(int num)
    {

        // If the number is equal to the
        // reverse of it then it
        // is a palindrome
        if (num == reverse(num))
            return true;

        return false;
    }

    // Function to print all the
    // d-digit palindrome numbers
    static void printPalindromes(int d)
    {
        if (d <= 0)
            return;

        // Smallest and the largest d-digit numbers
        int smallest = (int)Math.Pow(10, d - 1);
        int largest = (int)Math.Pow(10, d) - 1;

        // Starting from the smallest d-digit
        // number till the largest
        for (int i = smallest; i <= largest; i++)
        {

            // If the current number
            // is palindrome
            if (isPalindrome(i))
                Console.Write(i + " ");
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        int d = 2;

        printPalindromes(d);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the
    // reverse of num
    function reverse(num)
    {
        let rev = 0;
        while (num > 0)
        {
            rev = rev * 10 + num % 10;
            num = parseInt(num / 10, 10);
        }
        return rev;
    }

    // Function that returns true
    // if num is palindrome
    function isPalindrome(num)
    {

        // If the number is equal to the
        // reverse of it then it
        // is a palindrome
        if (num == reverse(num))
            return true;

        return false;
    }

    // Function to print all the
    // d-digit palindrome numbers
    function printPalindromes(d)
    {
        if (d <= 0)
            return;

        // Smallest and the largest d-digit numbers
        let smallest = Math.pow(10, d - 1);
        let largest = Math.pow(10, d) - 1;

        // Starting from the smallest d-digit
        // number till the largest
        for (let i = smallest; i <= largest; i++)
        {

            // If the current number
            // is palindrome
            if (isPalindrome(i))
                document.write(i + " ");
        }
    }

    let d = 2;

      printPalindromes(d);

</script>
```

**Output:** 

```
11 22 33 44 55 66 77 88 99
```