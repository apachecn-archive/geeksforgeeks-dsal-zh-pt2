# 计算字符 ASCII 值总和等于质数或阿姆斯特朗数的字符串

> 原文:[https://www . geeksforgeeks . org/count-strings-具有等于质数或阿姆斯特朗数的 ascii 字符值总和/](https://www.geeksforgeeks.org/count-strings-having-sum-of-ascii-values-of-characters-equal-to-a-prime-or-armstrong-number/)

给定一个包含字符串的大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算字符的 ASCII 值之和等于一个[阿姆斯特朗数](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)或一个[素数的字符串数。](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)

**示例:**

> **输入:** arr[] = {“你好”、“nace”}
> **输出:**
> 阿姆斯壮字符串个数为:1
> 质数字符串个数为:0
> **说明:**各字符串字符的 ASCII 值之和为:{532，407}，其中 407 为阿姆斯壮数，无一为质数。
> 因此，阿姆斯特朗看重的字符串是“nace”。
> 
> **输入:**arr[]= {“geeks forgeks”“a”“computer”“science”“portal”“for”“geeks”}
> **输出:**
> Armstrong 字符串个数为:0
> 质数为:2
> **说明:**各字符串字符的 ASCII 值之和为:{1381，97，879，730，658，327，527}，其中 1381 和 97 为
> 因此，素数值字符串是“geeksforgeeks”和“a”。

**方法:**这个问题可以通过计算每个字符串的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)来解决。按照以下步骤解决此问题:

*   初始化两个变量， **countPrime** 和 **countArmstrong** 为 **0** ，以存储 Prime 和 Armstrong 值字符串的计数。
*   [使用一个变量迭代指数**【0，N–1】**的范围](https://www.geeksforgeeks.org/range-based-loop-c/)，比如 **i** ，并执行以下步骤:
    *   将当前字符串**arr【I】**字符的 ASCII 值之和存储在一个变量中，比如 **val** 。
    *   如果数字**值**是一个[阿姆斯特朗数字](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)，则按 **1** 递增**计数阿姆斯特朗**。
    *   如果数字**值**是一个[质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)，将**计数质数**增加 **1** 。
*   打印 **countPrime** 和 **countArmstrong** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime number
bool isPrime(int num)
{

    // Define a flag variable
    bool flag = false;

    if (num > 1)
    {

        // Check for factors of num
        for(int i = 2; i < num; i++)
        {

            // If factor is found,
            // set flag to True and
            // break out of loop
            if ((num % i) == 0)
            {
                flag = true;
                break;
            }
        }
    }

    // Check if flag is True
    if (flag)
        return false;
    else
        return true;
}

// Function to calculate
// order of the number x
int order(int x)
{
    int n = 0;
    while (x != 0)
    {
        n = n + 1;
        x = x / 10;
    }
    return n;
}

// Function to check whether the given
// number is Armstrong number or not
bool isArmstrong(int x)
{
    int n = order(x);
    int temp = x;
    int sum1 = 0;

    while (temp != 0)
    {
        int r = temp % 10;
        sum1 = sum1 + pow(r, n);
        temp = temp / 10;
    }

    // If the condition satisfies
    return (sum1 == x);
}

// Function to count
// Armstrong valued strings
int count_armstrong(vector<string> li)
{

    // Stores the count of
    // Armstrong valued strings
    int c = 0;

    // Iterate over the list
    for(string ele : li)
    {

        // Store the value
        // of the string
        int val = 0;

        // Find value of the string
        for(char che:ele)
            val += che;

        // Check if it an Armstrong number
        if (isArmstrong(val))
            c += 1;
    }
    return c;
}

// Function to count
// prime valued strings
int count_prime(vector<string> li)
{

    // Store the count of
    // prime valued strings
    int c = 0;

    // Iterate over the list
    for(string ele:li)
    {

        // Store the value
        // of the string
        int val = 0;

        // Find value of the string
        for(char che : ele)
            val += che;

        // Check if it
        // is a Prime Number
        if (isPrime(val))
            c += 1;
    }
    return c;
}

// Driver code
int main()
{
    vector<string> arr = { "geeksforgeeks", "a", "computer",
                           "science", "portal", "for", "geeks"};

    // Function Call
    cout << "Number of Armstrong Strings are: "
         << count_armstrong(arr) << endl;
    cout << "Number of Prime Strings are: "
         << count_prime(arr) << endl;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to check if a
    // number is prime number
    static boolean isPrime(int num)
    {

        // Define a flag variable
        boolean flag = false;

        if (num > 1) {

            // Check for factors of num
            for (int i = 2; i < num; i++) {

                // If factor is found,
                // set flag to True and
                // break out of loop
                if ((num % i) == 0) {
                    flag = true;
                    break;
                }
            }
        }

        // Check if flag is True
        if (flag)
            return false;
        else
            return true;
    }

    // Function to calculate
    // order of the number x
    static int order(int x)
    {
        int n = 0;
        while (x != 0) {
            n = n + 1;
            x = x / 10;
        }
        return n;
    }

    // Function to check whether the given
    // number is Armstrong number or not
    static boolean isArmstrong(int x)
    {
        int n = order(x);
        int temp = x;
        int sum1 = 0;

        while (temp != 0) {
            int r = temp % 10;
            sum1 = sum1 + (int)(Math.pow(r, n));
            temp = temp / 10;
        }

        // If the condition satisfies
        return (sum1 == x);
    }

    // Function to count
    // Armstrong valued strings
    static int count_armstrong(String[] li)
    {

        // Stores the count of
        // Armstrong valued strings
        int c = 0;

        // Iterate over the list
        for(String ele : li)
        {

            // Store the value
            // of the string
            int val = 0;

            // Find value of the string
            for(char che : ele.toCharArray()) val += che;

            // Check if it an Armstrong number
            if (isArmstrong(val))
                c += 1;
        }
        return c;
    }

    // Function to count
    // prime valued strings
    static int count_prime(String[] li)
    {

        // Store the count of
        // prime valued strings
        int c = 0;

        // Iterate over the list
        for(String ele : li)
        {

            // Store the value
            // of the string
            int val = 0;

            // Find value of the string
            for(char che : ele.toCharArray()) val += che;

            // Check if it
            // is a Prime Number
            if (isPrime(val))
                c += 1;
        }
        return c;
    }

    // Driver code

    public static void main (String[] args) {
        String[] arr
            = { "geeksforgeeks", "a",      "computer",
                "science",       "portal", "for",
                "geeks" };

        // Function Call
        System.out.println(
            "Number of Armstrong Strings are: "
            + count_armstrong(arr));
        System.out.println("Number of Prime Strings are: "
                          + count_prime(arr));
    }
}

// This code is contributed by patel2127.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if a
# number is prime number
def isPrime(num):

    # Define a flag variable
    flag = False

    if num > 1:

        # Check for factors of num
        for i in range(2, num):

            # If factor is found,
            # set flag to True and
            # break out of loop
            if (num % i) == 0:
                flag = True
                break

    # Check if flag is True
    if flag:
        return False
    else:
        return True

# Function to calculate
# order of the number x
def order(x):
    n = 0
    while (x != 0):
        n = n + 1
        x = x // 10
    return n

# Function to check whether the given
# number is Armstrong number or not
def isArmstrong(x):
    n = order(x)
    temp = x
    sum1 = 0

    while (temp != 0):

        r = temp % 10
        sum1 = sum1 + r**n
        temp = temp // 10

    # If the condition satisfies
    return (sum1 == x)

# Function to count
# Armstrong valued strings
def count_armstrong(li):

    # Stores the count of
    # Armstrong valued strings
    c = 0

    # Iterate over the list
    for ele in li:

        # Store the value
        # of the string
        val = 0

        # Find value of the string
        for che in ele:
            val += ord(che)

        # Check if it an Armstrong number
        if isArmstrong(val):
            c += 1
    return c

# Function to count
# prime valued strings
def count_prime(li):

    # Store the count of
    # prime valued strings
    c = 0

    # Iterate over the list
    for ele in li:

        # Store the value
        # of the string
        val = 0

        # Find value of the string
        for che in ele:
            val += ord(che)

        # Check if it
        # is a Prime Number
        if isPrime(val):
            c += 1
    return c

# Driver code
arr = ["geeksforgeeks", "a", "computer",
       "science", "portal", "for", "geeks"]

# Function Call
print("Number of Armstrong Strings are:", count_armstrong(arr))
print("Number of Prime Strings are:", count_prime(arr))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to check if a
    // number is prime number
    static bool isPrime(int num)
    {

        // Define a flag variable
        bool flag = false;

        if (num > 1) {

            // Check for factors of num
            for (int i = 2; i < num; i++) {

                // If factor is found,
                // set flag to True and
                // break out of loop
                if ((num % i) == 0) {
                    flag = true;
                    break;
                }
            }
        }

        // Check if flag is True
        if (flag)
            return false;
        else
            return true;
    }

    // Function to calculate
    // order of the number x
    static int order(int x)
    {
        int n = 0;
        while (x != 0) {
            n = n + 1;
            x = x / 10;
        }
        return n;
    }

    // Function to check whether the given
    // number is Armstrong number or not
    static bool isArmstrong(int x)
    {
        int n = order(x);
        int temp = x;
        int sum1 = 0;

        while (temp != 0) {
            int r = temp % 10;
            sum1 = sum1 + (int)(Math.Pow(r, n));
            temp = temp / 10;
        }

        // If the condition satisfies
        return (sum1 == x);
    }

    // Function to count
    // Armstrong valued strings
    static int count_armstrong(string[] li)
    {

        // Stores the count of
        // Armstrong valued strings
        int c = 0;

        // Iterate over the list
        foreach(string ele in li)
        {

            // Store the value
            // of the string
            int val = 0;

            // Find value of the string
            foreach(char che in ele) val += che;

            // Check if it an Armstrong number
            if (isArmstrong(val))
                c += 1;
        }
        return c;
    }

    // Function to count
    // prime valued strings
    static int count_prime(string[] li)
    {

        // Store the count of
        // prime valued strings
        int c = 0;

        // Iterate over the list
        foreach(string ele in li)
        {

            // Store the value
            // of the string
            int val = 0;

            // Find value of the string
            foreach(char che in ele) val += che;

            // Check if it
            // is a Prime Number
            if (isPrime(val))
                c += 1;
        }
        return c;
    }

    // Driver code
    public static void Main()
    {
        string[] arr
            = { "geeksforgeeks", "a",      "computer",
                "science",       "portal", "for",
                "geeks" };

        // Function Call
        Console.WriteLine(
            "Number of Armstrong Strings are: "
            + count_armstrong(arr));
        Console.WriteLine("Number of Prime Strings are: "
                          + count_prime(arr));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if a
// number is prime number
function isPrime(num) {

    // Define a flag variable
    let flag = false;

    if (num > 1) {

        // Check for factors of num
        for (let i = 2; i < num; i++) {

            // If factor is found,
            // set flag to True and
            // break out of loop
            if ((num % i) == 0) {
                flag = true;
                break;
            }
        }
    }

    // Check if flag is True
    if (flag)
        return false;
    else
        return true;
}

// Function to calculate
// order of the number x
function order(x) {
    let n = 0;
    while (x != 0) {
        n = n + 1;
        x = x / 10;
    }
    return n;
}

// Function to check whether the given
// number is Armstrong number or not
function isArmstrong(x) {
    let n = order(x);
    let temp = x;
    let sum1 = 0;

    while (temp != 0) {
        let r = temp % 10;
        sum1 = sum1 + Math.pow(r, n);
        temp = temp / 10;
    }

    // If the condition satisfies
    return (sum1 == x);
}

// Function to count
// Armstrong valued strings
function count_armstrong(li) {

    // Stores the count of
    // Armstrong valued strings
    let c = 0;

    // Iterate over the list
    for (let ele of li) {

        // Store the value
        // of the string
        let val = 0;

        // Find value of the string
        for (let che of ele)
            val += che.charCodeAt(0);

        // Check if it an Armstrong number
        if (isArmstrong(val))
            c += 1;
    }
    return c;
}

// Function to count
// prime valued strings
function count_prime(li) {

    // Store the count of
    // prime valued strings
    let c = 0;

    // Iterate over the list
    for (let ele of li) {

        // Store the value
        // of the string
        let val = 0;

        // Find value of the string
        for (let che of ele)
            val += che.charCodeAt(0);

        // Check if it
        // is a Prime Number
        if (isPrime(val))
            c += 1;
    }
    return c;
}

// Driver code

let arr = ["geeksforgeeks", "a", "computer",
    "science", "portal", "for", "geeks"];

// Function Call
document.write("Number of Armstrong Strings are: "
    + count_armstrong(arr) + "<br>");
document.write("Number of Prime Strings are: "
    + count_prime(arr) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output**

```
Number of Armstrong Strings are: 0
Number of Prime Strings are: 2
```

***时间复杂度:** O(N*M)，其中 M 为* [*数组中最长字符串*](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/) *的长度**arr【】***
***辅助空间:** O(1)*