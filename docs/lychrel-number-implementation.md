# 莱卡号码实施

> 原文:[https://www . geesforgeks . org/lychrel-number-implementation/](https://www.geeksforgeeks.org/lychrel-number-implementation/)

**Lychrel Number** 是一个自然数，通过反复反转其数字并相加所得数字的迭代过程，无法形成回文。该过程有时被称为[196-算法](http://mathworld.wolfram.com/196-Algorithm.html)，以与该过程相关的最著名的数字命名。
当应用 196 算法(即先反后加序列)时，前几个不知道会产生回文的数字有时被称为 Lychrel 数。
**例:**

```
Input : 56
Output : 56 is lychrel  : false
Explanation : 56 becomes palindromic after one iteration : 
56 + 65 = 121

Input : 196
Output : 196 is lychrel  : true
Explanation : 196 becomes palindromic after 19 iterations :
196 + 691 = 887
887 + 788 = 1675
1675 + 5761 = 7436
7436 + 6347 = 13783
13783 + 38731 = 52514
....
16403234045 + 54043230461
70446464506 + 60546464407
```

任务是找出给定的数字是否是具有给定迭代次数限制的 Lycheral。

```
1\. Iterate given number of times
    1\. Add number to it's reverse
    2\. If 
         the newly formed number is palindrome
       then
          return false  // Number is not lychrel.
2\. return true         // Number is lychrel
```

## C++

```
// C++ Program to check whether the given number
// is Lychrel Number or not with given limit
// on number of iterations.
#include<iostream>
using namespace std;

long reverse(long);
bool isPalindrome(long);

// Max Iterations
static int MAX_ITERATIONS = 20;

// Function to check whether number is
// Lychrel Number
string isLychrel(long number)
{
    for (int i = 0; i < MAX_ITERATIONS; i++)
    {
        number = number + reverse(number);

        if (isPalindrome(number))
            return "false";
    }

    return "true";
}

// Function to check whether the number is
// Palindrome
bool isPalindrome(long number)
{
    return number == reverse(number);
}

// Function to reverse the number
long reverse(long number)
{
    long reverse = 0;
    while (number > 0)
    {
        long remainder = number % 10;
        reverse = (reverse * 10) + remainder;
        number = number / 10;
    }

    return reverse;
}

// Driver program
int main()
{
    long number = 295;
    cout<<number << " is lychrel? "
                       << isLychrel(number);
}

// This code is contributed by Smitha
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check whether the given number
// is Lychrel Number or not with given limit
// on number of iterations.
import java.io.*;

public class LychrelNumberTest
{
    // Max Iterations
    private static int MAX_ITERATIONS = 20;

    // Function to check whether number is Lychrel Number
    private static boolean isLychrel(long number)
    {
        for (int i = 0; i < MAX_ITERATIONS; i++)
        {
            number = number + reverse(number);
            if (isPalindrome(number))
                return false;

        }
        return true;
    }

    // Function to check whether the number is Palindrome
    private static boolean isPalindrome(final long number)
    {
        return number == reverse(number);
    }

    // Function to reverse the number
    private static long reverse(long number)
    {
        long reverse = 0;

        while (number > 0)
        {
            long remainder = number % 10;
            reverse = (reverse * 10) + remainder;
            number = number / 10;
        }
        return reverse;
    }

    // driver program
    public static void main(String[] args)
    {
        long number = 295;
        System.out.println(number + " is lychrel? "
                           + isLychrel(number));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to check whether the given number
# is Lychrel Number or not with given limit
# on number of iterations.

# Max Iterations
MAX_ITERATIONS = 20;

# Function to check whether number is
# Lychrel Number
def isLychrel(number):

    for i in range(MAX_ITERATIONS):
        number = number + reverse(number);

        if (isPalindrome(number)):
            return "false";

    return "true";

# Function to check whether the number
# is Palindrome
def isPalindrome(number):

    return number == reverse(number);

# Function to reverse the number
def reverse(number):

    reverse = 0;
    while (number > 0):

        remainder = number % 10;
        reverse = (reverse * 10) + remainder;
        number = int(number / 10);

    return reverse;

# Driver Code
number = 295;
print(number," is lychrel? ",isLychrel(number));

# This code is contributed by mits
```

## C#

```
// C# Program to check whether the given number
// is Lychrel Number or not with given limit
// on number of iterations.
using System;

class GFG
{
    // Max Iterations
    private static int MAX_ITERATIONS = 20;

    // Function to check whether number is Lychrel Number
    private static bool isLychrel(long number)
    {
        for (int i = 0; i < MAX_ITERATIONS; i++)
        {
            number = number + reverse(number);
            if (isPalindrome(number))
                return false;

        }
        return true;
    }

    // Function to check whether the number is Palindrome
    private static bool isPalindrome( long number)
    {
        return number == reverse(number);
    }

    // Function to reverse the number
    private static long reverse(long number)
    {
        long reverse = 0;

        while (number > 0)
        {
            long remainder = number % 10;
            reverse = (reverse * 10) + remainder;
            number = number / 10;
        }
        return reverse;
    }

    // Driver program
    public static void Main()
    {
        long number = 295;
        Console.Write(number + " is lychrel? "
                        + isLychrel(number));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check whether the given number
// is Lychrel Number or not with given limit
// on number of iterations.

// Max Iterations
$MAX_ITERATIONS = 20;

// Function to check whether number is
// Lychrel Number
function isLychrel($number)
{
    global $MAX_ITERATIONS;
    for ($i = 0; $i < $MAX_ITERATIONS; $i++)
    {
        $number = $number + reverse($number);

        if (isPalindrome($number))
            return "false";
    }

    return "true";
}

// Function to check whether the number
// is Palindrome
function isPalindrome($number)
{
    return $number == reverse($number);
}

// Function to reverse the number
function reverse($number)
{
    $reverse = 0;
    while ($number > 0)
    {
        $remainder = $number % 10;
        $reverse = ($reverse * 10) + $remainder;
        $number = (int)($number / 10);
    }

    return $reverse;
}

// Driver Code
$number = 295;
echo $number . " is lychrel? " .
             isLychrel($number);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to check
// whether the given number is Lychrel
// Number or not with given limit
// on number of iterations.

// Max Iterations
var MAX_ITERATIONS = 20;

// Function to check whether
// number is Lychrel Number
function isLychrel(number)
{
    for (var i = 0; i < MAX_ITERATIONS; i++)
    {
        number = number + reverse(number);
        if (isPalindrome(number))
            return false;

    }
    return true;
}

// Function to check whether the
// number is Palindrome
function isPalindrome(number)
{
    return number == reverse(number);
}

// Function to reverse the number
function reverse(number)
{
    var reverse = 0;

    while (number > 0)
    {
        var remainder = number % 10;
        reverse = (reverse * 10) + remainder;
        number = parseInt(number / 10);
    }
    return reverse;
}

// driver program
var number = 295;
document.write(number + " is lychrel ? "
                + isLychrel(number));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
295 is lychrel ? true
```

本文由**普拉莫德·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。