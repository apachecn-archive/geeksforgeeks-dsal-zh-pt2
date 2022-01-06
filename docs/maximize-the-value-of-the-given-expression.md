# 最大化给定表达式的值

> 原文:[https://www . geesforgeks . org/最大化给定表达式的价值/](https://www.geeksforgeeks.org/maximize-the-value-of-the-given-expression/)

给定三个非零整数 **a** 、 **b** 和 **c** 。任务是通过将加法和乘法符号以任何顺序放在它们之间来找到可能的最大值。

**注意:**允许整数重排，但加法和乘法符号必须使用一次。根据你的需要，大括号也可以放在方程之间。

**示例:**

> **输入:** a = 2，b = 1，c = 4
> **输出:** 12
> (1 + 2) * 4 = 3 * 4 = 12
> 
> **输入:** a = 2，b = 2，c = 2
> **输出:** 8
> (2 + 2) * 2 = 4 * 2 = 8

**方法:**要解决这个问题，可以选择生成所有可能性并计算它们以获得最大值的方法，但是这种方法效率不高。利用给定的条件，整数可以重新排列，并强制使用每个数学符号(+、*)。下面列出了总共要解决的四个案例:

1.  **所有三个整数都是非负的:**为此，只需将两个较小的整数相加，然后将其结果乘以最大的整数。
2.  **一个整数为负，其余两个为正:**将两个正整数相乘，并将其结果加到负整数上。
3.  **两个整数为负，一个为正:**由于两个负数的乘积为正，将两个负整数相乘，然后将其结果加到正整数上。
4.  **三个都是负整数:**将两个最大的整数相加，再乘以最小的一个。案例 3-:(总和–最小)*最小

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum result
int maximumResult(int a, int b, int c)
{

    // To store the count of negative integers
    int countOfNegative = 0;

    // Sum of all the three integers
    int sum = a + b + c;

    // Product of all the three integers
    int product = a * b * c;

    // To store the smallest and the largest
    // among all the three integers
    int largest = max(a,max(b,c));
    int smallest = min(a,min(b,c) );

    // Calculate the count of negative integers
    if (a < 0)
        countOfNegative++;
    if (b < 0)
        countOfNegative++;
    if (c < 0)
        countOfNegative++;

    // Depending upon count of negatives
    switch (countOfNegative) {

    // When all three are positive integers
    case 0:
        return (sum - largest) * largest;

    // For single negative integer
    case 1:
        return (product / smallest) + smallest;

    // For two negative integers
    case 2:
        return (product / largest) + largest;

    // For three negative integers
    case 3:
        return (sum - smallest) * smallest;
    }
}

// Driver Code
int main()
{
    int a=-2,b=-1,c=-4;
    cout << maximumResult(a, b, c);

    return 0;
}
// This code contributed by Nikhil
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum result
static int maximumResult(int a, int b, int c)
{

    // To store the count of negative integers
    int countOfNegative = 0;

    // Sum of all the three integers
    int sum = a + b + c;

    // Product of all the three integers
    int product = a * b * c;

    // To store the smallest and the largest
    // among all the three integers
    int largest = (a > b) ? ((a > c) ? a : c) :
                            ((b > c) ? b : c);
    int smallest= (a<b)?((a<c)? a : c):((b<c) ? b : c);
    // Calculate the count of negative integers
    if (a < 0)
        countOfNegative++;
    if (b < 0)
        countOfNegative++;
    if (c < 0)
        countOfNegative++;

    // Depending upon count of negatives
    switch (countOfNegative)
    {

        // When all three are positive integers
        case 0:
            return (sum - largest) * largest;

        // For single negative integer
        case 1:
            return (product / smallest) + smallest;

        // For two negative integers
        case 2:
            return (product / largest) + largest;

        // For three negative integers
        case 3:
            return (sum - smallest) * smallest;
    }
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    int a=-2,b=-1,c=-4;
    System.out.print(maximumResult(a, b, c));
}
}

// This code contributed by Nikhil
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum result
# Python3 implementation of the approach

# Function to return the maximum result
def maximumResult(a, b, c):

    # To store the count of negative integers
    countOfNegative = 0

    # Sum of all the three integers
    Sum = a + b + c

    # Product of all the three integers
    product = a * b * c

    # To store the smallest and the
    # largest among all the three integers
    largest = max(a, b, c)
    smallest = min(a, b, c)

    # Calculate the count of negative integers
    if a < 0:
        countOfNegative += 1
    if b < 0:
        countOfNegative += 1
    if c < 0:
        countOfNegative += 1

    # When all three are positive integers
    if countOfNegative == 0:
        return (Sum - largest) * largest

    # For single negative integer
    elif countOfNegative == 1:
        return (product // smallest) + smallest

    # For two negative integers
    elif countOfNegative == 2:
        return (product // largest) + largest

    # For three negative integers
    elif countOfNegative == 3:
        return (Sum - smallest) * smallest

# Driver Code
if __name__ == "__main__":

    a, b, c = -2, -1, -4
    print(maximumResult(a, b, c))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum result
static int maximumResult(int a, int b, int c)
{

    // To store the count of negative integers
    int countOfNegative = 0;

    // Sum of all the three integers
    int sum = a + b + c;

    // Product of all the three integers
    int product = a * b * c;

    // To store the smallest and the largest
    // among all the three integers
    int largest = (a > b) ? ((a > c) ? a : c) :
                            ((b > c) ? b : c);
    int smallest=(a<b)?((a<c)? a : c):((b<c) ? b : c);

    // Calculate the count of negative integers
    if (a < 0)
        countOfNegative++;
    if (b < 0)
        countOfNegative++;
    if (c < 0)
        countOfNegative++;

    // Depending upon count of negatives
    switch (countOfNegative)
    {

        // When all three are positive integers
        case 0:
            return (sum - largest) * largest;

        // For single negative integer
        case 1:
            return (product / smallest) + smallest;

        // For two negative integers
        case 2:
            return (product / largest) + largest;

        // For three negative integers
        case 3:
            return (sum - smallest) * smallest;
    }
    return -1;
}

// Driver Code
static void Main()
{
    int a = -2, b = -1, c = -4;
    Console.WriteLine(maximumResult(a, b, c));
}
}

// This code is contributed by mits & Nikhil
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum result
function maximumResult($a, $b, $c)
{

    // To store the count of
    // negative integers
    $countOfNegative = 0;

    // Sum of all the three integers
    $sum = $a + $b + $c;

    // Product of all the three integers
    $product = $a * $b * $c;

    // To store the smallest and the largest
    // among all the three integers
    $largest = max($a ,$b, $c);
    $smallest = min($a ,$b, $c);

    // Calculate the count of negative integers
    if ($a < 0)
        $countOfNegative++;
    if ($b < 0)
        $countOfNegative++;
    if ($c < 0)
        $countOfNegative++;

    // Depending upon count of negatives
    switch ($countOfNegative)
    {

        // When all three are positive integers
        case 0:
            return ($sum - $largest) *
                           $largest;

        // For single negative integer
        case 1:
            return ($product / $smallest) +
                               $smallest;

        // For two negative integers
        case 2:
            return ($product / $largest) +
                               $largest;

        // For three negative integers
        case 3:
             return ($sum - $smallest) *
                           $smallest;
    }
}

// Driver Code
$a = -2;
$b = -1;
$c = -4;
echo maximumResult($a, $b, $c);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach

// Function to return the maximum result
function maximumResult(a, b, c)
{

    // To store the count of negative integers
    let countOfNegative = 0;

    // Sum of all the three integers
    let sum = a + b + c;

    // Product of all the three integers
    let product = a * b * c;

    // To store the smallest and the largest
    // among all the three integers
    let largest = Math.max(a,Math.max(b,c));
    let smallest = Math.min(a,Math.min(b,c) );

    // Calculate the count of negative integers
    if (a < 0)
        countOfNegative++;
    if (b < 0)
        countOfNegative++;
    if (c < 0)
        countOfNegative++;

    // Depending upon count of negatives
    switch (countOfNegative) {

    // When all three are positive integers
    case 0:
        return (sum - largest) * largest;

    // For single negative integer
    case 1:
        return (product / smallest) + smallest;

    // For two negative integers
    case 2:
        return (product / largest) + largest;

    // For three negative integers
    case 3:
        return (sum - smallest) * smallest;
    }
}

// Driver Code

    let a = -2, b = -1, c = -4;
    document.write(maximumResult(a, b, c));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
12
```